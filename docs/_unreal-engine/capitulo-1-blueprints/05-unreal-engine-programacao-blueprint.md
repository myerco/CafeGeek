---
title: Criando seu primeiro Blueprint
excerpt: Neste capítulo será apresentado o modelo da lógica de programação utilizando Blueprints.
permalink: /pages/unreal-engine/blueprint
last_modified_at: 2023-03-28T08:48:05-04:00
layout: single
order: 2
sidebar:
    nav: dev_unreal_1
toc: true  
categories:
  - Unreal Engine
tags:
  - Blueprint
  - Actors
  - Classes
---

## 1. O que são Blueprints e Visual Scripting?

{% include imagelocal.html
    src="unreal/actor/unreal-engine-blueprint.webp"
    alt="Figura: Unreal Engine com Blueprint"
%}

O sistema *Blueprints Visual Scripting* no **Unreal Engine** é um sistema completo de script de jogo baseado no conceito de usar uma interface baseada em nós para criar elementos de jogo a partir do *Unreal Editor*. Como acontece com muitas linguagens de script comuns, ele é usado para definir classes orientadas a objetos (OO) ou objetos na *engine* .

{% include imagelocal.html
    src="unreal/actor/uml-jogos.webp"
    alt="Figura: Exemplo do conceito de objetos na programação."
    caption="No exemplo acima visualizamos uma classe que pode representar um objeto do tipo gato, com seus atributos e ações."
%}

**Blueprints** focam em ser acessíveis, versáteis para qualquer membro do projeto e isso simplifica tarefas para programadores e engenheiros de projeto, o que facilita entender, interagir e construir.  

Para que o **Unreal Engine** possa construir os nós gráficos que representam a instruções de programação **C++** é importante entender como é a hierarquia de elementos que compõem o projeto, segue abaixo a representação baseado no arquivo de referência no seguinte em [unreal_schematics](https://github.com/drstreit/unreal_schematics "https://github.com/drstreit/unreal_schematics").

```bash
└── C++  
    ├── Herança                         # Classes derivam e herdam de suas classes pai  
    |   ├── Framework                   # Classes Padrão  
    |   |   └── Actor  
    |   |       ├── GameMode
    |   |       |   ├── Pawn
    |   |       |   ├── Controller
    |   |       |   ├── GameState
    |   |       |   └── PlayerState
    |   |       └── GameInstance
    |   └── Events/Functions/Var        # Eventos, funções e variáveis.
    ├── Blueprint
    |   ├── Components
    |   |   ├── Static Mesh
    |   |   └── Emiter
    |   ├── Editores
    |   |   ├── Timeline
    |   |   ├── Componentes
    |   |   └── Editor de script
    |   └── Communication BP to BP      # Comunicação entre Blueprints
    |       ├── Casting
    |       ├── Interface
    |       └── Event Dispacher
    ├── Compilação                      # Compilação do Bytecode.
    |   └── Navitization                # Durante o processo de preparação, o Blueprint pode ser cruzado para c ++ e nativizado*
    └── VM                              # Executado em uma máquina virtual
```

**Nativização:** A nativização é uma funcionalidade relativamente nova no **Unreal Engine**, que permite aos desenvolvedores converter suas classes criadas em **Blueprint** para código nativo **C++** no momento em que é construído o pacote final do jogo. Isso faz com que seja possível aliar a facilidade de prototipação dos **Blueprints** ao desempenho do **C++**, acelerando o processo de desenvolvimento e também reduzindo a possibilidade de erros na programação, levando em consideração que ao desenvolver em **Blueprint** todas as entradas e saídas de dados, assim como o fluxo das operações são verificados pela máquina virtual enquanto os testes estão sendo realizados, isso permite garantir que tudo funcione conforme o esperado, ou na pior das hipóteses, alerte ao desenvolvedor caso algo não saia como o esperado, por meio de mensagens intuitivas e claras.
{: .notice--info}

## 2. Trabalhando com Level ou níveis

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
    src="unreal/actor/unreal-engine-new-level.webp"
    alt="Figura: New Level."
    caption="Utilizando o menu podemos criar um novo level ou mapa."
%}

Logo em seguida podemos definir um modelo pre-definido para auxiliar na construção do mapa.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-new-level-template.webp"
    alt="Figura: New Level."
    caption="Apresentando vários modelos prontos para servir como base."
%}

`Default`: Selecione para criar um novo `Level` com uma configuração básica que inclui um início de jogador, uma luz, uma cúpula do céu e outros vários atores que você precisa para um *Level* funcionar corretamente;

`TimeofDay`: selecione para criar um novo `Level` com uma configuração que permite que você visualize as configurações da atmosfera da hora do dia em tempo real;

`VR-Basic`: selecione para criar um novo `Level` com atores para interagir, projetado para guiá-lo no aprendizado dos controles do Editor de VR;

`Empty Level`: selecione para criar um novo `Level` completamente vazio.

### 2.2. Salvando um Level

Para salvar o *level* carregado utilizamos o menu `File` > `Save Current`.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-save-level.webp"
    alt="Figura: Save Current."
    caption="Salva o level aberto."
%}

### 2.3. Carregando um Level

É possível abrir um  *Level* utilizando `File` > `Open Level`.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-open-level.webp"
    alt="Figura: Open Level."
    caption="Abre um level."
%}

## 3. O que é Level Blueprint?  

Um `Level Blueprint` é um tipo especializado de **Blueprint** que atua como um gráfico de evento global em todo o nível ou *Level*. Cada *Level* em seu projeto tem seu próprio `Level Blueprint` criado por padrão, que pode ser editado no *Unreal Editor*.

Para editar utilizamos a opção `Blueprints` > `Open Level Blueprint`.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-open-level-blueprint.webp"
    alt="Figura:  Open Level Blueprint."
    caption="O Level Blueprint contém a lógica que controla todo o mapa."
%}

Para entender como funciona a lógica do *Blueprint* vamos escrever uma mensagem no `ViewPort` utilizando o `Level Blueprint` quando o *level* iniciar utilizaremos o evento `BeginPlay` e conectaremos o nó `Print String` para escrever uma mensagem na tela.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-blueprint-beginplay-printstring.webp"
    alt="Figura: Iniciando o level e escrevendo uma mensagem na tela."
    caption="O nó BeginPlay é executado quando o level é carregado e o nó associado, nó PrintString, e executado."
%}

Os nós utilizados são os seguintes:

`BeginPlay`: Este evento é executado quando o *level* é carregado.

`Print String`: É uma função que recebe como parâmetro um texto (*String*) e a escreve na tela.

### 3.1. Exemplo de BeginPlay e Tick no Level Blueprint

{% include iframe.html
    src="https://blueprintue.com/render/46vsgoyi/"
    title="Cafegeek - Exemplo de BeginPlay e Tick."
    caption="BeginPlay é executado somente ao carregar o level, Tick é executado a cada renderização dos quadros na cena."
    ref="https://blueprintue.com/render/46vsgoyi/"
%}
