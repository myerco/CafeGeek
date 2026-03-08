---
title: "Fase 3: Consultas e Programação Avançada"
excerpt: "Uma atividade prática e guiada para o desenvolvimento de um projeto completo de banco de dados relacional, desde a modelagem inicial até a implementação de funcionalidades avançadas com PostgreSQL."
categories:
  - "banco-de-dados"
  - "atividades"
date: 2026-01-31T08:48:05-04:00
order: 10
tags:
  - banco-de-dados
  - postgresql
  - modelagem
  - sql
sidebar:
  nav: introducao-a-banco-de-dados
---

Agora, com o banco de dados estruturado e populado, você irá demonstrar sua habilidade em extrair informações e automatizar processos.

## Consultas

Crie e execute as seguintes consultas (`SELECT`):

- Uma consulta que liste entidades por um critério (ex: pessoas por idade e sexo).
- Uma consulta que agregue dados por um período (ex: total de atividades por dia).
- Uma consulta que use `GROUP BY` e `COUNT` (ex: total de pessoas por sexo).
- Uma consulta que use `JOIN` para combinar dados de pelo menos 3 tabelas.

## Visões (`VIEW`)

Crie e use as seguintes visões (`VIEW`):

- Uma visão que sumarize dados com agregações (ex: total de atividades por ano, semestre e dia).
- Uma visão que desnormalize dados de várias tabelas para facilitar consultas complexas (ex: listar pessoas com seus cargos e departamentos).

## Programação

Implemente os seguintes procedimentos (`FUNCTION` / `PROCEDURE`):

- Uma função para realizar uma carga de dados em lote (ex: importar dados estatísticos).
- Uma função que recebe parâmetros para remover registros (ex: remover pessoas com base em um critério).
- Uma função que atualiza valores com base em um parâmetro de entrada (ex: aplicar um reajuste de valor).

## Triggers

Implemente os seguintes gatilhos:

- Um trigger para auditar (registrar em uma tabela de log) as principais alterações (`INSERT`, `UPDATE`, `DELETE`) em uma tabela crítica.
- Um trigger que impeça uma ação com base em uma regra de negócio (ex: bloquear atividades em um determinado dia ou para um usuário específico).

## 3. Ferramentas

- **Modelagem:** [Mermaid Live](https://mermaid.live/)
- **Tutoriais Mermaid:** [Mermaid Tutorials](https://mermaid.js.org/ecosystem/tutorials.html), [Diagramas ER](https://mermaid.js.org/syntax/entityRelationshipDiagram.html)
- **Controle de Versão:** [Github](https://github.com/)
- **Banco de Dados:** [Instância PostgreSQL do Curso](https://comp-pga.qute.com.br/login?next=/)
