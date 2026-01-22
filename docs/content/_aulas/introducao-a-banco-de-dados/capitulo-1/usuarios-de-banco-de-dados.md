---
title: Usuários de Banco de Dados
excerpt: "Explore os diferentes tipos de usuários de bancos de dados, incluindo DBA e perfis de acesso."
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

## Objetivos

- Compreender o papel do DBA (Administrador de Banco de Dados).
- Identificar os diferentes tipos de usuários de bancos de dados.
- Explorar ferramentas como SQL Developer para gerenciamento de usuários.
- Entender perfis de acesso e segurança.


## O que é um DBA?
O DBA (Database Administrator ou Administrador de Banco de Dados) é o profissional responsável pelo controle centralizado dos dados e programas de acesso. Ele garante que o sistema funcione de forma segura, eficiente e consistente.

**Definição:** "Uma das principais razões que motivam o uso dos SGBDs é o controle centralizado tanto dos dados quanto dos programas de acesso a eles. A pessoa que centraliza esse controle é chamada de Administrador de Dados (DBA)."

## Funções do DBA

O DBA desempenha várias funções críticas no gerenciamento do banco de dados:

### Definição do Esquema

- Cria o esquema original do banco de dados.
- Define tabelas, relacionamentos e estruturas básicas.
- Utiliza comandos DDL para implementar as definições.

### Estrutura de Dados e Acesso

- Define estruturas físicas de armazenamento.
- Configura índices e métodos de acesso otimizados.
- Garante performance adequada às necessidades da aplicação.

### Autorização de Acesso

- Controla permissões de usuários e aplicações.
- Define níveis de acesso (leitura, escrita, administração).
- Implementa políticas de segurança granular.

### Regras de Integridade

- Estabelece restrições para manter consistência dos dados.
- Define chaves primárias, estrangeiras e validações.
- Garante que os dados atendam às regras de negócio.

## Tipos de Usuários de Banco de Dados

Os usuários de bancos de dados podem ser classificados em diferentes categorias:

### Programadores de Aplicações

- Desenvolvem software que interage com o banco.
- Usam linguagens como Java, Python, PHP para acessar dados.
- Fazem chamadas DML (Data Manipulation Language) via APIs.

### Usuários Sofisticados

- Interagem diretamente com o banco sem escrever programas.
- Usam ferramentas visuais ou comandos SQL avançados.
- Realizam consultas complexas e análises de dados.

### Usuários Especialistas

- Profissionais que criam aplicações especializadas.
- Desenvolvem sistemas não tradicionais de processamento de dados.
- Trabalham com requisitos específicos de negócio.

### Usuários Navegantes

- Usuários finais que acessam aplicações prontas.
- Não precisam conhecer SQL ou estrutura do banco.
- Interagem através de interfaces gráficas amigáveis.

## SQL Developer e Gerenciamento de Usuários

O SQL Developer oferece ferramentas visuais para administração de usuários:

### Conexão como Administrador

Para gerenciar usuários, conecte-se com credenciais administrativas:

- **Usuário**: System (ou outro DBA)
- **Senha**: Definida na instalação
- **Atribuição**: SYSDBA para privilégios completos

> **Atenção**: O usuário SYSTEM possui privilégios administrativos totais. Use com cuidado!

### Painel DBA

1. No menu: **Exibir → DBA**
2. Selecione a conexão apropriada
3. Navegue em: **Segurança → Usuários**
4. Visualize e gerencie contas de usuário

## Perfis de Acesso e Segurança

Os perfis definem permissões padrão para grupos de usuários:

- **PADRÃO**: Permissões básicas de consulta
- **SYSDBA**: Privilégios administrativos completos
- **Perfis customizados**: Definidos pelo DBA para necessidades específicas

A segurança adequada garante que cada usuário acesse apenas os dados necessários para suas funções.

## Benefícios da Gestão de Usuários

- **Segurança**: Controle granular de acesso aos dados.
- **Auditoria**: Rastreamento de operações por usuário.
- **Conformidade**: Atendimento a regulamentações de privacidade.
- **Performance**: Otimização baseada em perfis de uso.

Uma gestão adequada de usuários é fundamental para a segurança e eficiência do sistema de banco de dados.
