---
title: restricoes-de-integridade
excerpt: "Regras de integridade e exemplos de domínio e referencial."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-2"
date: 2026-01-31T08:48:05-04:00
order: 3
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# Restrições de Integridade

As regras de integridade garantem que mudanças feitas por usuários autorizados não resultem em perda de consistência, protegendo o banco de danos acidentais.

- **Integridade de Domínio:** Define valores válidos para atributos, comparável a variáveis tipadas em linguagens de programação. Exemplos no Oracle incluem o uso de `CHECK`, `NOT NULL` e `CREATE DOMAIN`.
- **Integridade Referencial:** Define que tabelas relacionadas devem manter a consistência entre chaves primárias (PK) e estrangeiras (FK).
  - Tabela Pai (referenciada pela PK) e Tabela Filho (dependente, contém a FK).
  - Opção CASCADE: permite que a exclusão de uma linha na tabela pai remova automaticamente as linhas correspondentes na tabela filha. Alternativamente, pode-se usar `SET NULL` para anular as referências na tabela filha.
