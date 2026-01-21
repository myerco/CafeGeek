---

title: EspecializaÇÃO E GENERALIZAÇÃO
excerpt: "Entenda conceitos fundamentais de bancos de dados relacionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 11
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# ESPECIALIZAÇÃO E GENERALIZAÇÃO

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Especialização
- Generalização

---

## ESPECIALIZAÇÃO

Vamos considerar a entidade Médico, ela pode ser definida em um conjunto de entidades classificados como:
- Pediatra;
- Cardiologista;
- Clínico Geral;
- Neurologista.

O processo de projetar os subgrupos dentro de um conjunto de entidades é chamado de **especialização**, o qual nos permite distinguir os tipos de Médicos.

---

## ESPECIALIZAÇÃO - DIAGRAMA


MÉDICO
├── CARDIOLOGISTA
├── PEDIATRA
└── ORTOPEDISTA

---

## GENERALIZAÇÃO

Praticamente a generalização é o inverso da especialização.

Por exemplo, imagine: a entidade **Médico** é na realidade uma generalização para diversas classes de dados de médicos.

Pode-se considerar a entidade Médico como uma **Classe (Superclasse ou Supertipo)** e suas especializações as suas **Subclasses (Subtipo)**.

É representada pelo triângulo rotulado de **ISA (isa)**. (Silberschatz)

---

## GENERALIZAÇÃO - DIAGRAMA


  MÉDICO
     │
     │ ISA
     ▼

┌─────────────────┐
│ CARDIOLOGISTA │
│ PEDIATRA │
│ ORTOPEDISTA │
└─────────────────┘

---

## Próximo tópico

- Relacionamentos

### O que foi visto

- Especialização
- Generalização
