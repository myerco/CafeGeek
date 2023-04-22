---
title: Atores e seus componentes
excerpt: Neste capítulo serão apresentados os objetos do tipo Actor ou Atores e seus componentes.
permalink: /pages/unreal-engine/atores-estruturas
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true  
categories:
  - Unreal Engine
tags:
  - Blueprint
  - Actors
  - Classes
---

{{ page.excerpt }}
{: .notice}

## 1. Atores e Classes utilizando Blueprint

Atores são objetos de uma determinada classe que suportam vários componentes, métodos e variáveis. Por exemplo:

**Personagem Herói:** Tem atributos, como vida e velocidade, tem componentes, como esqueleto e malha, e métodos, como direção e movimentação.
{: .notice--info}

A lógica de programação dos atores é expressada em **Blueprint** e nos próximos capítulos vamos abordar este tema com mais detalhes.

### 1.1. Atores predefinidos ou Place Actors

No nível mais fundamental, um ator é qualquer objeto que você pode colocar em um *Level*.

Para adicionar o ator predefinido na cena utilizamos a opção `Create` e escolhemos o tipo de ator.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-blueprint-place-actors-bar.webp"
    alt="Figura: Create > Shapes para criar um objeto poligonal."
    caption="Os objetos são apresentados por categoria, por exemplo, a categoria Lights agrupa todos os atores que implementam algum tipo de emissão de luz, ou a categoria Shapes que agrupa objetos poligonais básicos."
%}

Ou podemos acessar o menu principal `Menu` > `Place Actors` para ter acesso a mais atores.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-place-actors.webp"
    alt="Figura: Windows > Place Actors."
    caption="Esta opção apresenta mais categorias de objetos."
%}

### 1.2. Classes Blueprint ou Blueprint Class

Uma classe **Blueprint**, muitas vezes abreviada como Blueprint, é um ativo que permite que os criadores de conteúdo adicionem funcionalidades facilmente às classes de jogo existentes. Os projetos são criados dentro do **Unreal Editor** visualmente, em vez de digitar o código, e salvos como ativos em um pacote de conteúdo. Essencialmente, eles definem uma nova classe ou tipo de ator que pode então ser colocado em mapas como instâncias que se comportam como qualquer outro tipo de ator.  

Para adicionar um ator na cena utilizamos o menu de acesso rápido `Context Menu` e acionando com o botão direito do mouse na aba `Content Drawer` ou o ícone Blueprint na barra de tarefas e escolher `New empty Blueprint Class...`.  

{% include imagelocal.html
    src="unreal/actor/unreal-engine-context-menu.webp"
    alt="Figura: Get Content."
    caption="O menu exibe uma lista agrupada por tipo de ator ou recurso."
%}

Escolha de Classe de atores  `Blueprint Class`.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-pick-class.webp"
    alt="Figura: Pick Parent Classe e All Classes."
    caption="Esta opção exibe uma lista das classes mais comuns, como por exemplo, atores básicos. A opção All Classes realiza uma busca por uma determinada classe."
%}

## 2. Componentes

Os *Components* ou componentes são um tipo especial de objeto que os atores podem anexar a si próprios como subobjetos.

Os componentes são úteis para compartilhar comportamentos comuns, como a capacidade de exibir uma representação visual e reproduzir sons. Eles também podem representar conceitos específicos do projeto, como a maneira como um veículo interpreta a entrada e muda sua própria velocidade e orientação.

Por exemplo, um projeto com carros, aeronaves e barcos controláveis pelo usuário pode implementar as diferenças no controle e movimento do veículo, alterando qual componente um ator do veículo usa.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-add-component.webp"
    alt="Figura: Add Components."
    caption="Esta janela exibe a lista de componentes que podem ser associados a uma classe Actor."
%}

### 2.1. Components e a aba My Blueprint

Para ter acesso aos componentes que estão associados a um determinado objeto utilizamos a aba `My Blueprint`, que é uma representação visual do agrupamento de componentes, funções, variáveis e macros, abaixo um exemplo.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-myblueprint.webp"
    alt="Figura: Aba My Blueprint."
    caption="Podemos associar várias funções, macros, variáveis ou outros objetos programáveis à classe."
%}

## 3. Estrutura da classe Actor no Unreal Engine

