---
title: Visões e restrições de acesso
excerpt: "Visões (views) e restrições de acesso em bancos de dados."
categories:
  - "banco-de-dados"
  - "estruturas"
date: 2026-01-31T08:48:05-04:00
order: 4
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

No nível externo da arquitetura ANSI/SPARC, o banco de dados  é percebido como uma “visão externa”, definida por um esquema externo. Diversos usuários podem ter visões externas diversas. **C.J. Date**
{: .notice}

Uma visão é considerada uma **tabela virtual**; ela não existe fisicamente, mas aparece ao usuário como uma tabela real.

<div class="mermaid">
graph TD
    subgraph Tabela_Base [Tabela Base: Funcionários]
        direction TB
        DB[(Banco de Dados)]

        %% Uso de aspas duplas para permitir o caractere pipe |
        T_Cols["ID | Nome | Salário | Departamento | Telefone"]
        T_Rows["Ana | 9.0000 | TI| (69) 96584-5475<br/>João | 9.500 | TI| (69) 8694-4758<br/>Maria |10000| RH| (69) 7845-4756<br/>Humberto | 9000|ADM| (69) 9869-5874"]
        
        DB --- T_Cols
        T_Cols --- T_Rows
    end

    Tabela_Base --> Processo{Definição da VIEW}

    subgraph Restricoes [Mecanismos de Filtro]
        direction LR
        V_Rest["<b>Restrição Vertical</b><br/>(Colunas Selecionadas)"]
        H_Rest["<b>Restrição Horizontal</b><br/>(Cláusula WHERE)"]
    end

    Processo --> V_Rest
    Processo --> H_Rest

    V_Rest --> View_Final
    H_Rest --> View_Final

    subgraph View_Virtual [Objeto: VIEW]
        View_Final[[Virtual: vw_ti_contatos]]
        V_Display["Nome | Departamento<br/>---<br/>Ana | TI<br/>João | TI"]
    end

    %% Estilização
    style Tabela_Base fill:#f9f9f9,stroke:#333,stroke-width:2px
    style View_Virtual fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style V_Rest fill:#fff9c4,stroke:#fbc02d
    style H_Rest fill:#fff9c4,stroke:#fbc02dgraph TD
    
</div>

## Características

- A visão é operada como se fosse uma tabela real
- É uma janela para um subconjunto de dados de uma tabela
- Toda mudança na tabela é automaticamente e instantaneamente refletida através desta janela
- Mostra Linhas pertinentes para os usuários
- Visões podem ser usadas para aumentar a segurança escondendo detalhes das estruturas das tabelas
- Podem esconder a complexidade de uma consulta

## Sintaxe SQL

```sql
CREATE VIEW nome_da_view AS subquery
```

- Exemplos mostram a criação de visões para filtrar funcionários com salários específicos e a execução de consultas normais sobre essas visões.

Implementando a tabela de funcionários.

```sql
CREATE TABLE FUNCIONARIOS (
  ID SERIAL PRIMARY KEY,
  NOME VARCHAR(100),
  MATRICULA VARCHAR(20) UNIQUE,
  DATA_NASCIMENTO DATE
);
```

Inserindo funcionários na tabela.

```sql
INSERT INTO
  FUNCIONARIOS (NOME, MATRICULA, DATA_NASCIMENTO)
VALUES
  ('Joel Miller', 'TLOU-001', '1981-09-26'),
  ('Ellie Williams', 'TLOU-002', '2019-04-14'),
  ('Tommy Miller', 'TLOU-003', '1985-05-12'),
  ('Tess Servopoulos', 'TLOU-004', '1978-08-20'),
  ('Bill', 'TLOU-005', '1975-11-30'),
  ('Frank', 'TLOU-006', '1976-03-15'),
  ('Marlene', 'TLOU-007', '1980-01-10'),
  ('Riley Abel', 'TLOU-008', '2018-02-25'),
  ('Henry Burrell', 'TLOU-009', '1998-06-05'),
  ('Sam Burrell', 'TLOU-010', '2010-09-12');
```

Implementando a VIEW vw_funcionarios apresentando somente um atributo da tabela e calculando a idade

```sql
CREATE OR REPLACE VIEW VW_FUNCIONARIOS AS
SELECT
  NOME,
  EXTRACT(
      YEAR
      FROM
          AGE (CURRENT_DATE, DATA_NASCIMENTO)
  ) AS IDADE
FROM
  FUNCIONARIOS;
```

Implementando uma VIEW para esconder a complexidade de uma consulta que apresenta a diferença de idade entre funcionários.

```sql
CREATE OR REPLACE VIEW VW_FUNCIONARIOS_POR_IDADE AS 
WITH ListaIdades AS (
    SELECT 
        nome, 
        EXTRACT(YEAR FROM AGE(CURRENT_DATE, data_nascimento)) AS idade
    FROM FUNCIONARIOS
)
SELECT 
    nome,
    idade,
    idade - LAG(idade) OVER (ORDER BY idade ASC) AS diferenca_anos
FROM ListaIdades
ORDER BY idade ASC;
```

Executando a VIEW

```sql
SELECT * FROM VW_FUNCIONARIOS;
SELECT * FROM VW_FUNCIONARIOS ORDER BY  NOME ;
SELECT NOME FROM  VW_FUNCIONARIOS WHERE IDADE > 40;
SELECT * FROM VW_FUNCIONARIOS_POR_IDADE;
```

## Schemas e Views

Podemos construir um schema com todas as visões das tabelas, separando assim a estrutura das tabelas.

**OBSERVAÇÃO**: feito isso e aliado a uma administração de ROLEs aumenta a segurança dos dados.
{: .notice}

Repare que o usuário do esquema consulta é diferente do usuário de produção

Criando o schema consulta

```sql
CREATE SCHEMA CONSULTA AUTHORIZATION  usuario_online;
```

Alterando o schema da view

```sql
ALTER VIEW VW_FUNCIONARIOS SET SCHEMA consulta;
```

Ou prodemos implementar a view dentro do esquema consulta

```sql
CREATE VIEW CONSULTA.VW_FUNCIONARIOS AS
SELECT nome 
FROM funcionarios;
```
