---

title: UsuÁRIOS DE BANCO DE DADOS
excerpt: "Entenda conceitos fundamentais de bancos de dados relacionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 21
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# USUÁRIOS DE BANCO DE DADOS

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- DBA - Administrador de Banco de Dados
- Usuários de banco de dados
- SQL Developer e os usuários

---

## DBA

"Uma das principais razões que motivam o uso dos SGBDs é o controle centralizado tanto dos dados quanto dos programas de acesso à ele. A pessoa que centraliza esse controle do sistema é chamado de Administrador de Dados (DBA)."

Dentre as funções de um DBA destacamos as seguintes:

---

## FUNÇÕES DO DBA

1. **Definição do esquema**:
   O DBA cria o esquema de banco de dados original descrevendo um conjunto de definições que são transformadas pelo compilador DDL em um conjunto de tabelas armazenadas de modo permanente no dicionário de dados.

2. **Definição da estrutura de dados e método de acesso**:
   O DBA cria estruturas de dados e métodos de acesso apropriado escrevendo um conjunto de definições, as quais são traduzidas pelo compilador de armazenamento de dados e pelo compilador de linguagem de definição de dados.

---

## FUNÇÕES DO DBA (CONTINUAÇÃO)

3. **Fornecer autorização de acesso ao sistema**:
   O fornecimento de diferentes tipos de autorização no acesso aos dados permite que o administrador de dados regule o acesso dos diversos usuários às diferentes partes do sistema.

4. **Especificação de regras de integridade**:
   Os valores dos dados armazenados no banco de dados devem satisfazer certas restrições para manutenção de sua integridade.

---

## USUÁRIOS DE BANCO DE DADOS

1. **Programadores de Aplicações**:
   São profissionais em computação que interagem com o sistema por meio de chamadas DML, as quais são envolvidas por programas escritos na linguagem hospedeira, por exemplo: Java, Ruby, PHP, etc.

---

## USUÁRIOS DE BANCO DE DADOS (CONTINUAÇÃO)

2. **Usuários Sofisticados**:
   Interagem com o sistema sem escrever programas.

3. **Usuários Especialistas**:
   São usuários sofisticados que escrevem aplicações especializadas de banco de dados que não podem ser classificadas como aplicações tradicionais em processamento de dados.

---

## USUÁRIOS DE BANCO DE DADOS (CONTINUAÇÃO)

4. **Usuários Navegantes**:
   São usuários comuns que interagem com o sistema chamando um dos programas aplicativos permanentes já escritos.

---

## SQL DEVELOPER

Para conectar no banco de dados necessitamos de um usuário autorizado:

- **Nome do usuário**: System
- **Senha**: 12345678
- **Atribuição**: Padrão
- **Perfil de acesso**: PADRÃO, SYSDBA

> **CUIDADO**: O usuário **SYSTEM** é o administrador do banco.

---

## PAINEL DBA

1. Menu **Exibir -> DBA**
2. Escolha a conexão
3. Na árvore de objetos: **Segurança -> Usuários**

---

## Próximo tópico

- Modelo de Entidade de Relacionamento

### O que foi visto

- DBA - Administrador de Banco de Dados
- Usuários de banco de dados
- SQL Developer e os usuários
