---
title: Restrições de Integridade
excerpt: "Entenda as principais restrições de integridade em bancos de dados relacionais, exemplos práticos e comandos SQL."
categories:
    - "introducao-a-banco-de-dados"
    - "capitulo-1"
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

### Exemplo Prático integridade referencial

Imagine uma tabela de `Produtos` onde o preço não pode ser negativo.

**Tabela de Produtos:**

| ID   | Nome    | Preço  | Categoria                    |
| :--- | :------ | :----- | :--------------------------- |
| 1    | Teclado | 150.00 | Eletrônicos                  |
| 2    | Mouse   | -5.00  | **ERRO! Violaria o domínio** |

**Comando SQL (PostgreSQL):**

```sql
CREATE TABLE produtos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    preco NUMERIC(10, 2) CHECK (preco > 0), -- Restrição de Domínio
    categoria VARCHAR(50) DEFAULT 'Geral'
);

```

## 2. Integridade Referencial

A **Integridade Referencial** garante que as relações entre as tabelas permaneçam consistentes. Em termos simples: se a Tabela A aponta para a Tabela B (via Chave Estrangeira), o registro na Tabela B **deve existir**.

Ela impede que tenhamos "registros órfãos" (ex: um pedido de um cliente que não está cadastrado).

### Exemplo Prático integridade de domínio

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
CREATE TABLE clientes (
    cliente_id INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);

CREATE TABLE pedidos (
    pedido_id SERIAL PRIMARY KEY,
    valor NUMERIC(10, 2),
    id_cliente INT,
    -- Restrição de Integridade Referencial
    CONSTRAINT fk_cliente 
        FOREIGN KEY (id_cliente) 
        REFERENCES clientes (cliente_id)
        ON DELETE CASCADE
);

```

O comando `ON DELETE CASCADE` é uma estratégia de manutenção da integridade. Se o cliente for excluído, todos os pedidos dele também serão removidos automaticamente, evitando dados órfãos.
{: .notice--primary}

## Resumo das Restrições

| Tipo de Integridade  | Foco               | Principal Ferramenta SQL |
| -------------------- | ------------------ | ------------------------ |
| **Vazio (Nullity)**  | Presença de dados  | `NOT NULL`               |
| **Domínio**          | Validade do valor  | `CHECK`, `DATA TYPE`     |
| **Chave (Entidade)** | Unicidade da linha | `PRIMARY KEY`, `UNIQUE`  |
| **Referencial**      | Relacionamento     | `FOREIGN KEY`            |

Espero que essa explicação tenha clareado como protegemos a qualidade dos dados no PostgreSQL!

**Gostaria que eu demonstrasse como criar gatilhos (triggers) para validações de integridade mais complexas que um simples CHECK não resolve?**
