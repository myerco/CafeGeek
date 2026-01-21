---
title: ABSTRAÇÃO DE DADOS
excerpt: "**BANCO DE DADOS I** Marco Yerco Mendizabel Cabrera Analista de Sistemas"
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 1
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---
# ABSTRAÇÃO DE DADOS

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Conceitos de Abstração
- Níveis de abstração

---

## CONCEITO

Um SGBD deve garantir uma visão abstrata do banco de dados aos usuários, desta forma três níveis de abstração de dados foram desenvolvidos para facilitar a interação de usuários com a arquitetura do sistema. São eles:

1. **Físico**
2. **Lógico ou Conceitual**
3. **Visão**

---

## NÍVEL FÍSICO

É o mais baixo nível de abstração que descreve como esses dados estão armazenados.

**Exemplo**: pode ser um bloco consecutivo de memória onde o registro está armazenado (este bloco é descrito em bytes, memória primária ou memória secundária).

---

## NÍVEL LÓGICO

Este é o nível médio de abstração e descreve quais dados estão armazenados no banco de dados e quais os inter-relacionados entre eles.

**Exemplo** usando uma linguagem de programação como analogia:
```java
class Cliente {
    string Nome;
    float Salario;
    string Cidade;
}

Tabelas, índices e outros objetos do banco.
NÍVEL DE VISÃO

O mais alto nível de abstração descreve apenas parte do banco de dados, a despeito das estruturas simples do nível lógico.

Neste nível, algumas visões do banco de dados são definidas e os usuários têm acesso a essas visões.

São usadas como mecanismo de segurança, restringindo o acesso a usuários em determinadas partes do banco de dados.
PRÓXIMO TÓPICO

    Modelo de Dados

O que foi visto:

    Conceitos de Abstração

    Níveis de abstração
