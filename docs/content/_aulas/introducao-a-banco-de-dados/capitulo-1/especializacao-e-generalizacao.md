---
title: Especialização e Generalização
excerpt: "Entenda os conceitos de especialização e generalização no modelo Entidade-Relacionamento para hierarquias de dados."
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

## Objetivos

- Compreender os conceitos de especialização e generalização.
- Identificar quando aplicá-los em modelagem de dados.
- Aplicar em exemplos práticos com diagramas.


## O que é Especialização?

Especialização é o processo de dividir uma entidade geral em subgrupos mais específicos, baseados em características distintas. Isso permite representar hierarquias onde subclasses herdam atributos da superclasse, mas têm propriedades únicas.

**Por que usar?**

- Organiza dados de forma hierárquica.
- Evita redundância de atributos comuns.
- Facilita consultas específicas por tipo.

---

## Exemplo de Especialização

Considere a entidade `MÉDICO`. Ela pode ser especializada em:
- Pediatra (atende crianças).
- Cardiologista (especialista em coração).
- Clínico Geral (atendimento geral).
- Neurologista (sistema nervoso).

Cada especialidade herda atributos comuns (nome, CRM), mas tem atributos específicos (ex: cardiologista tem "anos de experiência em cirurgia").

---

## Diagrama de Especialização

```text
MÉDICO
├── CARDIOLOGISTA
├── PEDIATRA
└── ORTOPEDISTA
```

No modelo físico, isso pode ser implementado com tabelas separadas ou uma tabela única com discriminador.

---

## O que é Generalização?

Generalização é o inverso da especialização: agrupa entidades similares em uma superclasse comum. É útil quando várias entidades compartilham atributos e comportamentos.

**Por que usar?**

- Reduz duplicação de dados.
- Simplifica o modelo quando entidades são muito parecidas.
- Representa conceitos abstratos.

---

## Exemplo de Generalização

Imagine entidades separadas: `CARDIOLOGISTA`, `PEDIATRA`, `ORTOPEDISTA`. Elas podem ser generalizadas em `MÉDICO`, que é a superclasse.

A entidade `MÉDICO` é uma generalização, e as especialidades são subclasses.

---

## Diagrama de Generalização

```text
  MÉDICO
     │
     │ ISA
     ▼
┌─────────────────┐
│ CARDIOLOGISTA  │
│ PEDIATRA       │
│ ORTOPEDISTA     │
└─────────────────┘
```

O triângulo "ISA" indica "é um" (ex: cardiologista é um médico).

---

## Diferenças e Aplicações

- **Especialização**: Divide uma entidade geral em específicas (top-down).
- **Generalização**: Une entidades específicas em uma geral (bottom-up).

Ambos são ferramentas para modelar herança e hierarquias no E-R.

