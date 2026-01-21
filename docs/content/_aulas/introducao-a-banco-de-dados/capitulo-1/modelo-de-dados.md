---

title: Modelo De Dados
excerpt: "Entenda conceitos fundamentais de bancos de dados relacionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 13
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# MODELO DE DADOS

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Modelos de dados
- Tipos de modelos
- Linguagem de manipulação de dados
- Definição de SQL

---

## CONCEITO

"Sob a estrutura do banco de dados está o modelo de dados: um conjunto de ferramentas conceituais usadas para a descrição de dados, relacionamentos entre dados, semântica de dados e regras de consistência."

Classificam em 3 grupos de:
1. Modelos lógicos com base em objetos
2. Modelos lógicos com base em registros
3. Modelos Físicos

---

## MODELO DE DADOS

**Modelos lógicos com base em objetos**:
1. Modelo de Entidade de Relacionamento
2. Modelo Orientado a objetos

---

## M.E.R

A disciplina abordará o **Modelo de Entidade de Relacionamento** por ser o modelo mais utilizado atualmente.

---

## LINGUAGENS DE BANCO DE DADOS

1. **Linguagem de Definição de Dados (DDL)**
   Um esquema de dados é especificado por um conjunto de definições expressas por uma linguagem especial chamada linguagem de definição de dados. O resultado da compilação dos parâmetros DDLs é armazenado em um conjunto de tabelas que constituem um arquivo (esquema) especial chamado dicionário de dados.

2. **Linguagem de Manipulação de dados (DML)**
   É a linguagem que viabiliza o acesso ou manipulação dos dados de forma compatível ao modelo de dados apropriado.

---

## DDL - Principais comandos:

- CREATE
- DROP
- ALTER

### Exemplo:

```sql
```
CREATE TABLE tabela (
    campo1 tipo,
    campo2 tipo
);
```

ALTER TABLE tabela ADD campo3 tipo;

DROP TABLE tabela;

DML - Principais comandos:

    INSERT

    ```
DELETE

    ```
UPDATE

    ```
SELECT

Exemplo:
sql

```
INSERT INTO tabela VALUES (valor1, valor2, valor3);
```

```
UPDATE tabela SET campo1 = valor1;

```
DELETE FROM tabela;

```
SELECT * FROM tabela;

SQL

Structured Query Language (Linguagem de Consulta Estruturada ou SQL) é a linguagem de pesquisa declarativa padrão para banco de dados relacional (base de dados relacional). Muitas das características originais do SQL foram inspiradas na álgebra relacional.
SQL DEVELOPER

(Interface gráfica do SQL Developer)

    Abre um painel

    Comando

    Executa

PRÓXIMO TÓPICO

    Usuários de banco de dados

O que foi visto:

    Modelos de dados

    Tipos de modelos

    Linguagem de manipulação de dados

    Definição de SQL


## Próximo tópico
- [Próximo conceito]

### O que foi visto
- Conceitos abordados neste tópico