---
title: controle-de-concorrencia
excerpt: "Controle de concorrência, bloqueios e deadlock."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-2"
date: 2026-01-31T08:48:05-04:00
order: 9
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# Controle de Concorrência

Necessário para gerenciar a interação entre transações simultâneas e preservar o isolamento.

**Mecanismos:**
- Bloqueios (Locks): podem ser Compartilhados (S), permitindo apenas leitura, ou Exclusivos (X), permitindo leitura e escrita.
- Deadlock: situação de espera mútua onde transações aguardam a liberação de bloqueios umas das outras.
- Protocolo de Bloqueio em Duas Fases: consiste na Fase de Expansão (obtenção de bloqueios) e Fase de Encolhimento (liberação de bloqueios).
