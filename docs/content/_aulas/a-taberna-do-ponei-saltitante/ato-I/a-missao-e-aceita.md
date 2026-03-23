---
title: "A Missão é Aceita"
excerpt: "O herói aceita a missão! Nesta etapa, você irá se aprofundar nos problemas da Taberna do Pônei Saltitante, detalhando as regras de negócio e os requisitos para salvar nosso estalajadeiro do caos."
categories:
  - "a-taberna-do-ponei-saltitante"
  - "ato-i"
date: 2026-03-01T08:48:05-04:00
order: 3
tags:
  - banco-de-dados
sidebar:
  nav: a-taberna-do-ponei-saltitante
---

No capítulo anterior, você testemunhou o caos iminente na Taberna do Pônei Saltitante. Seu gerente, Cevado Carrapicho, fez um chamado por um herói — um mestre da organização capaz de trazer ordem ao seu negócio em expansão.

> ![thought-bubble](https://game-icons.net/icons/000000/transparent/1x1/seregacthtuf/thought-bubble.svg){: .align-left width="48"}
> Você aceitou o chamado. É o caminho para o **aumento da consciência**.
{: .notice--info}

Agora, a verdadeira jornada começa. Você cruza o primeiro limiar, deixando o "mundo comum" para trás. Sua primeira tarefa é sentar-se com o estalajadeiro, pena e pergaminho em mãos, e entender a fundo as leis que regem seu pequeno reino. Esta é a fase de **levantamento de requisitos**.

## O Pergaminho de Regras

![scroll-unfurled](https://game-icons.net/icons/000000/transparent/1x1/lorc/scroll-unfurled.svg){:width="48" .align-left} Cevado, aliviado com sua presença, começa a desabafar e a listar tudo o que ele precisa registrar em seu novo "sistema de organização". Ele desenrola um longo pergaminho com as regras da taverna:

### Sobre Clientes e Funcionários

- **Clientes (`Clientes`):** Precisamos registrar os clientes, seus **e-mails**, **endereços** e a qual **raça** pertencem (para personalizar o atendimento). Além disso, eles são classificados por tipos: `Padrão`, `Especial` e `Classe A`.
- **Funcionários (`Funcionarios`):** Cada funcionário tem um número de **matrícula**, um **salário base** e um cargo.
- **Cargos (`Cargos`):** Os cargos possuem uma estrutura hierárquica (um gerente supervisiona um barman, por exemplo). Cada cargo também define um valor a ser **acrescido no salário** do funcionário.

### Sobre Produtos e Pedidos

- **Pedidos (`Pedidos`):** Os pedidos dos clientes são hoje feitos em um caderno e, atenção, **nem sempre resultam em uma venda**! (Isso sugere um status no pedido: `em andamento`, `finalizado`, `cancelado`).
- **Produtos (`Produtos`):** Temos uma tabela de preços para nossos produtos.
- **Produtos Compostos:** Alguns produtos, como uma "Espada Élfica com Gemas", são compostos por outros itens (a espada e as gemas). É importante saber que vendemos tanto o produto final quanto os componentes em separado.

## As Perguntas do Estalajadeiro

![magnifying-glass](https://game-icons.net/icons/000000/transparent/1x1/lorc/magnifying-glass.svg){:width="48" .align-left} Depois de listar as regras, Cevado olha para você com esperança e diz: "Com este novo sistema, eu finalmente poderei ter respostas para minhas perguntas mais urgentes!":

- Quantos clientes de cada **raça** eu tenho?
- Quantos clientes de cada **classe** (`Padrão`, `Especial`, `Classe A`) estão registrados?
- Qual o **valor total das vendas** para os clientes da classe `Padrão`?
- Qual o meu **volume de vendas** por semana, mês e ano?
- **Quem vendeu mais**? Quero saber o desempenho de cada funcionário em um determinado período.
- Qual é a bebida (ou espada) **mais popular** da taverna?

Essas perguntas são o seu objetivo. O banco de dados que você construir deverá ser capaz de respondê-las.

## Sua Missão: Decifrar o Enigma

Com as regras e perguntas em mãos, sua missão agora é traduzir essa narrativa em uma estrutura de dados lógica. Você irá atualizar o mapa que começou a desenhar na etapa anterior.

Edite seu arquivo `README.md` no GitHub com as seguintes análises:

1. ![drakkar](https://game-icons.net/icons/000000/transparent/1x1/delapouite/drakkar.svg){:width="48" .align-left}
    **Identifique as Entidades:** Liste as principais "coisas" ou "substantivos" da história. (Ex: `Clientes`, `Funcionarios`, `Pedidos`, `Produtos`, `Cargos`...).
    <br clear="left">

2. ![checklist](https://game-icons.net/icons/000000/transparent/1x1/delapouite/checklist.svg){:width="48" .align-left}
    **Liste os Atributos:** Para cada entidade, liste suas propriedades ou características. (Ex: Para `Clientes`, temos `nome`, `email`, `raca`, `classe`...).
    <br clear="left">

3. ![relationship-bounds](https://game-icons.net/icons/000000/transparent/1x1/lorc/relationship-bounds.svg){:width="48" .align-left}
    **Defina os Relacionamentos:** Descreva como as entidades se conectam, usando "verbos". (Ex: Um `Cliente` *faz um* `Pedido`. Um `Pedido` *contém vários* `Produtos`. Um `Funcionario` *tem um* `Cargo`).
    <br clear="left">

4. ![treasure-map](https://game-icons.net/icons/000000/transparent/1x1/lorc/treasure-map.svg){:width="48" .align-left}
    **Atualize o Mapa (Diagrama MERMAID):** Com base na sua nova análise, melhore a primeira versão do seu diagrama de Entidade e Relacionamento no `README.md`. Adicione as novas entidades, atributos e os relacionamentos que você descobriu.
    <br clear="left">
