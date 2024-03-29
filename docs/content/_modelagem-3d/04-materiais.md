---
title: Materiais
excerpt: Apresentação de materiais
permalink: /modelagem-3d/materiais
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 103
tags:
  - materiais
---

## 1. Materiais

No Maya, os nós de material definem como as superfícies reagem à luz. O Maya contém vários tipos de nós de material que ajudam a simular as qualidades ou comportamentos do mundo real de superfícies à luz: nós de material de superfície (*Surface Material*), nós de material volumétrico (*Volumetric Material*)e o nó de material de deslocamento (*Displacement Material*).

Você pode definir os atributos de um material, como cor, especularidade, refletividade, transparência e detalhes da superfície dos elementos da cena para criar uma ampla variedade de imagens realistas.

> Observação:
>
>Quando você cria um objeto pela primeira vez, o Maya atribui uma versão especial do material `Lambert` (um material de superfície ou *Surface Material*) por padrão.

### 1.1. Surface Material

Os materiais de superfície representam os tipos de superfícies nas quais você pode mapear texturas. Atributos como brilho, fosco, refletividade, brilho e assim por diante variam entre os diferentes tipos de materiais no Maya. Por exemplo, se a textura exigir uma superfície brilhante, como cromo, use um material `Phong`.

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-surface-material.webp"
    alt="Figura: Surface Material."
    caption="Figura: Menu Assign New Material - Maya > Surface. "
%}

Para obter uma descrição detalhada dos atributos de um material de superfície, consulte [Nós de material de superfície](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-LightingShading/files/GUID-634CAFBE-AC48-4B73-89CA-82D64FA1BC70-htm.html).

### 1.2. Displacement Material

O material de deslocamento permite que você use uma imagem para especificar o relevo da superfície em objetos em sua cena. Para saber mais sobre o relevo de superfície, consulte [Sobre o relevo de superfície](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-LightingShading/files/GUID-F403A3FF-55BE-43A0-B6E1-49BA7C6BF5EE-htm.html).

### 1.3. Volumetric material (atmosphere)

No mundo real, quando você fotografa um objeto, geralmente ele está dentro de uma atmosfera (ar) e cercado por outros objetos (fundo).

Materiais volumétricos descrevem a aparência física de fenômenos que ocupam um volume de espaço (por exemplo, neblina, fumaça, poeira ou outras partículas finas). Você pode rastrear materiais volumétricos e produzir efeitos como exibir neblina de luz por meio de reflexões e refrações de espelho.

Para obter uma descrição de materiais volumétricos, consulte [Sobre materiais volumétricos](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-LightingShading/files/GUID-6FF09EBA-CD7C-45B7-8B49-305D748EE7B4-htm.html).

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-volumetric-material.webp"
    alt="Figura: Volumetric Material."
    caption="Figura: Menu Assign New Material - Maya > Volumetric"
%}

### 1.4. Hypershade

{% include image.html
    src="https://help.autodesk.com/cloudhelp/2020/ENU/Maya-LightingShading/images/GUID-C59B74F1-2AFF-4EB1-8745-3D742EE005F7.png"
    alt="Figura: Hypershader Editor"
    caption="Figura: O editor do Hypershader"
%}

Para criar um material utilize a aba `Create tab`, selecionando o tipo os nós serão construídos no `Work Area`.

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-material-hypershader-create-material.webp"
    alt="Figura: Create material."
    caption="Figura: Crie um material e renomeie para representar o elemento ao qual deve ser aplicado."
%}

Ao clicar com o RMB no material listado no `Browser` acionamos o menu de contexto do mateial, pemite abrir os nós do material na `Work Area`.

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-material-hypershader-open-graph-network.webp"
    alt="Figura: RMB open graph network."
    caption="Figura: Podemos listar os nós do material escolhendo a opção Open Graph Network."
%}

### 1.5. Criando materiais com as opções do menu

Para criar um material utilize:

Status Line: `Rendering` > `Light/Shading` > `New Material`.

Status Line: `Rendering` > `Light/Shading` > `Assing New Material`, para criar e associar o material a um objeto selecionado.

### 1.6. Atributos do material

Status Line: `Rendering` > `Light/Shading` > `Material Attributes`.

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-material-attibutes1.webp"
    alt="Figura: Material Attributes."
    caption="Figura: Apresentando os atributos do material."
%}

- Color: Escolha da cor base do material;

- Transparency: Transparência;

- Incandescence: Emissão da luz;

