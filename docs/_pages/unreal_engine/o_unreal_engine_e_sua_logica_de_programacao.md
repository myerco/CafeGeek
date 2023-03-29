---
title: Blueprint
description: Neste capítulo será apresentado o modelo da lógica de programação utilizando **Blueprint** e os seus elementos.
tags: [Unreal Engine,lógica de programação, blueprint]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
sidebar:  
  - title: "UNREAL ENGINE COM C++ E BLUEPRINT"
    image: /imagens/unreal/logos/unreal_engine.webp
    nav: "dev_unreal"
date: 2022-09-21 
---

***

- [1. O que são Blueprints e Visual Scripting?](#1-o-que-são-blueprints-e-visual-scripting)
  - [1.1. Nativização](#11-nativização)
- [2. Trabalhando com Level ou níveis](#2-trabalhando-com-level-ou-níveis)
  - [2.1. Criando um Level](#21-criando-um-level)
  - [2.2. Salvando um Level](#22-salvando-um-level)
  - [2.3. Carregando um Level](#23-carregando-um-level)
- [3. O que é Level Blueprint?](#3-o-que-é-level-blueprint)
  - [3.1. Exemplo de BeginPlay e Tick no Level Blueprint](#31-exemplo-de-beginplay-e-tick-no-level-blueprint)
- [4. Atores e Classes utilizando Blueprint](#4-atores-e-classes-utilizando-blueprint)
  - [4.1. Atores predefinidos ou Place Actors](#41-atores-predefinidos-ou-place-actors)
  - [4.2. Classes Blueprint ou Blueprint Class](#42-classes-blueprint-ou-blueprint-class)
- [5. Componentes - Components](#5-componentes---components)
  - [5.1. Components e a aba My Blueprint](#51-components-e-a-aba-my-blueprint)
- [6. Estrutura da classe Actor no Unreal Engine](#6-estrutura-da-classe-actor-no-unreal-engine)
  - [6.1. Construction Script](#61-construction-script)
    - [6.1.1. Exemplo da lógica de um Construction Script](#611-exemplo-da-lógica-de-um-construction-script)
  - [6.2. Event Graph](#62-event-graph)
    - [6.2.1. BeginPlay](#621-beginplay)
    - [6.2.2. ActorBeginOverlap](#622-actorbeginoverlap)
    - [6.2.3. Tick](#623-tick)
- [7. Comentários](#7-comentários)
  - [7.1. Exemplo de comentário](#71-exemplo-de-comentário)

***

{% include image.html
    src="unreal/actor/unreal_engine_blueprint.webp"
    alt="Figura: Unreal Engine com Blueprint"
%}

## 1. O que são Blueprints e Visual Scripting?

***

O sistema *Blueprints Visual Scripting* no **Unreal Engine** é um sistema completo de script de jogo baseado no conceito de usar uma interface baseada em nós para criar elementos de jogo a partir do *Unreal Editor*. Como acontece com muitas linguagens de script comuns, ele é usado para definir classes orientadas a objetos (OO) ou objetos na *engine* .

{% include imagelocal.html
    src="unreal/actor/uml_jogos.webp"
    alt="Figura: Exemplo do conceito de objetos na programação."
    caption="No exemplo acima visualizamos uma classe que pode representar um objeto do tipo gato, com seus atributos e ações."
%}

**Blueprints** focam em ser acessíveis, versáteis para qualquer membro do projeto e isso simplifica tarefas para programadores e engenheiros de projeto, o que facilita entender, interagir e construir.  

Para que o **Unreal Engine** possa construir os nós gráficos que representam a instruções de programação **C++** é importante entender como é a hierarquia de elementos que compõem o projeto, segue abaixo a representação baseado no arquivo de referência no seguinte em [unreal_schematics](https://github.com/drstreit/unreal_schematics "https://github.com/drstreit/unreal_schematics").

```bash
|-- C++  
|   |-- Herança - Classes derivam e herdam de suas classes pai  
|   |   |-- Framework - Classes Padrão  
|   |   |   |-- Actor  
|   |   |   |   |-- GameMode
|   |   |   |   |   |-- Pawn
|   |   |   |   |   |-- Controller
|   |   |   |   |   |-- GameState
|   |   |   |   |   |-- PlayerState
|   |   |   |   |-- GameInstance
|   |   |-- Events/Functions/Var - Eventos, funções e variáveis.
|   |-- Blueprint
|   |   |-- Components
|   |   |   |-- Static Mesh
|   |   |   |-- Emiter
|   |   |-- Editores
|   |   |   |-- Timeline
|   |   |   |-- Componentes
|   |   |   |-- Editor de script
|   |   |-- Communication BP to BP - Comunicação entre Blueprints
|   |   |   |-- Casting
|   |   |   |-- Interface
|   |   |   |-- Event Dispacher
|   |-- Compilação - Compilação do Bytecode.
|   |   |-- Navitization - Durante o processo de preparação, o Blueprint pode ser cruzado para c ++ e nativizado*
|   |-- VM - Executado em uma máquina virtual
```

### 1.1. Nativização

"A nativização é uma funcionalidade relativamente nova no **Unreal Engine**, que permite aos desenvolvedores converter suas classes criadas em **Blueprint** para código nativo **C++** no momento em que é construído o pacote final do jogo. Isso faz com que seja possível aliar a facilidade de prototipação dos **Blueprints** ao desempenho do **C++**, acelerando o processo de desenvolvimento e também reduzindo a possibilidade de erros na programação, levando em consideração que ao desenvolver em **Blueprint** todas as entradas e saídas de dados, assim como o fluxo das operações são verificados pela máquina virtual enquanto os testes estão sendo realizados, isso permite garantir que tudo funcione conforme o esperado, ou na pior das hipóteses, alerte ao desenvolvedor caso algo não saia como o esperado, por meio de mensagens intuitivas e claras."

## 2. Trabalhando com Level ou níveis

***

Todo os objetos que estão visíveis em um jogo estão armazenados em um *Level* ou mapa de jogo, o *Level* no **Unreal Engine** é composto por iluminação, objetos poligonais e personagens controlados pelos jogadores.

{% include image.html
    src="https://www.worldofleveldesign.com/images/tutorial-topics/cat-ue4-680x300.jpg"
    alt="Figura: Tutorial List."
    caption="O personagem, a grama, as árvores e os elementos que compõem a iluminação estão organizados em um level."
    ref="https://www.worldofleveldesign.com"
%}

### 2.1. Criando um Level

Para criar um *level* utilizamos o menu principal `File` > `New Level`.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_new_level.webp"
    alt="Figura: New Level."
    caption="Utilizando o menu podemos criar um novo level ou mapa."
%}

Logo em seguida podemos definir um modelo pre-definido para auxiliar na construção do mapa.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_new_level_template.webp"
    alt="Figura: New Level."
    caption="Apresentando vários modelos prontos para servir como base."
%}

- `Default`: Selecione para criar um novo `Level` com uma configuração básica que inclui um início de jogador, uma luz, uma cúpula do céu e outros vários atores que você precisa para um *Level* funcionar corretamente;

- `TimeofDay`: selecione para criar um novo `Level` com uma configuração que permite que você visualize as configurações da atmosfera da hora do dia em tempo real;

- `VR-Basic`: selecione para criar um novo `Level` com atores para interagir, projetado para guiá-lo no aprendizado dos controles do Editor de VR;

- `Empty Level`: selecione para criar um novo `Level` completamente vazio.

### 2.2. Salvando um Level

Para salvar o *level* carregado utilizamos o menu `File` > `Save Current`.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_save_level.webp"
    alt="Figura: Save Current."
    caption="Salva o level aberto."
%}

### 2.3. Carregando um Level

É possível abrir um  *Level* utilizando `File` > `Open Level`.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_open_level.webp"
    alt="Figura: Open Level."
    caption="Abre um level."
%}

## 3. O que é Level Blueprint?  

***

Um `Level Blueprint` é um tipo especializado de **Blueprint** que atua como um gráfico de evento global em todo o nível ou *Level*. Cada *Level* em seu projeto tem seu próprio `Level Blueprint` criado por padrão, que pode ser editado no *Unreal Editor*.

Para editar utilizamos a opção `Blueprints` > `Open Level Blueprint`.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_open_level_blueprint.webp"
    alt="Figura:  Open Level Blueprint."
    caption="O Level Blueprint contém a lógica que controla todo o mapa."
%}

Para entender como funciona a lógica do *Blueprint* vamos escrever uma mensagem no `ViewPort` utilizando o `Level Blueprint` quando o *level* iniciar utilizaremos o evento `BeginPlay` e conectaremos o nó `Print String` para escrever uma mensagem na tela.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_blueprint_beginplay_printstring.webp"
    alt="Figura: Iniciando o level e escrevendo uma mensagem na tela."
    caption="O nó BeginPlay é executado quando o level é carregado e o nó associado, nó PrintString, e executado."
%}

Os nós utilizados são os seguintes:

- `BeginPlay`: Este evento é executado quando o *level* é carregado.

- `Print String`: É uma função que recebe como parâmetro um texto (*String*) e a escreve na tela.

### 3.1. Exemplo de BeginPlay e Tick no Level Blueprint

{% include iframe.html
    src="https://blueprintue.com/render/46vsgoyi/"
    title="Cafegeek - Exemplo de BeginPlay e Tick."
    caption="BeginPlay é executado somente ao carregar o level, Tick é executado a cada renderização dos quadros na cena."
    ref="https://blueprintue.com/render/46vsgoyi/"
%}

## 4. Atores e Classes utilizando Blueprint

***

Atores são objetos de uma determinada classe que suportam vários componentes, métodos e variáveis. Por exemplo:

- Personagem Herói - tem atributos, como vida e velocidade, tem componentes, como esqueleto e malha, e métodos, como direção e movimentação.

A lógica de programação dos atores é expressada em **Blueprint** e nos próximos capítulos vamos abordar este temo com mais detalhes.

### 4.1. Atores predefinidos ou Place Actors

No nível mais fundamental, um ator é qualquer objeto que você pode colocar em um *Level*.

Para adicionar o ator predefinido na cena utilizamos a opção `Create` e escolhemos o tipo de ator.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_blueprint_place_actors_bar.webp"
    alt="Figura: Create > Shapes para criar um objeto poligonal."
    caption="Os objetos são apresentados por categoria, por exemplo, a categoria Lights agrupa todos os atores que implementam algum tipo de emissão de luz, ou a categoria Shapes que agrupa objetos poligonais básicos."
%}

Ou podemos acessar o menu principal `Menu` > `Place Actors` para ter acesso a mais atores.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_place_actors.webp"
    alt="Figura: Windows > Place Actors."
    caption="Esta opção apresenta mais categorias de objetos."
%}

### 4.2. Classes Blueprint ou Blueprint Class

Uma classe **Blueprint**, muitas vezes abreviada como Blueprint, é um ativo que permite que os criadores de conteúdo adicionem funcionalidades facilmente às classes de jogo existentes. Os projetos são criados dentro do **Unreal Editor** visualmente, em vez de digitar o código, e salvos como ativos em um pacote de conteúdo. Essencialmente, eles definem uma nova classe ou tipo de ator que pode então ser colocado em mapas como instâncias que se comportam como qualquer outro tipo de ator.  

Para adicionar um ator na cena utilizamos o menu de acesso rápido `Context Menu` e acionando com o botão direito do mouse na aba `Content Drawer` ou o ícone Blueprint na barra de tarefas e escolher `New empty Blueprint Class...`.  

{% include imagelocal.html
    src="unreal/actor/unreal_engine_context_menu.webp"
    alt="Figura: Get Content."
    caption="O menu exibe uma lista agrupada por tipo de ator ou recurso."
%}

Escolha de Classe de atores  `Blueprint Class`.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_pick_class.webp"
    alt="Figura: Pick Parent Classe e All Classes."
    caption="Esta opção exibe uma lista das classes mais comuns, como por exemplo, atores básicos. A opção All Classes realiza uma busca por uma determinada classe."
%}

## 5. Componentes - Components

***

Os *Components* ou componentes são um tipo especial de objeto que os atores podem anexar a si próprios como subobjetos.

Os componentes são úteis para compartilhar comportamentos comuns, como a capacidade de exibir uma representação visual e reproduzir sons. Eles também podem representar conceitos específicos do projeto, como a maneira como um veículo interpreta a entrada e muda sua própria velocidade e orientação.

Por exemplo, um projeto com carros, aeronaves e barcos controláveis pelo usuário pode implementar as diferenças no controle e movimento do veículo, alterando qual componente um ator do veículo usa.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_add_component.webp"
    alt="Figura: Add Components."
    caption="Esta janela exibe a lista de componentes que podem ser associados a uma classe Actor."
%}

### 5.1. Components e a aba My Blueprint

Para ter acesso aos componentes que estão associados a um determinado objeto utilizamos a aba `My Blueprint`, que é uma representação visual do agrupamento de componentes, funções, variáveis e macros, abaixo um exemplo.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_myblueprint.webp"
    alt="Figura: Aba My Blueprint."
    caption="Podemos associar várias funções, macros, variáveis ou outros objetos programáveis à classe."
%}

## 6. Estrutura da classe Actor no Unreal Engine

***

A classe `Actor` é composta por vários elementos, entre eles estão as variáveis, métodos e funções, abaixo uma representação dessa estrutura.

```bash
|-- Objeto
|   |-- Events
|   |   |-- BeginPlay
|   |   |-- ActorBeginOverlap
|   |   |-- Tick
|   |-- Functions
|   |   |-- ConstructionScript
|   |-- Variables      
|   |   |-- VariavelLocal
```

A representação visual da lógica de programação da classe `Actor` é divida em:

- `Construction Script`;

- `Event Graph`.

A seguir vamos aprender mais sobre esses elementos.

### 6.1. Construction Script

Lógica de que é executada na construção do objeto, similares ao eventos *Construtor* em C++.  

#### 6.1.1. Exemplo da lógica de um Construction Script

{% include imagelocal.html
    src="unreal/actor/unreal_engine_construction_script.webp"
    alt="Figura: Construction Script."
    caption="A lógica acima apresenta uma mensagem ao construir o objeto."
%}

### 6.2. Event Graph

Contém o gráfico principal de nós e suas ligações representando a lógica de um **Blueprint**.  

"Exibe a representação visual de um gráfico específico de nós, pois mostra todos os nós contidos no gráfico, bem como as conexões entre eles. Ele fornece recursos de edição para adicionar e remover nós, organizar nós e criar links entre nós. Os pontos de interrupção também podem ser definidos na guia Gráfico para auxiliar na depuração de Blueprints."

{% include imagelocal.html
    src="unreal/actor/unreal_engine_event_graph_example.webp"
    alt="Figura: Event Graph."
    caption="Exemplo do Event Graph com vários nós."
%}

#### 6.2.1. BeginPlay

Este evento é acionado para todos os Atores quando o jogo é iniciado, quaisquer Atores gerados após o jogo ser iniciado terão isso chamado imediatamente.

#### 6.2.2. ActorBeginOverlap

Este evento será executado quando uma série de condições forem atendidas ao mesmo tempo:

- A resposta à colisão entre os atores deve permitir sobreposições.

- Ambos os Atores que devem executar o evento têm que gerar Eventos de Sobreposição definido como verdadeiro.
- E, finalmente, a colisão de ambos os Atores começa a se sobrepor; movendo-se juntos ou um é criado sobrepondo-se ao outro.

#### 6.2.3. Tick

Este é um evento simples que é chamado em todos os quadros do jogo. Tem como parâmetro a variável **Delta Seconds**.

"Vários motores gráficos ou *Game Engines*, como por exemplo *Unity* e *Pico-8*  tem os mesmos eventos com as mesmas Características."s

## 7. Comentários

***

Os comentários podem ser incluídos diretamente em nós **Blueprint** únicos ou podem ser incluídos como caixas de comentários para agrupar nós relacionados e fornecer descrições sobre sua funcionalidade.

Eles podem ser usados apenas para fins organizacionais para tornar os gráficos mais legíveis, mas também podem ser usados para fins informativos, pois permitem que descrições textuais sejam adicionadas da mesma forma que adicionar comentários ao código.

Selecione os nós e digite "C" no teclado para adicionar um comentário.  

### 7.1. Exemplo de comentário

{% include imagelocal.html
    src="unreal/actor/unreal_engine_comment_example.webp"
    alt="Figura: Comment Example."
    caption="Adicionando um comentário para documentar a lógica."
%}

Podemos adicionar Características aos comentários que detalham melhor a lógica dos nós envolvidos, como por exemplo adicionando cores.

- **Vermelho** - Lógica principal ou crítica.  

- **Azul** - Lógica de atores.  

- **Verde** - Lógica de estruturas de controle.  

Clicando no cabeçalho do comentário temos acesso os seus parâmetros.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_comment_details.webp"
    alt="Figura: Comment Details."
    caption="Alteramos o texto, cor, tamanho da fonte e como exibir uma mensagem flutuante."
%}
