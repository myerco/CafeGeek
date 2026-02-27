---
title: Restrições de Integridade
excerpt: "Entenda as principais restrições de integridade em bancos de dados relacionais, exemplos práticos e comandos SQL."
categories:
  - banco-de-Dados
  - modelo-de-dados
date: 2026-01-22T08:48:05-04:00
order: 8
tags:
    - banco-de-dados
sidebar:
    nav: introducao-a-banco-de-dados
---

## Objetivos

- Compreender o conceito de restrições de integridade.
- Identificar os principais tipos de restrições.
- Visualizar exemplos práticos e comandos SQL.

No Modelo Entidade-Relacionamento (MER), as restrições de integridade são regras que garantem que a informação armazenada seja precisa, consistente e confiável. Sem elas, o banco de dados se torna uma "sucata digital" cheia de informações órfãs ou contraditórias.

## Integridade de Domínio

A **Integridade de Domínio** define os valores válidos para um atributo específico. Ela garante que todos os dados em uma coluna pertençam a um conjunto de valores permitido (tipo de dado, formato, intervalo).

No PostgreSQL, aplicamos isso através de:

- **Tipos de Dados:** `INTEGER`, `VARCHAR`, `DATE`.
- **Constraints:** `NOT NULL` (não aceita vazios) e `CHECK` (valida condições).

### Exemplo Prático integridade de domínio

Imagine uma tabela de `Produtos` onde o preço não pode ser negativo.

**Tabela de Produtos:**

| ID   | Nome    | Preço  | Categoria                    |
| :--- | :------ | :----- | :--------------------------- |
| 1    | Teclado | 150.00 | Eletrônicos                  |
| 2    | Mouse   | -5.00  | **ERRO! Violaria o domínio** |

**Comando SQL (PostgreSQL):**

```sql
CREATE TABLE IF NOT EXISTS produtos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    preco NUMERIC(10, 2) CHECK (preco > 0), -- Restrição de Domínio
    categoria VARCHAR(50) DEFAULT 'Geral'
);

```

## Integridade Referencial

A **Integridade Referencial** garante que as relações entre as tabelas permaneçam consistentes. Em termos simples: se a Tabela A aponta para a Tabela B (via Chave Estrangeira), o registro na Tabela B **deve existir**.

Ela impede que tenhamos "registros órfãos" (ex: um pedido de um cliente que não está cadastrado).

### Exemplo Prático integridade referêncial

Temos as tabelas `Clientes` e `Pedidos`. Um pedido só pode existir se estiver vinculado a um cliente real.

**Tabela Clientes:**

| cliente_id (PK) | Nome      |
| :-------------- | :-------- |
| 10              | Ana Silva |

**Tabela de Pedidos:**

| pedido_id | cliente_id (FK) | Valor                           |
| :-------- | :-------------- | :------------------------------ |
| 501       | 10              | 250.00                          |
| 502       | 99              | **ERRO! Cliente 99 não existe** |

**Comando SQL (PostgreSQL):**

```sql
CREATE TABLE IF NOT EXISTS CLIENTES (
    id INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);

CREATE TABLE IF NOT EXISTS PEDIDOS (
    id SERIAL PRIMARY KEY,
    valor NUMERIC(10, 2),
    id_cliente INT,
    -- Restrição de Integridade Referencial
    CONSTRAINT fk_cliente 
        FOREIGN KEY (id_cliente) 
        REFERENCES CLIENTES (cliente_id)
        ON DELETE CASCADE
);
```

O comando `ON DELETE CASCADE` é uma estratégia de manutenção da integridade. Se o cliente for excluído, todos os pedidos dele também serão removidos automaticamente, evitando dados órfãos.
{: .notice--primary}

