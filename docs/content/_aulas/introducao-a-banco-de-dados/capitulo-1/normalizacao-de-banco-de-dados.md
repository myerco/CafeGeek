---
title: Normalização de Banco de Dados
excerpt: "Explore os conceitos fundamentais da normalização de bancos de dados: anomalias, 1FN e dependências funcionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 15
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Objetivos

- Compreender o conceito de normalização em bancos de dados.
- Identificar anomalias em tabelas não normalizadas.
- Aplicar a Primeira Forma Normal (1FN).
- Entender dependências funcionais: total, parcial e transitiva.

## O que é Normalização?

A normalização é um processo matemático formal introduzido por E. F. Codd em 1970. Consiste em decompor tabelas complexas em estruturas mais simples, eliminando anomalias de atualização e redundâncias desnecessárias.

**Objetivo principal:** Criar esquemas relacionais "puros" que evitem problemas como:

- Grupos repetitivos de dados
- Dependências parciais em chaves concatenadas
- Redundância desnecessária
- Perda acidental de informação
- Dificuldade na representação da realidade

## Anomalias em Tabelas Não Normalizadas

Quando uma tabela não está adequadamente estruturada, podem ocorrer três tipos principais de anomalias:

### Anomalia de Inclusão

Não é possível incluir um novo registro sem que ele esteja relacionado a outro dado existente.

**Exemplo:** Não se pode cadastrar um cliente que ainda não fez compras.

### Anomalia de Exclusão

Ao excluir um registro, informações importantes podem ser perdidas.

**Exemplo:** Excluir um cliente remove também o histórico de suas compras.

### Anomalia de Alteração

Alterações em um campo podem exigir múltiplas modificações na mesma tabela.

**Exemplo:** Alterar o preço de um produto requer atualizar todas as vendas desse produto.

## Formas Normais

A normalização é aplicada através de uma série de regras chamadas Formas Normais:

1. **Primeira Forma Normal (1FN)**
2. **Segunda Forma Normal (2FN)**
3. **Terceira Forma Normal (3FN)**
4. **Forma Normal de Boyce-Codd (FNBC)**
5. **Quarta Forma Normal (4FN)**
6. **Quinta Forma Normal (5FN)**

## Primeira Forma Normal (1FN)

A 1FN estabelece que **cada atributo deve conter apenas valores atômicos** (indivisíveis), não permitindo grupos repetitivos.

**Regra:** Uma tabela está na 1FN se todos os seus atributos contêm apenas valores simples, sem listas ou estruturas complexas.

### Aplicando 1FN - Exemplo Prático

Considere uma tabela PEDIDO com itens repetitivos:

**Tabela original (não normalizada):**

| Nº Pedido | Cliente | Produto1 | Qtd1 | Produto2 | Qtd2 |
|-----------|---------|----------|------|----------|------|
| 001       | João    | Caneta   | 2    | Lápis    | 1    |

**Após 1FN - Duas tabelas:**
**PEDIDO:**

| Nº Pedido | Cliente |
|-----------|---------|
| 001       | João    |

**ITEM_PEDIDO:**

| Nº Pedido | Produto | Quantidade |
|-----------|---------|------------|
| 001       | Caneta  | 2          |
| 001       | Lápis   | 1          |

## Dependência Funcional

Uma dependência funcional existe quando um atributo (ou conjunto de atributos) determina unicamente o valor de outro atributo.

**Notação:** A → B (A determina B)

**Exemplo:** Em uma tabela ALUNO:

- Matrícula → Nome (cada matrícula tem um único nome)
- Matrícula → Curso (cada matrícula tem um único curso)

### Dependência Funcional Total vs Parcial

Em chaves primárias compostas, analisamos se a dependência é da chave completa ou de parte dela.

**Dependência Total:** O atributo depende de TODOS os campos da chave composta.

**Dependência Parcial:** O atributo depende apenas de PARTE da chave composta.

**Exemplo - Tabela ITEM_VENDA (Nº_Venda + Cod_Produto):**

- Quantidade depende TOTALMENTE de (Nº_Venda + Cod_Produto)
- Nome_Produto depende PARCIALMENTE apenas de Cod_Produto

### Dependência Funcional Transitiva

Ocorre quando um atributo não-chave determina outro atributo não-chave.

**Notação:** A → B → C (C depende transitivamente de A através de B)

**Exemplo:** Em uma tabela FUNCIONARIO:

- CPF → Departamento
- Departamento → Localização

Portanto: CPF → Localização (dependência transitiva)

## Benefícios da Normalização

- **Redução de redundância:** Dados armazenados uma única vez
- **Eliminação de anomalias:** Atualizações consistentes
- **Manutenção da integridade:** Relacionamentos bem definidos
- **Flexibilidade:** Facilita alterações futuras no esquema

A normalização é fundamental para criar bancos de dados robustos e eficientes.
