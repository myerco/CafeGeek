---
title: CHAVE ESTRANGEIRA
excerpt: "**BANCO DE DADOS I** Marco Yerco Mendizabel Cabrera Analista de Sistemas"
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 8
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---
# CHAVE ESTRANGEIRA

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Chave estrangeira

---

## CHAVE ESTRANGEIRA

É uma coluna ou conjunto de colunas incluídas na definição das regras de integridade referencial, que referenciam uma **"CHAVE REFERENCIADA"**.

### Definições:

- **Chave Referenciada**: É uma chave primária da mesma ou diferente tabela que é referenciada por uma chave estrangeira.
- **Tabela dependente ou filha**: É uma tabela que contém uma chave estrangeira.
- **Tabela pai**: É referenciada por uma tabela filha através de uma chave estrangeira.

---

## DIAGRAMA COM CHAVES


ALUNO ─── TURMA ─── DISCIPLINA ─── PROFESSOR
1 1 N N
N 1

PK - Matricula
PK - NumeroTurma
FK - MatriculaAluno
FK - CodDisciplina
FK - MatriculaProfessor
PK - Cod
PK - Matricula

---

## Próximo tópico

- Agregação

### O que foi visto

- Chave estrangeira