- Bump Mapping - Adiciona uma imagem para [Bump Mapping](https://pt.wikipedia.org/wiki/Bump_mapping)

### 1.7. Checker ou Fluxo de trabalho

Ao escolher um atributo, color, por exemplo, é possível ligar o material a outro elemento ou material, construindo um fluxo de elementos.

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-material-attibutes-flow1.webp"
    alt="Figura: Material Attributes checker."
    caption="Figura: Atributo checker permite ligar o material a outro elemento."
%}

Usamos os comandos abaixo para navegar pelos elementos dentro do painel de atributos do material.

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-material-attibutes-flow2.webp"
    alt="Figura: Material Attributes next."
    caption="Figura: Próximo e Anterior ícones respectivamente e o ícone apresentando a ligação com outro elemento."
%}

Para quebrar a conexão selecione o atributo e RMB > `Break Connection`.

### 1.8. Adicionando uma imagem

Crie um novo material, logo em seguida altere o atributo `color` e associe a um elemento do tipo `file`.

Propriedades:

`Filter type` : Filtro interno para carregar imagens;

O elemento `Place2DTexture` é associado automáticamente a imagem para que possamos alterar as propriedades.

`Coverage`: Especifica qual proporção da superfície o mapa de textura cobre. O intervalo válido é de 0 a + infinito para superfícies NURBS. Um valor de 1 (o padrão) cobre toda a superfície na direção U ou V.

`Translate`: Os atributos Translate posicionam o mapa de textura na superfície e movem a área de cobertura pela superfície. O intervalo é de - infinito a + infinito.

### 1.9. Tipos de Materiais (Maya)

#### 1.9.1. Lambert

simples sem reflexo, brilho e transparência)

- Color: cor do material;

- transparência: Aumenta o alpha;

- Ambiente color: aumenta a tonalidade da cor;

- Incandescência: Adiciona uma luz ao material;

- Bump Mapping: adiciona textura para associar rugosidade ou padrões;

- Diffuse: Torna mais claro ou escuro a cor.

#### 1.9.2. Blind

Com brilho e reflexo

- Specular [Reflexão especular](https://pt.wikipedia.org/wiki/Reflex%C3%A3o_especular)
  
- Eccentricty: Aumenta o brilho
  
- Specular Roll off: Desfoque aplicado no brilho
  
- Specular color : Cor do brilho
  
- Reflectivity: Aumenta a intensidade do reflexo

#### 1.9.3. Phong

Parecido com o Blind mas com mais parâmetros.

[Sobre o phong](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Maya/files/GUID-3EDEB1B3-4E48-485A-9714-9998F6E4944D-htm.html)

- Specular Shadding

- Roughness: rugosidade

- Highlight size: tamanho do desfoque

- Anisotropic

- Specular Shader

- Angle: ângulo da luz

### 1.10. Usando Normal Map

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-material-base-color-normal-map.webp"
    alt="Figura: Base color Normal Camera."
    caption="Figura: Adicionamos duas texturas em Base Color e Normal Camera, textura completa e outra com as normais calculadas, em seguida usamos aiNormalMap do Arnold."
%}

## 2. Renderização e Iluminação

***

### 2.1. Cameras

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-camera.webp"
    alt="Figura: Create camera."
    caption="Figura: Para criar uma câmera utilize Create > Cameras > Camera Type."
%}

- `Viewport` - Selecione a as opções de câmera : `Select Camera`, `Lock Camera`, `Camera Attributes`.

- `Viewport Panels` - Escolha a `Perspective` > `Camera 1` ou o nome da câmera para a visão da câmera.

### 2.2. Renderização

Podemos alterar o `Viewport` para renderizar a cena escolhendo `Renderer` > `Arnold`

Para visualizar a cena renderizada ou cena final devemos configurar o software utilizado para renderizar a cena, `Render` > `Render Settings` > `Render Using` > `Arnold Renderer`.

- O ícone de renderização, que é apenas o filme, renderizará o quadro atual;

- Para renderizar novamente apenas uma determinada região, clique e segure na imagem renderizada (pode ser necessário clicar no botão no menu – Imediatamente ao lado do ícone de renderização de quadro único);

- O próximo botão é o botão de instantâneo, isso nos permite salvar uma imagem em nosso computador da renderização;

- Render Sequence: Permite renderizar vários quadros ou uma animação;

- IPR: Você pode habilitar isso, e cada vez que você fizer uma atualização na área de trabalho para um modelo ou valores, as alterações serão atualizadas na visualização de renderização;

