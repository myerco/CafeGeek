---
title: processamento-e-otimizacao-de-consultas
excerpt: "Processamento e otimização de consultas em bancos de dados."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-2"
date: 2026-01-31T08:48:05-04:00
order: 7
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# Processamento e Otimização de Consultas

Envolve as atividades de extrair dados e traduzir consultas de alto nível para expressões físicas eficientes.

**Etapas:**
1. Análise Sintática: traduz o SQL para uma expressão de álgebra relacional.
2. Otimização: seleciona o plano de execução mais eficiente baseando-se em algoritmos, índices e estatísticas de custo.
3. Avaliação: estima custos via tempo de CPU, acesso a disco (IO) e uso de RAM.

- Execução de Joins: o otimizador decide o caminho de acesso (varredura total ou índice), o método de união (Nested loop, Sort merge ou Hash joins) e a ordem de execução.
- Fases no Oracle: Parse (verificação e busca no dicionário), Execute (aplicação física) e Fetch (retorno dos dados).
