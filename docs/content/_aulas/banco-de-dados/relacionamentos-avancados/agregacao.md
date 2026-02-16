---
title: Agregação
excerpt: "Explore o conceito de agregação no modelo Entidade-Relacionamento, permitindo representar relacionamentos complexos de forma estruturada."
categories:
  - banco-de-dados
  - relacionamentos-avancados
date: 2024-03-01T08:48:05-04:00
order: 2
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Objetivos

- Compreender o conceito de agregação no modelo E-R.
- Identificar situações onde a agregação é necessária.
- Aplicar agregação em exemplos práticos de modelagem.

## O que é Agregação?

A agregação é um conceito avançado no modelo Entidade-Relacionamento (E-R) que permite tratar um relacionamento como uma entidade em si. Isso resolve situações onde um relacionamento precisa se relacionar com outras entidades, o que não é possível diretamente no E-R padrão.

Em termos simples: imagine que você tem um relacionamento entre duas entidades, mas esse relacionamento precisa interagir com uma terceira entidade. A agregação agrupa o relacionamento em uma "super-entidade" para facilitar isso.

## Quando Usar Agregação?

O modelo E-R básico não permite relacionamentos entre relacionamentos. Por exemplo, se você tem um relacionamento "Compra" entre Cliente e Produto, e quer associar uma "Nota Fiscal" a essa compra, a agregação ajuda a estruturar isso.

**Exemplo Prático**: Em um sistema de vendas, uma "Compra" envolve Cliente, Produto e uma Nota Fiscal. A compra é um relacionamento que se torna uma entidade agregada.

## Exemplo Detalhado

Considere um cenário onde "Funcionários" trabalham em "Projetos" usando "Ferramentas". O relacionamento "Trabalha" entre Funcionário e Projeto precisa se associar a Ferramentas.

### Sem Agregação (Problema)

<div class="mermaid">
erDiagram
  FUNCIONARIO ||--o{ TRABALHA : "N"
  PROJETO ||--o{ TRABALHA : "N"
  TRABALHA o{--o{ FERRAMENTA : "N"
</div>

Isso cria confusão, pois "Usa" relaciona o relacionamento "Trabalha" com Ferramenta.

### Com Agregação (Solução)

A agregação trata "Trabalha" como uma entidade agregada:

<div class="mermaid">
erDiagram
  FUNCIONARIO ||--o{ TRABALHA : "N"
  PROJETO ||--o{ TRABALHA : "N"
  TRABALHA ||--o{ USA : "N"
  FERRAMENTA ||--o{ USA : "1"
</div>

Agora, "Trabalha" é uma entidade composta, e "Usa" relaciona essa entidade com Ferramenta.

## Modelo Físico

No banco de dados físico, a agregação se traduz em tabelas:

- Tabela **FUNCIONARIO** (id, nome)
- Tabela **PROJETO** (id, nome)
- Tabela **TRABALHA** (funcionario_id, projeto_id, data_inicio) — representa o relacionamento agregado
- Tabela **FERRAMENTA** (id, nome)
- Tabela **USA** (trabalha_id, ferramenta_id) — relaciona a agregação com ferramenta

Isso permite consultas como: "Quais ferramentas são usadas em projetos específicos?"

## Benefícios da Agregação

- **Flexibilidade**: Modela cenários complexos que o E-R básico não cobre.
- **Clareza**: Organiza relacionamentos hierárquicos.
- **Extensibilidade**: Facilita adição de atributos ao relacionamento (ex: data, quantidade).

A agregação é útil em sistemas complexos, como gestão de projetos ou vendas, onde interações múltiplas precisam ser representadas.
