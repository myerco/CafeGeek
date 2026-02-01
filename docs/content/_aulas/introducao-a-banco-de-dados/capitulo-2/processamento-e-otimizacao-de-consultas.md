---
title: processamento-e-otimizacao-de-consultas
excerpt: "Processamento e otimização de consultas em bancos de dados."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-2"
date: 2026-01-31T08:48:05-04:00
order: 7
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Processamento e Otimização de Consultas

Envolve as atividades de extrair dados e traduzir consultas de alto nível para expressões físicas eficientes.

**Etapas:**

1. Análise Sintática: traduz o SQL para uma expressão de álgebra relacional.
2. Otimização: seleciona o plano de execução mais eficiente baseando-se em algoritmos, índices e estatísticas de custo.
3. Avaliação: estima custos via tempo de CPU, acesso a disco (IO) e uso de RAM.

- Execução de Joins: o otimizador decide o caminho de acesso (varredura total ou índice), o método de união (Nested loop, Sort merge ou Hash joins) e a ordem de execução.
- Fases no Oracle: Parse (verificação e busca no dicionário), Execute (aplicação física) e Fetch (retorno dos dados).

## Análise sintática

- Comando SQL
  - Select saldo From conta Where saldo < 25000
- Expressões algébrica relacional
  - σ saldo < 2500 (π saldo (conta))
  - π saldo (σ saldo < 2500(conta))
- Plano de execução
  - π saldo
  - σ saldo < 2500; use índice 1

## Álgebra relacional

```sql
SELECT nome
FROM empregado;
```

AR>π nome (empregado);

```sql
SELECT nome,sal
FROM empregado;
```

- AR>π nome,sal (empregado);

```sql
SELECT *
FROM empregado;
WHERE sal > 5000
```

- AR>σ sal > 5000 (empregado);

```sql
SQL>SELECT sal
FROM empregado;
WHERE sal > 5000
```

- AR>σ sal > 5000 ( π sal(empregado));

- AR> π sal ( σ sal > 5000 (empregado));

## Exemplos

### Tabela 1

| ID (5B) | NOME (40B)    | SAL (10B) |
| ------- | ------------- | --------- |
| 1       | ANA MARIA     | 6000      |
| 2       | JOÃO SALDANHA | 5000      |

- Considere o tamanho da tabela:  110B + 3MB;
- O comando SQL abaixo pode ser interpretado com as duas expressões de algebra relacional:

```sql
SELECT sal
FROM empregado;
WHERE sal > 5000
```

- AR 1>σ sal > 5000 ( π sal(empregado));

- AR 2> π sal ( σ sal > 5000 (empregado));

- A avaliação do resultado de acesso medido em Bytes de cada expressão deverá ser:
  - AR1 = (20B) + 10B = 30B
  - AR2 = (55B) + 10 = 65B

### Tabela 2

| ID (5B) | NOME (40B)    | SAL (10B) | FOTO (3MB) |
| ------- | ------------- | --------- | ---------- |
| 1       | ANA MARIA     | 6000      | ...        |
| 2       | JOÃO SALDANHA | 5000      | ...        |

- Se na tabela existir um atributo com características distintas de tamanho e acesso, como por exemplo um campo BLOB ou LOB, o acesso aos dados pode aumentar consideravelmente quando usada a expressão:

  - AR2 = (3MB + 55B) + 10 = 3MB + 65B

- Recomenda-se fortemente separar o atributo da tabela.

## Otimização

- Processo para selecionar o plano de execução mais eficiente para uma consulta;
- Escolha do algoritmo de execução;
- Escolha de índices;
- Obtém informações estatísticas sobre as relações como os tamanhos das relações e as profundidades dos índices para realizar uma boa estimativa.
