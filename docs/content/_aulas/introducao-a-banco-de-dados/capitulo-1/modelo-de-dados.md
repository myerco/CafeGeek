---
title: Modelo de Dados
excerpt: "Explore os tipos de modelos de dados, linguagens DDL e DML, e a definição de SQL em bancos de dados relacionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2026-01-22T08:48:05-04:00
order: 13
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Objetivos

- Compreender o conceito de modelo de dados.
- Identificar tipos de modelos (lógicos e físicos).
- Explorar linguagens DDL e DML.
- Entender a definição e uso de SQL.

## O que é um Modelo de Dados?

Um modelo de dados é um conjunto de ferramentas conceituais para descrever dados, relacionamentos, semântica e regras de consistência. Ele serve como ponte entre o mundo real e a implementação técnica do banco de dados.

**Classificações principais:**

1. **Modelos lógicos com base em objetos**: Focam em entidades e relacionamentos.
2. **Modelos lógicos com base em registros**: Usam tabelas e campos.
3. **Modelos físicos**: Descrevem armazenamento em disco, índices, etc.

---

## Modelos Lógicos com Base em Objetos

- **Modelo de Entidade de Relacionamento (E-R)**: O mais usado. Representa entidades, atributos e relacionamentos.
- **Modelo Orientado a Objetos**: Integra conceitos de OOP (herança, encapsulamento).

Esta disciplina foca no **Modelo E-R** devido à sua simplicidade e poder para bancos relacionais.

---

## Linguagens de Banco de Dados

Duas linguagens principais interagem com o modelo de dados:

1. **Linguagem de Definição de Dados (DDL)**: Define a estrutura do banco (tabelas, índices, restrições).
2. **Linguagem de Manipulação de Dados (DML)**: Manipula os dados (inserir, consultar, atualizar, excluir).

---

## DDL - Principais Comandos

- `CREATE`: Cria objetos (tabelas, índices).
- `DROP`: Remove objetos.
- `ALTER`: Modifica objetos existentes.

**Exemplo:**

```sql
CREATE TABLE tabela (
    campo1 INT,
    campo2 VARCHAR(50)
);

ALTER TABLE tabela ADD campo3 DATE;

DROP TABLE tabela;
```

## DML - Principais Comandos

- `INSERT`: Adiciona registros.
- `UPDATE`: Modifica registros.
- `DELETE`: Remove registros.
- `SELECT`: Consulta dados.

**Exemplo:**

```sql
INSERT INTO tabela VALUES (1, 'Exemplo');

UPDATE tabela SET campo2 = 'Novo' WHERE campo1 = 1;

DELETE FROM tabela WHERE campo1 = 1;

SELECT * FROM tabela;
```

## O que é SQL?

SQL (Structured Query Language) é a linguagem padrão para bancos de dados relacionais. Declarativa, permite consultas e manipulações inspiradas na álgebra relacional.

**Ferramentas como SQL Developer** oferecem interface gráfica para executar comandos SQL, facilitando o aprendizado e depuração.

## Benefícios dos Modelos de Dados

- Estruturação clara dos dados.
- Facilita comunicação entre desenvolvedores e usuários.
- Suporte a integridade e consistência.
- Base para implementação eficiente em SGBDs.
