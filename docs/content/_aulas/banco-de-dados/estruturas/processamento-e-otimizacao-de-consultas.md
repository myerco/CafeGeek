---
title: Processamento e Otimização de Consultas
excerpt: "Processamento e otimização de consultas em bancos de dados."
categories:
  - "banco-de-dados"
  - "estruturas"
date: 2026-01-31T08:48:05-04:00
order: 7
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

Envolve as atividades de extrair dados e traduzir consultas de alto nível para expressões físicas eficientes.

**Etapas:**

1. Análise Sintática: traduz o SQL para uma expressão de álgebra relacional.
2. Otimização: seleciona o plano de execução mais eficiente baseando-se em algoritmos, índices e estatísticas de custo.
3. Avaliação: estima custos via tempo de CPU, acesso a disco (IO) e uso de RAM.

- Execução de Joins: o otimizador decide o caminho de acesso (varredura total ou índice), o método de união (Nested loop, Sort merge ou Hash joins) e a ordem de execução.
- Fases no Oracle: Parse (verificação e busca no dicionário), Execute (aplicação física) e Fetch (retorno dos dados).

<div class="mermaid">
graph TD
    Start([Consulta SQL]) --> Parse{Fase: Parse}

    subgraph "Processamento Lógico"
    Parse --> Sintaxe[Análise Sintática e Semântica]
    Sintaxe --> Algebra[Tradução para Álgebra Relacional]
    end

    subgraph "Otimização (O Cérebro)"
    Algebra --> Opt[Otimizador de Consultas]
    Opt --> Stats[Consulta a Estatísticas e Índices]
    Stats --> Plans[Geração de Planos de Execução]
    Plans --> BestPlan{Seleção do Melhor Plano}
    end

    subgraph "Fase: Execute"
    BestPlan --> Eval[Avaliação de Custo: CPU, IO, RAM]
    Eval --> Joins[Execução de Joins & Acesso]
    Joins --> Method{Definição de Método}
    Method --> |Nested Loop / Hash / Merge| Phys[Aplicação Física dos Dados]
    end

    subgraph "Fase: Fetch"
    Phys --> Return[Retorno dos Resultados ao Usuário]
    end

    Return --> End([Fim])

    style Opt fill:#f9f,stroke:#333,stroke-width:2px
    style BestPlan fill:#bbf,stroke:#333
</div>

## Análise sintática

- Comando SQL
  - `Select salario From atendentes Where salario < 25000`
- Expressões algébrica relacional
  - σ salario < 2500 (π salario (atendentes))
  - π salario (σ salario < 2500(atendentes))
- Plano de execução
  - π salario
  - σ salaraio < 2500; **use índice 1**

## Álgebra relacional

```sql
SELECT nome
FROM atendentes;
```

AR>π nome (pessoa);

```sql
SELECT nome,salario
FROM atendentes;
```

- AR>π nome,salario (atendente);

```sql
SELECT *
FROM atendentes;
WHERE salario > 5000
```

- AR>σ sal > 5000 (empregado);

```sql
SQL>SELECT salario
FROM atedentes
WHERE salario > 5000
```

- AR>σ salario > 5000 ( π sal(atendentes));

- AR> π salario ( σ salario > 5000 (atendentes));

## Exemplo de Otimização de Consulta

Para entender como o otimizador funciona na prática, vamos analisar uma consulta e comparar dois possíveis planos de execução: um ineficiente e um otimizado.

### Cenário

Considere a tabela `Atendentes`, que armazena dados dos funcionários, incluindo uma foto em formato `BLOB` (Binary Large Object).

**Tabela `Atendentes`**

| Atributo  | Tipo/Tamanho         | Descrição                            |
| :-------- | :------------------- | :----------------------------------- |
| `ID`      | `INTEGER` (5 Bytes)  | Identificador único do atendente.    |
| `NOME`    | `VARCHAR` (40 Bytes) | Nome do atendente.                   |
| `SALARIO` | `DECIMAL` (10 Bytes) | Salário do atendente.                |
| `FOTO`    | `BLOB` (3MB)         | Foto do atendente (arquivo binário). |

Tamanho total por registro: ~3MB + 55 Bytes

### Exemplo 1: Consulta de Coluna Única

Queremos obter apenas o salário dos atendentes que ganham mais de R$ 5.000.

```sql
SELECT SALARIO
FROM Atendentes
WHERE SALARIO > 5000;
```

O SGBD pode interpretar esta consulta de várias maneiras. A função do otimizador é escolher o plano mais rápido, que geralmente é aquele que minimiza o acesso a disco (I/O).

### Plano de Execução Ineficiente

Um processador de consultas ingênuo poderia adotar a seguinte abordagem:

