---
title: banco-de-dados-distribuidos
excerpt: "Banco de dados distribuídos: replicação, fragmentação, vantagens e desafios."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-2"
date: 2026-01-31T08:48:05-04:00
order: 10
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# Banco de Dados Distribuídos

Consiste em múltiplas localidades conectadas por redes, onde o usuário pode acessar dados de qualquer site.

**Armazenamento:**
- Replicação: o sistema mantém cópias idênticas da relação em diferentes sites, aumentando a disponibilidade e o paralelismo.
- Fragmentação: a relação é particionada em fragmentos horizontais (subconjuntos de tuplas) ou verticais (subconjuntos de atributos).

**Vantagens e Desafios:**
- Oferece autonomia local e eficiência, mas dificulta o processamento de consultas, o controle de concorrência e a recuperação.
