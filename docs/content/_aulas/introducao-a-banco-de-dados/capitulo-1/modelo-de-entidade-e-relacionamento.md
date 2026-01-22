---
title: Modelo de Entidade e Relacionamento
excerpt: "Explore o Modelo Entidade-Relacionamento (MER), entidades, atributos e sua representação em bancos de dados."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 14
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Objetivos

- Compreender o Modelo Entidade-Relacionamento (MER).
- Identificar entidades e seus atributos.
- Explorar tipos de atributos e suas características.
- Aprender a representação gráfica e tabular das entidades.

---

## O que é o Modelo Entidade-Relacionamento?

O Modelo Entidade-Relacionamento (MER) é uma técnica de modelagem conceitual que representa o mundo real através de objetos chamados entidades e seus relacionamentos.

**Definição:** "O Modelo Entidade-Relacionamento tem por base a percepção de que o mundo real é formado por um conjunto de objetos chamados entidades e pelo conjunto dos relacionamentos entre esses objetos."

Este modelo permite criar esquemas puramente conceituais sobre a essência de um sistema, focando no negócio e não em procedimentos técnicos.

---

## Objetos Conceituais do MER

Os principais componentes do modelo são:

1. **Entidades**: Objetos do mundo real com existência independente
2. **Atributos**: Propriedades que descrevem as entidades
3. **Relacionamentos**: Associações entre entidades
4. **Especialização/Generalização**: Hierarquias entre entidades

---

## Entidades

Uma entidade é qualquer objeto do mundo real que possui identificação distinta e significado próprio no contexto do negócio.

**Características:**

- Existência independente
- Conjunto de propriedades únicas
- Representa "coisas" do negócio

**Exemplos de entidades:**

- Pessoas em uma empresa
- Empréstimos bancários
- Alunos matriculados
- Disciplinas oferecidas

---

### Identificação Única

Cada entidade possui um conjunto de propriedades cujos valores devem ser únicos, permitindo identificar cada instância.

**Exemplos:**

- **Pessoa**: CPF identifica unicamente cada pessoa
- **Aluno**: Matrícula identifica dentro do contexto acadêmico
- **Empréstimo**: Número identifica cada operação

---

## Representação Gráfica das Entidades

No diagrama ER, as entidades são representadas por retângulos com o nome da entidade em maiúsculo.

```text
┌─────────────┐ ┌──────────┐ ┌─────────────┐ ┌──────────────┐
│   PESSOA    │ │  ALUNO   │ │ DISCIPLINA  │ │ EMPRÉSTIMO   │
└─────────────┘ └──────────┘ └─────────────┘ └──────────────┘
```

---

## Representação Tabular

Cada entidade corresponde a uma tabela no banco de dados, onde cada linha representa uma instância específica.

**Exemplo - Tabela ALUNO:**

| Matrícula   | Nome          | Turma | Curso     |
|-------------|---------------|-------|-----------|
| 001.201501 | Ana Claudia   | A     | Sistemas  |
| 002.201501 | João Silva    | B     | Direito   |

---

## Atributos

Atributos são as propriedades descritivas de cada entidade. Toda entidade é definida por um conjunto de atributos que descrevem suas características.

**Definição:** "Todo objeto para ser uma entidade possui propriedades que são descritas por atributos e valores."

### Exemplo Prático

Cada instância da entidade PESSOA terá valores específicos para seus atributos:

| CPF  | Nome    | Sexo | Salário   | Data Nasc. |
|------|---------|------|-----------|------------|
| 001  | João    | M    | 1000.00   | 21/06/1989 |

---

## Tipos de Atributos

### 1. Simples vs Compostos

- **Simples**: Valor indivisível (sexo, telefone)
- **Compostos**: Podem ser divididos em subpartes (nome: primeiro + último; endereço: rua + cidade + CEP)

### 2. Monovalorados vs Multivalorados

- **Monovalorado**: Um único valor (idade, data nascimento)
- **Multivalorado**: Múltiplos valores possíveis (telefones, salários históricos)

### 3. Nulos

Atributos que podem não ter valor em algumas instâncias (estado civil, fax).

### 4. Derivados

Valores calculados a partir de outros atributos (idade derivada da data nascimento, total derivado de itens).

---

## Importância do MER

- **Abstração**: Foca no essencial do negócio
- **Comunicação**: Linguagem comum entre usuários e desenvolvedores
- **Base sólida**: Fundamento para implementação em qualquer SGBD
- **Flexibilidade**: Independente de tecnologia específica

O Modelo ER é a base para projetar bancos de dados que refletem com precisão o mundo real que representam.
