---
title: "Atividade Prática: Projeto de Banco de Dados com PostgreSQL"
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

## 1. Projetos

A seguir, apresento uma lista de temas para o seu projeto. Escolha um deles e, no seu `README.md`, elabore uma breve descrição do seu objetivo geral e público-alvo, antes de partirmos para a modelagem.

### Tema: Aluguel de Carros

**Objetivo:** Desenvolver um sistema para uma empresa de aluguel de carros, com foco em motoristas de aplicativos.
**Requisitos:**

- O sistema deve diferenciar clientes de atendentes, sendo que atendentes também podem ser clientes.
- **Veículos:** Devem ser registrados com placa, marca, modelo e tipo (moto, caminhão, carro de passeio).
- **Clientes:** Devem ser registrados com CPF, nome, sobrenome, endereço, dados bancários e e-mail.
- **Contratos:** Devem registrar o tipo de pagamento (Cartão, PIX), número do contrato, data, cliente associado, veículo alugado e o período de vigência.

### Tema: Clínica Veterinária

**Objetivo:** Criar um sistema para gerenciar uma clínica veterinária, abrangendo tanto o tratamento de animais domésticos quanto a venda de produtos.
**Requisitos:**

- **Animais:** Devem ser registrados com nome, espécie/classe, sexo e data de nascimento.
- **Atendimentos:** Devem registrar a data, o atendente, o cliente (tutor), o animal, o veterinário responsável, um descritivo da consulta, e os produtos e serviços utilizados com seus respectivos valores.
- **Produtos:** Devem ser registrados por tipo, marca, descrição e valor de compra.
- **Veterinários:** Devem ser registrados com CPF, nome e especialidade.
- Atendentes também podem ser clientes.

### Tema: Sistema de Atendimento

**Objetivo:** Implementar um sistema para uma empresa que precisa gerenciar o registro e o fluxo de atendimentos, controlando filas, atendentes e clientes.
**Requisitos:**

- **Entidades:** O sistema deve permitir o registro de atendentes e clientes (um atendente pode ser um cliente).
- **Filas:** Deve ser possível registrar diferentes filas de atendimento e associar os atendentes a elas.
- **Atendimentos:** Cada atendimento deve registrar a data e hora, a fila correspondente, o atendente que realizou e o cliente que foi atendido.

### Tema: Rede Social de Moda

**Objetivo:** Desenvolver uma rede social voltada para a divulgação, venda e troca de roupas, permitindo que os usuários organizem seus guarda-roupas e interajam.
**Requisitos:**

- **Usuários:** Devem se registrar com e-mail, nome e sobrenome.
- **Roupas:** Devem ser registradas com tipo, descrição, cor e tamanho.
- **Looks (Modelos):** Um look é uma combinação de 1 a N roupas. Deve ter uma descrição.
- **Interações:** O sistema deve registrar interações sociais como comentários, compartilhamentos e reações (visualização, gostei, não gostei).

### Tema: Gestão de Natação

**Objetivo:** Construir um aplicativo para gerenciar campeonatos de natação, incluindo o registro de atletas, árbitros, provas e resultados.
**Requisitos:**

- **Competidores:** Devem ser registrados com matrícula, nome, sexo e idade.
- **Locais:** Devem ser registrados com nome e endereço.
- **Categorias:** O sistema deve suportar categorias como máster, principiante, etc.
- **Provas:** Devem ser registradas (ex: 100m livre), cada uma com seu árbitro. Uma prova ocorre em um local específico.
- **Inscrições:** Um competidor pode se inscrever em várias provas dentro de uma categoria. O tempo do competidor para cada prova deve ser registrado, não excedendo 1 hora.

### Tema: Gerenciamento de Projetos

**Objetivo:** Desenvolver uma ferramenta para gerenciamento de projetos corporativos, controlando atividades, usuários, departamentos e permissões.
**Requisitos:**

- **Estrutura Organizacional:** O sistema deve registrar `Departamentos`, `Cargos` e `Usuários`.
- **Alocação:** Um `Usuário` é alocado em um `Departamento` (`Lotação`).
- **Projetos e Atividades:** O sistema deve permitir o registro de `Projetos` e `Atividades` vinculadas a eles.
- **Permissões:** O sistema deve ter um mecanismo para atribuir `Permissões` de acesso ou execução aos usuários.

### Tema: Agregador de Notícias

**Objetivo:** Criar um aplicativo para buscar, armazenar e compartilhar notícias da internet, fomentando uma comunidade de leitores.
**Requisitos:**

- **Notícias:** O sistema deve permitir o registro de notícias (ex: título, link, fonte).
- **Usuários:** Devem poder se registrar no sistema.
- **Interações:** Os usuários devem poder interagir com as notícias através de `Comentários` e `Reações` (ex: relevante, sem interesse).

## 2. Atividades

As atividades estão divididas em fases. Cumpra cada uma delas na ordem indicada para garantir uma progressão lógica no desenvolvimento do seu projeto.

### Fase 1: Modelagem e Implementação Inicial

Nesta fase, você irá transformar o tema escolhido em um modelo de dados e criar a primeira versão funcional do seu banco de dados no PostgreSQL.

1. **Criação do Repositório no GitHub:**
    - Crie ou utilize uma conta existente no GitHub.
    - Crie um novo repositório com um nome relacionado ao projeto escolhido.
