---
title: Relacionamentos
excerpt: "Explore os tipos de relacionamentos entre entidades em bancos de dados: 1:1, 1:N e N:N."
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

## Objetivos

- Compreender o conceito de relacionamentos entre entidades.
- Identificar os tipos de relacionamentos: 1:1, 1:N, N:N.
- Aprender a representação gráfica e implementação em tabelas.
- Explorar exemplos práticos de relacionamentos.

## O que são Relacionamentos?

Relacionamentos são associações estabelecidas entre entidades no modelo de dados. Eles representam como as entidades se conectam no mundo real.

**Definição:** "Um relacionamento é uma associação entre uma ou várias entidades."

### Exemplo Básico

Um cliente pode estar associado a um empréstimo específico. Esta associação cria um relacionamento entre as entidades CLIENTE e EMPRÉSTIMO.

## Representação Gráfica

No Modelo Entidade-Relacionamento, relacionamentos são representados por losangos conectando as entidades:

```text
┌─────────┐     ┌────────────┐
│ CLIENTE │ ──○ │ EMPRÉSTIMO │
└─────────┘     └────────────┘
```

O losango (○) representa o relacionamento, e as linhas conectam às entidades participantes.

## Tipos de Relacionamentos

### Relacionamento 1:1 (Um para Um)

Cada instância de uma entidade se relaciona com no máximo uma instância da outra entidade.

**Exemplo:** Um cidadão possui um CPF único.

- Um PESSOA → Um CPF
- Um CPF → Uma PESSOA

```
┌─────────┐     ┌─────┐
│ PESSOA  │ ──○ │ CPF │
└─────────┘     └─────┘
      1             1
```

### Relacionamento 1:N (Um para Muitos)

Uma instância da entidade A pode se relacionar com múltiplas instâncias da entidade B, mas cada instância de B se relaciona com apenas uma de A.

**Exemplo:** Um cliente pode ter vários empréstimos, mas cada empréstimo pertence a apenas um cliente.
- Um CLIENTE → Muitos EMPRÉSTIMOS
- Um EMPRÉSTIMO → Um CLIENTE

```text
┌─────────┐     ┌────────────┐
│ CLIENTE │ ──○ │ EMPRÉSTIMO │
└─────────┘     └────────────┘
      1             N
```

### Relacionamento N:N (Muitos para Muitos)

Instâncias de ambas as entidades podem se relacionar com múltiplas instâncias da outra.

**Exemplo:** Alunos matriculados em disciplinas.

- Um ALUNO → Muitas DISCIPLINAS
- Uma DISCIPLINA → Muitos ALUNOS

```text
┌─────────┐     ┌─────────────┐
│  ALUNO  │ ──○ │ DISCIPLINA │
└─────────┘     └─────────────┘
      N             N
```

## Implementação em Tabelas
Relacionamentos são implementados através de chaves estrangeiras (FK - Foreign Key).

### 1:1 - Chave Estrangeira Opcional

```text
CLIENTE (PK: id_cliente)
- id_cliente
- nome
- cpf (FK para PESSOA, opcional)

PESSOA (PK: cpf)
- cpf
- nome_completo
- data_nascimento
```

### 1:N - Chave Estrangeira no Lado "Muitos"

```text
CLIENTE (PK: id_cliente)
- id_cliente
- nome
- endereco

EMPRESTIMO (PK: id_emprestimo)
- id_emprestimo
- valor
- data
- id_cliente (FK para CLIENTE)
```

### N:N - Tabela Associativa

```
ALUNO (PK: matricula)
- matricula
- nome

DISCIPLINA (PK: codigo)
- codigo
- nome
- carga_horaria

MATRICULA (PK: matricula + codigo)
- matricula (FK para ALUNO)
- codigo (FK para DISCIPLINA)
- semestre
- nota
```

## Exemplos Práticos

### Sistema Acadêmico

```text
ALUNO ─── MATRICULA ─── DISCIPLINA ─── PROFESSOR
  1              N              1           1
     N                       N
```

- Um aluno pode se matricular em várias disciplinas
- Uma disciplina pode ter vários alunos matriculados
- Cada disciplina é ministrada por um professor
- Um professor pode ministrar várias disciplinas

### Sistema de Vendas

```
CLIENTE ─── PEDIDO ─── ITEM_PEDIDO ─── PRODUTO
  1            1              N             1
     1         N                          N
```

- Um cliente pode fazer vários pedidos
- Cada pedido pertence a um cliente
- Um pedido pode conter vários itens
- Cada item refere-se a um produto
- Um produto pode estar em vários pedidos

## Cardinalidade e Participação

- **Cardinalidade:** Número mínimo e máximo de ocorrências (1:1, 1:N, N:N)
- **Participação:**
  - **Total:** Toda instância deve participar (linha obrigatória)
  - **Parcial:** Participação é opcional (linha pode ser nula)

## Benefícios dos Relacionamentos

- **Integridade referencial:** Garante consistência entre tabelas
- **Evita redundância:** Dados compartilhados corretamente
- **Consultas complexas:** Permite JOINs e análises avançadas
- **Manutenção:** Mudanças centralizadas

Relacionamentos são fundamentais para criar bancos de dados relacionais eficientes e consistentes.
