---
title: HUD - Interface com o jogador
description: Neste capitulo vamos implementar o HUD (Heads-up Display) do jogo.
tags: [Unreal Engine, HUD, user interface,UI]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
date: 2022-09-25 
---

***

- [Como interagir com o jogador?](#como-interagir-com-o-jogador)
  - [Menos é Melhor](#menos-é-melhor)
- [Implementando o Widget para o construir o menu do jogo](#implementando-o-widget-para-o-construir-o-menu-do-jogo)
  - [Criando o Widget](#criando-o-widget)
  - [Usando o editor de de Widget](#usando-o-editor-de-de-widget)
  - [Hierarchy - Hierarquia de elementos](#hierarchy---hierarquia-de-elementos)
  - [Entendo alinhamento utilizando Anchors](#entendo-alinhamento-utilizando-anchors)
  - [Horizontal ou Vertical Box](#horizontal-ou-vertical-box)
  - [Grid Panel](#grid-panel)
  
***

HUD (*Heads-up Display*) ou UI (*Use Interface*) é um objeto especial do **Unreal Engine** para apresentar informações sobrepostas na tela e interagir com o jogador.

Neste capitulo vamos apresentar formas de interação com o jogador e depois construir objetos os necessários.

## Como interagir com o jogador?

***

Durante o tempo do jogo é necessário interagir com o jogador de diversas formas, informando status de jogo, personagem e até mesmo guias de missões. Geralmente são informações em formatado texto e imagens 2D que se sobrepõe a tela para informar o jogador.

De outra forma, o comunicação de ações globais do jogo como por exemplo iniciar uma missão, salvar o jogo, sair do jogo e gerenciamento de configuração são formas de interação jogo vs player que utilizam menus através de botões, caixas rolantes e outros componentes.

### Menos é Melhor

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

## Implementando o Widget para o construir o menu do jogo

***

No **Unreal Engine** utilizamos um objeto com atributos e métodos próprios para o tratamento e organização de informação na interface do jogador, a classe de objetos `Widget` que vem acompanhado por um editor especial.

{% include imagebase.html
    src="unreal/interface_ui_hud/EditEditorUtilityWidgetBlueprint.webp"
    alt="Figura: Widget Editor Blueprint - Unreal Engine doc."
    caption="Figura: Widget Editor Blueprint - Unreal Engine doc."
%}

### Criando o Widget

Utilizando o `Context Menu` escolha a opção `User Interface/Widget Blueprint`.

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_hud_menu.webp"
    alt="Figura: Context Menu/ User Interface/ Widget Blueprint."
    caption="Figura: Context Menu/ User Interface/ Widget Blueprint."
%}

### Usando o editor de de Widget

O editor de Widget é divido em :

- `Designer` para apresentação e manipulação de elementos visualmente.

- `Graph` para inserir a lógica de ações utilizando **Blueprint**.

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_hud_designer_graph.webp"
    alt="Figura: Widget Designer e Graph."
    caption="Figura: Widget Designer e Graph."
%}

### Hierarchy - Hierarquia de elementos

Os elementos apresentados na Widget seguem uma hierarquia que determina o posicionamento relativo na tela.

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_hud_hierarquia.webp"
    alt="Figura: Widget Hierarchy."
    caption="Figura: Widget Hierarchy."
%}

- Observe que tem vários objetos alinhados hierarquicamente e que neste caso vão nos ajudar e organizar a tela, sendo a raiz da árvore o objeto `BP_HUD_demo`;

- Os elementos `Canvas Panel`, `Horizontal Box`, `Vertical Box Grid Panel` tem propriedades para alinhamento dos elementos hierarquicamente abaixo;

- `Grid Panel` está hierarquicamente superior ao `Image_968`, isso significa que o texto deverá ser alinhado em relação ao `Grid Panel`;

- Abaixo a apresentação dos elementos.

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_hud_designer.webp"
    alt="Figura: Widget Designer."
    caption="Figura: Widget Designer."
%}

### Entendo alinhamento utilizando Anchors

Para gerenciar melhor o posicionamento de objetos no `Widget Designer` vamos entender o objeto `Anchor` (Âncora).

- Ancorar um elemento é definir uma posição predefinida na tela.

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_hud_select_anchors.webp"
    alt="Figura: Widget Anchor alinhamento."
    caption="Figura: Widget Anchor alinhamento."
%}

- No exemplo abaixo o elemento `Text` está posicionado na tela respeitando a âncora predefinida. A âncora pode ser alterada.  

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_anchor_alinhamento.webp"
    alt="Figura: Widget icon Anchor."
    caption="Figura: Widget icon Anchor."
%}

- Observe os valores de **Position** **X** e **Y** são zero, isso nos diz que a texto esta totalmente alinhado a âncora.

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_anchor_alinhamento_position.webp"
    alt="Figura: Widget Acnhors position UMG. "
    caption="Figura: Widget Acnhors position UMG. "
%}

- Agora vamos dividir a âncora e alinhar o texto dentro das fronteiras da âncora.

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_anchor_alinhamento_separado.webp"
    alt="Figura: Widget Anchors Alinhamento separado UMG."
    caption="Figura: Widget Anchors Alinhamento separado UMG. "
%}

- Agora temos as propriedades `Offset Left` e `Right` com um valor que determina a posição do texto entre as fronteiras da âncora.

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_anchor_alinhamento_offset.webp"
    alt="Figura: Widget Canvas propriedades Alinhamento."
    caption="Figura: Widget Canvas propriedades Alinhamento."
%}

