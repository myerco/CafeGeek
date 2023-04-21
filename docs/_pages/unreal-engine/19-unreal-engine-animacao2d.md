---
title: Trabalhando com Animação 2D
excerpt: Em este capitulo iremos implementar animações em duas dimensões utilizando o Plugin Paper2D no Unreal Engine.
permalink: /pages/unreal-engine/animacao-2d
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true 
categories:
  - Unreal Engine
tags:
  - Animação 
  - Animação 2D
---

## 1. O que é Animação 2D?

Animação em duas dimensões é uma técnica que utiliza sequenciamento de imagens estáticas.

{% include image.html
    src="https://maestrofilmes.com.br/wp-content/uploads/2019/10/alfabeta_maio_texto1-1080x614-1024x582.png"
    alt="Figura: Animação 2D: de um simples desenho à solução para uma empresa"
    caption="O vídeo em animação nada mais é que a passagem rápida de objetos ou imagens que, posicionados, dão a ilusão do movimento. A animação é uma Ilusão de ótica, ou seja, ela mostra movimento com imagens que, na verdade, são estáticas"
    ref="https://maestrofilmes.com.br/animacao-2d/"
%}

## 2. Como o Unreal Engine trabalha com animação 2D?

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-project.webp"
    alt="Figura: Editor 2D"
    caption="Viewport com visualização Right ou Left, para apresentar objetos planos na cena "
%}

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
    src="unreal/animacao/unreal-engine-paper2d-plugin.webp"
    alt="Figura: Unreal Engine - Animação 2d - habilitando o Plugin Paper2D (Enabled)."
    caption="Após habilitar o plugin é necessário reiniciar o Unreal Engine."
%}