2. **Documentação Inicial (`README.md`):**
    - No arquivo `README.md`, inclua:
        - Uma apresentação do projeto (tema, objetivo geral e público-alvo).
        - O diagrama do seu modelo de dados relacional (pode ser uma imagem ou gerado com Mermaid).
3. **Implementação no PostgreSQL:**
    - Escreva os scripts SQL para criar todas as tabelas (`CREATE TABLE`).
    - Defina os tipos de dados adequados, chaves primárias, estrangeiras e outras restrições de integridade (`NOT NULL`, `UNIQUE`, etc.).
4. **Manipulação de Dados (DML):**
    - Crie scripts SQL (`INSERT`) para popular o banco com dados de exemplo. Insira registros suficientes para testar todos os relacionamentos e regras.
    - Execute comandos `UPDATE` e `DELETE` para validar o comportamento do banco de dados.
5. **Commit e Entrega:**
    - Adicione todos os arquivos SQL e o `README.md` atualizado ao seu repositório.
    - Faça o commit inicial com uma mensagem clara.
    - Compartilhe o link do repositório no ambiente da disciplina para avaliação.

### Fase 2: Inovação e Prototipação

Nesta fase, você irá propor e implementar elementos inovadores no seu projeto, tornando-o mais atrativo e alinhado com tendências tecnológicas atuais.

1. **Proposta de Inovação:** Escolha **uma** das ideias abaixo para integrar ao seu projeto:
    - **Gamificação:** Adicione pontuações, conquistas, níveis ou rankings para engajar os usuários.
    - **Interações Sociais:** Implemente funcionalidades como curtidas, comentários, compartilhamentos ou seguidores.
    - **Inteligência de Dados:** Explore o uso de IA, mineração de dados para extrair insights ou integração com APIs externas.
2. **Atualização do Modelo:**
    - Incorpore as novas tabelas e relacionamentos necessários para a sua inovação.
    - Atualize o diagrama de entidade-relacionamento no seu `README.md`.
3. **Protótipo de Interface:**
    - Desenvolva um protótipo simples da interface da aplicação (pode ser um rascunho, um mockup em uma ferramenta de design ou uma tela HTML básica). O objetivo é visualizar como o usuário interagiria com a funcionalidade inovadora.
4. **Entrega:**
    - Publique o novo modelo e o protótipo (link ou imagem) no seu repositório GitHub.

### Fase 3: Consultas e Programação Avançada

Agora, com o banco de dados estruturado e populado, você irá demonstrar sua habilidade em extrair informações e automatizar processos.

1. **Consultas (`SELECT`):** Crie e execute as seguintes consultas:
    - Uma consulta que liste entidades por um critério (ex: pessoas por idade e sexo).
    - Uma consulta que agregue dados por um período (ex: total de atividades por dia).
    - Uma consulta que use `GROUP BY` e `COUNT` (ex: total de pessoas por sexo).
    - Uma consulta que use `JOIN` para combinar dados de pelo menos 3 tabelas.
2. **Visões (`VIEW`):** Crie as seguintes visões:
    - Uma visão que sumarize dados com agregações (ex: total de atividades por ano, semestre e dia).
    - Uma visão que desnormalize dados de várias tabelas para facilitar consultas complexas (ex: listar pessoas com seus cargos e departamentos).
3. **Programação (`FUNCTION` / `PROCEDURE`):** Implemente os seguintes procedimentos:
    - Uma função para realizar uma carga de dados em lote (ex: importar dados estatísticos).
    - Uma função que recebe parâmetros para remover registros (ex: remover pessoas com base em um critério).
    - Uma função que atualiza valores com base em um parâmetro de entrada (ex: aplicar um reajuste de valor).
4. **Triggers:** Implemente os seguintes gatilhos:
    - Um trigger para auditar (registrar em uma tabela de log) as principais alterações (`INSERT`, `UPDATE`, `DELETE`) em uma tabela crítica.
    - Um trigger que impeça uma ação com base em uma regra de negócio (ex: bloquear atividades em um determinado dia ou para um usuário específico).

## 3. Ferramentas

- **Modelagem:** [Mermaid Live](https://mermaid.live/)
- **Tutoriais Mermaid:** [Mermaid Tutorials](https://mermaid.js.org/ecosystem/tutorials.html), [Diagramas ER](https://mermaid.js.org/syntax/entityRelationshipDiagram.html)
- **Controle de Versão:** [Github](https://github.com/)
- **Banco de Dados:** [Instância PostgreSQL do Curso](https://comp-pga.qute.com.br/login?next=/)

## 4. Referências

- [Modelo de Dados](https://cafegeek.eti.br/curso/banco-de-dados/modelo-de-dados/modelo-de-dados/)
- [Normalização de Banco de Dados](https://cafegeek.eti.br/curso/banco-de-dados/normalizacao/normalizacao-de-banco-de-dados/)
- [Visões e Restrições de Acesso](https://cafegeek.eti.br/curso/banco-de-dados/estruturas/visoes-e-restricoes-de-acesso/)
- [Programação de Banco de Dados](https://cafegeek.eti.br/curso/banco-de-dados/estruturas/programacao-de-banco-de-dados/)
- [Triggers](https://cafegeek.eti.br/curso/banco-de-dados/estruturas/triggers)
