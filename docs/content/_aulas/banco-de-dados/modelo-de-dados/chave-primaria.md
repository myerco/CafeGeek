---
title: Chave Primária
excerpt: "Entenda o conceito de chave primária em bancos de dados relacionais, sua importância e exemplos práticos."
categories:
  - banco-de-Dados
  - modelo-de-dados
date: 2026-01-22T08:48:05-04:00
order: 5
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## O que é uma Chave Primária?

A chave primária é um atributo (ou conjunto de atributos) que identifica exclusivamente cada registro em uma tabela. Ela garante que não haja duplicatas e permite referenciar registros de forma única.

Em termos simples: imagine uma tabela de alunos. A matrícula de cada aluno é única — nenhum outro aluno tem a mesma matrícula. Isso faz da matrícula uma chave primária perfeita.

## A Tabela Pessoas

Considere a tabela `PESSOAS`:

| ID  | Nome               | e-mail                      |
| --- | ------------------ | --------------------------- |
| 1   | Aragorn II Elessar | aragorn.rei@gondor.com      |
| 2   | Arwen Undómiel     | arwen.estrela@rivendell.com |

Aqui, o atributo `ID` é a chave primária, pois cada valor é único e identifica um aluno específico.

<div class="mermaid">
graph TD
    A[Novo Registro: Aluno] --> B{A Matrícula já existe?}
    B -- Sim --> C[Erro: Violação de Chave Primária]
    B -- Não --> D[Registro Inserido com Sucesso]
    C --> E[Garante a Unicidade dos Dados]
    D --> E
</div>

Ao tentar inserir o `ID`  com valor repetido, o banco rejeita o comando, pois o valor já existe na tabela.

```sql
INSERT INTO PESSOAS (ID, NOME, DATA_NASCIMENTO, ID_SEXO, EMAIL) VALUES 
    (1, 'Balrock', '2021-03-01', 1, 'ballrock.rei@gondor.com');

--ERROR:  duplicate key value violates unique constraint "pessoas_pkey"
--Key (id)=(1) already exists. 

--SQL state: 23505
--Detail: Key (id)=(1) already exists.
    
```

## Requisitos de uma Chave Primária

Para ser uma chave primária válida, o atributo deve atender a estes critérios:

- **Não pode ser nulo**: Todo registro deve ter um valor para a chave primária.
- **Deve ser único**: Não pode haver dois registros com o mesmo valor.
- **Imutável**: O valor não deve mudar ao longo do tempo (idealmente).
- **É um índice**: A chave vai estar associada a uma estrutura de indexação. As chaves primárias são automaticamente indexadas pelo SGBD para otimizar consultas.

## Chave candidata

Na tabela `PESSOAS`, o CPF pode servir como chave primária, pois cada pessoa tem um CPF único, podemos chamar essa chave candidata.

| CPF            | Nome       | email               |
| -------------- | ---------- | ------------------- |
| 123.456.789-00 | Ana Costa  | anacasota@gmail.com |
| 987.654.321-00 | Pedro Lima | pedrolima@gmail.com |

Se não houver um atributo único natural, podemos usar uma combinação (chave composta) ou um ID artificial gerado automaticamente.

## Chave primária autonumerada

```sql
CREATE TABLE IF NOT EXISTS DEPARTAMENTOS (
  ID SERIAL PRIMARY KEY,
  NOME VARCHAR(100) NOT NULL,
  DESCRICAO VARCHAR(200) NOT NULL
);
```

Inserindo um novo registro com chaves autonumerada.

```sql
INSERT INTO DEPARTAMENTOS (NOME, DESCRICAO) VALUES 
    ('RH', 'Recursos Humanos'),
    ('TI', 'Tecnologia da Informação'),
    ('Vendas', 'Departamento de Vendas');
```

## Chave primária composta

```sql
CREATE TABLE ATENDENTES (
  ID_PESSOA BIGINT,
  ID_DEPARTAMENTO INT,
  SALARIO NUMERIC(10, 2),
  CONSTRAINT PK_ATENDENTE PRIMARY KEY (ID_PESSOA, ID_DEPARTAMENTO),
  CONSTRAINT FK_PESSOA_ATENDENTE FOREIGN KEY (ID_PESSOA) REFERENCES PESSOAS (ID),
  CONSTRAINT FK_DEPARTAMENTO_ATENDENTE FOREIGN KEY (ID_DEPARTAMENTO) REFERENCES DEPARTAMENTOS (ID),
  CONSTRAINT CK_SALARIO_ATENDENTE CHECK (SALARIO BETWEEN 2000 AND 40000)
);

INSERT INTO ATENDENTES (ID_PESSOA,ID_DEPARTAMENTO, SALARIO) VALUES 
    (6, 1, 15000.00), -- Legolas Greenleaf (ID_PESSOA 6) no RH (ID_DEPARTAMENTO 1)
    (7, 2, 35500.00), -- Éowyn de Rohan (ID_PESSOA) no TI (ID_DEPARTAMENTO 2)
    (8, 3, 8200.50);  -- Gimli, Filho de Glóin (ID_PESSOA 8) no Vendas (ID_DEPARTAMENTO 3)
    
```
