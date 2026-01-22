---
title: SQL - Linguagem Estruturada de Consulta
excerpt: "Explore os comandos fundamentais de SQL: CREATE, DESCRIBE, INSERT e SELECT para manipulação de dados."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 20
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Objetivos

- Compreender os comandos básicos de SQL.
- Aprender a criar tabelas com CREATE TABLE.
- Explorar DESCRIBE para visualizar estruturas.
- Praticar inserção de dados com INSERT.
- Realizar consultas básicas com SELECT.

## O que é SQL?

SQL (Structured Query Language) é a linguagem padrão para trabalhar com bancos de dados relacionais. Ela permite definir estruturas de dados, manipular informações e realizar consultas complexas.

**Comandos principais abordados:**

- DDL: CREATE, ALTER, DROP
- DML: INSERT, UPDATE, DELETE, SELECT
- DCL: GRANT, REVOKE

## CREATE TABLE - Criando Estruturas

O comando CREATE TABLE define a estrutura de uma nova tabela no banco de dados.

**Sintaxe básica:**

```sql
CREATE TABLE nome_tabela (
    coluna1 tipo_dado(tamanho),
    coluna2 tipo_dado(tamanho),
    ...
);
```

**Exemplo prático - Tabela pessoa:**

```sql
CREATE TABLE pessoa (
    cpf varchar(13),
    nome varchar(40),
    sexo char(1),
    salario number(8,2),
    data_nasc date
);
```

**Exemplo - Tabela aluno:**

```sql
CREATE TABLE aluno (
    matricula varchar(10),
    nome varchar(40),
    turma varchar(20),
    curso varchar(40)
);
```

**Exemplo - Tabela empréstimo:**

```sql
CREATE TABLE emprestimo (
    numero number(8),
    dt_emprestimo date,
    valor number(8,2),
    cliente varchar(40)
);
```

## DESCRIBE - Visualizando Estruturas

O comando DESCRIBE (ou DESC) mostra a estrutura de uma tabela existente.

**Sintaxe:**

```sql
DESCRIBE nome_tabela;
-- ou
DESC nome_tabela;
```

**Exemplos:**

```sql
DESCRIBE pessoa;
DESC aluno;
DESC emprestimo;
```

### ALTER TABLE - Modificando Estruturas

Para adicionar colunas a uma tabela existente:
```sql
ALTER TABLE pessoa ADD telefone varchar(15);
ALTER TABLE aluno ADD sexo char(1);
ALTER TABLE emprestimo ADD conta varchar(10);
```

## INSERT - Inserindo Dados

O comando INSERT adiciona novos registros às tabelas.

**Sintaxe completa:**

```sql
INSERT INTO nome_tabela VALUES (valor1, valor2, ...);
```

**Sintaxe com colunas específicas:**

```sql
INSERT INTO nome_tabela (coluna1, coluna2) VALUES (valor1, valor2);
```

**Exemplos práticos:**

```sql
INSERT INTO pessoa VALUES ('001','João','M',1000, '21/06/1989');

INSERT INTO aluno (matricula, nome) VALUES ('001.201501','Ana Claudia Nunes');

INSERT INTO emprestimo (dt_emprestimo, valor, numero, cliente)
VALUES ('08/12/2015',1500,100201501,'Hugo Silva');
```

## SELECT - Consultando Dados

O comando SELECT recupera dados das tabelas.

**Sintaxe básica:**

```sql
SELECT colunas FROM nome_tabela;
```

**Selecionar todas as colunas:**

```sql
SELECT * FROM nome_tabela;
```

**Exemplos:**

```sql
SELECT * FROM pessoa;

SELECT matricula, nome FROM aluno;

SELECT numero, cliente FROM emprestimo ORDER BY numero;
```

### ORDER BY - Ordenação

A cláusula ORDER BY organiza os resultados:

```sql
SELECT numero, cliente FROM emprestimo ORDER BY numero;
```

## Exercícios Práticos

Para praticar os comandos aprendidos:

1. Crie uma tabela `produto` com campos: codigo, nome, preco, estoque
2. Use DESCRIBE para verificar a estrutura
3. Insira alguns produtos na tabela
4. Faça consultas para listar todos os produtos e produtos ordenados por preco

## Benefícios do SQL

- **Padronização**: Linguagem universal para bancos relacionais
- **Simplicidade**: Sintaxe intuitiva para operações complexas
- **Flexibilidade**: Suporte a consultas simples e avançadas
- **Integração**: Compatível com diversas linguagens de programação

Dominar estes comandos básicos é fundamental para trabalhar com bancos de dados relacionais.