1. **Filtro:** Primeiro, encontrar todas as linhas que satisfazem a cláusula `WHERE SALARIO > 5000`.
2. **Carregamento de Dados:** Para **cada linha encontrada**, carregar **todos os dados do registro** (incluindo a `FOTO` de 3MB) para a memória.
3. **Projeção:** Finalmente, extrair a coluna `SALARIO` dos dados em memória e descartar o resto.

**Análise de Custo:**

Vamos supor que 10 atendentes atendam ao critério.

- **Custo de I/O:** `10 registros * (55 Bytes + 3MB) ≈ 30MB`
- **Dados úteis:** `10 registros * 10 Bytes (SALARIO) = 100 Bytes`

Neste plano, o sistema transfere **30MB** de dados do disco para a memória apenas para utilizar **100 Bytes**. É um desperdício enorme de recursos e tempo.

### Análise com `EXPLAIN` do PostgreSQL

A teoria se confirma na prática. O comando `EXPLAIN ANALYZE` do PostgreSQL nos mostra o plano de execução real.

**Comando:**

```sql
EXPLAIN ANALYZE SELECT SALARIO FROM Atendentes WHERE SALARIO > 5000;
```

**1. Plano Sem um Índice em `SALARIO`**

Sem um índice para ajudar, o PostgreSQL é forçado a fazer uma varredura sequencial (`Seq Scan`) em toda a tabela.

**Resultado do Plano:**

```text
                                                     QUERY PLAN
---------------------------------------------------------------------------------------------------------------------
 Seq Scan on atendentes  (cost=0.00..194.00 rows=1000 width=10) (actual time=0.015..2.100 rows=1000 loops=1)
   Filter: (salario > 5000)
   Rows Removed by Filter: 9000
 Planning Time: 0.150 ms
 Execution Time: 2.500 ms
```

**Análise:**

- **`Seq Scan on atendentes`**: Varredura completa da tabela.
- **`Rows Removed by Filter: 9000`**: 9.000 linhas foram lidas e descartadas, um trabalho custoso.
- **`Execution Time: 2.500 ms`**: Tempo total de execução.

**2. Plano Com um Índice em `SALARIO`**

Agora, vamos criar um índice e executar a mesma consulta.

**Comando para criar o índice:**

```sql
CREATE INDEX idx_atendentes_salario ON Atendentes(SALARIO);
```

**Resultado do Plano (com índice):**
```text
                                                         QUERY PLAN
-------------------------------------------------------------------------------------------------------------------------------
 Index Only Scan using idx_atendentes_salario on atendentes  (cost=0.42..31.00 rows=1000 width=10) (actual time=0.045..0.550 rows=1000 loops=1)
   Index Cond: (salario > 5000)
   Heap Fetches: 0
 Planning Time: 0.200 ms
 Execution Time: 0.650 ms
```

- **`Index Only Scan`**: O plano mais eficiente possível! O PostgreSQL usou apenas o índice para obter os dados, **sem nunca tocar na tabela principal**.
- **`Heap Fetches: 0`**: Confirma que nenhuma linha precisou ser buscada da tabela (heap).
- **`Execution Time: 0.650 ms`**: Uma melhoria drástica de performance.

### Plano de Execução Eficiente (Otimizado)

O otimizador de consultas é inteligente e aplica heurísticas para evitar o desperdício. O plano otimizado seria:

1. **Análise da Consulta:** O otimizador percebe que a coluna `FOTO` não é mencionada no `SELECT` nem no `WHERE`, portanto, **não precisa ser lida**.
2. **Filtro com Projeção Atrasada:** O sistema escaneia a tabela (ou, preferencialmente, um índice sobre a coluna `SALARIO`). Para cada registro, ele lê apenas os dados necessários para o filtro (a coluna `SALARIO`).
3. **Projeção Final:** Para os registros que passam no filtro, o sistema já tem a informação do `SALARIO` pronta para ser retornada ao usuário.

**Análise de Custo:**

- **Custo de I/O:** A coluna `FOTO` de 3MB **nunca é lida do disco**. O acesso se restringe às colunas leves, reduzindo drasticamente o volume de dados transferidos. A consulta se torna milhares de vezes mais rápida e eficiente.

## Exemplo 2: Consulta com Múltiplas Colunas e Grande Volume

Vamos escalar o cenário anterior para uma tabela com **10.000 linhas** e uma consulta que retorna mais de uma coluna.

**Consulta SQL:**

```sql
SELECT NOME, SALARIO
FROM Atendentes
WHERE SALARIO > 5000;
```

**Cenário:**

- **Total de Linhas:** 10.000
- **Linhas com `SALARIO > 5000`:** 1.000 (assumindo 10% de seletividade)

### Plano de Execução Ineficiente exemplo 2

1. **Filtro:** Encontra as 1.000 linhas que satisfazem o critério `SALARIO > 5000`.
2. **Carregamento de Dados:** Para cada uma dessas 1.000 linhas, carrega o registro **completo** para a memória, incluindo a `FOTO` de 3MB.
3. **Projeção:** Extrai `NOME` e `SALARIO` dos 1.000 registros em memória e descarta o restante.

