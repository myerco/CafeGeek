---
title: Modelagem usando Autodesk Maya
description: Modelagem com Autodesk Maya
keywords: [Autodesk Maya, modelagem 3d]
tags: [Autodesk Maya, modelagem 3d]
layout: page
---

O objetivo deste curso é apresentar e construir elementos na ferramenta de modelagem artística 3D Autodesk Maya. O curso está associado a construção **Estética** do jogo pois nele definimos elementos como sensação, desafio, descoberta e passatempo.

**Habilidades que serão aprendidas.**

- Interface e estrutura de menus;
- Configuração de ambiente de trabalho e projeto;
- Movimentação, dimensionamento e Rotacionamento de objetos;
- Extrudar, inserir e deformar elementos;
- Mapeamento UV;
- Iluminação de cenas;
- Animação de elementos;
- Construção de objetos com NURBS;

| M         |  D          | A         |
|:-         |:-           |:-         |
| Mecânicas | Dinâmicas   | **Estéticas** |


***

<a name="indice"></a>
**[CAPÍTULO  1 - Modelagem 3D](#1 "CAPÍTULO  I - Modelagem 3D")**

&nbsp;&nbsp;[1.1 O que é Modelagem de objetos 3D?](#1.1)

&nbsp;&nbsp;[1.2 Tipos de modelagem 3D](#1.2)

&nbsp;&nbsp;[1.3 Processo de construção de cenas 3D](#1.3)

&nbsp;&nbsp;[1.4 Softwares para modelagem tridimensional](#1.4)

***

**[CAPÍTULO  2 - Modelos poligonais com Autodesk Maya](#2)**

&nbsp;&nbsp;[2.1 Interface básico](#2.1)

&nbsp;&nbsp;[2.2 Configurando a Interface](#2.2)

&nbsp;&nbsp;[2.3 Configurando projetos](#2.3)

&nbsp;&nbsp;[2.4 Comandos de navegação](#2.4)

&nbsp;&nbsp;[2.5 Configuração de ViewPort](#2.5)

&nbsp;&nbsp;[2.6 Seleção de objetos](#2.6)

&nbsp;&nbsp;[2.7 Pivot](#2.7)

&nbsp;&nbsp;[2.8 Extrude](#2.8)

&nbsp;&nbsp;[2.9 Bevel](#2.9)

&nbsp;&nbsp;[2.10 Removendo edges](#2.10)

&nbsp;&nbsp;[2.11 Multicut](#2.11)

&nbsp;&nbsp;[2.12 Merge de vértices](#2.12)

***

**[CAPÍTULO  3 - Organizando objetos](#3)**

&nbsp;&nbsp;[3.1 Organizando em camadas](#3.1)

&nbsp;&nbsp;[3.2 Grupos](#3.1)

&nbsp;&nbsp;[3.3 Combine e Separate](#3.3)

&nbsp;&nbsp;[3.4 Duplicando](#3.4)

&nbsp;&nbsp;[3.5 Booleans](#3.5)

***

**[CAPÍTULO  4 - Modelos de curvas com Autodesk Maya](#4)**

&nbsp;&nbsp;[4.1 Modelagem NURBS](#3.1)

***

**[CAPÍTULO  5 - Materiais e mapeamento UV](#5)**

&nbsp;&nbsp;[5.1 Materiais](#5.1)

&nbsp;&nbsp;[5.2 Tipos de Materiais (Maya)](#5.2)

&nbsp;&nbsp;[5.3 Mapeamento UV](#5.3)

***

**[CAPÍTULO  6 - Iluminação e Renderização](#6)**

***

**[CAPÍTULO  7 - Animando cenas no Autodesk Maya](#7)**

***

[Atividades e Referências](autodesk_maya_atividades_referencias.html)

***

<a name="1"></a>
## CAPÍTULO  1 - Modelagem 3D

<a name="1.1"></a>
## 1.1 O que é Modelagem de objetos 3D?
Podemos entender a Modelagem 3D como a criação de objetos sólidos através da representação matemática de uma superfície ou de um objeto volumétrico, vivo ou inanimado. É a criação do modelo de um objeto tridimensional através de um software de processamento 3D.

![Cabeça low poly de um modelo 3D (fonte: TurboSquid)](https://ecdd.infnet.edu.br/wp-content/uploads/sites/7/2021/04/modelo-3d-lowpoly-1024x576.jpg "Figura: Cabeça low poly de um modelo 3D (fonte: TurboSquid).")   

> Figura: Cabeça low poly de um modelo 3D (fonte: TurboSquid).

Podemos aplicar em várias áreas como por exemplo:

- Design, Engenharia e Produção de Produtos;

- Arquitetura e Engenharia Civil, Elétrica, Mecânica;

- Cinema e Jogos;

- Ilustrações.

<a name="1.2"></a>
## 1.2 Tipos de modelagem 3D

- **Hard Surface** - (superfícies duras), são quaisquer objetos feitos ou construídos pelo homem. Exemplos de *hard surface* podem ser estruturas arquitetônicas, veículos, robôs, entre outros;

- **Organic** - (Orgânicos) são modelos, obviamente, orgânicos, ou seja, que existem na natureza. Isso inclui humanos, animais, árvores, pedras, terrenos, etc;

- **Render** - Fase para gerar a Iluminação e renderizar toda a cena.

<a name="1.3"></a>
## 1.3 Processo de construção de cenas 3D

**Conceito** - *Concept art* ou arte conceitual;

![Figura: Arte conceitual (Artstation)](https://cdnb.artstation.com/p/media_assets/images/images/000/649/263/large/sketch_viking_house.jpg?1600679970 "Figura: Arte conceitual (Artstation)")

> Figura: Arte conceitual (Artstation)

**Modelagem** - Construção de modelos tridimensionais;

![Figura: Modelo tridimensional Blue Wooden house - https://blenderartists](https://blenderartists.org/uploads/default/original/4X/f/d/0/fd0375c46a3df8b8fd489ab6a1d259b28ecb3ec4.jpeg "Figura: Modelo tridimensional Blue Wooden house - https://blenderartists")

> Figura: Modelo tridimensional Blue Wooden house - https://blenderartists.

**Configuração de layout de cena** - Mapeamento, Iluminação e geração de câmeras;

![Figura: Modelo tridimensional com Mapeamento e Iluminação Blue Wooden house - https://blenderartists](https://blenderartists.org/uploads/default/original/4X/5/5/9/559c984fb29dadab1ae2cab740d99e94bd371779.jpeg "Figura: Modelo tridimensional com Mapeamento e Iluminação Blue Wooden house - https://blenderartists")

> Figura: Modelo tridimensional com Mapeamento e Iluminação Blue Wooden house - https://blenderartists.

- **Geração de cenas** - Renderização e animação.

<a name="1.4"></a>
## 1.4 Softwares para modelagem tridimensional
Segue abaixo quatro ferramentas para arte tridimensional e animação 3D. Todas elas tem versões educacionais gratuitas para praticar.

- Substance Painter;

- Autodesk Maya;

- Autodesk Mudbox

- Blender;

<a name="2"></a>
## CAPÍTULO  2 - Começando a trabalhar com Autodesk Maya


<a name="2"></a>
## 2.1 Interface básico

1. [Menus](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-Basics/files/GUID-D90A2BDB-FD05-4528-8A95-C33A02D15129-htm.html)
   - Create - Cria objetos
   - Select - Seleciona objetos;
   - Modify - modifica objetos;
   - Display - apresenta objetos;
   - Windows - Apresenta e configura os Editores;
2. Barra de tarefas
   - Modeling toolKit.

3. Fluxos de trabalho

4. [Tools box](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2018/ENU/Maya-Basics/files/GUID-B345E162-0149-4E09-AC98-48DCFC227F33-htm.html)

5. Layout

6. [Outliner](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-Basics/files/GUID-4B9A9A3A-83C5-445A-95D5-64104BC47406-htm.html)

7. [Workspace](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2019/ENU/Maya-Basics/files/GUID-0384C282-3CA1-4587-9775-F7164D3F6980-htm.html)

   - Modeling - Standard

<a name="2.2"></a>
## 2.2 Configurando a Interface   

1. Para habilitar ou desabilitar a janela inicial de avisos de mudanças de versão.
   - Windows > Settings / Preferences > Preferences > `Show - What´s new`

2. Window > Settings / Preferences > Preferences
   - Interface (Menu Set,Show...)  

<a name="2.3"></a>
## 2.3 Configurando projetos
1. Configurando as pastas do projeto
  - File > Project Window

2. Criando novas cenas
  - File > New Scene

3. Configurando projeto novos importados
  - File > Set Project

<a name="2.4"></a>
## 2.4 Comandos de navegação
1. Alt + RMB - Movimentação de câmera.
1. Alt + LMB - Zoom.
1. Alt + Scroll - Scroll da a câmera.
1. Scroll - Zoom

<a name="2.4"></a>
## 2.5 Configuração de ViewPort
1. Mostrando a quantidade de polígonos e vértices.
   - [Display > Heads Up Display > Poly Count](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2019/ENU/Maya-Modeling/files/GUID-53E46D0C-4B7B-4404-AEB0-3BDD1FF8608A-htm.html).    

2. Visualização
    1. [Shading](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-Basics/files/GUID-C6188583-EA9E-4880-AAE7-8D895FD94DD6-htm.html)

3. Hotbox - pressione a barra de espaço

4. RMB - Menu de contexto

<a name="2.6"></a>
## 2.6 Seleção de objetos
1. Seleciona um objetos.

2. Seleciona elementos do objeto.

3. CTRL + RMB - Adiciona um elemento na Seleção      

4. CTRL + LMB - Remove um elemento da Seleção      

5. CTRL no ícone para entrar nas configurações.

6. Shift + 2 click no elemento ao lado - Seleciona todos os elementos ao redor

<a name="2.7"></a>
## 2.7 Pivot
1. Modify > Center Pivot
Centralizar pivot

2. Movendo Pivot
  Tecla D

3. Snap to points para alinhar o pivot nos elementos.

<a name="2.8"></a>
## 2.8 Extrude

1. Extrude
    - shift + mouse (Move tool Preferences > Smart Duplicate Settings > Shift + drag to..)
    - Ctrl + E
    - Menu > Edit Mesh > Extrude
2. Adicionando edges
    - Menu > Mesh Tools > Insert Edge loop
    - Mesh Tools > Insert Edge loop Settings > Number of edge loops

<a name="2.9"></a>
## 2.9 Bevel

1. Ctrl + B
    - Fraction - espaço entre segmentos
    - Segments - Número de segmentos

<a name="2.10"></a>
## 2.10 Removendo edges
1. Ctrl + Backspace - Remove edges e vértices.


<a name="2.11"></a>
## 2.11 Multicut
Cuidado não podemos ter vértices sem conexão com outros
1. Adicione edges    

<a name="2.12"></a>
## 2.12 Merge de vértices
1. Menu > Edit Mesh  > Merge (Antes Selecione dois vértices)


<a name="3"></a>
## CAPÍTULO  3 - Organizando objetos

<a name="3.1"></a>
## 3.1 Organizando em camadas
1.  Layer
- V - Mostra ou oculta uma camada. Consulte Ocultar camadas de exibição para obter mais informações.
- P - Um "P" na caixa significa que a camada está visível durante a reprodução. Desligue o "P" para ocultar a camada durante a reprodução.
- T - Um “T” significa que os objetos na camada são modelados: eles são exibidos em estrutura de arame e não podem ser selecionados. Um “R” significa que os objetos aos quais a camada está referenciada: eles não podem ser selecionados, mas mantêm o modo de exibição atual. Uma caixa em branco significa que os objetos na camada são normais e podem ser selecionados.

<a name="3.2"></a>
## 3.2 Grupos

1. Hierarquia
  MMB (Botão do meio) arreste os elementos para dentro de outros.
  Selecionando o objeto principal todos os objetos são selecionados.
  As alterações do objeto principal refletem em todos os objetos.

2. Selecione os objetos (ctrl+G)  
  Diferente de Hierarquia é criado um objeto separado para controlar os demais.

<a name="3.3"></a>
## 3.3 Combine e Separate
1. Combine - Selecione os objetos `Mesh` > `Combine`
1. Separate - Selecione o objeto `Mesh` > `Separate` vai ser criado um grupo.

<a name="3.4"></a>
## 3.4 Duplicando
1. Duplicando - Ctrl + D
1. Duplicando aproveitando a transformação  -  shift + D

<a name="3.5"></a>
## 3.5 Booleans

1. `Mesh` > `Booleans`

<a name="4"></a>
## CAPÍTULO 4 - Modelos de curvas com Autodesk Maya

<a name="4.1"></a>
## 4.1 Modelagem NURBS

1. Revolve
  1. Ordem de seleção do objeto altera a forma final;
  1. A curva fica associada ao objeto criado até que o histórico seja removido;
1. Loft
1. Extrude
  1. É possível criar um objeto poligonal na construção usando as configurações
1. Isoparm
  1. É possível separar ou juntar usando `Surface` > `Detach` ou `Attach`
1. Project Curve on Surface
  1. Trim Tool para cortar surface


<a name="5"></a>
## CAPÍTULO 5 - Materiais e mapeamento UV

<a name="5.1"></a>
## 5.1 Materiais
- Render
  - Menu: `Arnold` > `Arnold RenderView`
  - Cameras
  - Iluminação

<a name="5.2"></a>
## 5.2 Tipos de Materiais (Maya)
- Lambert (simples sem reflexo, brilho e transparência)
  - Color: cor do material
  - transparência: Aumenta o alpha
  - Ambiente color: aumenta a tonalidade da cor
  - Incandescência: Adiciona uma luz ao material
  - Bump Mapping: adiciona textura para associar rugosidade ou padrões.
  - Diffuse: Torna mais claro ou escuro a cor
- Blind (Com brilho e reflexo)
  - Specular [Reflexão especular](https://pt.wikipedia.org/wiki/Reflex%C3%A3o_especular)
  - Eccentricty: Aumenta o brilho
  - Specular Roll off: Desfoque aplicado no brilho
  - Specular color : Cor do brilho   
  - Reflectivity: Aumenta a intensidade do reflexo
- [Phong](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Maya/files/GUID-3EDEB1B3-4E48-485A-9714-9998F6E4944D-htm.html) (Parecido com o Blind mas com mais parâmetros)  
  - Specular Shadding
  - Roughness: rugosidade
  - Highlight size: tamanho do desfoque
- Anisotropic
  - Specular Shader
  - Angle: ângulo da luz

<a name="5.3"></a>
## 5.3 Mapeamento UV
- Menu `UV` > `UV Editor`;
- Painéis lado a lado
  - ViewPort `Panels` > `Saved Layouts` > `Persp/UV Editor`
- Menu UV toolKit
  - `Tools` > `Show UV toolKit`;
- UV Shells : Context Menu > UV > select vertex > ctrl > context menu > To UV shells

- Cortando `3D Cut and Sew UV`
  - O corte é realizado por material utilizado;
  - Clicando e arrastrando;
  - Desmarcando CTRL+2x na vértice selecionado;
  - Quando uma área é fechada é criada "UV Shells";
  - Podemos selecionar as UV Shells;
- Costurando  `Cut and Sew`
  - Selecione dois vértices e depois clique em `Sew`;
  - `Sew Tool` - Costura interativa, selecione e arrastre;

- Expandindo/desdobra o Elemento  
  - `UV Toolkit` > `Unfold`;
- Movimentando ou aumentando
  -  `Transform` > `Move`
- Copiando dados de um Shells para outra  
  -  `Transform` > `Texel Density` > `Get` - copia os valores de um elemento selecionado;
  -  `Transform` > `Texel Density` > `Set` - cola os valores para um elemento selecionado;
- Invertendo Shells `Tools`
  - `Flip` > `U` ou `V` - Horizontal ou vertical;
- `Arrange and Layout`
  - `Stack Shells` - Quando a textura aparece em duas faces é recomendado utilizar o recurso para empilhar uma sobre a outra;
  - `Orient Shells` - Separa e orienta as shells;
  - `Layout` - Organiza as Shells lado a lado;  
- `Align and Snap`  Alinhando
  - `Align` - Alinhando UV;
  - `Match UVs` - Alinha duas Shells empilhadas;
- `Pin`   Bloqueando
  - `Pin Tool` - Selecionando usando tecla `B` ou `P` para bloquear áreas;

<a name="6"></a>
## CAPÍTULO 6 - Iluminação e Renderização


<a name="7"></a>
## CAPÍTULO 7 - Animando cenas no Autodesk Maya

- S - Marcar frame
- Shift + LMB = Seleciona

- Preferences = timecode

- Adicionar uma curva no objeto = p

- Travar camera = lock

- key select em atributos

- Arnold - SkyDomeLight

- Playback

- Visualize > Ghost Selectd/Unselect

- Visualize > Create Editable Montion trail

- Visualize > Create Animation Snapshot

## Primeiros passos na modelagem 3D

Introdução ao desenho 3D e ao Maya  -Conceitos de modelos 3D e desenho por computador

Estrutura do ambiente - Conhecendo editores e comandos básicos de navegação

Modelo Poligonal - Extrusão de elementos, copiando elementos

Modelo Poligonal - Deslocando pivot, seleção de áreas

Modelo poligonal - Manipulação de arestas e preenchimento de áreas

Modelo de curvas - Trabalhando com curvas e suas estruturas .

Modelo de curvas - Estruturas complexas de curvas, preenchimento automático

Modelos de curvas - Construindo caminhos para objetos poligonais ou de curvas

##   Modelagem 3D Luz, Câmera e Ação


Materiais - Conceitos de materiais

Materiais - Aplicando materiais no Maya e trabalhando com diversos tipos

Materiais - Aplicando Mapeamento UV

Materiais - Estruturando o mapeamento UV

Iluminação - Utilizando o Arnold Render

Iluminação - Aplicando vários tipos de iluminação

Animação - Trabalhando com várias câmeras  e animando objetos

Animação - Animando cenas no Maya com curvas
