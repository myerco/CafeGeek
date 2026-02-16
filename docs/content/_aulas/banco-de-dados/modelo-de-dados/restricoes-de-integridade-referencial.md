---
title: Restrições de integriadade referencial
excerpt: "Explore as restrições em bancos de dados: cardinalidade, dependência de existência e integridade referencial."
categories:
  - banco-de-Dados
  - modelo-de-dados
date: 2024-03-01T08:48:05-04:00
order: 18
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Objetivos

- Compreender os tipos de restrições em bancos de dados.
- Explorar cardinalidade: 1:1, 1:N, N:N.
- Entender dependência de existência.
- Aprender sobre integridade referencial.

## O que são Restrições?

Restrições são regras que definem as condições que os dados devem satisfazer para manter a consistência e integridade do banco de dados.

**Definição:** "O esquema E-R de uma empresa pode definir certas restrições, as quais o conteúdo do banco de dados deve respeitar."

### Tipos Principais de Restrições

1. **Cardinalidade:** Define quantas ocorrências de uma entidade podem se relacionar com outra
2. **Dependência de Existência:** Regras sobre existência obrigatória de entidades relacionadas
3. **Integridade Referencial:** Garante que relacionamentos entre tabelas sejam válidos

## Cardinalidade

A cardinalidade especifica o número de ocorrências de uma entidade que pode estar associado a ocorrências de outra entidade em um relacionamento.

### Tipos de Cardinalidade

#### 1:1 (Um para Um)

Cada elemento de uma entidade se relaciona com no máximo um elemento da outra entidade.

**Exemplo:** Relacionamento entre PESSOA e CPF

- Uma pessoa tem no máximo um CPF
- Um CPF pertence a no máximo uma pessoa

```text
┌─────────┐     ┌─────┐
│ PESSOA  │ ──○ │ CPF │
└─────────┘     └─────┘
      1             1
```

**Implementação:**

```sql
-- Tabela PESSOA
CREATE TABLE pessoa (
    id_pessoa INT PRIMARY KEY,
    nome VARCHAR(100),
    id_cpf INT UNIQUE -- FK opcional
);

-- Tabela CPF
CREATE TABLE cpf (
    id_cpf INT PRIMARY KEY,
    numero VARCHAR(14) UNIQUE,
    id_pessoa INT, -- FK opcional
    FOREIGN KEY (id_pessoa) REFERENCES pessoa(id_pessoa)
);
```

#### 1:N (Um para Muitos)

Um elemento da entidade A se relaciona com múltiplos elementos da entidade B, mas cada elemento de B se relaciona com apenas um de A.

**Exemplo:** Cliente e Empréstimos

- Um cliente pode ter vários empréstimos
- Cada empréstimo pertence a apenas um cliente

```
┌─────────┐     ┌────────────┐
│ CLIENTE │ ──○ │ EMPRÉSTIMO │
└─────────┘     └────────────┘
      1             N
```

**Implementação:**

```sql
-- Tabela CLIENTE
CREATE TABLE cliente (
    id_cliente INT PRIMARY KEY,
    nome VARCHAR(100)
);

-- Tabela EMPRESTIMO
CREATE TABLE emprestimo (
    id_emprestimo INT PRIMARY KEY,
    valor DECIMAL(10,2),
    id_cliente INT NOT NULL,
    FOREIGN KEY (id_cliente) REFERENCES cliente(id_cliente)
);
```

#### N:N (Muitos para Muitos)

Elementos de ambas as entidades podem se relacionar com múltiplos elementos da outra.

**Exemplo:** Produtos e Notas Fiscais
- Um produto pode aparecer em várias notas fiscais
- Uma nota fiscal pode conter vários produtos

```
┌──────────┐     ┌──────────────┐
│ PRODUTO  │ ──○ │ NOTA_FISCAL │
└──────────┘     └──────────────┘
      N              N
```

**Implementação:** Requer tabela associativa

```sql
-- Tabela PRODUTO
CREATE TABLE produto (
    id_produto INT PRIMARY KEY,
    nome VARCHAR(100),
    preco DECIMAL(10,2)
);

-- Tabela NOTA_FISCAL
CREATE TABLE nota_fiscal (
    id_nota INT PRIMARY KEY,
    data_emissao DATE,
    total DECIMAL(10,2)
);

-- Tabela associativa PRODUTO_NOTA
CREATE TABLE produto_nota (
    id_produto INT,
    id_nota INT,
    quantidade INT,
    valor_unitario DECIMAL(10,2),
    PRIMARY KEY (id_produto, id_nota),
    FOREIGN KEY (id_produto) REFERENCES produto(id_produto),
    FOREIGN KEY (id_nota) REFERENCES nota_fiscal(id_nota)
);
```

## Participação em Relacionamentos

Além da cardinalidade, devemos considerar a participação:

- **Participação Total:** Toda instância deve participar do relacionamento (linha obrigatória)
- **Participação Parcial:** Participação é opcional (pode ser nula)

**Notação:** Min-Max

- 1:1 (obrigatório dos dois lados)
- 0:1 (opcional de um lado, obrigatório do outro)
- 0:N (opcional de um lado, múltiplo do outro)

## Integridade Referencial

Garante que os relacionamentos entre tabelas sejam válidos:

- **Chaves Estrangeiras:** Referenciam chaves primárias de outras tabelas
- **Regras de Exclusão:** O que fazer quando uma entidade referenciada é excluída
- **Regras de Atualização:** Como propagar mudanças nas chaves

### Exemplo de Integridade

```sql
-- Restrição de integridade referencial
ALTER TABLE emprestimo
ADD CONSTRAINT fk_emprestimo_cliente
FOREIGN KEY (id_cliente) REFERENCES cliente(id_cliente)
ON DELETE CASCADE  -- Exclui empréstimos se cliente for excluído
ON UPDATE CASCADE; -- Atualiza id_cliente se chave primária mudar
```

## Benefícios das Restrições

- **Consistência:** Dados sempre válidos e consistentes
- **Integridade:** Relacionamentos preservados
- **Segurança:** Prevenção de dados inválidos
- **Manutenção:** Regras automáticas de validação

Restrições são essenciais para manter a qualidade e confiabilidade dos dados em sistemas de banco de dados.