```sql
CREATE TABLE IF NOT EXISTS SEXO (
    ID INT PRIMARY KEY, 
    DESCRICAO VARCHAR(20)
);

INSERT INTO SEXO VALUES 
    (1, 'Masculino'),
    (2, 'Feminino');

CREATE TABLE IF NOT EXISTS PESSOAS (
    ID BIGINT PRIMARY KEY,
    NOME VARCHAR(80) NOT NULL,
    DATA_NASCIMENTO DATE NOT NULL,
    ID_SEXO INT,
    EMAIL VARCHAR(200) UNIQUE,
    CONSTRAINT FK_SEXO FOREIGN KEY (ID_SEXO) REFERENCES SEXO (ID),
    CONSTRAINT CHK_IDADE_MINIMA CHECK (EXTRACT(YEAR FROM AGE(CURRENT_DATE, data_nascimento)) >= 16)
);

INSERT INTO PESSOAS (ID, NOME, DATA_NASCIMENTO, ID_SEXO, EMAIL) VALUES 
    (1, 'Aragorn II Elessar', '1987-03-01', 1, 'aragorn.rei@gondor.com'),
    (2, 'Arwen Undómiel', '1990-05-20', 2, 'arwen.estrela@rivendell.com'),
    (3, 'Frodo Bolseiro', '2000-09-22', 1, 'frodo.portador@shire.com'),
    (4, 'Galadriel', '1950-12-10', 2, 'galadriel.luz@lothlorien.com'),
    (5, 'Gandalf, o Cinzento', '1940-01-01', 1, 'gandalf.istari@maiar.com'),
    (6, 'Legolas Greenleaf', '1995-04-15', 1, 'legolas.arco@mirkwood.com'),
    (7, 'Éowyn de Rohan', '2002-07-07', 2, 'eowyn.escudeira@rohan.com'),
    (8, 'Gimli, Filho de Glóin', '1992-10-30', 1, 'gimli.machado@erebor.com'),
    (9, 'Samwise Gamgee', '2001-04-06', 1, 'sam.fiel@shire.com'),
    (10, 'Boromir de Gondor', '1982-01-25', 1, 'boromir.capitao@denethor.com');

CREATE TABLE IF NOT EXISTS ATENDENTES (
    ID BIGINT PRIMARY KEY,
    ID_PESSOA BIGINT,
    SALARIO NUMERIC(10, 2),
    CONSTRAINT FK_PESSOA_ATENDENTE FOREIGN KEY ID_PESSOA REFERENCES PESSOAS (ID),
    CONSTRAINT CK_SALARIO_ATENDENTE CHECK (SALARIO BETWEEN 2000 AND 40000)
);

INSERT INTO ATENDENTES (ID, ID_PESSOA, SALARIO) VALUES 
    (1, 1, 15000.00), -- Aragorn II Elessar (ID_PESSOA 1)
    (2, 5, 35500.00), -- Gandalf, o Cinzento (ID_PESSOA 5)
    (3, 2, 8200.50),  -- Arwen Undómiel (ID_PESSOA 2)
    (4, 10, 5400.00), -- Boromir de Gondor (ID_PESSOA 10)
    (5, 4, 28000.00); -- Galadriel (ID_PESSOA 4);

INSERT INTO PESSOAS (ID, NOME, DATA_NASCIMENTO, ID_SEXO, EMAIL) VALUES 
    (11, 'Belfast', '2021-03-01', 1, 'belfast.rei@gondor.com');
-- ERROR:  new row for relation "pessoas" violates check constraint "chk_idade_minima"
Failing row contains (11, Belfast, 2021-03-01, 1, belfast.rei@gondor.com). 

```

## Resumo das Restrições

| Tipo de Integridade  | Foco               | Principal Ferramenta SQL |
| -------------------- | ------------------ | ------------------------ |
| **Vazio (Nullity)**  | Presença de dados  | `NOT NULL`               |
| **Domínio**          | Validade do valor  | `CHECK`, `DATA TYPE`     |
| **Chave (Entidade)** | Unicidade da linha | `PRIMARY KEY`, `UNIQUE`  |
| **Referencial**      | Relacionamento     | `FOREIGN KEY`            |
