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

Esta atividade consiste em iniciar o desenvolvimento de um projeto de banco de dados relacional utilizando o PostgreSQL. O objetivo é criar a estrutura inicial do projeto, sem detalhar regras de negócio ou requisitos avançados neste momento. Os detalhes e regras de negócio serão definidos e implementados posteriormente, no passo 2.

Escolha um dos projetos sugeridos abaixo para iniciar sua atividade.

## Passo 1 - Escolha e apresentação inicial do projeto

Escolha um dos temas abaixo para seu projeto:

- **Aluguel de carros** - Aplicativo para empresa de aluguel de carros para motoristas de aplicativos
- **Clínica veterinária** - Aplicativo para clínica veterinária (tratamento de animais domésticos e venda de produtos)
- **Atendimento** - Aplicativo para empresa de registro de atendimento (controle de filas, registro de atendentes e pessoas atendidas)
- **Rede de roupas** - Aplicativo para rede social de divulgação, venda e troca de roupas (organização de guarda-roupa, combinação de roupas, registro de reações e negociações)

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

- **Aplicativo para empresa de aluguel de carros para motoristas de aplicativos**  
  - Os atendentes podem ser clientes
  - Registro de veículos: placa, marca, modelo, tipo (moto, caminhão, carro de passeio)
  - Os clientes são registrados com os seguintes dados: CPF, nome, sobrenome, endereço, dados bancários e e-mail
  - Os contratos têm os seguintes dados: tipo de pagamento (Cartão, Pix), número do contrato, data, cliente, veículo e período de contrato

- **Aplicativo para clínica veterinária (tratamento de animais domésticos e venda de produtos)**
  - Os atendentes podem ser clientes
  - Registro de animais: nome, classe, sexo, data de nascimento
  - Atendimentos: data, atendente, cliente, animal, veterinário, texto da consulta, produtos e serviços com valores de venda
  - Registro de produtos: tipo, marca, descrição, valor de compra
  - Registro de veterinários: CPF, nome, especialidade

- **Aplicativo para empresa de registro de atendimento (controle de filas, registro de atendentes e pessoas atendidas)**
  - Registro de atendentes
  - Registro de clientes (clientes podem ser atendentes)
  - Registro de filas de atendimento e seus atendentes
  - Registro de atendimentos: data e hora, fila, atendente, cliente

- **Aplicativo para rede social de divulgação, venda e troca de roupas (organização de guarda-roupa, combinação de roupas, registro de reações e negociações)**
  - Registro de usuários: e-mail, nome, sobrenome
  - Registro de roupas: tipo, descrição, cor e tamanho
  - Registro de modelos: descrição, roupa (1...99)
  - Registro de combinações: data e modelo
  - Registro de interações com outros usuários: comentários, compartilhamentos e ações (visualização, gostei, não gostei)

### Regras da atividade do passo 2

Siga o passo a passo abaixo para implementar e apresentar seu projeto:

1. Conecte-se ao banco de dados PostgreSQL no link [https://comp-pga.qute.com.br/login?next=/](https://comp-pga.qute.com.br/login?next=/)
2. Usuário de conexão: u001
3. Senha: `fale com o orientador em sala de aula`

## Passo 3 - Inovação

Neste passo, você é incentivado a propor e implementar elementos inovadores no seu projeto, tornando-o mais atrativo, moderno e alinhado com tendências tecnológicas atuais. Veja algumas sugestões detalhadas:

- **Gamificação:** Adicione mecanismos de gamificação ao seu sistema, como pontuação, conquistas, níveis, rankings ou recompensas para usuários que completam determinadas ações. Por exemplo, usuários podem ganhar medalhas ao completar tarefas, participar de desafios ou contribuir com a comunidade. Isso aumenta o engajamento e incentiva a participação ativa.

- **Interações de redes sociais:** Implemente funcionalidades inspiradas em redes sociais, como curtidas, comentários, compartilhamentos, seguidores ou notificações. Permita que os usuários interajam entre si, criem comunidades, compartilhem experiências ou colaborem em projetos. Essas interações tornam o sistema mais dinâmico e social.

- **Novas perspectivas tecnológicas:** Explore o uso de tecnologias emergentes, como Inteligência Artificial (IA) para análise de dados, identificação de imagens, recomendações personalizadas ou automação de processos. Considere também mineração de dados para extrair insights relevantes do uso do sistema, ou integração com APIs externas para ampliar as funcionalidades do seu projeto.

Sinta-se livre para propor outras inovações que possam agregar valor ao seu projeto, tornando-o diferenciado e relevante para o público-alvo.

### Regras da atividade do passo 3

- Publique o movo modelo no github
- Apresente um protótipo da interface da aplicação

## Passo 4 - Implementação

Neste passo, você irá transformar o modelo do seu projeto em uma implementação prática no PostgreSQL. O objetivo é criar e testar todos os componentes essenciais do banco de dados, garantindo que a estrutura esteja funcional e pronta para uso. Siga as orientações detalhadas abaixo:

- **Criação de tabelas e relacionamentos:** Implemente todas as tabelas do seu modelo, definindo os tipos de dados, chaves primárias e estrangeiras, restrições de integridade e relacionamentos entre as entidades. Certifique-se de que as tabelas reflitam corretamente o diagrama elaborado nas etapas anteriores.

- **Criação de visões (views):** Desenvolva visões para facilitar consultas frequentes ou para apresentar dados de forma consolidada e segura aos usuários. As views podem simplificar relatórios, dashboards ou fornecer abstrações para diferentes perfis de acesso.

- **Procedures e funções armazenadas:** Implemente procedures e funções para automatizar operações recorrentes, como cálculos, validações, processamento de dados ou regras de negócio. Utilize-as para centralizar lógicas importantes e garantir consistência nas operações do banco.

- **Triggers:** Crie triggers para executar ações automáticas em resposta a eventos no banco de dados, como inserções, atualizações ou exclusões. Triggers podem ser usadas para auditoria, atualização de dados relacionados, validação adicional ou integração com outros sistemas.

- **Manipulação de dados (inserção, alteração e remoção):** Realize operações de inserção, atualização e exclusão de dados para popular e testar o banco. Crie scripts de exemplo para inserir registros iniciais, atualizar informações e remover dados conforme necessário, validando o funcionamento de todas as regras e restrições.

Documente cada etapa da implementação, incluindo os scripts SQL utilizados, exemplos de uso e eventuais desafios encontrados. Isso facilitará a manutenção e a evolução do projeto.

### Regras da atividade do passo 4

- Publique no github todos os scripts utilizados na pasta `scripts` utilizando a regra de nome:

```sql
 -- comando+ '_' + objeto-de-banco-de-dados 
 -- Exemplo:
    create_table_pessoas.sql
    create_view_pessoas_atendentes.sql
    insert_indo_pessoas.sql
    create_or_replace_procedure_calcula_nota_fiscal.sql
```  

- Implemente todos os comanandos no site do passo 2.

## Passo 5 - Consultas avançadas

Em construção...

## Referências

- [Mermaid Live](https://mermaid.live/)
- [Mermaid Tutorials](https://mermaid.js.org/ecosystem/tutorials.html)
- [Mermaid Entity Relationships Diagrams  - ER](https://mermaid.js.org/syntax/entityRelationshipDiagram.html)
- [Github](https://github.com/)
