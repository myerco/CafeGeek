---
title: Trabalhando com Animação 2D
description: Em este capitulo iremos implementar animações em duas dimensões utilizando o Plugin Paper2D no Unreal Engine.
tags: [Unreal Engine, Animação 2D,Paper 2D]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
date: 2022-10-03 
---

***

- [1. O que é Animação 2D?](#1-o-que-é-animação-2d)
- [2. Como o Unreal Engine trabalha com animação 2D?](#2-como-o-unreal-engine-trabalha-com-animação-2d)
  - [2.1. Sprites](#21-sprites)
  - [2.2. Flipbook](#22-flipbook)
  - [2.3. Tile Sets](#23-tile-sets)
  - [2.4. Tile Maps](#24-tile-maps)
- [3. Habilitando o plugin Paper2D e criando as pastas do projeto](#3-habilitando-o-plugin-paper2d-e-criando-as-pastas-do-projeto)
- [4. Preparando o ViewPort](#4-preparando-o-viewport)
- [5. Preparando as texturas](#5-preparando-as-texturas)
- [6. Preparando os Sprites do projeto](#6-preparando-os-sprites-do-projeto)
  - [6.1. Criando sprites](#61-criando-sprites)
  - [6.2. Agrupando sprites em Tile Sets](#62-agrupando-sprites-em-tile-sets)
  - [6.3. Implementando uma cena utilizando Tile Map](#63-implementando-uma-cena-utilizando-tile-map)
  - [6.4. Criando sequencias de animação utilizando Flipbooks](#64-criando-sequencias-de-animação-utilizando-flipbooks)
- [7. Adicionando e configurando o personagem do tipo PaperCharacter](#7-adicionando-e-configurando-o-personagem-do-tipo-papercharacter)
  - [7.1. Implementando a lógica de animação do personagem do tipo PaperCharacter](#71-implementando-a-lógica-de-animação-do-personagem-do-tipo-papercharacter)
  - [7.2. Implementando o canhão](#72-implementando-o-canhão)

***

{% include imagebase.html
    src="unreal/animacao/unreal_engine_paper2d_project.webp"
    alt="Figura: Paper 2D"
    caption=""
%}

## 1. O que é Animação 2D?

***

Animação em duas dimensões é uma técnica que utiliza sequenciamento de imagens estáticas.

{% include image.html
    src="https://maestrofilmes.com.br/wp-content/uploads/2019/10/alfabeta_maio_texto1-1080x614-1024x582.png"
    alt="Figura: Animação 2D: de um simples desenho à solução para uma empresa"
    caption="O vídeo em animação nada mais é que a passagem rápida de objetos ou imagens que, posicionados, dão a ilusão do movimento. A animação é uma Ilusão de ótica, ou seja, ela mostra movimento com imagens que, na verdade, são estáticas"
    ref="https://maestrofilmes.com.br/animacao-2d/"
%}

## 2. Como o Unreal Engine trabalha com animação 2D?

***

O Unreal Engine implementa animação 2D utilizando o plugin **Paper2D** que facilita a manipulação e importação de elementos em duas dimensões. O sistema **Paper 2D** é um sistema baseado em *sprite* para a criação de jogos híbridos 2D e 2D / 3D inteiramente dentro do editor.

O **Paper 2D** é baseado em um conjunto de elementos que são :

### 2.1. Sprites

Desenhos de duas dimensões, é uma malha plana com textura mapeada e um material associado.

{% include image.html
    src="https://producaodejogos.com/wp-content/uploads/2018/05/exemplo_pixel.jpg"
    alt="Figura: Piskel - Guia do Editor Online para Pixel Art e Sprites Animados [2018]"
    caption="O pixel é o menor ponto de uma imagem digital e uma pixel art é a criação de um objeto ponto a ponto utilizando pixels. Na imagem abaixo temos uma boa visualização do que é pixel e como podemos criar um objeto trabalhando cores e pontos no Piskel."
    ref="https://producaodejogos.com/piskel-guia-para-pixel-art-e-sprites-animados/"
%}

### 2.2. Flipbook

Objeto para sequenciar um conjunto de *sprites* simulando animações;

{% include image.html
    src="https://docs.unrealengine.com/5.1/Images/animating-characters-and-objects/Paper2D/Flipbooks/flipbook-banner-2.webp"
    alt="Figura: Paper 2D Flipbooks"
    caption="A melhor maneira de pensar em Paper 2D Flipbooks (ou Flipbooks para abreviar) é na forma de animação desenhada à mão, onde uma série de imagens ligeiramente diferentes são viradas para produzir o que parece ser movimento."
    ref="https://docs.unrealengine.com/5.1/en-US/paper-2d-flipbooks-in-unreal-engine/"
%}

### 2.3. Tile Sets

Objeto para agrupar e manipular um conjunto de *sprites*;

{% include image.html
    src="https://docs.unrealengine.com/5.1/Images/animating-characters-and-objects/Paper2D/TileMaps/CreatedTitleSet.webp"
    alt="Figura: Paper 2D Tile Sets / Tile Mapss"
    caption="Editor de Tile Set."
    ref="https://docs.unrealengine.com/5.1/en-US/paper-2d-tile-sets-and-tile-maps-in-unreal-engine/"
%}

### 2.4. Tile Maps

Objeto para "pintar" um grupo de *sprites* as cenas utilizando `Tile Set`.

{% include image.html
    src="https://docs.unrealengine.com/5.1/Images/animating-characters-and-objects/Paper2D/TileMaps/TileMapEditorWindow.webp"
    alt="Figura: Paper 2D Tile Sets / Tile Mapss"
    caption="Editor de Tile Map."
    ref="https://docs.unrealengine.com/5.1/en-US/paper-2d-tile-sets-and-tile-maps-in-unreal-engine/"
%}

## 3. Habilitando o plugin Paper2D e criando as pastas do projeto

Antes de iniciar o trabalho devemos habilitar o plugin `Paper2D` em menu `Edit` > `Plugins`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_paper2d_plugin.webp"
    alt="Figura: Unreal Engine - Animação 2d - habilitando o Plugin Paper2D (Enabled)."
    caption="Após habilitar o plugin é necessário reiniciar o Unreal Engine."
%}

Abixo a sugestão de organização de pastas.

```bash
|-- Animacao2D
|   |-- Core
|   |   |-- Characters
|   |       |-- BP_Character
|   |   |-- DataSets
|   |       |-- ECharacterState
|   |   |-- Engine
|   |       |-- BP_GameMode
|   |       |-- BP_PlayerController
|   |   |-- Inputs
|   |   |-- Itens
|   |       |-- BP_Item
|   |-- Characters
|   |   |-- Samurai
|   |   |-- FlatBoy
|   |   |-- Punk
|   |-- Environment
|   |   |-- Factory
|   |   |-- Forest
|   |-- Maps      
|   |   |-- LevelTest
```

## 4. Preparando o ViewPort

Podemos organizar os elementos que são apresentados na cena predefinindo coordenadas no eixo Y, utilizando o menu `Edit` > `Project Settings` navegue até `2D` para adicionar camadas/*Layers* e coordenadas de profundidade ao `ViewPort`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_paper2d_project_settings.webp"
    alt="Figura: Unreal Engine - Animação 2D - Project Settings 2D."
    caption="Adicionando Snap Layers do exemplo acima podemos criar 3 camadas em profundidades diferentes."
%}

- `Foreground` - Camada para os *sprites* que devem ficar na frente da cena, `Depth` = 100;

- `Default` - Camada para os *sprites* que devem estão alinhados com o personagem, `Depth` = 0;

- `Background` - Camada para os *sprites* que devem ficar atrás da cena, `Depth` = -500;

Após a configuração no `ViewPort` devem aparecer as opções para organizar os objetos em camadas na cena.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_paper2d_viewport.webp"
    alt="Figura: Unreal Engine - Animação 2D - ViewPort Snap."
    caption="As layers criadas anteriormente devem aparecer na barra de ações."
%}

Os objetos adicionados na cena devem ficar no *snap* selecionado obedecendo a localização Y predefinida, esse processo é similar ao trabalho de desenho por camadas.

Para movimentar objetos entre os *snaps* selecione o objeto e pressione :

- CTRL + PAGE DOWN para posicionar o objeto na camada anterior;

- CTRL + PAGE UP para posicionar o objeto na camada posterior;

Para melhorar a visualização do cenário podemos configurar a visualização do `ViewPort` para **Right** a fim de controlar somente os eixos Z e X.

{% include imagebase.html
    src="unreal/animacao/unreal_engine_paper2d_viewport_xy.webp"
    alt="Figura: Unreal Engine - Animação 2D - ViewPort Rigth Z,X."
    caption="Visualização Right no ViewPort."
%}

## 5. Preparando as texturas

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_paper2d_details_texture_2d.webp"
    alt="Figura: Unreal Engine - Animação 2D, preparando a textura - Details Texture parameters 2D."
    caption="A fim de otimizar a renderização das texturas aplicamos os seguintes parâmetros para cada objeto."
%}

- `Compression Settings`: UseInterface2D (RGBA);

- `Mip Gen Settings`: NoMipMaps

> "A geração do Mip-map ocorre durante a importação da Textura e cria uma cadeia de Mip-map para a Textura. A cadeia mip-map consiste em vários níveis da imagem de amostra, cada um com metade da resolução do nível anterior. Esses dados permitem que a placa gráfica renderize mais rápido ao usar os mips inferiores (menos largura de banda da memória) e também reduz o aliasing da textura (cintilante) que se torna visível ao ter textura detalhada em certas distâncias."

Podemos aplicar automaticamente para uma ou várias texturas selecionadas usamos o menu de contexto selecionando o arquivo e depois `Sprite Actions` > `Apply Paper2D Texture Settings`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_paper2d_apply_texture_settings.webp"
    alt="Figura: Unreal Engine - Animação 2D - Apply Papper2D Texture Settings."
    caption="Aplicamos a configuração em vários arquivos."
%}

## 6. Preparando os Sprites do projeto

***

Um Sprite em papel 2D é uma malha plana com mapeamento de textura e material associado que pode ser renderizado no mundo, criado inteiramente no Unreal Engine 4 (UE4). Em termos mais simples, é uma maneira rápida e fácil de desenhar imagens 2D no UE4.

### 6.1. Criando sprites

Neste passo vamos criar os *sprites* utilizando texturas como base, seguindo os passos:

1. Selecione uma textura para ser apresentada no fundo da cena utilizando o menu de contexto acione `Sprite Actions` > `Create Sprite`;

1. Renomeie para SPR_Factory_Background, por exemplo;

1. [Usando o editor de Sprite](https://docs.unrealengine.com/4.27/en-US/AnimatingObjects/Paper2D/Sprites/Editor/)

1. Toolbar

    - `Add Box/Add Polygon/Add Circle`  - Adiciona um área adicional para colisão ou renderização da geometria;

1. Mode Switching Toolbar

    - `Edit Source Region` - Exibe a textura de origem completa e permite que você defina a área que compõe o sprite individual;

    - `Edit RenderGeom` - Exibe e permite a edição da geometria de renderização do sprite.

    - `Edit Collision` - Exibe e permite a edição das formas de colisão do sprite;

1. Podemos adicionar física nos sprites em `Details` > `Simulate Physisc`;

1. Agora os *Sprites* podem ser adicionados na cena.

### 6.2. Agrupando sprites em Tile Sets

`Tile Sets` e `Tile Maps` no `Paper 2D` fornecem uma maneira rápida e fácil de fazer o layout da estrutura ou "layout geral" de seus níveis 2D. Ao criar e usar um conjunto de blocos (uma coleção de blocos extraídos de uma textura) com um mapa de blocos (uma grade 2D com largura e altura definidas em blocos), você pode selecionar vários blocos para "pintar" no mapa de blocos, que podem ser usado para seu layout de nível. Você também pode pintar ladrilhos (tiles) em várias camadas, cada uma das quais pode especificar qual ladrilho deve aparecer em cada célula do mapa para aquela camada específica.

Com `Tile Sets` podemos criar uma 'Paleta' de *sprites* para ser usadas no `Tile Maps`.

1. [O editor Tile Sets](https://docs.unrealengine.com/4.27/en-US/AnimatingObjects/Paper2D/TileMaps/);

1. Podemos criar acionando o menu `Paper2D` > `Tile Set`;

1. Editando Tile Set:

- `Tile Size`: Tamanho de cada Tile/Área que pode ser usada;

- `Tile Sheet Texture`:  Arquivo Textura;

Para adicionar colisão nos elementos realizamos :

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_paper2d_tileset_colision.webp"
    alt="Figura: Unreal Engine - Animação 2D - colisão de objetos usando Tile Set Collision."
    caption="Colliding Tiles apresenta os tiles que tem colisão e ao no Single Tile Editor é possível alterar a sua forma."
%}

- Selecione a opção `Colliding Tiles` para mostrar os elementos com colisão;

- Adicione as coordenadas de colisão com `Add Box`;

### 6.3. Implementando uma cena utilizando Tile Map

`Tile Map` é um mapa de *sprites* para auxiliar na composição da cena.

1. Selecione um `Tile Set` para ser usado como paleta;

1. Para melhor controle dos elementos adicione 3 camadas na seguinte ordem:

    - Foreground - Camada para os elementos que devem ficar na frente do personagem;

    - Default - Camada para os elementos na mesma linha do personagem;c

    - Background - Camada para os elementos que ficam atrás do personagem;

1. `Projection Mode` - Orthogonal;

1. `Separation Per Layer` - Adicione um valor em pixel para separar cada camada;

### 6.4. Criando sequencias de animação utilizando Flipbooks

No **Unreal Engine 4**, os `Flipbooks` consistem em uma série de quadros-chave, cada um dos quais contém um Sprite a ser exibido e uma duração (em quadros) para exibi-lo. Uma opção de quadros por segundo determina a rapidez com que os quadros serão exibidos, indicando quantas "batidas" de animação ocorrerão em um segundo e os próprios quadros-chave podem ser editados no painel Detalhes ou usando uma linha do tempo que pode ser encontrada na parte inferior do Flipbook Editor.

Para implementar uma animação de corrida:

1. Utilizando o `Content Browser` selecione todos os *sprites* que simulam o movimento de corrida;

2. Com o botão direito do mouse escolha a opção `Create Flipbook`;

3. Exclua ou movimente os elementos para melhorar a animação;

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_paper2d_flipbook.webp"
    alt="Figura: Unreal Engine - Animação 2d com animação de corrida usando Flipbook Animation Run."
    caption="Sequencia de sprites."
%}

## 7. Adicionando e configurando o personagem do tipo PaperCharacter

***

Neste passo vamos adicionar um personagem do tipo `Paper Character` para ser o player principal do projeto.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_paper_character.webp"
    alt="Figura: Unreal Engine - Animação 2d - Personagem da Blueprint class PaperCharacter para 2D."
    caption="Selecionando a classe PaperCharacter."
%}

Os componentes e parâmetros são diferentes aos do `Character` com malhas/*Mesh* então vamos adicionar e configurar os seguintes componentes:

1. `Sprite`.

    - `Source Flipbook`: FB_Animacao_idle criado anteriormente.

1. `Camera`;

    - `Projection mode` - Orthographic;

    - `Ortho Width` - 1024;

1. `SpringArm`;

    - `Do Collision Set` - False;

    - `Rotation` - Z= (-90);  

    - `Target Arm Length` - 1000;

    - `Inherit Yaw` - False (**Importante para a movimentação em Z (Yaw)**).

1. `Capsule` - Temos que ajustar o tamanho da capsula para a largura e altura do *sprite*.

    - `Capsule Half Height`;

    - `Capsule Radius`;

1. `Character Movement`.

    - `Use Flat Base for floor Checks` - true;

    - `Gravity Scale` - 2;  

    - `Jump Z Velocity` - 1000;

    - `Constraint to Plane`- true;

    - `Plane Constraint Normal` - Y=(-1);

### 7.1. Implementando a lógica de animação do personagem do tipo PaperCharacter

Neste passo vamos implementar a animação do personagem e definir um objeto de controle de estados de animação utilizando uma variável `Enumeration`.

Vamos criar uma variável `Enumeration` para controlar o estado da animação:

{% include imagelocal html
    src="unreal/animacao/unreal_engine_paper2d_enum_state.webp"
    alt="Figura: Enumeration EStateCharacter."
    caption="Implementando um Enumeration para os estados do personagem."
%}

- Idle;

- Running;

- Jumping.

No personagem definimos as seguintes variáveis:

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_paper2d_character_variables.webp"
    alt="Figura: Unreal Engine - Animação 2D - Character Varáveis."
    caption="Lista de variáveis."
%}

- Moving `Boolean` - Para identificar quando o personagem se movimenta;

- Falling `Boolean` - Para identificar quando o personagem esta caindo;

- IdleFlipbook `Paper Flipbook` - Com o valor do Flipbook definido para Idle;

- RunFlipbook `Paper Flipbook` - Flipbook Run;  

- JumpFlipbook `Paper Flipbook` - Flipbook Jump.  

Vamos utilizar o evento `MoveRight` para adicionar movimento travando a coordenada X em 1;

{% include imagebase.html
    src="unreal/animacao/unreal_engine_paper2d_movement.webp"
    alt="Figura: Unreal Engine - Animação 2D - lógica Blueprint do movimento do personagem - Movement MoveRight."
    caption="Figura: Unreal Engine - Animação 2D - lógica Blueprint do movimento do personagem - Movement MoveRight."
%}

A seguir implementamos um novo evento `UpdateAnimation` para inicializar variáveis, chamar uma função `Animation State Machine` que iremos implementar;

{% include imagebase.html
    src="unreal/animacao/unreal_engine_paper2d_event_movement.webp"
    alt="Figura: Unreal Engine - Animação 2D - Evento de atualização do movimento - Event UpdateAnimation."
    caption="Figura: Unreal Engine - Animação 2D - Evento de atualização do movimento - Event UpdateAnimation."
%}

Abaixo a lógica da função `Animation State Machine`;

{% include imagebase.html
    src="unreal/animacao/unreal_engine_paper2d_function_state_machine.webp"
    alt="Figura: Unreal Engine - Animação 2D, lógica Blueprint dos estados do personagem - Function State Machine."
    caption="Figura: Unreal Engine - Animação 2D, lógica Blueprint dos estados do personagem - Function State Machine."
%}

### 7.2. Implementando o canhão

Neste passo vamos implementar um canhão que localiza e atira no player.

Para implementar as balas do canhão vamos criar um objeto **BP_FireBullet** do tipo `Actor` com as seguintes propriedades e componentes;

- `PaperSprite` - Adicione um *Sprite*;

- `Simulate Physisc` - Temos que habilitar a física do objeto;

Implementamos  **BP_Cannon** do tipo `Actor`;

- `PaperSprite`;

- `Sphere Collision` - Ajuste a colisão para servir como área de detecção do player;

- `PointBullet` - Tipo  `Scene` para ser utilizada como ponto inicial das balas;

Inicializamos as variáveis;

{% include imagebase.html
    src="unreal/animacao/unreal_engine_paper2d_cannon_begin_init.webp"
    alt="Figura: Unreal Engine - Animação 2D - BeginPlay inicializando variáveis."
    caption="Figura: Unreal Engine - Animação 2D - BeginPlay inicializando variáveis."
%}

Implementamos as lógica para localizar o personagem e movimentar o canhão na direção do player;

{% include imagebase.html
    src="unreal/animacao/unreal_engine_paper2d_cannon_find_look.webp"
    alt="Figura: Unreal Engine - Animação 2D - função para apontar o canhão no personagem - Function Find Look."
    caption="Figura: Unreal Engine - Animação 2D - função para apontar o canhão no personagem - Function Find Look."
%}

Implementação da lógica para disparar as balas `PB_FireBullet`;

{% include imagebase.html
    src="unreal/animacao/unreal_engine_paper2d_cannon_fire_bullet.webp"
    alt="Figura: Unreal Engine - Animação 2D- Lógica Blueprint para disparar o canhão - Function Impulse para disparar as balas."
    caption="Figura: Unreal Engine - Animação 2D- Lógica Blueprint para disparar o canhão - Function Impulse para disparar as balas."
%}

Quanto o player colide com a área de detecção do canhão as variáveis **Look** e **Fire** são atualizadas para `True`, informando que o player foi detectado e o canhão pode disparar. Devemos adicionar uma `tag` no player para facilitar o seu reconhecimento;

{% include imagebase.html
    src="unreal/animacao/unreal_engine_paper2d_cannon_player_in.webp"
    alt="Figura: Unreal Engine - Animação 2D - Lógica Blueprint detectar o personagem - BeginOverLap e Player."
    caption="Figura: Unreal Engine - Animação 2D - Lógica Blueprint detectar o personagem - BeginOverLap e Player."
%}

O player sai da área de detecção as variáveis de controle são atualizadas para `false`;

{% include imagebase.html
    src="unreal/animacao/unreal_engine_paper2d_cannon_player_out.webp"
    alt="Figura: Unreal Engine - Animação 2D - Lógica Bluerint para interromper o ataque e a visualização - EndOverLap e Player."
    caption="Figura: Unreal Engine - Animação 2D - Lógica Bluerint para interromper o ataque e a visualização - EndOverLap e Player."
%}
