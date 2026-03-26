---
title: Modelo de Entidade e Relacionamento
excerpt: "Explore o Modelo Entidade-Relacionamento (MER), entidades, atributos e sua representação em bancos de dados."
categories:
  - banco-de-Dados
  - modelo-de-dados
date: 2026-01-22T08:48:05-04:00
order: 14
tags:
  - "Banco de Dados"
  - "Conceitos Fundamentais"
sidebar:
  nav: introducao-a-banco-de-dados
---

{% include imagelocal.html
    src="introducao-a-banco-de-dados/mer.png"
    alt="Figura: Mode de Entididade e Relacionamento."
    caption="Figura: Mode de Entididade e Relacionamento."
%}

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

### Representação

**Representação Gráfica:**

No diagrama ER, as entidades são representadas por retângulos com o nome da entidade em maiúsculo.

<div class="mermaid">
erDiagram
  PESSOA
  ALUNO
  DISCIPLINA
  EMPRESTIMO
</div>

**Representação Tabular:**

Cada entidade corresponde a uma tabela no banco de dados, onde cada linha representa uma instância específica.

**Tabela ALUNO:**

| Matrícula  | Nome        | Turma | Curso    |
| ---------- | ----------- | ----- | -------- |
| 001.201501 | Ana Claudia | A     | Sistemas |
| 002.201501 | João Silva  | B     | Direito  |

---

## Atributos

Atributos são as propriedades descritivas de cada entidade. Toda entidade é definida por um conjunto de atributos que descrevem suas características.

**Definição:** "Todo objeto para ser uma entidade possui propriedades que são descritas por atributos e valores."

**Tabela PESSOAS:**

Cada instância da entidade PESSOAS terá valores específicos para seus atributos:

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

### Tipos de Atributos

#### Simples vs Compostos

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

#### Monovalorados vs Multivalorados

- **Monovalorado**: Atributo Monovalorado (ou Single-Valued):
    É um atributo que pode armazenar apenas um valor para uma entidade.
    Exemplo: Uma pessoa tem apenas uma data de nascimento, um CPF, um nome principal.
- **Multivalorado**: É um atributo que pode armazenar um conjunto de valores para uma mesma entidade.
    Exemplo: Uma pessoa pode ter vários telefones, vários e-mails, ou vários endereços.

**Atributos:**

- matricula (monovalorado) – chave primária.
- nome (monovalorado).
- data_nascimento (monovalorado).
- telefones (multivalorado) – um aluno pode ter vários números de telefone.
- emails (multivalorado) – um aluno pode ter vários e-mails.

**Importante:** No modelo relacional (tabelas), não implementamos um atributo multivalorado diretamente em uma coluna. Em vez disso, criamos uma tabela separada para representar esse relacionamento.
{: .notice}

**Implementação incorreta (não recomendada):**

Um erro comum de quem está começando é tentar colocar os multivalorados em uma única coluna, separando por vírgula:

```sql
CREATE TABLE pessoa_errado (
    id SERIAL PRIMARY KEY,
    cpf VARCHAR(14) UNIQUE,
    nome VARCHAR(100),
    data_nascimento DATE,
    telefones TEXT,  -- '1199999999, 1188888888'
    emails TEXT      -- 'joao@email.com, joao.trabalho@email.com'
);
```

| cpf            | Nome        | data_nascimento | telefones                     | emails                                    |
| -------------- | ----------- | --------------- | ----------------------------- | ----------------------------------------- |
| 001.201.501-25 | Ana Claudia | 03/02/2000      | 199999999, 1188888888         | ana@hotmail.com, ana.trabalho@email.com   |
| 002.201.501-30 | João Silva  | 20/10/2004      | (98) 8993-9999,(61) 9999-5457 | joao@hotmail.com, joao.trabalho@email.com |

**Problemas:**

- Viola a primeira forma normal (1FN), pois os valores não são atômicos.
- Dificuldade para consultar um telefone específico.
- Problemas de integridade (não podemos garantir formato único).
- Dificuldade para adicionar ou remover um telefone individualmente.

**Implementação correta:**

```sql
-- Tabela principal (monovalorados)
CREATE TABLE pessoas (
    id INTEGER PRIMARY KEY,
    cpf VARCHAR(14) UNIQUE,
    nome VARCHAR(100) NOT NULL,
    data_nascimento DATE
);

-- Tabela para telefones (multivalorado)
CREATE TABLE pessoa_telefones (
    id SERIAL PRIMARY KEY,
    id_pessoa INTEGER REFERENCES pessoas(id) ON DELETE CASCADE,
    telefone VARCHAR(20) NOT NULL,
    -- Podemos incluir um tipo (celular, residencial, comercial)
    tipo VARCHAR(20)
);

-- Tabela para emails (multivalorado)
CREATE TABLE pessoa_emails (
    id SERIAL PRIMARY KEY,
    id_pessoa INTEGER REFERENCES pessoas(id) ON DELETE CASCADE,
    email VARCHAR(100) NOT NULL UNIQUE,
    -- Flag para indicar se é o principal
    principal BOOLEAN DEFAULT FALSE
);
```

**Inserindo dados:**

```sql
-- 1. Inserir o pessoas (monovalorados)
INSERT INTO pessoas (cpf, nome, data_nascimento)
VALUES (2024001, 'Ana Maria Souza', '1995-03-12');

-- 2. Inserir os telefones (multivalorados)
INSERT INTO pessoa_telefones (id_pessoa, telefone, tipo)
VALUES 
    (1, '(11) 91234-5678', 'celular'),
    (1, '(11) 3456-7890', 'residencial');

-- 3. Inserir os e-mails (multivalorados)
INSERT INTO pessoa_emails (id_pessoa, email, principal)
VALUES 
    (1, 'ana.souza@email.com', TRUE),
    (1, 'ana.trabalho@empresa.com', FALSE);
```

**Consultas:**

```sql
SELECT p.cpf, p.nome, pt.telefone, pt.tipo
FROM pessoas p
LEFT JOIN pessoa_telefones  pt ON pt.id = p.id
WHERE p.matricula = '2024001';
```

#### Nulos

Atributos que podem não ter valor em algumas instâncias (estado civil, Grau de instrução).

```sql
CREATE TABLE pessoa_nulo (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100),
  estado_civil VARCHAR(20) NULL,
  grau_instrucao VARCHAR(30) NULL
);
```

#### Derivados

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
