---
title: gatilhos-triggers
excerpt: "Gatilhos (triggers): definição, requisitos, vantagens e sintaxe."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-2"
date: 2026-01-31T08:48:05-04:00
order: 6
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# Gatilhos (Triggers)

Um gatilho é um comando executado automaticamente pelo sistema como consequência de uma modificação (INSERT, UPDATE ou DELETE) no banco de dados.

- **Requisitos:** Deve-se especificar as condições de execução e as ações a serem tomadas.
- **Vantagens:** Prevenção de transações inválidas, auditoria sofisticada, sincronismo de tabelas replicadas e geração de colunas derivadas.
- **Sintaxe:** Define-se o momento (`BEFORE` ou `AFTER`), o comando e se a execução é para cada linha (`FOR EACH ROW`).
