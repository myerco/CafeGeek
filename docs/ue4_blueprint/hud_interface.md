---
title: HUD - Interface com o jogador
tags: [Unreal Engine,HUD,user interface,hud]
---

[CafeGeek](https://myerco.github.io/unreal-engine)  / [Desenvolvimento de jogos utilizando Unreal Engine 4](https://myerco.github.io/unreal-engine/ue4_blueprint/index.html)

# HUD - Interface com o jogador
HUD (Heads-up Display) ou UI (Use Interface) é um objeto especial da **Unreal Engine** para apresentar informações sobrepostas na tela e interagir com o jogador.

Vamos apresentar formas de interação e depois construir objetos os necessários.

## Índice
1. [Como interagir com o jogador?](#1)
    1. [Menos é Melhor](#11)
1. [Implementando o Widget para o construir o menu do jogo](#2)
    1. [Criando o Widget](#21)
    1. [Editor de de Widget](#22)
    1. [Hierarquia de elementos](#23)
    1. [Entendo alinhamento utilizando Anchors](#24)            
    1. [Horizontal ou Vertical Box](#25)    
    1. [Grid Panel](#26)    
1. [Lógica de programação do Widget - Graph](#3)
    1. [Event Construct para inicializar variáveis utilizadas no Widget](#31)
    1. [Button e eventos](#32)
    1. [Acionando o botão para abrir um Level](#33)    
    1. [Acionando o botão Sair para finalizar o jogo](#34)        
1. [ Criando um Level Vazio para adicionar o Widget](#4)

<a name="1"></a>
## 1. Como interagir com o jogador?
Durante o tempo do jogo é necessário interagir com o jogador de diversas formas, informando status de jogo, personagem e até mesmo guias de missões. Geralmente são informações em formatado texto e imagens 2D que se sobrepõe a tela para informar o jogador.       

De outra forma, o comunicação de ações globais do jogo como por exemplo iniciar uma missão, salvar o jogo, sair do jogo e gerenciamento de configuração são formas de interação jogo vs player que utilizam menus através de botões, caixas rolantes e outros componentes.

<a name="11"></a>
## 1.1 Menos é Melhor!
Uma dica simples, segundo as boas práticas de IHC (Interface Homem Computador), é **"Menos é melhor"**, onde devemos apresentar somente o necessário para o jogador e deixar a maior parte da experiência do jogador para o *Gameplay*.

<a name="2"></a>
## 2. Implementando o Widget para o construir o menu do jogo

<a name="21"></a>
### 2.1 Criando o Widget
Utilizando o **Context Menu** escolha a opção **User Interface/Widget Blueprint**.   
![](../imagens/interface_ui_hud/blueprint_hud_menu.jpg)

<a name="2.2"></a>
### 2.2 Editor de de Widget
O editor de Widget é divido em :
- **Designer** para apresentação e manipulação de elementos visualmente.
- **Graph** para inserir a lógica de ações utilizando **Blueprint**.      
  ![](../imagens/interface_ui_hud/blueprint_hud_designer_graph.jpg)

<a name="2.3"></a>
### 2.3 Hierarquia de elementos
Os elementos apresentados na Widget seguem uma hierarquia que determina o posicionamento relativo na tela.  
![](../imagens/interface_ui_hud/blueprint_hud_hierarquia.jpg)
- Observe que tem vários objetos alinhados hierarquicamente e que neste caso vão nos ajudar e organizar a tela, sendo a raiz da árvore o objeto **BP_HUD_demo**.
- **Canvas Panel, Horizontal Box, Vertical Box Grid Panel** tem propriedades para alinhamento dos elementos hierarquicamente abaixo.
- **Grid Panel** está hierarquicamente superior ao **Image_968"**, isso significa que o texto deverá ser alinhado em relação ao **Grid Panel**
- Abaixo a apresentação dos elementos.  
![](../imagens/interface_ui_hud/blueprint_hud_designer.jpg)

<a name="2.4"></a>
### 2.4 Entendo alinhamento utilizando Anchors
Para gerenciar melhor o posicionamento de objetos no **Widget Designer** vamos entender o objeto **Anchor** (Âncora).   

- Ancorar um elemento é definir uma posição predefinida na tela.   
![](../imagens/interface_ui_hud/blueprint_hud_select_anchors.jpg)
- No exemplo abaixo o elemento **Text** está posicionado na tela respeitando a âncora predefinida. A âncora pode ser alterada.  
![](../imagens/interface_ui_hud/blueprint_anchor_alinhamento.jpg)
- Observe os valores de **Position** **X** e **Y** são zero, isso nos diz que a texto esta totalmente alinhado a âncora.  
![](../imagens/interface_ui_hud/blueprint_anchor_alinhamento_position.jpg)
- Agora vamos dividir a âncora e alinhar o texto dentro das fronteiras da âncora.   
![](../imagens/interface_ui_hud/blueprint_anchor_alinhamento_separado.jpg)
- Agora temos as propriedades **Offset Left** e **Right** com um valor que determina a posição do texto entre as fronteiras da âncora.   
![](../imagens/interface_ui_hud/blueprint_anchor_alinhamento_offset.jpg)

<a name="25"></a>
### 2.5 Horizontal ou Vertical Box
Ao adicionar elementos hierarquicamente abaixo de um **Vertical** ou **Horizontal box** eles serão organizados um ao lado do outro.   
![](../imagens/interface_ui_hud/blueprint_horizontal_box.jpg)     
![](../imagens/interface_ui_hud/blueprint_vertical_box.jpg)

- Nas propriedades do elemento dentro do **Vertical Box** selecione **Size Fill** para preencher todo espaço do painel.  
![](../imagens/interface_ui_hud/blueprint_horizontal_box_fill.jpg)

<a name="26"></a>
### 2.6 Grid Panel
Como o nome anuncia, os elementos hierarquicamente agrupados abaixo do painel serão organizados em forma de um grid (matriz).   
![](../imagens/interface_ui_hud/blueprint_grid_panel.jpg)
- **Grid Panel** tem uma propriedade especial que determina qual o valor de preenchimento de cada coluna ou linha dentro do grid. O valor varia de 0 a 1, onde 0,5 é metade do espaço e 1 totalmente preenchido.  

![](../imagens/interface_ui_hud/blueprint_hud_grip_panel_column_fill.jpg)
- O elemento agrupado também terá as propriedades **Row** e **Col** preenchidas sinalizando qual a posição do elemento dentro do grid.    
]![](../imagens/interface_ui_hud/blueprint_hud_grip_panel_row_col.jpg)

<a name="3"></a>
## 3.  Lógica de programação do Widget - Graph
A lógica de controle de ações dos botões e a inicialização está em **Graph**, onde encontramos alguns eventos já conhecidos como por exemplo **Event Construct** e **Tick**.    

<a name="31"></a>
### 3.1 Event Construct para inicializar variáveis utilizadas no Widget
![](../imagens/interface_ui_hud/blueprint_hud_event_construct.jpg)
- Ao iniciar o Widget definimos uma variável **Jogador** do tipo **BP_Hero** para que possamos ter acesso as propriedades nome e vida por exmeplo.

<a name="32"></a>
### 3.2 Button e eventos
Os elementos do tipo **Button** tem eventos relacionados na sua estrutura, como por exemplo:**On Clicked**,**On Pressed** e outros.

<a name="33"></a>
### 3.3 Acionando o botão para abrir um Level
Vamos utilizar o evento OnClick para executar a função **Open Level**. Deverá ser informado o nome do *Level* que queremos abrir.   
![](../imagens/interface_ui_hud/blueprint_hud_open_level.jpg)

<a name="34"></a>
### 3.4 Acionando o botão Sair para finalizar o jogo
Ao clicar no botão Sair vamos chamar a função **Quit Game** que finaliza do jogo.  
![](../imagens/interface_ui_hud/blueprint_hud_quit_game.jpg)

<a name="4"></a>
## 4. Criando um Level Vazio para adicionar o Widget
Neste passo vamos criar um *Level* Vazio para que possamos adicionar a lógica de chamada do Widget menu.   
![](../imagens/interface_ui_hud/blueprint_empty_level.jpg)

Caso o Widget seja o menu principal que deverá ser chamado no início do jogo é necessário adicionar o mesmo em [Level e inicialização](https://myerco.github.io/unreal-engine/ue4_blueprint/organizando.html#2)

***
## Referências
- [1.1 - HUD Example](https://docs.unrealengine.com/en-US/Resources/ContentExamples/Blueprints_HUD/1_1/index.html)
- [User Interfaces & HUDs](https://docs.unrealengine.com/en-US/InteractiveExperiences/Framework/UIAndHUD/index.html)
-[Anchors](https://docs.unrealengine.com/en-US/InteractiveExperiences/UMG/UserGuide/Anchors/index.html)
- [Quick Start](https://docs.unrealengine.com/en-US/InteractiveExperiences/UMG/QuickStart/index.html)

***
## Tags
[Blueprint](https://myerco.github.io/unreal-engine/ue4_blueprint/blueprint.html), [Unreal Engine](https://myerco.github.io/unreal-engine/ue4_blueprint/index.html), [CafeGeek](https://myerco.github.io/unreal-engine/)