**Nota:** Utilize a estrutura de pastas definidas em [Organizando as Pastas](https://cafegeek.eti.br/pages/unreal-engine/instalacao-configuracao#6-organizando-as-pastas).
{: .notice--warning}

## 4. Preparando o ViewPort

Podemos organizar os elementos que são apresentados na cena predefinindo coordenadas no eixo Y, utilizando o menu `Edit` > `Project Settings` navegue até `2D` para adicionar camadas/*Layers* e coordenadas de profundidade ao `ViewPort`.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-project-settings.webp"
    alt="Figura: Unreal Engine - Animação 2D - Project Settings 2D."
    caption="Adicionando Snap Layers do exemplo acima podemos criar 3 camadas em profundidades diferentes."
%}

`Foreground` - Camada para os *sprites* que devem ficar na frente da cena, `Depth` = 100;

`Default` - Camada para os *sprites* que devem estão alinhados com o personagem, `Depth` = 0;

`Background` - Camada para os *sprites* que devem ficar atrás da cena, `Depth` = -500;

Após a configuração no `ViewPort` devem aparecer as opções para organizar os objetos em camadas na cena.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-viewport.webp"
    alt="Figura: ViewPort Snap."
    caption="As layers criadas anteriormente devem aparecer na barra de ações."
%}

Os objetos adicionados na cena devem ficar no *snap* selecionado obedecendo a localização Y predefinida, esse processo é similar ao trabalho de desenho por camadas.

Para movimentar objetos entre os *snaps* selecione o objeto e pressione :

**CTRL + PAGE DOWN** para posicionar o objeto na camada anterior;

**CTRL + PAGE UP** para posicionar o objeto na camada posterior;

Para melhorar a visualização do cenário podemos configurar a visualização do `ViewPort` para **Right** a fim de controlar somente os eixos Z e X.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-viewport-xy.webp"
    alt="Figura: ViewPort Rigth Z,X."
    caption="Visualização Right no ViewPort."
%}

## 5. Preparando as texturas

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-details-texture-2d.webp"
    alt="Figura: Preparando a textura - Details Texture parameters 2D."
    caption="A fim de otimizar a renderização das texturas aplicamos os seguintes parâmetros para cada objeto."
%}

`Compression Settings`: UseInterface2D (RGBA);

`Mip Gen Settings`: NoMipMaps

**Informação:** A geração do Mip-map ocorre durante a importação da Textura e cria uma cadeia de Mip-map para a Textura. A cadeia mip-map consiste em vários níveis da imagem de amostra, cada um com metade da resolução do nível anterior. Esses dados permitem que a placa gráfica renderize mais rápido ao usar os mips inferiores (menos largura de banda da memória) e também reduz o aliasing da textura (cintilante) que se torna visível ao ter textura detalhada em certas distâncias.
{: .notice--info}

Podemos aplicar automaticamente para uma ou várias texturas selecionadas usamos o menu de contexto selecionando o arquivo e depois `Sprite Actions` > `Apply Paper2D Texture Settings`.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-apply-texture-settings.webp"
    alt="Figura: Unreal Engine - Animação 2D - Apply Papper2D Texture Settings."
    caption="Aplicamos a configuração em vários arquivos."
%}

## 6. Preparando os Sprites do projeto

Um Sprite em papel 2D é uma malha plana com mapeamento de textura e material associado que pode ser renderizado no mundo, criado inteiramente no Unreal Engine 4 (UE4). Em termos mais simples, é uma maneira rápida e fácil de desenhar imagens 2D no UE4.

### 6.1. Criando sprites

Neste passo vamos criar os *sprites* utilizando texturas como base, seguindo os passos:

1. Selecione uma textura para ser apresentada no fundo da cena utilizando o menu de contexto acione `Sprite Actions` > `Create Sprite`;

1. Renomeie para SPR_Factory_Background, por exemplo;

### 6.2. Editor de Sprites

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-sprite-editor.webp"
    alt="Figura: Editor de Sprite."
    caption="Para editar várias parâmetros dos objetos utilizamos o editor de sprites."
    ref="https://docs.unrealengine.com/4.27/en-US/AnimatingObjects/Paper2D/Sprites/Editor/"
%}

**1.** Toolbar

- `Add Box/Add Polygon/Add Circle`  - Adiciona um área adicional para colisão ou renderização da geometria;

**2.** Mode Switching Toolbar

- `Edit Source Region` - Exibe a textura de origem completa e permite que você defina a área que compõe o sprite individual;

- `Edit RenderGeom` - Exibe e permite a edição da geometria de renderização do sprite.

- `Edit Collision` - Exibe e permite a edição das formas de colisão do sprite;

**3.** Detalhes

- `Sprite Collision Domain` - Parâmetro para aplicar física na colisão.

  - `Use 3D Physics` - A geometria de colisão será gerada para uso com o PhysX. A geometria de colisão 2D definida no sprite será extrudada usando as unidades de Espessura de Colisão no fundo do eixo perpendicular para criar a geometria de colisão 3D;
  
- `Collision Geometry Type` - Parâmetro para deformar a caixa de colisão automaticamente.

  - `Tight Bounding Box`  - Colisão delimitada;

  - `Shrink Wwrapped` - Colisão calculada;

## 7. Agrupando sprites em Tile Sets

`Tile Sets` e `Tile Maps` no `Paper 2D` fornecem uma maneira rápida e fácil de fazer o layout da estrutura ou "layout geral" de seus níveis 2D. Ao criar e usar um conjunto de blocos (uma coleção de blocos extraídos de uma textura) com um mapa de blocos (uma grade 2D com largura e altura definidas em blocos), você pode selecionar vários blocos para "pintar" no mapa de blocos, que podem ser usado para seu layout de nível. Você também pode pintar ladrilhos (tiles) em várias camadas, cada uma das quais pode especificar qual ladrilho deve aparecer em cada célula do mapa para aquela camada específica.

Com `Tile Sets` podemos criar uma 'Paleta' de *sprites* para ser usadas no `Tile Maps`.

1. [O editor Tile Sets](https://docs.unrealengine.com/4.27/en-US/AnimatingObjects/Paper2D/TileMaps/);

1. Podemos criar acionando o menu `Paper2D` > `Tile Set`;

1. Editando Tile Set:

- `Tile Size`: Tamanho de cada Tile/Área que pode ser usada;

- `Tile Sheet Texture`:  Arquivo Textura;

Para adicionar colisão nos elementos realizamos :

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-tileset-colision.webp"
    alt="Figura: Unreal Engine - Animação 2D - colisão de objetos usando Tile Set Collision."
    caption="Colliding Tiles apresenta os tiles que tem colisão e ao no Single Tile Editor é possível alterar a sua forma."
%}

- Selecione a opção `Colliding Tiles` para mostrar os elementos com colisão;

- `Add Box` permite adicionar e manipular uma caixa de colisão;

- `Add Polygon` permite adicionar polígono inserindo as coordenadas da colisão;

- `Add Circle` - Adiciona um círculo de colisão;

## 8. Implementando uma cena utilizando Tile Map

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-tilemap.webp"
    alt="Figura: Tile Map."
    caption="É um mapa de sprites para auxiliar na composição da cena."
%}

Selecione um `Tile Set` para ser usado como paleta, selecionando o arquivo no `Content Browser` e logo em seguida o menu de contexto `Create Tile Map`;

Para melhor controle no desenho dos elementos adicione 3 camadas na seguinte ordem:

**Foreground** - Camada para os elementos que devem ficar na frente do personagem;

**Default** - Camada para os elementos na mesma linha do personagem;c

**Background** - Camada para os elementos que ficam atrás do personagem;

Configure os parâmetros:

`Projection Mode` - Orthogonal;

`Separation Per Layer` - Permite adicionar um valor em pixel para separar cada camada na ViewPort;

`Collision Thickness` - Usado para aumentar ou diminuir a largura de colisão quando usado colisão 3D.

## 9. Criando sequencias de animação utilizando Flipbooks

No **Unreal Engine 4**, os `Flipbooks` consistem em uma série de quadros-chave, cada um dos quais contém um Sprite a ser exibido e uma duração (em quadros) para exibi-lo. Uma opção de quadros por segundo determina a rapidez com que os quadros serão exibidos, indicando quantas "batidas" de animação ocorrerão em um segundo e os próprios quadros-chave podem ser editados no painel Detalhes ou usando uma linha do tempo que pode ser encontrada na parte inferior do Flipbook Editor.

### 9.1. Extraindo as animações de arquivo

{% include imagelocal.html
    src="unreal/animacao/samurai-run.wepb"
    alt="Figura: Arquivo Samurai."
    caption="Para exemplificar vamos utilizar o arquivo acima com um sequência de poses de um personagem."
    ref="https://craftpix.net/freebies/free-samurai-pixel-art-sprite-sheets/"
%}

Extrai o arquivo em qualquer pasta e copie o conteúdo para a dentro do projeto na pasta `Characters\Samurai\Textures`;

Utilizando o `Content Browser` selecione o arquivo `run.png` e acionando o menu de contexto selecione `Sprite Actions` > `Extract Sprites`;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-extract-sprites.webp"
    alt="Figura: Extract Sprites."
    caption="Utilize a opção Sprite Extract Mode Auto para que o programa selecione automaticamente as imagens que correspondem a uma pose do personagem e clique em Extract para completar a operação."
%}

Copie os arquivos extraídos para a pasta `Characters\Samurai\Sprites`;

### 9.2. Animação de corrida usando os sprites extraídos do arquivo

Utilizando o `Content Browser` selecione todos os *sprites* que simulam o movimento de corrida.

Com o botão direito do mouse escolha a opção `Create Flipbook`.

Exclua ou movimente os elementos para melhorar a animação.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-flipbook.webp"
    alt="Figura: Animação de corrida usando Flipbook Animation Run."
    caption="Sequencia de sprites."
%}

Salve o arquivo com o nome PFB_Run na pasta `Characters\Samurai\Logic` e repita a ação para as diversas poses que o personagem deve apresentar, como por exemplo PFB_Idle, PFB_Attack e outros.

## 10. Adicionando e configurando o personagem do tipo PaperCharacter

Neste passo vamos adicionar um personagem do tipo `Paper Character` que deve ser a base (pai) de outros personagens, por conseguinte a classe deve ser salva na pasta `Core\Characters` com o nome BP_CharacterBase.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper-character.webp"
    alt="Figura: Classe PaperCharacter."
    caption="Esta classe apresenta componentes e específicos para a movimentação e animação do personagem."
%}

### 10.1. Ajustando os componentes

Os componentes e parâmetros são diferentes então vamos adicionar e configurar os seguintes componentes para exemplificar:

`Sprite`

- `Source Flipbook`: PFB_idle criado anteriormente.

`Camera`

- `Projection mode` = Orthographic;

- `Ortho Width` = 1024;

`SpringArm`;

- `Do Collision Set` = False;

- `Rotation` (Z) = (-90);  

- `Target Arm Length` = 150;

- `Inherit Yaw` = False (**Importante para a movimentação em Z (Yaw)**).

`Capsule`

Temos que ajustar o tamanho da capsula para a largura e altura do *sprite*.

- `Capsule Half Height` = Ajuste ao personagem;

- `Capsule Radius` = Ajuste ao personagem;

`Character Movement`

- `Use Flat Base for floor Checks` = true;

- `Gravity Scale` = 2;  

- `Jump Z Velocity` = 1000;

- `Constraint to Plane` = true;

- `Plane Constraint Normal` (Y) =(-1);

### 10.2. Variáveis do personagem

Para definir as características ou propriedades do personagem vamos criar variáveis com os seguintes valores separados por categoria:

`Category` - Character

- fHealth (Float) = 100;

- cColor (Color);

- tImage (Texture 2D);

- sSound (Sound Cue);

### 10.3. Implementando a lógica de animação do personagem do tipo PaperCharacter

Neste passo vamos implementar a animação do personagem e definir um objeto de controle de estados de animação utilizando uma variável `Enumeration`.

Vamos criar uma variável `Enumeration` para controlar o estado da animação:

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-enum-state.webp"
    alt="Figura: Enumeration EStateCharacter."
    caption="A variável deve armazenar os estados ou poses do personagem."
%}

- Idle;

- Running;

- Jumping.

No personagem definimos as seguintes variáveis:

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-character-variables.webp"
    alt="Figura: Character Varáveis."
    caption="Lista de variáveis."
%}

Moving `Boolean` - Para identificar quando o personagem se movimenta;

Falling `Boolean` - Para identificar quando o personagem esta caindo;

IdleFlipbook `Paper Flipbook` - Com o valor do Flipbook definido para Idle;

RunFlipbook `Paper Flipbook` - Flipbook Run;  

JumpFlipbook `Paper Flipbook` - Flipbook Jump.  

Vamos utilizar o evento `MoveRight` para adicionar movimento travando a coordenada X em 1;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-movement.webp"
    alt="Figura: Movement MoveRight."
    caption="Lógica Blueprint do movimento do personagem."
%}

A seguir implementamos um novo evento `UpdateAnimation` para inicializar variáveis, chamar uma função `Animation State Machine` que iremos implementar;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-event-movement.webp"
    alt="Figura: Event UpdateAnimation."
    caption="Evento de atualização do movimento."
%}

Abaixo a lógica da função `Animation State Machine`;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-function-state-machine.webp"
    alt="Figura: Function State Machine."
    caption="Lógica Blueprint dos estados do personagem."
%}

### 10.4. Implementando o canhão

Neste passo vamos implementar um canhão que localiza e atira no player.

Para implementar as balas do canhão vamos criar um objeto **BP_FireBullet** do tipo `Actor` com as seguintes propriedades e componentes;

`PaperSprite` - Adicione um *Sprite*;

`Simulate Physisc` - Temos que habilitar a física do objeto;

Implementamos  **BP_Cannon** do tipo `Actor`;

`PaperSprite`;

`Sphere Collision` - Ajuste a colisão para servir como área de detecção do player;

`PointBullet` - Tipo  `Scene` para ser utilizada como ponto inicial das balas;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-cannon-begin-init.webp"
    alt="Figura: BeginPlay inicializando variáveis."
    caption="Inicializamos as variáveis."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-cannon-find-look.webp"
    alt="Figura: Function Find Look."
    caption="Implementamos as lógica para localizar o personagem e movimentar o canhão na direção do player."
%}

Implementação da lógica para disparar as balas `PB_FireBullet`;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-cannon-fire-bullet.webp"
    alt="Figura: Function Impulse para disparar as balas."
    caption="Lógica Blueprint para disparar o canhão."
%}

Quanto o player colide com a área de detecção do canhão as variáveis **Look** e **Fire** são atualizadas para `True`, informando que o player foi detectado e o canhão pode disparar. Devemos adicionar uma `tag` no player para facilitar o seu reconhecimento;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-cannon-player-in.webp"
    alt="Figura: BeginOverLap e Player."
    caption="Lógica Blueprint detectar o personagem."
%}

O player sai da área de detecção as variáveis de controle são atualizadas para `false`;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-paper2d-cannon-player-out.webp"
    alt="Figura: EndOverLap e Player."
    caption="Lógica Blueprint para interromper o ataque e a visualização."
%}
