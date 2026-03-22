---
title: SQL - Linguagem Estruturada de Consulta
excerpt: "Explore os comandos fundamentais de SQL: CREATE, DESCRIBE, INSERT e SELECT para manipulação de dados."
categories:
  - banco-de-Dados
  - sql-linguagem-estruturada-de-consulta
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

## CREATE TABLE

O comando CREATE TABLE define a estrutura de uma nova tabela no banco de dados.

**Sintaxe básica:**

```sql
CREATE TABLE nome_tabela (
    coluna1 tipo_dado(tamanho),
    coluna2 tipo_dado(tamanho),
    ...
);
```

**Exemplo - Tabela pessoas:**

```sql
CREATE TABLE pessoas (
    cpf varchar(13),
    nome varchar(40),
    sexo char(1),
    salario number(8,2),
    data_nasc date
);

CREATE TABLE sexo (
  id varchar(1),
  descricao varchar(10)
)

```

**Exemplo - Tabela alunos:**

```sql
CREATE TABLE alunos (
    matricula varchar(10),
    nome varchar(40),
    turma varchar(20),
    curso varchar(40)
);
```

**Exemplo - Tabela empréstimo:**

```sql
CREATE TABLE emprestimos (
    numero number(8),
    dt_emprestimo date,
    valor number(8,2),
    cliente varchar(40)
);
```

## DESCRIBE

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

### ALTER TABLE 

Para adicionar colunas a uma tabela existente:

```sql
ALTER TABLE pessoas ADD telefone varchar(15);
ALTER TABLE alunos ADD sexo char(1);
ALTER TABLE emprestimos ADD conta varchar(10);
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

**Exemplos :**

```sql
INSERT INTO pessoas VALUES ('001','João','M',1000, '21/06/1989');

INSERT INTO alunos (matricula, nome) VALUES ('001.201501','Ana Claudia Nunes');
INSERT INTO alunos (matricula, nome) VALUES ('002.589.57','Frodo Baggins');

INSERT INTO emprestimos (dt_emprestimo, valor, numero, cliente)
VALUES ('08/12/2015',1500,100201501,'Hugo Silva');

INSERT INTO sexo (id, descricao) VALUES ('M', 'Masculino');
INSERT INTO sexo (id, descricao) VALUES ('F', 'Feminino');

```

## SELECT

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
SELECT * FROM pessoas;

SELECT matricula, nome FROM alunos;

SELECT numero, cliente FROM emprestimos ORDER BY numero;

select * from pessoas where cpf = '001';

select * from pessoas where nome = 'João';

select * from alunos where matricula

-- Quando se utiliza "=", o resultado precisa ser exatamente igual ao que foi pedido
-- Nesse caso, se tiver um valor 'Frodo Baggins', ele não
-- será retornado porque 'Frodo Baggins' != 'Frodo'

select nome, sexo from pessoas nome like 'J%';
-- O "like" significa que não precisa ser exatamente igual, mas
-- parecido. A "%" indica que depois de "Frodo" pode ter qualquer
-- outra coisa escrita, mas tem que começar com Frodo

select nome, sexo from pessoas nome like '%Claudia%';

```

**Selecionando duas tabelas**

```sql
-- O resultado é a multiplicação das colunas e linhas das duas tabelas
select * from pessoas, alunos;

-- Juntando corretamente as tabelas
select from pessoas, sexo where pessoas.sexo = sexo.id;

-- No exemplo abaixo usando alias "AS" ou "apelido" para as colunas e tabelas
SELECT A.NOME AS "Nome do aluno"
  , B.DESCRICAO AS "Sexo do aluno"
FROM PESSOAS A JOIN SEXO B ON (B.ID = A.ID_SEXO)

```

### ORDER BY

A cláusula ORDER BY organiza os resultados:

```sql
SELECT numero, cliente FROM emprestimos ORDER BY numero;
```

## UPDATE

O comando update altera registros existentes.

**Sintaxe:**

```sql
UPDATE nome_tabela SET coluna1 = valor1, coluna2 = valor2 WHERE condição;
```

**Exemplo:**

```sql
update pessoas
set sexo = 'M'
where cpf = '001';

update alunos
set sexo = 'F'
where matricula = '001.201501';
```

## DELETE

O comando DELETE FROM nome_tabela WHERE condição;

**Sintaxe completa:**

```sql
delete from nome_tabela where coluna1 = valor1;
```

**Exemplo:**

```sql
delete from pessoas where cpf = '001';

delete from alunos where matricula = '001.201501';
```

## GROUP BY

Comandos de grupo group by agrupam linhas baseadas em um ou mais campos.

**Sintaxe:**

```sql
select campo1, campo2, função_grupo
from tabela
group by campo1, campo2
```

```sql

-- Contando todos as pessoas
select count(*) from pessoas;

-- Apresentando todos as pessoas por sexo
select sexo, count(*) from pessoas group by sexo;

-- Valor máximo da data de nascimento
select max(data_nasc) from pessoas;

-- Valor mínimo da data de nascimento
select min(data_nasc) from pessoas;

-- Valor médio dos salários
select avg(salario) from pessoas;

-- Somatório dos salários
select sum(salario) from pessoas;

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
