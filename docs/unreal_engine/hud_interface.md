---
title: HUD - Interface com o jogador
description: HUD (Heads-up Display) ou UI (User Interface) é um objeto especial do Unreal Engine para apresentar informações sobrepostas na tela e interagir com o jogador.
tags: [Unreal Engine, HUD, user interface,UI]
---

[CafeGeek](http://CafeGeek.eti.br)  / [Desenvolvimento de jogos utilizando Unreal Engine](http://cafeGeek.eti.br/unreal_engine/index.html)

# HUD - Interface com o jogador
HUD (*Heads-up Display*) ou UI (*Use Interface*) é um objeto especial do **Unreal Engine** para apresentar informações sobrepostas na tela e interagir com o jogador.

Neste capitulo vamos apresentar formas de interação com o jogador e depois construir objetos os necessários.

## Índice
1. [Como interagir com o jogador?](#1)
    1. [Menos é Melhor](#1.1)
    1. [Para apresentar informações do personagem na tela do jogador com Unreal Engine os passos são seguintes:](#1.2)
    1. [Para apresentar informações do personagem na tela do jogador com Unreal Engine os passos são seguintes:](#1.3)
1. [Implementando o Widget para o construir o menu do jogo](#2)
    1. [Criando o Widget](#2.1)
    1. [Editor de de Widget](#2.2)
    1. [Hierarquia de elementos](#2.3)
    1. [Entendo alinhamento utilizando Anchors](#2.4)            
    1. [Horizontal ou Vertical Box](#2.5)    
    1. [Grid Panel](#26)    
1. [Lógica de programação do Widget - Graph](#3)
    1. [Event Construct para inicializar variáveis utilizadas no Widget](#3.1)
    1. [Button e eventos](#3.2)
    1. [Acionando o botão para abrir um Level](#3.3)    
    1. [Acionando o botão Sair para finalizar o jogo](#3.4)        
1. [Executando o menu](#4)
1. [Apresentando informações para o jogador](#5)
    1. [Barra de vida do jogador](#5.1)
    1. [O nome do jogador](#5.2)
1. [Organizando os objetos](#6)
    1. [Criando o objeto SaveGame para salvar dados do jogo](#6.1)    
    1. [Evento para apresentar o menu na tela](#6.2)    
    1. [Evento para abrir um Level](#6.3)    
    1. [Salvando dados](#6.4)    
    1. [Voltando ao jogo](#6.5)    
    1. [Evento para carregar dados](#6.6)        
    1. [Iniciando Game Instance no Widget](#6.7)                    
    1. [Efetuando as chamadas das funções](#6.8)
1. [ATIVIDADES](#7)
    1. [Apresentando mensagens para interagir com o personagem](#7.1)                      
    1. [Implementando o menu do jogo usando Game Instance](#7.2)                      

<a name="1"></a>
## 1. Como interagir com o jogador?
Durante o tempo do jogo é necessário interagir com o jogador de diversas formas, informando status de jogo, personagem e até mesmo guias de missões. Geralmente são informações em formatado texto e imagens 2D que se sobrepõe a tela para informar o jogador.       

De outra forma, o comunicação de ações globais do jogo como por exemplo iniciar uma missão, salvar o jogo, sair do jogo e gerenciamento de configuração são formas de interação jogo vs player que utilizam menus através de botões, caixas rolantes e outros componentes.

<a name="1.1"></a>
### 1.1 Menos é Melhor!
Uma dica simples, segundo as boas práticas de IHC (Interface Homem Computador), é **"Menos é melhor"**, onde devemos apresentar somente o necessário para o jogador e deixar a maior parte da experiência do jogador para o *Gameplay*.

<a name="1.2"></a>
### 1.2 Para construir um menu do jogo com Unreal Engine os passos são seguintes:
1. Crie uma pasta para organizar os arquivos:
```sh
 Content\UI\
 ```
1. Crie um objeto blueprint **Widget** na pasta criada anteriormente.
```sh
Content\UI\WBP_Menu
```
1. Edite e organize os elementos visuais do **Widget** e a lógica de programação.
1. Crie um *level* vazio para servir como base do menu.
1. Utilizando **Open Level Blueprint** para ao iniciar o *level*, **Begin Play** implemente a lógica para carregar o menu na cena.

<a name="1.3"></a>
### 1.3 Para apresentar informações do personagem na tela do jogador com Unreal Engine os passos são seguintes:
1. Crie um objeto blueprint **Widget** na pasta criada anteriormente.
```sh
Content\UI\WBP_Character_info
```
1. Edite e organize os elementos visuais do **Widget** e a lógica de programação.
1. Na lógica de construção do **Widget** adicione uma variável para ter acesso a classe *Character* do personagem.
1. É possível apresentar o **Widget** quando o personagem é instancia na cena.

<a name="2"></a>
## 2. Implementando o Widget para o construir o menu do jogo
No **Unreal Engine** utilizamos um objeto com atributos e métodos próprios para o tratamento e organização de informação na interface do jogador, a classe de objetos **Widget** que vem acompanhado por um editor especial.    

![Widget Editor](https://docs.unrealengine.com/Images/InteractiveExperiences/UMG/UserGuide/EditorUtilityWidgets/EditEditorUtilityWidgetBlueprint.webp)
*Figura: Widget Editor Blueprint - Unreal Engine doc*


<a name="2.1"></a>
### 2.1 Criando o Widget
Utilizando o **Context Menu** escolha a opção **User Interface/Widget Blueprint**.      
![blueprint_hud_menu](imagens/interface_ui_hud/blueprint_hud_menu.jpg)    
  *Figura: Context Menu/ User Interface/ Widget Blueprint*

<a name="2.2"></a>
### 2.2 Editor de de Widget
O editor de Widget é divido em :
- **Designer** para apresentação e manipulação de elementos visualmente.
- **Graph** para inserir a lógica de ações utilizando **Blueprint**.    

  ![blueprint_hud_designer_graph](imagens/interface_ui_hud/blueprint_hud_designer_graph.jpg)    
  *Figura: Widget Designer e Graph*

<a name="2.3"></a>
### 2.3 Hierarchy - Hierarquia de elementos
Os elementos apresentados na Widget seguem uma hierarquia que determina o posicionamento relativo na tela.      
![blueprint_hud_hierarquia](imagens/interface_ui_hud/blueprint_hud_hierarquia.jpg)  
  *Figura: Widget Hierarchy*

- Observe que tem vários objetos alinhados hierarquicamente e que neste caso vão nos ajudar e organizar a tela, sendo a raiz da árvore o objeto **BP_HUD_demo**.
- Os elementos **Canvas Panel, Horizontal Box, Vertical Box Grid Panel** tem propriedades para alinhamento dos elementos hierarquicamente abaixo.
- **Grid Panel** está hierarquicamente superior ao **Image_968"**, isso significa que o texto deverá ser alinhado em relação ao **Grid Panel**
- Abaixo a apresentação dos elementos.

![blueprint_hud_designer](imagens/interface_ui_hud/blueprint_hud_designer.jpg)    
  *Figura: Widget Designer*

<a name="2.4"></a>
### 2.4 Entendo alinhamento utilizando Anchors
Para gerenciar melhor o posicionamento de objetos no **Widget Designer** vamos entender o objeto **Anchor** (Âncora).   

- Ancorar um elemento é definir uma posição predefinida na tela.   
![blueprint_hud_select_anchors](imagens/interface_ui_hud/blueprint_hud_select_anchors.jpg)      
  *Figura: Widget Anchor alinhamento*
- No exemplo abaixo o elemento **Text** está posicionado na tela respeitando a âncora predefinida. A âncora pode ser alterada.  
![blueprint_anchor_alinhamento](imagens/interface_ui_hud/blueprint_anchor_alinhamento.jpg)    
  *Figura: Widget Anchor*
- Observe os valores de **Position** **X** e **Y** são zero, isso nos diz que a texto esta totalmente alinhado a âncora.  
![blueprint_anchor_alinhamento_position](imagens/interface_ui_hud/blueprint_anchor_alinhamento_position.jpg)    
  *Figura: Widget Acnhors position UMG*

- Agora vamos dividir a âncora e alinhar o texto dentro das fronteiras da âncora.   
![blueprint_anchor_alinhamento_separado](imagens/interface_ui_hud/blueprint_anchor_alinhamento_separado.jpg)
  *Figura: Widget Anchors Alinhamento separado UMG*
- Agora temos as propriedades **Offset Left** e **Right** com um valor que determina a posição do texto entre as fronteiras da âncora.   
![blueprint_anchor_alinhamento_offset](imagens/interface_ui_hud/blueprint_anchor_alinhamento_offset.jpg)    
  *Figuera: Widget Canvas propriedades Alinhamento*
- **Size to Content** determina que o elemento se ajustara ao tamanho do conteúdo.
- **Alignment**  permite alinhar o elemento com a **Anchors**, como por exemplo inserir os valores X = 0.5 e Y = 0.5 para centralizar o objeto com a **Anchor**.

<a name="2.5"></a>
### 2.5 Horizontal ou Vertical Box
Estes elementos são utilizados para organizar os objetos Horizontal ou verticalmente. Ao adicionar elementos hierarquicamente abaixo de um **Vertical** ou **Horizontal box** eles serão organizados um ao lado do outro.   

- Horizontal box  
![blueprint_horizontal_box](imagens/interface_ui_hud/blueprint_horizontal_box.jpg)     
  *Figura: Widget Horizontal Box UMG*

- Vertical box  
![blueprint_vertical_box](imagens/interface_ui_hud/blueprint_vertical_box.jpg)    
  *Figura: Widget Vertical Box UMG*

- Nas propriedades do elemento dentro do **Vertical Box** selecione **Size Fill** para preencher todo espaço do painel.  
![blueprint_horizontal_box_fill](imagens/interface_ui_hud/blueprint_horizontal_box_fill.jpg)      
  *Figura: Widget Vertical Box Size fill UMG*

<a name="2.6"></a>
### 2.6 Grid Panel
Como o nome anuncia, os elementos hierarquicamente agrupados abaixo do painel serão organizados em forma de um grid (matriz).   
  ![blueprint_grid_panel](imagens/interface_ui_hud/blueprint_grid_panel.jpg)    
  *Figura: Widget Grid Panel UMG*
- **Grid Panel** tem uma propriedade especial que determina qual o valor de preenchimento de cada coluna ou linha dentro do grid. O valor varia de 0 a 1, onde 0,5 é metade do espaço e 1 totalmente preenchido.  
  ![blueprint_hud_grip_panel_column_fill](imagens/interface_ui_hud/blueprint_hud_grip_panel_column_fill.jpg)    
  *Figura: Widget Grid panel Column Fill UMG*

- O elemento agrupado também terá as propriedades **Row** e **Col** preenchidas sinalizando qual a posição do elemento dentro do grid.    
  ![blueprint_hud_grip_panel_row_col](imagens/interface_ui_hud/blueprint_hud_grip_panel_row_col.jpg)    
  *Figura: Widget Grid Panel Row Col UMG*

<a name="3"></a>
## 3.  Lógica de programação do Widget - Graph
A lógica de controle de ações dos botões e a inicialização está em **Graph**, onde encontramos alguns eventos já conhecidos como por exemplo **Event Construct** e **Tick**.    

<a name="3.1"></a>
### 3.1 Event Construct para inicializar variáveis utilizadas no Widget
Para que o objeto menu tenha acesso a propriedades da classe do jogador vamos inicialiazar a uma variável local utilizando **Event Construct**.
Ao iniciar o Widget definimos uma variável **Jogador** do tipo **BP_Hero** para que possamos ter acesso as propriedades nome e vida por exemplo.      
![blueprint_hud_event_construct](imagens/interface_ui_hud/blueprint_hud_event_construct.jpg)
  *Figura: Widget Graph Event Construct*

<a name="3.2"></a>
### 3.2 Botões e eventos (Button and Events)
Os elementos do tipo **Button** tem eventos relacionados na sua estrutura, como por exemplo:**On Clicked**,**On Pressed** e outros.

<a name="3.3"></a>
### 3.3 Acionando o botão para abrir um Level
Vamos utilizar o evento **OnClick** para executar a função **Open Level** para carregar outro *level* do projeto. Deverá ser informado o nome do *Level* que queremos abrir.   
![blueprint_hud_open_level](imagens/interface_ui_hud/blueprint_hud_open_level.jpg)    
  *Figura: Widget HUD Blueprint open Level*

<a name="3.4"></a>
### 3.4 Acionando o botão Sair para finalizar o jogo
Ao clicar no botão Sair vamos chamar a função **Quit Game** que finaliza do jogo.  
![blueprint_hud_quit_game](imagens/interface_ui_hud/blueprint_hud_quit_game.jpg)    
  *Figura: Widget HUD Blueprint Quit Game*

<a name="4"></a>
## 4. Executando o menu
Neste passo vamos criar um *Level* vazio para executar o menu, quando o menu for chamado a tela inteira deve mudar.   
Caso o Widget seja o menu principal que deverá ser chamado no início do jogo é necessário adicionar o mesmo em [Level e inicialização](organizando_pastas_e_logo.html#2)

1. *Empty Level* (Level Vazio).    
![blueprint_empty_level](imagens/interface_ui_hud/blueprint_empty_level.jpg)      
  *Figura: Widget Empty Level*
1. Em **Open Level blueprint** vamos adicionar a lógica para criar um objeto do tipo **BP_HUD_Demo** e adicionar na tela com a função **AddToViewPort**.   
![blueprint_hud_addviewport](imagens/interface_ui_hud/blueprint_hud_addviewport.jpg)
  *Figura: Widget HUD Add ViewPort*

<a name="5"></a>
## 5. Apresentando informações para o Jogador

Para este passo vamos implementar os seguintes elementos para apresentar informações para o jogador, como por exemplo a vida do personagem.    

![blueprint_hud_player_elements](imagens/interface_ui_hud/blueprint_hud_player_elements.jpg)    
  *Figura: Widget HUD Player Elements*

- **TextBlock** - Para apresentar o nome do jogador.
- **ProgressBar** - Para apresentar a vida do jogador.

<a name="5.1"></a>
### 5.1 Fazendo a ligação do elemento da interface com uma função
Devemos conectar os elementos da interface com funções por meio de uma propriedade **Bind**.   
![blueprint_hud_progressbar_bind](imagens/interface_ui_hud/blueprint_hud_progressbar_bind.jpg)      
  *Figura: Widget HUD Progress Bar Bind*

<a name="5.2"></a>
### 5.2 Função do calculo de vida do jogador
Para calcular o valor da vida do jogador vamos implementar uma função, abaixo a lógica da função associada a elemento **ProgressBar**.    

![blueprint_hud_function_vida_jogador](imagens/interface_ui_hud/blueprint_hud_function_vida_jogador.jpg)    
  *Figura: Widget HUD Progress Bar function*

<a name="5.3"></a>
### 5.3 Função para pegar o nome do jogador
Podemos utilizar [Variáveis estruturadas](structure_variaveis_estruturadas.html) para manipulação das propriedades do jogador.   
![blueprint_hud_function_nome_jogador](imagens/interface_ui_hud/blueprint_hud_function_nome_jogador.jpg)      
  *Figura: Widget HUD name player function*

<a name="6"></a>
## 6. Organizando os objetos
Vamos organizar todos os objetos criados para controlar melhor a lógica de programação de cada elemento, considerando:  
- Separação da lógica de negócios e os visuais de sua IU
- Permite iteração rápida de layout e visuais
- Depuração eficaz da lógica de negócios
- Performance

<a name="6.1"></a>
### 6.1 Criando o objeto SaveGame para salvar dados do jogo
Para exemplificar algumas funções do menu como por exemplo salvar dados do jogo vamos realizar as seguintes operações.

1.  Implementar um objeto BP_SaveGameDemo do tipo **SaveGame**, para isso utilizamos o menu de contexto e escolhemos **Blueprint**.        

  ![blueprint_save_game_object](imagens/saveload/blueprint_save_game_object.jpg)    
  *Figura: Class SaveGame*   
1. Adicionamos variáveis dentro do objeto para definir o que deve ser salvo, neste exemplo utilizaremos a variável **JogadorInfo** do tipo **S_jogador** que é uma
  [Variável Structure](structure_variaveis_estruturadas.html).     

  ![blueprint_save_game_variable](imagens/saveload/blueprint_save_game_variable.jpg)    
  *Figura: SaveGame variáveis*

Nos próximos passos vamos criar o objeto *BP_GameInstanceJogo* do tipo [**GameInstance**](gameinstance_state_mode.html#5) e adicionar os eventos customizados (*Add custon event*) a seguir.

<a name="6.2"></a>
### 6.2 Evento para apresentar o menu na tela
Implementamos um evento customizado para adicionar lógica dos eventos.
![blueprint_gameinstance_openmenu](imagens/gamemode/blueprint_gameinstance_openmenu.jpg)    
  *Figura: Widget HUD Blueprint Logic Add to ViewPort*
- **Show Mouse Cursor** - Esta variável é uma propriedade de **PlayerController**  e Configurando para **true** o ponteiro do mouse deve aparecer na tela.
- **Set Input Mode UI Only** - Esta função determina que o controle de entrada de dados será somente pelo **Widget**.

<a name="6.3"></a>
### 6.3 Evento para abrir um Level
Neste passo vamos adicionar um evento customizado ,*add custom event*, para carregar um *level* na cena.    
![blueprint_gameinstance_openlevel](imagens/gamemode/blueprint_gameinstance_openlevel.jpg)      
  *Figura: Logic Open Level*
- **Open Level** - Função para abrir um *Level* do jogo. É necessário informar o nome do *level* no parâmetro *Level Name*.
- **Set Input Mode Game Only** - Esta função determina que o controle de entrada de dados será somente pelo jogo.

<a name="6.4"></a>
### 6.4 Salvando dados
Para salvar informações vamos utilizar a função **Save Game to Slot**.
![blueprint_gameinstance_savegame](imagens/gamemode/blueprint_gameinstance_savegame.jpg)
*Figura: Logic SaveGame slot*
- **Create Save Game Object** - Cria um objeto do tipo **BP_SaveGameDemo**, definido anteriormente.
- **Save Game to Slot** - Salva os dados e cria um **Slot Name** *Salvo1*.

<a name="6.5"></a>
### 6.5 Evento para carregar dados
Para carregar dados salvos utilizamos a função **Load Game from Slot** passando como parâmetro o nome do *slot*.
![blueprint_gameinstance_loaddada](imagens/gamemode/blueprint_gameinstance_loaddada.jpg)      
  *Figura: Logic Load Game From Slot*
- **Does Save Game Exist** - Retorna verdadeiro se encontra um jogo salvo com o nome *Salvo1* informado em **Slot Name**.
- **Load Game from Slot** - Carrega as variáveis salvas em **Slot Name**, neste caso *Salvo1*.

<a name="6.6"></a>
### 6.6 Voltando ao jogo
Vamos agora remover o menu ou objeto **Widget** da cena utilizando a função **Remove from parent**.
![blueprint_gameinstance_returngame](imagens/gamemode/blueprint_gameinstance_returngame.jpg)    
  *Figura: Remove From Parent*
- **Remove from Parent** - Remove o widget de seu **Widget** pai. Se este **widget** foi adicionado à tela do jogador ou à janela de visualização, ele também será removido desses recipientes.

<a name="6.7"></a>
### 6.7 Iniciando Game Instance no Widget
No objeto BP_HUD_Demo vamos substituir ou adicionar a lógica dos botões, mas antes devemos inicializar a **Game Instance**.    
![blueprint_hud_gameinstance](imagens/gamemode/blueprint_hud_gameinstance.jpg)
*Figura: Widget HUD gameinstance*

<a name="6.8"></a>
### 6.8 Efetuando as chamadas das funções
No evento click dos botões vamos adicionar os eventos construídos dentro da *Game Instance* isolando a regra de negócios (dados e lógica e manipulação).   
![blueprint_hud_gameinstance_openlevel](imagens/gamemode/blueprint_hud_gameinstance_openlevel.jpg)      
  *Figura: Widget HUD with Game Instance on click*
> Repetimos esse processo para associar todos os eventos aos botões.

<a name="7"></a>
## 7 ATIVIDADES
<a name="7.1"></a>
### 7.1 Apresentando mensagens para interagir com o personagem
1. Regras
    1. Implemente um objeto *Widget* com um texto colorido e formatado.
    1. O *Widget* é acionado pressionando a tecla F quando o personagem ficar próximo.
1. Desafio      
    1. Implemente um gameplay em primeira pessoa dentro de uma casa

### 7.2 Implementando o menu do jogo usando Game Instance
1. Regras
    1. Implemente o menu principal do jogo com as opções : Play e Quit.
    1. Implemente o menu de Resumo do jogo com as opções : Resume, Load, Save, Home e Quit. O menu é acionado com a tecla M durante a *gameplay*. Implemente também toda a lógica das ações dos botões Load, Save e Quit.
    1. Implemente uma Game Instance e adicione os seguintes objetos:
      - **Open Menu Principal** para abrir o menu principal;
      - **Open Menu Resume** para abrir o menu de pausa e resumo do jogo;
1. Desafio
    1. Apresente vários elementos visuais no menu, como por exemplo: Botões e imagens de fundo personalizados.

***
## Referências
- [1.1 - HUD Example](https://docs.unrealengine.com/en-US/Resources/ContentExamples/Blueprints_HUD/1_1/index.html)
- [User Interfaces & HUDs](https://docs.unrealengine.com/en-US/InteractiveExperiences/Framework/UIAndHUD/index.html)
-[Anchors](https://docs.unrealengine.com/en-US/InteractiveExperiences/UMG/UserGuide/Anchors/index.html)
- [Quick Start](https://docs.unrealengine.com/en-US/InteractiveExperiences/UMG/QuickStart/index.html)