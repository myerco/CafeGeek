---
title: Modelo de Entidade e Relacionamento
excerpt: "Explore o Modelo Entidade-Relacionamento (MER), entidades, atributos e sua representação em bancos de dados."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2026-01-22T08:48:05-04:00
order: 14
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

{% include imagelocal.html
    src="introducao-a-banco-de-dados/mer.png"
    alt="Figura: Mode de Entididade e Relacionamento."
    caption="Figura: Mode de Entididade e Relacionamento."
%}

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

## Objetos Conceituais do MER

Os principais componentes do modelo são:

1. **Entidades**: Objetos do mundo real com existência independente
2. **Atributos**: Propriedades que descrevem as entidades
3. **Relacionamentos**: Associações entre entidades
4. **Especialização/Generalização**: Hierarquias entre entidades

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

### Identificação Única

Cada entidade possui um conjunto de propriedades cujos valores devem ser únicos, permitindo identificar cada instância.

**Exemplos:**

- **Pessoa**: CPF identifica unicamente cada pessoa
- **Aluno**: Matrícula identifica dentro do contexto acadêmico
- **Empréstimo**: Número identifica cada operação

---

## Representação Gráfica das Entidades

No diagrama ER, as entidades são representadas por retângulos com o nome da entidade em maiúsculo.

<div class="mermaid">
erDiagram
  PESSOA
  ALUNO
  DISCIPLINA
  EMPRESTIMO
</div>

## Representação Tabular

Cada entidade corresponde a uma tabela no banco de dados, onde cada linha representa uma instância específica.

**Exemplo - Tabela ALUNO:**

| Matrícula  | Nome        | Turma | Curso    |
| ---------- | ----------- | ----- | -------- |
| 001.201501 | Ana Claudia | A     | Sistemas |
| 002.201501 | João Silva  | B     | Direito  |

---

## Atributos

Atributos são as propriedades descritivas de cada entidade. Toda entidade é definida por um conjunto de atributos que descrevem suas características.

**Definição:** "Todo objeto para ser uma entidade possui propriedades que são descritas por atributos e valores."

### Exemplo Prático

Cada instância da entidade PESSOA terá valores específicos para seus atributos:

| CPF   | Nome          | Sexo | Salário  | Data Nasc.  | Endereço                 | Estado Cívil | Grau de instrução  | Idade | Nota |
| ----- | ------------- | ---- | -------- | ----------- | ------------------------ | ------------ | ------------------ | ----- | ---- |
| 10001 | Frodo Baggins | M    | 1500.00  | 22/09/2980  | Bolsão, Vila dos Hobbits | Solteiro     | Ensino Médio       | 50    | 10   |
| 10002 | Samwise Gamgi | M    | 1200.00  | 06/04/2980  | Vila dos Hobbits         | Casado       | Ensino Fundamental | 38    | 9    |
| 10003 | Gandalf       | M    | 10000.00 | 01/01/2000* | Terra Média              | Nulo         | Superior           | 2019  | 10   |
| 10004 | Aragorn       | M    | 3000.00  | 01/03/2931  | Reino de Gondor          | Casado       | Superior           | 87    | 10   |
| 10005 | Legolas       | M    | 2500.00  | 01/01/2879  | Floresta das Trevas      | Solteiro     | Superior           | 221   | 9    |
| 10006 | Gimli         | M    | 2200.00  | 01/01/2879  | Montanhas Azuis          | Solteiro     | Médio              | 140   | 8    |
| 10007 | Galadriel     | F    | 9000.00  | 01/01/1362  | Lothlórien               | Casada       | Superior           | 7000  | 10   |
| 10008 | Boromir       | M    | 2000.00  | 23/06/2978  | Minas Tirith             | Solteiro     | Superior           | 41    | 8    |
| 10009 | Arwen         | F    | 2500.00  | 01/01/241   | Rivendell                | Casada       | Superior           | 2777  | 10   |
| 10010 | Saruman       | M    | 9500.00  | 01/01/2000* | Isengard                 | Nulo         | Superior           | 2019  | 7    |

*Datas fictícias e idades aproximadas para fins didáticos.

## Tipos de Atributos

### 1. Simples vs Compostos

- **Simples**: Valor indivisível (sexo, telefone)
- **Compostos**: Podem ser divididos em subpartes (nome: primeiro + último; endereço: rua + cidade + CEP)
  
```sql
-- Simples
CREATE TABLE pessoa_simples (
  id SERIAL PRIMARY KEY,
  sexo CHAR(1),
  telefone VARCHAR(20)
);

-- Composto (endereços e nomes podem ser divididos em colunas)
CREATE TABLE pessoa_composto (
  id SERIAL PRIMARY KEY,
  primeiro_nome VARCHAR(50),
  ultimo_nome VARCHAR(50),
  rua VARCHAR(100),
  cidade VARCHAR(50),
  cep VARCHAR(10)
);
```

### 2. Monovalorados vs Multivalorados

- **Monovalorado**: Um único valor (idade, data nascimento)
- **Multivalorado**: Múltiplos valores possíveis (telefones, salários históricos)

```sql
-- Monovalorado
CREATE TABLE pessoa_monovalorado (
  id SERIAL PRIMARY KEY,
  idade INTEGER,
  data_nascimento DATE
);

-- Multivalorado (relacionamento 1:N)
CREATE TABLE pessoa (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100)
);

CREATE TABLE telefone (
  id SERIAL PRIMARY KEY,
  pessoa_id INTEGER REFERENCES pessoa(id),
  numero VARCHAR(20)
);
```

### 3. Nulos

Atributos que podem não ter valor em algumas instâncias (estado civil, Grau de instrução).

```sql
CREATE TABLE pessoa_nulo (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100),
  estado_civil VARCHAR(20) NULL,
  grau_instrucao VARCHAR(30) NULL
);
```

### 4. Derivados

Valores calculados a partir de outros atributos (idade derivada da data nascimento, total derivado de itens).

```sql
CREATE TABLE pessoa_derivado (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100),
  data_nascimento DATE
);

-- Idade derivada (exemplo de view)
CREATE VIEW pessoa_idade AS
SELECT
  id,
  nome,
  data_nascimento,
  EXTRACT(YEAR FROM AGE(CURRENT_DATE, data_nascimento)) AS idade
FROM pessoa_derivado;
```

## Importância do MER

- **Abstração**: Foca no essencial do negócio
- **Comunicação**: Linguagem comum entre usuários e desenvolvedores
- **Base sólida**: Fundamento para implementação em qualquer SGBD
- **Flexibilidade**: Independente de tecnologia específica

O Modelo ER é a base para projetar bancos de dados que refletem com precisão o mundo real que representam.
