---
title: User Interface
excerpt: Neste capítulo vamos implementar o HUD (Heads-up Display) do jogo.
categories: 
  - "unreal-engine-com-c-e-blueprint"
  - "capitulo-3-interface-com-o-jogador"
permalink: /:categories/:title
date: 2024-05-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 301
tags:
  - hud
---

HUD (*Heads-up Display*) ou UI (*Use Interface*) é um objeto especial do **Unreal Engine** para apresentar informações sobrepostas na tela e interagir com o jogador.

Neste capítulo vamos apresentar formas de interação com o jogador e depois construir objetos os necessários.

## 1. Como interagir com o jogador?

Durante o tempo do jogo é necessário interagir com o jogador de diversas formas, informando status de jogo, personagem e até mesmo guias de missões. Geralmente são informações em formatado texto e imagens 2D que se sobrepõe a tela para informar o jogador.

De outra forma, o comunicação de ações globais do jogo como por exemplo iniciar uma missão, salvar o jogo, sair do jogo e gerenciamento de configuração são formas de interação jogo vs player que utilizam menus através de botões, caixas rolantes e outros componentes.

### 1.1. Menos é Melhor

Uma dica simples, segundo as boas práticas de IHC (Interface Homem Computador), é **"Menos é melhor"**, onde devemos apresentar somente o necessário para o jogador e deixar a maior parte da experiência do jogador para o *Gameplay*.

Para construir um menu do jogo com **Unreal Engine** vamos seguir os seguintes passos:

1. Crie uma pasta para organizar os arquivos:

    ```sh
    Content\UI\
    ```

1. Crie um objeto blueprint `Widget` na pasta criada anteriormente.

    ```sh
    Content\UI\WBP_Menu
    ```

1. Edite e organize os elementos visuais do `Widget` e a lógica de programação.

1. Crie um *level* vazio para servir como base do menu.

1. Utilizando `Open Level Blueprint` para ao iniciar o *level*, `Begin Play` implemente a lógica para carregar o menu na cena.

Agora vamos apresentar informações do personagem na tela do jogador:

1. Crie um objeto blueprint `Widget` na pasta criada anteriormente.

   ```sh
   Content\UI\WBP_Character_info
   ```

1. Edite e organize os elementos visuais do `Widget` e a lógica de programação.

1. Na lógica de construção do `Widget` adicione uma variável para ter acesso a classe *Character* do personagem.

1. É possível apresentar o `Widget` quando o personagem é instancia na cena.

## 2. Implementando o Widget para o construir o menu do jogo

No **Unreal Engine** utilizamos um objeto com atributos e métodos próprios para o tratamento e organização de informação na interface do jogador, a classe de objetos `Widget` que vem acompanhado por um editor especial.

{% include imagelocal.html
    src="unreal/interface-ui-hud/EditEditorUtilityWidgetBlueprint.webp"
    alt="Figura: Widget Editor Blueprint."
    caption="Figura: Unreal Engine doc."
%}

### 2.1. Criando o Widget

![image-left](/assets/images/unreal/interface-ui-hud/unreal-engine-hud-menu.webp){: .align-left}
Utilizando o `Context Menu` escolha a opção `User Interface/Widget Blueprint`.

### 2.2. Usando o editor de de Widget

![image-left](/assets/images/unreal/interface-ui-hud/unreal-engine-hud-designer-graph.webp){: .align-left}
O editor de Widget é divido em :

- `Designer` para apresentação e manipulação de elementos visualmente.
- `Graph` para inserir a lógica de ações utilizando **Blueprint**.

### 2.3. Hierarchy - Hierarquia de elementos

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-hud-hierarquia.webp"
    alt="Figura: Widget Hierarchy."
    caption="Figura: Os elementos apresentados na Widget seguem uma hierarquia que determina o posicionamento relativo na tela."
%}

- Observe que tem vários objetos alinhados hierarquicamente e que neste caso vão nos ajudar e organizar a tela, sendo a raiz da árvore o objeto `BP_HUD_demo`;

- Os elementos `Canvas Panel`, `Horizontal Box`, `Vertical Box Grid Panel` tem propriedades para alinhamento dos elementos hierarquicamente abaixo;

