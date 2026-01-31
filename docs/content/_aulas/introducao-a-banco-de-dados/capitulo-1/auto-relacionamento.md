---

title: Auto-Relacionamento
excerpt: "Descubra como entidades podem se relacionar consigo mesmas em bancos de dados, com exemplos práticos e linguagem acessível."
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

## Objetivos

- Entender o conceito de auto-relacionamento em bancos de dados.
- Identificar exemplos práticos e aplicações desse tipo de relacionamento.

## O que é Auto-relacionamento?

Auto-relacionamento ocorre quando uma entidade se relaciona com ela mesma. Ou seja, os registros de uma mesma tabela podem estar conectados entre si, representando hierarquias, dependências ou composições.

Esse conceito é fundamental para modelar estruturas como árvores genealógicas, organogramas, listas de componentes e outros cenários onde elementos do mesmo tipo se conectam.

---

## Exemplos de Auto-relacionamento

### 1. Um para Muitos

Imagine uma tabela `PESSOAS` onde cada pessoa pode ser filha de outra pessoa. O relacionamento "é_filho_de" conecta registros da tabela consigo mesma:

<div class="mermaid">
erDiagram
  PESSOAS ||--o{ PESSOAS : "é_filho_de"
</div>

Na prática, a tabela pode ter um campo `id_pai` que referencia o `id` de outra pessoa na mesma tabela.

| id | nome         | id_pai |
|----|--------------|--------|
| 1  | João         | NULL   |
| 2  | Maria        | 1      |
| 3  | Pedro        | 1      |

Assim, Maria e Pedro são filhos de João.

#### Exemplo SQL

```sql
-- Criação da tabela
CREATE TABLE pessoas (
  id INT PRIMARY KEY,
  nome VARCHAR(100),
  id_pai INT,
  FOREIGN KEY (id_pai) REFERENCES pessoas(id)
);

-- Inserção de personagens do Senhor dos Anéis
INSERT INTO pessoas (id, nome, id_pai) VALUES (1, 'Elrond', NULL);
INSERT INTO pessoas (id, nome, id_pai) VALUES (2, 'Arwen', 1);
INSERT INTO pessoas (id, nome, id_pai) VALUES (3, 'Elladan', 1);

-- Consulta para listar todos com seus pais
SELECT f.nome AS filho, p.nome AS pai
FROM pessoas f
LEFT JOIN pessoas p ON f.id_pai = p.id;
```

### 2. Muitos para Muitos

Em uma indústria, um produto pode ser composto por vários outros produtos (componentes), e um componente pode participar de vários produtos. Isso é um auto-relacionamento muitos-para-muitos:

<div class="mermaid">
erDiagram
  PRODUTO ||--o{ COMPONENTE: "N"
  COMPONENTE ||--o{ PRODUTO: "N"
</div>

Para modelar isso, usamos uma tabela associativa:

| id_produto | id_componente |
|------------|---------------|
| 1          | 2             |
| 1          | 3             |
| 2          | 4             |

Assim, o produto 1 é composto pelos componentes 2 e 3, e assim por diante.

#### Exemplo SQL

```sql
-- Criação das tabelas
CREATE TABLE produto (
  id INT PRIMARY KEY,
  nome VARCHAR(100)
);

CREATE TABLE produto_componente (
  id_produto INT,
  id_componente INT,
  PRIMARY KEY (id_produto, id_componente),
  FOREIGN KEY (id_produto) REFERENCES produto(id),
  FOREIGN KEY (id_componente) REFERENCES produto(id)
);

-- Inserção de produtos (personagens do Senhor dos Anéis)
INSERT INTO produto (id, nome) VALUES (1, 'Anel Único');
INSERT INTO produto (id, nome) VALUES (2, 'Frodo');
INSERT INTO produto (id, nome) VALUES (3, 'Sam');

-- Associação de componentes
INSERT INTO produto_componente (id_produto, id_componente) VALUES (1, 2);
INSERT INTO produto_componente (id_produto, id_componente) VALUES (1, 3);
INSERT INTO produto_componente (id_produto, id_componente) VALUES (2, 3);

-- Consulta para listar produtos e seus componentes
SELECT p.nome AS produto, c.nome AS componente
FROM produto_componente pc
JOIN produto p ON pc.id_produto = p.id
JOIN produto c ON pc.id_componente = c.id;
```

## Por que usar auto-relacionamento?

- Representa hierarquias e estruturas recursivas.
- Permite consultas como "quem são os subordinados de um funcionário?" ou "quais produtos compõem este item?".
- Facilita a manutenção e expansão do modelo de dados.
