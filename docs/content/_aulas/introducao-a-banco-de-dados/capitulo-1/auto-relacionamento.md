---

title: Auto-RELACIONAMENTO
excerpt: "Entenda conceitos fundamentais de bancos de dados relacionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 6
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# AUTO-RELACIONAMENTO

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Auto-relacionamento

---

## AUTO-RELACIONAMENTO

É um tipo especial de relacionamento onde as entidades se relacionam com elas mesmas.

### Tipos de auto-relacionamentos:

1. Auto-relacionamento Um-para-Muitos
2. Auto-relacionamento Muitos-para-Muitos

---

## UM PARA MUITOS

Vamos considerar uma entidade Pessoas, cujas ocorrências são representativas de inúmeras pessoas de um determinado local. Entre estas inúmeras ocorrências de pessoas existem relacionamentos bem-definidos, como **É_filho_de**. Isto é, algumas pessoas são filhas de outras pessoas.

PESSOAS
│
│ TEM
│ 1 N
▼
PESSOAS

### TABELA:

**PESSOAS** (com auto-relacionamento)

---

## MUITOS PARA MUITOS

Vamos considerar o seguinte caso: em uma indústria, um produto é composto de vários outros produtos, que são componentes. Por outro lado, um produto componente pode participar da composição de muitos produtos.

Observe que isso significa estamos lidando com um único tipo de objeto produto.

PRODUTO
│
│ COMPONENTE
│ N N
▼
PRODUTO

### TABELAS:

**PRODUTOS** e **COMPONENTES** (auto-relacionamento N:N)

---

## Próximo tópico

- Normalização I

### O que foi visto

- Auto-Relacionamento
