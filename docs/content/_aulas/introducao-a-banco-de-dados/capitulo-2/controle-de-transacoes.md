---
title: controle-de-transacoes
excerpt: "Controle de transações e propriedades ACID."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-2"
date: 2026-01-31T08:48:05-04:00
order: 8
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# Controle de Transações

Uma transação é uma unidade de execução que acessa ou atualiza itens de dados.

**Propriedades ACID:**
- Atomicidade: ou todas as operações são refletidas ou nenhuma será.
- Consistência: a execução isolada preserva a integridade do banco.
- Isolamento: transações concorrentes não interferem umas nas outras.
- Durabilidade: mudanças persistem após o sucesso, mesmo em falhas de sistema.

**Estados:**
- Ativa
- Efetivação Parcial
- Em Falha
- Abortada (Rolled Back)
- Efetivada (Committed)