- `Grid Panel` está hierarquicamente superior ao `Image_968`, isso significa que o texto deverá ser alinhado em relação ao `Grid Panel`;

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-hud-designer.webp"
    alt="Figura: Widget Designer."
    caption="Figura: Apresentação dos elementos descritos anteriormente."
%}

### 2.4. Entendo alinhamento utilizando Anchors

Para gerenciar melhor o posicionamento de objetos no `Widget Designer` vamos entender o objeto `Anchor` (Âncora).

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-hud-select-anchors.webp"
    alt="Figura: Widget Anchor alinhamento."
    caption="Figura: Ancorar um elemento é definir uma posição predefinida na tela."
%}

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-anchor-alinhamento.webp"
    alt="Figura: Widget icon Anchor."
    caption="Figura: No exemplo acima o elemento `Text` está posicionado na tela respeitando a âncora predefinida. A âncora pode ser alterada."
%}

Observe os valores de **Position** **X** e **Y** são zero, isso nos diz que a texto esta totalmente alinhado a âncora.

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-anchor-alinhamento-position.webp"
    alt="Figura: Widget Acnhors position UMG. "
    caption="Figura: Alterando a posição do objeto."
%}

Agora vamos dividir a âncora e alinhar o texto dentro das fronteiras da âncora.

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-anchor-alinhamento-separado.webp"
    alt="Figura: Widget Anchors Alinhamento separado UMG."
    caption="Figura: Alinhando o objeto. "
%}

Agora temos as propriedades `Offset Left` e `Right` com um valor que determina a posição do texto entre as fronteiras da âncora.

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-anchor-alinhamento-offset.webp"
    alt="Figura: Widget Canvas."
    caption="Figura: Propriedades Alinhamento."
%}

- `Size to Content` determina que o elemento se ajustara ao tamanho do conteúdo;

- `Alignment`  permite alinhar o elemento com a `Anchors`, como por exemplo inserir os valores X = 0.5 e Y = 0.5 para centralizar o objeto com a `Anchor`.

### 2.5. Horizontal ou Vertical Box

Estes elementos são utilizados para organizar os objetos Horizontal ou verticalmente. Ao adicionar elementos hierarquicamente abaixo de um `Vertical` ou `Horizontal box` eles serão organizados um ao lado do outro.

`Horizontal box`- Alinhamento Horizontal dos elementos.  

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-horizontal-box.webp"
    alt="Figura: Widget Horizontal Box UMG."
    caption="Figura: Alinhamento horizontal."
%}

`Vertical box` - Alinhamento vertical dos elementos.  

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-vertical-box.webp"
    alt="Figura: Widget Vertical Box UMG."
    caption="Figura: Alinhamento vertical."
%}

Nas propriedades do elemento dentro do `Vertical Box` selecione `Size Fill` para preencher todo espaço do painel.  

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-horizontal-box-fill.webp"
    alt="Figura: Widget Vertical Box Size fill UMG."
    caption="Figura: Preenchendo a área do objeto."
%}

### 2.6. Grid Panel

Como o nome anuncia, os elementos hierarquicamente agrupados abaixo do painel serão organizados em forma de um grid (matriz).

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-grid-panel.webp"
    alt="Figura: Widget Grid Panel UMG."
    caption="Figura: Vários objetos agrupados dentro de uma grade ou Grid."
%}

`Grid Panel` tem uma propriedade especial que determina qual o valor de preenchimento de cada coluna ou linha dentro do grid. O valor varia de 0 a 1, onde 0,5 é metade do espaço e 1 totalmente preenchido.

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-hud-grip-panel-column-fill.webp"
    alt="Figura: Widget Grid panel Column Fill UMG."
    caption="Figura: Alterando parâmetros do Grid."
%}

O elemento agrupado também terá as propriedades `Row` e `Col` preenchidas sinalizando qual a posição do elemento dentro do grid.

{% include imagelocal.html
    src="unreal/interface-ui-hud/unreal-engine-hud-grip-panel-row-col.webp"
    alt="Figura: Widget Grid Panel Row Col UMG."
    caption="Figura: Posição dos objetos dentro do Grid."
%}