- `Size to Content` determina que o elemento se ajustara ao tamanho do conteúdo;

- `Alignment`  permite alinhar o elemento com a `Anchors`, como por exemplo inserir os valores X = 0.5 e Y = 0.5 para centralizar o objeto com a `Anchor`.

### Horizontal ou Vertical Box

Estes elementos são utilizados para organizar os objetos Horizontal ou verticalmente. Ao adicionar elementos hierarquicamente abaixo de um `Vertical` ou `Horizontal box` eles serão organizados um ao lado do outro.

- `Horizontal box`- Alinhamento Horizontal dos elementos.  

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_horizontal_box.webp"
    alt="Figura: Widget Horizontal Box UMG."
    caption="Figura: Widget Horizontal Box UMG."
%}

- `Vertical box` - Alinhamento vertical dos elementos.  

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_vertical_box.webp"
    alt="Figura: Widget Vertical Box UMG."
    caption="Figura: Widget Vertical Box UMG."
%}

- Nas propriedades do elemento dentro do `Vertical Box` selecione `Size Fill` para preencher todo espaço do painel.  

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_horizontal_box_fill.webp"
    alt="Figura: Widget Vertical Box Size fill UMG."
    caption="Figura: Widget Vertical Box Size fill UMG."
%}

### Grid Panel

Como o nome anuncia, os elementos hierarquicamente agrupados abaixo do painel serão organizados em forma de um grid (matriz).

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_grid_panel.webp"
    alt="Figura: Widget Grid Panel UMG."
    caption="Figura: Widget Grid Panel UMG."
%}

- `Grid Panel` tem uma propriedade especial que determina qual o valor de preenchimento de cada coluna ou linha dentro do grid. O valor varia de 0 a 1, onde 0,5 é metade do espaço e 1 totalmente preenchido.

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_hud_grip_panel_column_fill.webp"
    alt="Figura: Widget Grid panel Column Fill UMG."
    caption="Figura: Widget Grid panel Column Fill UMG."
%}

- O elemento agrupado também terá as propriedades `Row` e `Col` preenchidas sinalizando qual a posição do elemento dentro do grid.

{% include imagebase.html
    src="unreal/interface_ui_hud/blueprint_hud_grip_panel_row_col.webp"
    alt="Figura: Widget Grid Panel Row Col UMG."
    caption="Figura: Widget Grid Panel Row Col UMG."
%}
