---
title: SGBD - Sistemas Gerenciadores de Banco de Dados
excerpt: "Explore os conceitos, estrutura e características dos Sistemas Gerenciadores de Banco de Dados (SGBD)."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2026-01-22T08:48:05-04:00
order: 19
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

{% include imagelocal.html
    src="introducao-a-banco-de-dados/sgbd.png"
    alt="Figura: Sistema Gerenciador de Banco de Dados."
    caption="Figura: Sistema Gerenciador de Banco de Dados."
%}

## Objetivos

- Compreender o conceito e a importância dos SGBD.
- Explorar a estrutura e arquitetura dos sistemas gerenciadores.
- Identificar características e benefícios dos SGBD.
- Entender a relação entre SGBD e Sistema Operacional.

## O que é um SGBD?

Um Sistema Gerenciador de Banco de Dados (SGBD) é um conjunto de programas que permite armazenar, organizar e manipular dados de forma eficiente. Ele fornece uma interface entre os usuários/aplicações e o banco de dados físico, garantindo acesso seguro e consistente aos dados.

**Definição técnica:** "Um SGBD é constituído por um conjunto de dados associados a um conjunto de programas para acesso a esses dados."

## Estrutura dos SGBD

Os SGBD possuem uma arquitetura em camadas que organiza o armazenamento e acesso aos dados:

- **Camada física**: Gerencia o armazenamento em disco, índices e estruturas de baixo nível.
- **Camada lógica**: Define tabelas, relacionamentos e restrições.
- **Camada de aplicação**: Fornece interfaces para usuários e programas.

## Arquitetura Cliente-Servidor

{% include image.html
    src="https://sae.unb.br/cae/conteudo/unbfga/lbd/imagens/componentesSgbd.png"
    alt="Figura: Componentes SGBD."
    caption="Figura: Componentes SGBD."
    ref="https://sae.unb.br/cae/conteudo/unbfga/lbd/banco2_introducao.html"
%}

A maioria dos SGBD modernos segue o modelo cliente-servidor:

- **Cliente**: Interface de usuário ou aplicação que solicita operações.
- **Servidor**: Processa as requisições, gerencia dados e retorna resultados.

Este modelo permite acesso remoto e distribuição de carga.

## SGBD vs Sistema Operacional

Os SGBD compartilham algumas funções com Sistemas Operacionais:

- **Controle de processos**: Gerenciamento de transações simultâneas.
- **Controle de E/S**: Leitura e escrita otimizada em disco.
- **Segurança**: Controle de acesso e permissões aos dados.

No entanto, os SGBD focam especificamente em dados estruturados, oferecendo recursos como consultas complexas e integridade referencial.

## Características Principais

Os SGBD oferecem diversos recursos essenciais:

### Controle Centralizado

- Administração unificada por um DBA (Database Administrator).
- Definição de políticas globais de acesso e segurança.

### Controle de Concorrência

- Permite acesso simultâneo de múltiplos usuários.
- Garante consistência através de bloqueios e isolamento de transações.

### Recuperação de Falhas

- Mecanismos para restaurar dados em caso de falhas (logs, backups).
- Garantia de atomicidade das operações.

### Segurança das Informações

- Controle de acesso baseado em usuários e perfis.
- Criptografia e auditoria de operações.

## Benefícios dos SGBD

- **Redução de redundância**: Dados armazenados uma vez, compartilhados por todos.
- **Evitação de inconsistências**: Regras de integridade garantem dados válidos.
- **Compartilhamento de dados**: Múltiplas aplicações acessam os mesmos dados.
- **Aplicação de restrições**: Regras automáticas de validação.
- **Manutenção da integridade**: Relacionamentos e dependências preservados.
- **Equilíbrio de necessidades**: Atende requisitos conflitantes de usuários.

Estes recursos tornam os SGBD essenciais para aplicações empresariais e sistemas críticos.
