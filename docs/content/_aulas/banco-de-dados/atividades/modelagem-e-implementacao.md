---
title: "Modelagem e Implementação"
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

Nesta fase, você irá transformar o tema escolhido em um modelo de dados e criar a primeira versão funcional do seu banco de dados no PostgreSQL.

## Criação do Repositório no GitHub

- Crie ou utilize uma conta existente no GitHub.
- Crie um novo repositório com um nome relacionado ao projeto escolhido.

## Documentação Inicial

No arquivo `README.md`, inclua:

- Uma apresentação do projeto (tema, objetivo geral e público-alvo).
- O diagrama do seu modelo de dados relacional (pode ser uma imagem ou gerado com Mermaid).

## Implementação no PostgreSQL (DDL)

- Escreva os scripts SQL para criar todas as tabelas (`CREATE TABLE`).
- Defina os tipos de dados adequados, chaves primárias, estrangeiras e outras restrições de integridade (`NOT NULL`, `UNIQUE`, etc.).

## Manipulação de Dados (DML)

- Crie scripts SQL (`INSERT`) para popular o banco com dados de exemplo. Insira registros suficientes para testar todos os relacionamentos e regras.
- Execute comandos `UPDATE` e `DELETE` para validar o comportamento do banco de dados.

## Exemplos de scripts

Para fazer com que o script possa ser executado múltiplas vezes sem erro. Use `CREATE TABLE IF NOT EXISTS ou CREATE OR REPLACE`.
{: .notice--warning}

Publique no github todos os scripts utilizados na pasta `scripts` utilizando a regra de nome:

  `[Versão]__[acao]_[descricao/objeto].sql`

  ```sql
    create_table_pessoas.sql
    add_email_to_pessoas.sql    
    create_view_pessoas_atendentes.sql
    insert_into_pessoas.sql
    create_or_replace_procedure_calcula_nota_fiscal.sql
  ```  

## Commit e Entrega

- Adicione todos os arquivos SQL e o `README.md` atualizado ao seu repositório.
- Faça o commit inicial com uma mensagem clara.
- Compartilhe o link do repositório no ambiente da disciplina para avaliação.
