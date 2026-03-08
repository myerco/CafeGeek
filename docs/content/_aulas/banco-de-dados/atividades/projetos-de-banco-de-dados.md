---
title: "Projetos de Banco de Dados"
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

Sejam bem-vindos à nossa atividade prática de banco de dados. O objetivo deste exercício é conduzi-los pelo ciclo de vida completo do desenvolvimento de um banco de dados relacional, utilizando o SGBD PostgreSQL.

Vocês deverão escolher um dos temas propostos abaixo e seguir as etapas para construir um projeto coeso, bem estruturado e funcional.

As atividades estão divididas em fases. Cumpra cada uma delas na ordem indicada para garantir uma progressão lógica no desenvolvimento do seu projeto.

A seguir, apresento uma lista de temas para o seu projeto. Escolha um deles e, no seu `README.md`, elabore uma breve descrição do seu objetivo geral e público-alvo, antes de partirmos para a modelagem.

## Tema: Aluguel de Carros

**Objetivo:** Desenvolver um sistema para uma empresa de aluguel de carros, com foco em motoristas de aplicativos.
**Requisitos:**

- O sistema deve diferenciar clientes de atendentes, sendo que atendentes também podem ser clientes.
- **Veículos:** Devem ser registrados com placa, marca, modelo e tipo (moto, caminhão, carro de passeio).
- **Clientes:** Devem ser registrados com CPF, nome, sobrenome, endereço, dados bancários e e-mail.
- **Contratos:** Devem registrar o tipo de pagamento (Cartão, PIX), número do contrato, data, cliente associado, veículo alugado e o período de vigência.

## Tema: Clínica Veterinária

**Objetivo:** Criar um sistema para gerenciar uma clínica veterinária, abrangendo tanto o tratamento de animais domésticos quanto a venda de produtos.
**Requisitos:**

- **Animais:** Devem ser registrados com nome, espécie/classe, sexo e data de nascimento.
- **Atendimentos:** Devem registrar a data, o atendente, o cliente (tutor), o animal, o veterinário responsável, um descritivo da consulta, e os produtos e serviços utilizados com seus respectivos valores.
- **Produtos:** Devem ser registrados por tipo, marca, descrição e valor de compra.
- **Veterinários:** Devem ser registrados com CPF, nome e especialidade.
- Atendentes também podem ser clientes.

## Tema: Sistema de Atendimento

**Objetivo:** Implementar um sistema para uma empresa que precisa gerenciar o registro e o fluxo de atendimentos, controlando filas, atendentes e clientes.
**Requisitos:**

- **Entidades:** O sistema deve permitir o registro de atendentes e clientes (um atendente pode ser um cliente).
- **Filas:** Deve ser possível registrar diferentes filas de atendimento e associar os atendentes a elas.
- **Atendimentos:** Cada atendimento deve registrar a data e hora, a fila correspondente, o atendente que realizou e o cliente que foi atendido.

## Tema: Rede Social de Moda

**Objetivo:** Desenvolver uma rede social voltada para a divulgação, venda e troca de roupas, permitindo que os usuários organizem seus guarda-roupas e interajam.
**Requisitos:**

- **Usuários:** Devem se registrar com e-mail, nome e sobrenome.
- **Roupas:** Devem ser registradas com tipo, descrição, cor e tamanho.
- **Looks (Modelos):** Um look é uma combinação de 1 a N roupas. Deve ter uma descrição.
- **Interações:** O sistema deve registrar interações sociais como comentários, compartilhamentos e reações (visualização, gostei, não gostei).

## Tema: Gestão de Natação

**Objetivo:** Construir um aplicativo para gerenciar campeonatos de natação, incluindo o registro de atletas, árbitros, provas e resultados.
**Requisitos:**

- **Competidores:** Devem ser registrados com matrícula, nome, sexo e idade.
- **Locais:** Devem ser registrados com nome e endereço.
- **Categorias:** O sistema deve suportar categorias como máster, principiante, etc.
- **Provas:** Devem ser registradas (ex: 100m livre), cada uma com seu árbitro. Uma prova ocorre em um local específico.
- **Inscrições:** Um competidor pode se inscrever em várias provas dentro de uma categoria. O tempo do competidor para cada prova deve ser registrado, não excedendo 1 hora.

## Tema: Gerenciamento de Projetos

**Objetivo:** Desenvolver uma ferramenta para gerenciamento de projetos corporativos, controlando atividades, usuários, departamentos e permissões.
**Requisitos:**

- **Estrutura Organizacional:** O sistema deve registrar `Departamentos`, `Cargos` e `Usuários`.
- **Alocação:** Um `Usuário` é alocado em um `Departamento` (`Lotação`).
- **Projetos e Atividades:** O sistema deve permitir o registro de `Projetos` e `Atividades` vinculadas a eles.
- **Permissões:** O sistema deve ter um mecanismo para atribuir `Permissões` de acesso ou execução aos usuários.

## Tema: Agregador de Notícias

**Objetivo:** Criar um aplicativo para buscar, armazenar e compartilhar notícias da internet, fomentando uma comunidade de leitores.
**Requisitos:**

- **Notícias:** O sistema deve permitir o registro de notícias (ex: título, link, fonte).
- **Usuários:** Devem poder se registrar no sistema.
- **Interações:** Os usuários devem poder interagir com as notícias através de `Comentários` e `Reações` (ex: relevante, sem interesse).

## Ferramentas

- **Modelagem:** [Mermaid Live](https://mermaid.live/)
- **Tutoriais Mermaid:** [Mermaid Tutorials](https://mermaid.js.org/ecosystem/tutorials.html), [Diagramas ER](https://mermaid.js.org/syntax/entityRelationshipDiagram.html)
- **Controle de Versão:** [Github](https://github.com/)
- **Banco de Dados:** [Instância PostgreSQL do Curso](https://comp-pga.qute.com.br/login?next=/)