A classe `Actor` é composta por vários elementos, entre eles estão as variáveis, métodos e funções, abaixo uma representação dessa estrutura.

```bash
└── Objeto
    ├── Events
    |   ├── BeginPlay
    |   ├── ActorBeginOverlap
    |   └── Tick
    ├── Functions
    |   └── ConstructionScript
    └── Variables      
        └── VariavelLocal
```

A representação visual da lógica de programação da classe `Actor` é divida em:

- `Construction Script`;

- `Event Graph`.

A seguir vamos aprender mais sobre esses elementos.

### 3.1. Construction Script

Lógica executada na construção do objeto, similares ao eventos *Construtor* em C++.  

#### 3.1.1. Exemplo da lógica de um Construction Script

{% include imagelocal.html
    src="unreal/actor/unreal-engine-construction-script.webp"
    alt="Figura: Construction Script."
    caption="A lógica acima apresenta uma mensagem ao construir o objeto."
%}

### 3.2. Event Graph

Contém o gráfico principal de nós e suas ligações representando a lógica de um **Blueprint**.  

**Informação:** Exibe a representação visual de um gráfico específico de nós, pois mostra todos os nós contidos no gráfico, bem como as conexões entre eles. Ele fornece recursos de edição para adicionar e remover nós, organizar nós e criar links entre nós. Os pontos de interrupção também podem ser definidos na guia Gráfico para auxiliar na depuração de Blueprints.
{: .notice--info}

{% include imagelocal.html
    src="unreal/actor/unreal-engine-event-graph-example.webp"
    alt="Figura: Event Graph."
    caption="Exemplo do Event Graph com vários nós."
%}

#### 3.2.1. BeginPlay

![image-left](/assets/images/unreal/actor/unreal-engine-blueprint-beginplay.webp){: .align-left}
Este evento é acionado para todos os Atores quando o jogo é iniciado, quaisquer Atores gerados após o jogo ser iniciado terão isso chamado imediatamente.

#### 3.2.2. ActorBeginOverlap

![image-left](/assets/images/unreal/actor/unreal-engine-blueprint-beginoverlap.webp){: .align-left}
Este evento será executado quando uma série de condições forem atendidas ao mesmo tempo:

- A resposta à colisão entre os atores deve permitir sobreposições.

- Ambos os Atores que devem executar o evento têm que gerar Eventos de Sobreposição definido como verdadeiro.
- E, finalmente, a colisão de ambos os Atores começa a se sobrepor; movendo-se juntos ou um é criado sobrepondo-se ao outro.

#### 3.2.3. Tick

![image-left](/assets/images/unreal/actor/unreal-engine-blueprint-tick.webp){: .align-left}
Este é um evento simples que é chamado em todos os quadros do jogo. Tem como parâmetro a variável **Delta Seconds**.

**Nota:** Vários motores gráficos ou *Game Engines*, como por exemplo *Unity* e *Pico-8*  tem os mesmos eventos com as mesmas Características."s
{: .notice--primary}

## 4. Comentários

Os comentários podem ser incluídos diretamente em nós **Blueprint** únicos ou podem ser incluídos como caixas de comentários para agrupar nós relacionados e fornecer descrições sobre sua funcionalidade.

Eles podem ser usados apenas para fins organizacionais para tornar os gráficos mais legíveis, mas também podem ser usados para fins informativos, pois permitem que descrições textuais sejam adicionadas da mesma forma que adicionar comentários ao código.

Selecione os nós e digite "C" no teclado para adicionar um comentário.  

### 4.1. Exemplo de comentário

{% include imagelocal.html
    src="unreal/actor/unreal-engine-comment-example.webp"
    alt="Figura: Comment Example."
    caption="Adicionando um comentário para documentar a lógica."
%}

Podemos adicionar Características aos comentários que detalham melhor a lógica dos nós envolvidos, como por exemplo adicionando cores.

- **Vermelho** - Lógica principal ou crítica.  

- **Azul** - Lógica de atores.  

- **Verde** - Lógica de estruturas de controle.  

Clicando no cabeçalho do comentário temos acesso os seus parâmetros.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-comment-details.webp"
    alt="Figura: Comment Details."
    caption="Alteramos o texto, cor, tamanho da fonte e como exibir uma mensagem flutuante."
%}
