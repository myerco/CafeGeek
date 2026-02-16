---
title: Modelagem de Banco de Dados com PostgreSQL - Atividade Prática Passo a Passo
excerpt: Aprenda, passo a passo, como iniciar a modelagem de um banco de dados relacional no PostgreSQL a partir de projetos práticos, com orientações para estruturação inicial, escolha de tema e documentação no GitHub. Ideal para quem deseja aplicar conceitos de modelagem em situações reais.
categories:
  - "Banco de Dados"
tags:
  - "Tutorial"
  - "Curso"
  - "Banco de Dados"
---

## Apresentação

Esta atividade consiste em iniciar o desenvolvimento de um projeto de banco de dados relacional utilizando o PostgreSQL. O objetivo é criar a estrutura inicial do projeto, sem detalhar regras de negócio ou requisitos avançados neste momento. Os detalhes e regras negociais serão definidos e implementados posteriormente, no passo 2.

Escolha um dos projetos sugeridos abaixo para iniciar sua atividade.

## Passo 1 - Escolha e apresentação inicial do projeto

Escolha um dos temas abaixo para seu projeto:

- Aplicativo para empresa de aluguel de carros para motoristas de aplicativos
- Aplicativo para clínica veterinária (tratamento de animais domésticos e venda de produtos)
- Aplicativo para empresa de registro de atendimento (controle de filas, registro de atendentes e pessoas atendidas)
- Aplicativo para rede social de divulgação, venda e troca de roupas (organização de guarda-roupa, combinação de roupas, registro de reações e negociações)

Faça uma breve descrição do projeto escolhido, sem entrar em detalhes de regras de negócio. Foque apenas no objetivo geral e no público-alvo.

### Regras da atividade do passo 1

Siga o passo a passo abaixo para implementar e apresentar seu projeto:

1. Crie ou utilize uma conta existente no GitHub.
2. Crie um repositório com o nome do projeto escolhido.
3. No README.md do repositório, inclua:
   - Breve apresentação do projeto (tema e objetivo geral)
   - Estrutura inicial do projeto (pastas, arquivos principais)
   - Versão inicial do projeto
   - Modelo de dados do projeto (utilize o diagrama MERMAID para representar as tabelas e relações)
4. Faça o commit inicial com o README.md e o diagrama do modelo de dados.
5. Compartilhe o link do repositório no ambiente da disciplina para avaliação.

**Observação:** Os detalhes das regras de negócio e requisitos avançados serão definidos e implementados no passo 2 da atividade.
{: .notice}

## Passo 2 - Detalhamento do projeto

No passo 2, você irá aprofundar o projeto escolhido no passo 1, detalhando as regras de negócio, requisitos e principais entidades envolvidas. Abaixo, veja exemplos de detalhamento para cada tema sugerido:

### Aplicativo para empresa de aluguel de carros para motoristas de aplicativos

- Os atendes podem ser clientes
- Registro de veículos : placa, marca, modelo, tipo (moto, caminhão, carro de passeio)
- Os clientes são registrados com os seguintes dados: CPG, Nome, Sobrenome, Endereço, Dados bancários e e-mail
- Os contratos tem os seguintes dados: Tipo de pagamento (Cartão, Pix), Número do contrato, data, cliente, veículo e período de contrato

### Aplicativo para clínica veterinária (tratamento de animais domésticos e venda de produtos)

- Os atendes podem ser clientes
- Registro de animais: nome, classe, sexo, data nascimento
- Atendimentos : data, atendende, cliente, animal, veterinario, texto da consulta, produtos e serviços com valores de vendas
- Registro de produtos : tipo, marca, descrição, valor de compra
- Registro de veterinários: cpf, nome, especialidade

### Aplicativo para empresa de registro de atendimento (controle de filas, registro de atendentes e pessoas atendidas)

- Registro de atendentes;
- Registro de clientes (clientes pode ser clientes)
- Registro de filas de atendimento e seus atendentes
- Registro de atendimento : data e hora, fila, atendente, cliente

### Aplicativo para rede social de divulgação, venda e troca de roupas (organização de guarda-roupa, combinação de roupas, registro de reações e negociações)

- Registro de usuarios: email, nome, sobrenome
- Registro de roupas : tipo, descrição, cor e tamanho
- Registro de modelos: descrição, roupa (1...99)
- Registro de combinações : data e modelo
- Registro de interações com outros usuários: comentários, compartilhamentos e ações (visualização, gostei, não gostei)

### Regras da atividade do passo 2

Siga o passo a passo abaixo para implementar e apresentar seu projeto:

1. Conecte com o banco de dados Postegresql no link  [https://comp-pga.qute.com.br/login?next=/](https://comp-pga.qute.com.br/login?next=/)
2. Usuário de conexão: u001
3. Senha: `fale com o orientador em sala de aula`

## Referências

- [Mermaid Live](https://mermaid.live/)
- [Mermaid Tutorials](https://mermaid.js.org/ecosystem/tutorials.html)
- [Mermaid Entity Relationships Diagrams  - ER](https://mermaid.js.org/syntax/entityRelationshipDiagram.html)
- [Github](https://github.com/)
