---
title: visoes-e-restricoes-de-acesso
excerpt: "Visões (views) e restrições de acesso em bancos de dados."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-2"
date: 2026-01-31T08:48:05-04:00
order: 4
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# Visões (Views) e Restrições de Acesso

Uma visão é considerada uma **tabela virtual**; ela não existe fisicamente, mas aparece ao usuário como uma tabela real.

- Funciona como uma janela para um subconjunto de dados, refletindo automaticamente mudanças nas tabelas base.
- Sintaxe SQL: `CREATE VIEW nome_da_view AS subquery`.
- Exemplos mostram a criação de visões para filtrar funcionários com salários específicos e a execução de consultas normais sobre essas visões.
