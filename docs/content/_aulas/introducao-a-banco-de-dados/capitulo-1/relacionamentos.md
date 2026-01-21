---

title: Relacionamentos
excerpt: "Entenda conceitos fundamentais de bancos de dados relacionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 17
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# RELACIONAMENTOS

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Relacionamentos
- Exemplos

---

## RELACIONAMENTOS

"Um relacionamento é uma associação entre uma ou várias entidades".

Por exemplo, imagine: podemos definir um relacionamento que associa o cliente **ROMÁRIO** com o empréstimo **L-15**. Esse relacionamento especifica que cliente ROMÁRIO é um cliente com o empréstimo número L-15.

---

## REPRESENTAÇÃO

São representados por elipses:

CLIENTE EMPRÉSTIMO
○ ────────── ○

### TABELAS

**CLIENTE**
**EMPRÉSTIMO**

---

## EXEMPLO DE RELACIONAMENTO

Podemos citar duas entidades "distintas" que se relacionam:
- Entidade **Homens**
- Entidade **Mulheres**

Estas entidades estão relacionadas através do **casamento***.

HOMENS ──── MULHERES

---

## OUTRO EXEMPLO

As pessoas **Moram** em Apartamentos;
Os apartamentos **Formam** Condomínios;
Os Condomínios **Localizam-se** em Ruas ou Avenidas;
As Avenidas e Ruas **Estão** em uma Cidade.

*Obs: Perceba que os relacionamentos são construídos com verbos.*

PESSOAS ──┐
│
APARTAMENTOS ──┐
│
CONDOMÍNIOS ──┐
│
RUAS ─┴─ AVENIDAS

---

## EXEMPLO: ALUNOS


ALUNO ─── TURMA ─── DISCIPLINA ─── PROFESSOR

---

## EXEMPLO: VENDAS


CLIENTE ─── NOTA FISCAL ─── PRODUTO ─── VENDEDOR

---

## EXPRESSÃO RELACIONAL

O relacionamento efetiva-se através de uma expressão relacional que indica como deve ser feita a comparação entre os campos comuns às Entidades, só que agora com uma característica diferente.

A comparação é realizada entre campos das entidades e campos do relacionamento, formando uma expressão composta:

(aluno.matricula = turma.matriculaAluno)
(aluno.sexo = sexo.descricao)

---

## EXPRESSÃO - DIAGRAMA COM CARDINALIDADE


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

- Restrições

### O que foi visto

- Relacionamentos