- Você também acessa a configuração de renderização nesta janela clicando no botão com o ícone de engrenagem no canto inferior direito;

- Se você quiser comparar imagens, clique no ícone 'Manter imagem' (imagem de uma imagem), cada vez que você executar uma nova renderização, a imagem anterior será preservada e acessível através do controle deslizante na parte inferior da janela de visualização de renderização;

- Há também controles deslizantes de exposição e contraste de cores nesta janela

### 2.3. Iluminação

#### 2.3.1. Ambient

Ilumina todas as partes da cena uniformemente;

Útil para: Simular uma combinação de iluminação direta e indireta.

#### 2.3.2. Directional

Iluminação uniforme de uma cena usando paralelo raios de luz;

Útil para: Fontes extremamente distantes:

- Ex. Luz solar.

#### 2.3.3. Point

A luz irradia em todas as direções de um ponto único;

Ideal para: Fontes omnidirecionais:

- Ex. Lâmpada elétrica.

#### 2.3.4. Spot

Cria um cone de luz em uma direção;

Útil para: Feixes de luz;

- Ex. lanterna, farol.

#### 2.3.5. Area

Fontes de luz retangulares 2D;

Útil para: Janelas, Luzes de Teto;

Maior tempo de renderização;

#### 2.3.6. Volume

A luz preenche uma forma 3D (esfera, cilindro,etc.);

Útil para: Uma representação visual do extensão da luz.

### 2.4. Propriedades da luz

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-material-point-light.webp"
    alt="Figura: Planar mapping options."
    caption="Figura: UV > Planar > Planar Mapping Options >  Escolha uma coordenada X,Y,Z ou Camera para ajustar a textura. "
%}

- `Intensity` - Quanta luz emitida pela fonte de luz;

- `Decay` - Quanta luz diminui longe da fonte luz (queda);

- `Cone Angle` - Largura do cone de influência das luzes - área cone externo não iluminado;

- `Penumbra Angle` - Queda na borda do ângulo do cone - mais dá uma borda mais suave ao cone de luz;

- `Drop-off` - quanto a luz diminui no exterior arestas;

- `Color` - defina uma cor RGB para a luz - afeta a cor cena.

## 3. Mapeamento UV

***

É o processo de projetar uma textura bidimensional, mapa de textura, em um objeto 3D. As letras "UV" e "V" denotam os eixos de textura 2D porque o "X", "Y" e "Z" já são usados para indicar eixos 3D.

{% include imagelocal.html
    src="autodesk-maya/330px-Cube_Representative_UV_Unwrapping.webp"
    alt="Figura: Mapeamento UV."
    caption="Figura: Uma representação do mapeamento UV de um cubo. A planificação de um cubo faz parte do processo de mapeamento. <https://pt.wikipedia.org/wiki/Mapeamento_UV>"
%}

### 3.1. Mapeamento automático

Para mapeamento automático siga os passos a seguir:

#### 3.1.1. Planar Mapping Options

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-planar-mapping-options.webp"
    alt="Figura: Planar mapping options."
    caption="Figura: UV > Planar > Planar Mapping Options >  Escolha uma coordenada X,Y,Z ou Camera para ajustar a textura. "
%}

#### 3.1.2. Ajustes usando Planar Mapping Options

{% include imagelocal.html
    src="autodesk-maya/autodesk-maya-planar-mapping-options-ajust.webp"
    alt="Figura: Planar Ajustes."
    caption="Figura: Ajuste as coordenadas da textura clicando no indicador vermelho do objeto. "
%}

### 3.2. Mapeamento manual

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

  - `Transform` > `Move`

- Copiando dados de um Shells para outra  

  - `Transform` > `Texel Density` > `Get` - copia os valores de um elemento selecionado;

  - `Transform` > `Texel Density` > `Set` - cola os valores para um elemento selecionado;

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

## 4. Hide  

Selecione um objeto e pressione Ctrl + H ou `Display` > `Hide` > `Hide Selection`

No `Outliner` os objetos ocultos ficam com a cor mais escura;

No `Channel Box` é possível alterar a visibilidade colocando o valor 1 (on) na propriedade `Visibilty`.

Para mostrar o último objeto escondido podemos usar `Display` > `Show` > `Show Last Hidden`.

Para apresentar um objeto escondido usando o `Outliner` usamos `Display` > `Show` > `Show Selection`.

## 5. Animando cenas no Autodesk Maya

***

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
