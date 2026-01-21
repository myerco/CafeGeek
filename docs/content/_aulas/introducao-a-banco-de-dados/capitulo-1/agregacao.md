---
title: AGREGAÇÃO
excerpt: "**BANCO DE DADOS I** Marco Yerco Mendizabel Cabrera Analista de Sistemas"
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 2
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---
# AGREGAÇÃO

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Agregação

---

## AGREGAÇÃO

"Existem momentos em que temos uma visão dos dados que nos deixa dúvida de como representar um fato que está relacionado a outro fato. Isto equivaleria a dizer que um relacionamento está relacionado a outro. Mas conceitualmente, não existem relacionamentos entre relacionamentos, é uma inverdade conceitual" (Machado)

O modelo E-R não consegue expressar relacionamentos entre relacionamentos.

---

## EXEMPLO

Considere o seguinte relacionamento, onde a entidade meliante relaciona-se com a entidade vítima com cardinalidade Muitos-para-Muitos:

MELIANTE ─── VÍTIMA
N N
CHACINA

---

## EXEMPLO (CONTINUAÇÃO)

Porém o **meliante** para perpetuar o crime utiliza uma **arma**.

MELIANTE ─── VÍTIMA ARMA
N N │
CHACINA │
│
UTILIZA
N N

---

## EXEMPLO (AGREGAÇÃO)

A agregação permite que entidades de determinados tipos relacionadas entre si por meio de um relacionamento possam ser tratadas como um objeto agregado de mais alto nível:

MELIANTE ─── VÍTIMA ARMA
N N │
CHACINA │
│ │
└──────────────┘
UTILIZA
1 N

---

## EXEMPLO (MODELO FÍSICO)

Para expressar as entidades no modelo físico:

MELIANTE ─── VÍTIMA ARMA
N 1 N
│ │
└── CRIME ─────┘
1 1

---

## Próximo tópico

- Auto relacionamento

### O que foi visto

- Agregação
