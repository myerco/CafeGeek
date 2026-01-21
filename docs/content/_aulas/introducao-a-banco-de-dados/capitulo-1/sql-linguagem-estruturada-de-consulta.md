---

title: Sql - Linguagem Estruturada de Consulta
excerpt: "Entenda conceitos fundamentais de bancos de dados relacionais."
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

# SQL - Linguagem Estruturada de Consulta

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Create
- Describe
- Insert
- Select

---

## CREATE

Para construir o objeto no banco de dados utilizamos um comando DDL.

### ```
CREATE TABLE

```sql
```
CREATE TABLE pessoa (
    cpf varchar(13),
    nome varchar(40),
    sexo char(1),
    Salario number(8,2),
    DataNasc date
);
```

```
CREATE TABLE aluno (
    matricula varchar(10),
    nome varchar(40),
    turma varchar(20),
    curso varchar(40)
);
```

```
CREATE TABLE emprestimo (
    numero number(8),
    dt_emprestimo date,
    valor number(8,2),
    cliente varchar(40)
);
```

DESCRIBE

Verificando a estrutura das tabelas.
Exemplos:
sql

DESCRIBE pessoa;
DESC aluno;
DESC emprestimo;

DESCRIBE (Alterando a estrutura das tabelas)
sql

ALTER TABLE pessoa ADD telefone varchar(15);
```
ALTER TABLE aluno ADD sexo char(1);
```
ALTER TABLE emprestimo ADD conta varchar(10);
```

INSERT

Inserindo dados.
Exemplos:
sql

```
INSERT INTO pessoa VALUES ('001','João','M',1000, '21/06/1989');
```

```
INSERT INTO aluno (matricula, nome) VALUES ('001.201501','Ana Claudia Nunes');
```

```
INSERT INTO emprestimo (dt_emprestimo, valor, numero, cliente)
VALUES ('08/12/2015',1500,100201501,'Hugo Silva');
```

```
SELECT

Listando dados.
Exemplos:
sql

```
SELECT * FROM pessoa;

```
SELECT matricula, nome FROM aluno;

```
SELECT numero, cliente FROM emprestimo ORDER BY numero;

PRÓXIMO TÓPICO

    Atributo chave primária

O que foi visto:

    Comandos para definição e manipulação de entidades:

        Create

        Describe

        Insert

        Select

Faça o exercício


## Próximo tópico
- [Próximo conceito]

### O que foi visto
- Conceitos abordados neste tópico