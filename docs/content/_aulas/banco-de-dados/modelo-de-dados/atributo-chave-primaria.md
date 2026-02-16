---
title: Atributo Chave Primária
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
## Objetivos

- Compreender o conceito de chave primária.
- Identificar atributos que podem servir como chave primária.
- Entender os requisitos e exemplos de chaves primárias.

## O que é uma Chave Primária?

A chave primária é um atributo (ou conjunto de atributos) que identifica exclusivamente cada registro em uma tabela. Ela garante que não haja duplicatas e permite referenciar registros de forma única.

Em termos simples: imagine uma tabela de alunos. A matrícula de cada aluno é única — nenhum outro aluno tem a mesma matrícula. Isso faz da matrícula uma chave primária perfeita.

## Exemplo Prático

Considere a tabela `ALUNO`:

| matricula | nome          | turma |
|-----------|---------------|-------|
| 001       | João Silva    | A     |
| 002       | Maria Santos  | B     |

Aqui, o atributo `matricula` é a chave primária, pois cada valor é único e identifica um aluno específico.

<div class="mermaid">
graph TD
    A[Novo Registro: Aluno] --> B{A Matrícula já existe?}
    B -- Sim --> C[Erro: Violação de Chave Primária]
    B -- Não --> D[Registro Inserido com Sucesso]
    C --> E[Garante a Unicidade dos Dados]
    D --> E
</div>

## Requisitos de uma Chave Primária

Para ser uma chave primária válida, o atributo deve atender a estes critérios:

- **Não pode ser nulo**: Todo registro deve ter um valor para a chave primária.
- **Deve ser único**: Não pode haver dois registros com o mesmo valor.
- **Imutável**: O valor não deve mudar ao longo do tempo (idealmente).
- **É um índice**: A chave vai estar associada a uma estrutura de indexação.

Além disso, as chaves primárias são automaticamente indexadas pelo SGBD para otimizar consultas.

## Exemplo de comando SQL (PostgreSQL)

```sql
CREATE TABLE aluno (
  matricula VARCHAR(10) PRIMARY KEY,
  nome VARCHAR(100),
  turma VARCHAR(10)
);
```

## Outro Exemplo

Na tabela `PESSOA`, o CPF pode servir como chave primária, pois cada pessoa tem um CPF único.

| cpf            | nome          | idade |
|----------------|---------------|-------|
| 123.456.789-00 | Ana Costa     | 25    |
| 987.654.321-00 | Pedro Lima    | 30    |

Se não houver um atributo único natural, podemos usar uma combinação (chave composta) ou um ID artificial gerado automaticamente.

## Exemplo de chave primária autonumerada (PostgreSQL)

```sql
CREATE TABLE pessoa (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100),
  idade INTEGER
);
```

## Exemplo de chave primária composta (PostgreSQL)

```sql
CREATE TABLE matricula_disciplina (
  matricula VARCHAR(10),
  codigo_disciplina VARCHAR(10),
  ano INTEGER,
  PRIMARY KEY (matricula, codigo_disciplina, ano)
);
```
