---
title: Animação - 2d
description: Animação 2D.
tags: [Unreal Engine, Animação 2D,Paper 2D]
layout: page
---

## Índice

## Animação 2D

## Paper 2D
Paper 2D in Unreal Engine 4 (UE4) é um sistema baseado em sprite para a criação de jogos híbridos 2D e 2D / 3D inteiramente dentro do editor. No núcleo do Paper 2D estão os Sprites (que são uma malha plana com textura mapeada e um material associado). Você pode editar Sprites dentro do UE4 com o Sprite Editor e criar animações baseadas em sprites com Flipbooks (que animam uma série de Sprites sequencialmente usando quadros-chave e especificando uma duração em quadros para exibi-los).

## Sprites
Um Sprite em papel 2D é uma malha plana com mapeamento de textura e material associado que pode ser renderizado no mundo, criado inteiramente no Unreal Engine 4 (UE4). Em termos mais simples, é uma maneira rápida e fácil de desenhar imagens 2D no UE4.

## Tiles Set
Os conjuntos de blocos e os mapas de blocos no Paper 2D fornecem uma maneira rápida e fácil de fazer o layout da estrutura ou "layout geral" de seus níveis 2D. Ao criar e usar um conjunto de blocos (uma coleção de blocos retirados de uma textura) com um mapa de blocos (uma grade 2D com largura e altura definidas em blocos), você pode selecionar vários blocos para "pintar" no mapa de blocos, que podem ser usado para seu layout de nível. Você também pode pintar ladrilhos em várias camadas, cada uma das quais pode especificar qual ladrilho deve aparecer em cada célula do mapa para aquela camada específica.

## Tiles Maps

## Flipbooks

## Preparando o ViewPort
Podemos organizar os elementos que são apresentados na cena predefinindo coordenadas no eixo Y.

1. No menu `Edit` > `Project Settings` navegue até `2D`.
  ![Figura: Project Settings 2D](imagens/animacao/unreal_engine_paper2d_project_settings.jpg)

    *Figura: Project Settings 2D*

2. Após a configuração no ViewPort deve aparecer as opções para organizar os objetos na cena.
![Figura: ViewPort Snap](imagens/animacao/unreal_engine_paper2d_viewport.jpg)

    *Figura: ViewPort Snap*

3. Os objetos adicionados na cena devem ficar no *snap* selecionado obedecendo a localização Y predefinida, esse processo é similar ao trabalho de desenho por camadas.

4. Para movimentar objetos entre os *snaps* seleciona o objeto e pressione :
  - CTRL + DOWN para posicionar o objeto na camada anterior;
  - CTRL + UP para posicionar o objeto na camada posterior;

5. Para trabalhar com o cenário temos que configurar a visualização do ViewPort para **Right** para que possamos controlar somente os eixos Z e X.

  ![Figura: ViewPort Rigth Z,X](imagens/animacao/unreal_engine_paper2d_viewport_xx.jpg)

    *Figura: ViewPort Rigth Z,X*


## Preparando as texturas

A fim de otimizar a renderização das texturas aplicamos os seguintes parâmetros para cada objeto:

1. Parâmetros da textura.

  ![Figura: Details Texture parameteres 2D](imagens/animacao/unreal_engine_paper2d_details_texture_2d.jpg)

    *Figura: Figura: Details Texture parameteres 2D*

    - Compression Settings: UseInterface2D (RGBA) ;
    - Mip Gen Settings: NoMipMaps

  >A geração do Mip-map ocorre durante a importação da Textura e cria uma cadeia de Mip-map para a Textura. A cadeia mip-map consiste em vários níveis da imagem de amostra, cada um com metade da resolução do nível anterior. Esses dados permitem que a placa gráfica renderize mais rápido ao usar os mips inferiores (menos largura de banda da memória) e também reduz o aliasing da textura (cintilante) que se torna visível ao ter textura detalhada em certas distâncias.

2. Podemos aplicar automáticamente para um ou várias texturas selecionadas usando o menu de contexto `Sprite Actions` > `Apply Paper2D Texture Settings`.

  ![Figura: Apply Papper2D Texture Settings](imagens/animacao/unreal_engine_paper2d_apply_texture_settings.jpg)

    *Figura: Apply Papper2D Texture Settings*


## Preparando os sprites
1. Selecione uma textura para ser apresentada no fundo da cena utilizando o menu de contexto acione `Sprite Actions` > `Create Sprite`;
2. Renomeie para SPR_Factory_Background
3. [Editor de Sprite](https://docs.unrealengine.com/4.27/en-US/AnimatingObjects/Paper2D/Sprites/Editor/)
4. Toolbar
  - Add Box/Add Polygon/Add Circle  - Adiciona um área adicional para colisão ou renderização geometria;
5.  Mode Switching Toolbar
  - Edit Source Region - Exibe a textura de origem completa e permite que você defina a área que compõe o sprite individual;
  - Edit Collision - Exibe e permite a edição das formas de colisão do sprite;
  - Edit RenderGeom - Exibe e permite a edição da geometria de renderização do sprite.
6. Podemos adicionar física nos sprites em `Details` > `Simulate Physisc`;
7. Sprites podem ser adicionados na cena.

## Tile Sets
`Tile Sets` e `Tile Maps` no Paper 2D fornecem uma maneira rápida e fácil de fazer o layout da estrutura ou "layout geral" de seus níveis 2D. Ao criar e usar um conjunto de blocos (uma coleção de blocos extraídos de uma textura) com um mapa de blocos (uma grade 2D com largura e altura definidas em blocos), você pode selecionar vários blocos para "pintar" no mapa de blocos, que podem ser usado para seu layout de nível. Você também pode pintar ladrilhos (tiles) em várias camadas, cada uma das quais pode especificar qual ladrilho deve aparecer em cada célula do mapa para aquela camada específica.

Com `Tile Sets` podemos criar uma 'Paleta' de sprites para ser usadas pintadas no `Tile Maps`.

1. [O editor Tile Sets](https://docs.unrealengine.com/4.27/en-US/AnimatingObjects/Paper2D/TileMaps/);
2. Podemos criar acionando o menu `Paper2D` > `Tile Set`;
3. Editando Tile Set:
- `Tile Size`: Tamanho de cada Tile/Área que pode ser usada;
- `Tile Sheet Texture`:  Textura;

## Tile Map




## Referências

- [O que é animação 2D e o que a difere dos outros tipos de animações?](https://blog.saga.art.br/animacao-2d/)
- [Getting Started with Paper 2D | Community Led Training | Unreal Engine Livestream](https://www.youtube.com/watch?v=Tf9Qd4isHTM)
- [Introduction to Paper2D | v4.4 | Unreal Engine](https://www.youtube.com/playlist?list=PLZlv_N0_O1gauJh60307mE_67jqK42twB)
- [Paper 2D](https://docs.unrealengine.com/4.26/en-US/AnimatingObjects/Paper2D/)
- [Texture Properties](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Textures/Properties/)
- [Paper 2D Tile Sets / Tile Maps](https://docs.unrealengine.com/4.27/en-US/AnimatingObjects/Paper2D/TileMaps/)