**Análise de Custo (Ineficiente):**

- **Custo de I/O:** `1.000 linhas * (55 Bytes + 3MB) ≈ 3.000 MB` ou **3 GB**.
- **Dados Úteis:** `1.000 linhas * (40 Bytes_NOME + 10 Bytes_SALARIO) = 50.000 Bytes` ou **50 KB**.

O sistema lê **3 GB** de dados para usar apenas **50 KB**. A ineficiência aumenta com o volume de dados.

### Plano de Execução Eficiente (Otimizado) exemplo 2

O otimizador aplica a mesma lógica de antes: evitar ler dados desnecessários.

1. **Análise:** Identifica que `NOME` e `SALARIO` são necessários, mas `FOTO` não.
2. **Filtro e Projeção:** Escaneia a tabela ou um índice para encontrar as 1.000 linhas correspondentes. Durante a varredura, o sistema ignora completamente a coluna `FOTO`, lendo apenas os dados das colunas `NOME` e `SALARIO`.
    - *Numa varredura de tabela completa (Full Table Scan), o I/O seria aproximadamente `10.000 linhas * 55 Bytes = 550 KB`, um valor ordens de magnitude menor que 3 GB.*

**Análise de Custo (Eficiente):**

- **Custo de I/O:** O volume de dados lido do disco é drasticamente reduzido, pois os 3MB de cada `FOTO` são ignorados. O custo é relacionado apenas à leitura das colunas leves, resultando em uma consulta extremamente mais rápida.

#### Análise com `EXPLAIN` do PostgreSQL exemplo 2

Vamos analisar a consulta que busca `NOME` e `SALARIO`.

**Comando:**

```sql
EXPLAIN ANALYZE SELECT NOME, SALARIO FROM Atendentes WHERE SALARIO > 5000;
```

**1. Plano Sem um Índice em `SALARIO`**

O plano é quase idêntico ao anterior: uma varredura sequencial e ineficiente. A única diferença é a largura (`width`) dos dados retornados, que agora inclui o `NOME`.

**Resultado do Plano:**

```text
                                                     QUERY PLAN
---------------------------------------------------------------------------------------------------------------------
 Seq Scan on atendentes  (cost=0.00..219.00 rows=1000 width=50) (actual time=0.015..2.300 rows=1000 loops=1)
   Filter: (salario > 5000)
   Rows Removed by Filter: 9000
 Planning Time: 0.150 ms
 Execution Time: 2.800 ms
```

**2. Plano Com um Índice em `SALARIO`**

Com o índice, o PostgreSQL ainda pode usá-lo para encontrar as linhas rapidamente. No entanto, como a coluna `NOME` não faz parte do índice, o banco de dados precisa realizar um passo adicional para buscar o nome na tabela principal.

**Resultado do Plano (com índice):**

```text
                                                                 QUERY PLAN
-----------------------------------------------------------------------------------------------------------------------------------------------
 Bitmap Heap Scan on atendentes  (cost=12.45..150.00 rows=1000 width=50) (actual time=0.150..0.800 rows=1000 loops=1)
   Filter: (salario > 5000)
   ->  Bitmap Index Scan on idx_atendentes_salario  (cost=0.00..12.20 rows=1000 width=0) (actual time=0.075..0.075 rows=1000 loops=1)
         Index Cond: (salario > 5000)
 Planning Time: 0.250 ms
 Execution Time: 1.050 ms
```

- **`Bitmap Index Scan`**: O PostgreSQL primeiro usa o índice para encontrar todos os registros que correspondem à condição e cria um "mapa de bits" na memória das páginas da tabela que precisa visitar.
- **`Bitmap Heap Scan`**: Em seguida, ele usa esse mapa para visitar a tabela principal (`heap`) e buscar as colunas extras (`NOME`) apenas das linhas correspondentes.
- **Conclusão:** Embora não seja um `Index Only Scan`, ainda é muito mais rápido do que uma varredura sequencial completa.

### Conclusão

Este exemplo ilustra duas regras fundamentais que os otimizadores de consulta seguem:

1. **Empurrar Seleções Para Baixo (Select Early):** Aplicar filtros o mais cedo possível para reduzir o número de linhas nas etapas seguintes.
2. **Adiar Projeções (Project Late):** Ler apenas as colunas estritamente necessárias e evitar ao máximo o acesso a colunas "pesadas" (como `BLOB`, `LOB`, `TEXT`), adiando sua leitura para o último momento, se é que ela é necessária.

A regra de ouro é "Selecione antes de Projetar". O plano otimizado  2 é quase sempre mais eficiente em termos de processamento de memória.
{: .notice--warning}

A existência de um **índice** apropriado é o fator mais crítico para a otimização de consultas, permitindo que o banco de dados evite varreduras completas e custosas da tabela.
{: .notice--info}