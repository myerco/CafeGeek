---
title: Especialização e Generalização
excerpt: "Entenda os conceitos de especialização e generalização no modelo Entidade-Relacionamento para hierarquias de dados."
categories:
  - banco-de-dados
  - relacionamentos-avancados
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

<div class="mermaid">
graph TD
    MÉDICO --> CARDIOLOGISTA
    MÉDICO --> PEDIATRA
    MÉDICO --> ORTOPEDISTA
</div>

No modelo físico, isso pode ser implementado com tabelas separadas ou uma tabela única com discriminador.

---

### Exemplo SQL: Especialização

Neste exemplo, usaremos uma tabela única `personagem` com um campo discriminador `tipo` para representar especializações (por exemplo: mago, elfo, hobbit).

```sql
-- Criação da tabela
CREATE TABLE personagem (
  id INT PRIMARY KEY,
  nome VARCHAR(100),
  tipo VARCHAR(50) -- ex: 'Mago', 'Elfo', 'Hobbit'
);

-- Inserção de personagens do Senhor dos Anéis
INSERT INTO personagem (id, nome, tipo) VALUES (1, 'Gandalf', 'Mago');
INSERT INTO personagem (id, nome, tipo) VALUES (2, 'Legolas', 'Elfo');
INSERT INTO personagem (id, nome, tipo) VALUES (3, 'Frodo', 'Hobbit');

-- Visão para cada especialização
CREATE VIEW magos AS SELECT * FROM personagem WHERE tipo = 'Mago';
CREATE VIEW elfos AS SELECT * FROM personagem WHERE tipo = 'Elfo';
CREATE VIEW hobbits AS SELECT * FROM personagem WHERE tipo = 'Hobbit';

-- Consulta geral
SELECT * FROM personagem;
-- Consulta específica
SELECT * FROM magos;
```

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

### Exemplo SQL: Generalização

Neste exemplo, usaremos tabelas separadas para cada especialidade e uma visão para generalizar todos como "personagem".

```sql
-- Criação das tabelas
CREATE TABLE mago (
  id INT PRIMARY KEY,
  nome VARCHAR(100)
);
CREATE TABLE elfo (
  id INT PRIMARY KEY,
  nome VARCHAR(100)
);
CREATE TABLE hobbit (
  id INT PRIMARY KEY,
  nome VARCHAR(100)
);

-- Inserção de personagens do Senhor dos Anéis
INSERT INTO mago (id, nome) VALUES (1, 'Gandalf');
INSERT INTO elfo (id, nome) VALUES (2, 'Legolas');
INSERT INTO hobbit (id, nome) VALUES (3, 'Frodo');

-- Visão para generalizar todos como personagem
CREATE VIEW personagem AS
  SELECT id, nome, 'Mago' AS tipo FROM mago
  UNION ALL
  SELECT id, nome, 'Elfo' AS tipo FROM elfo
  UNION ALL
  SELECT id, nome, 'Hobbit' AS tipo FROM hobbit;

-- Consulta geral
SELECT * FROM personagem;
-- Consulta específica
SELECT * FROM personagem WHERE tipo = 'Elfo';
```

---

## Diagrama de Generalização

<div class="mermaid">
graph TD
    MÉDICO --> ISA
    ISA -->CARDIOLOGISTA
    ISA -->CARDIOLIGISTA
    ISA -->ORTOPEDISTA
ISA@{ shape: manual-file, label: "ISA"}
</div>

O triângulo "ISA" indica "é um" (ex: cardiologista é um médico).

---

## Diferenças e Aplicações

- **Especialização**: Divide uma entidade geral em específicas (top-down).
- **Generalização**: Une entidades específicas em uma geral (bottom-up).

Ambos são ferramentas para modelar herança e hierarquias no E-R.
