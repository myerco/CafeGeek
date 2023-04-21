---
title: Introdução aos Materiais
excerpt: Neste capítulo vamos apresentar o que são materiais e a sua estrutura.
permalink: /pages/unreal-engine/materiais-introducao
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true 
categories:
  - Unreal Engine
tags:
  - materiais
  - texturas
  - PBR
---

## 1. O que é um material?

Podemos definir como uma coleção de imagens e instruções computacionais que são adicionadas a superfícies poligonais. Contudo materiais não são somente cores mas representação de imperfeições da superfície a qual foram aplicadas, como por exemplo, rasuras, aspereza e transparência.

{% include image.html
    src="https://cdn2.unrealengine.com/Unreal+Engine%2Fonlinelearning-courses%2Fmaterials---exploring-essential-concepts%2FMaterialEssentialConcepts-1920x1080-1920x1080-2414bb5cf0b0c3bd7ac4b993e725d2acedd45334.png?resize=1&w=1400"
    alt="Figura: Material - Unreal Engine"
    caption=" Material Essential Concepts."
%}

No exemplo acima podemos verificar uma esfera com diferentes tipos de materiais adicionados na sua superfície, onde cada um interage de forma diferente a iluminação.

## 2. Materiais de base física - PBR

PBR *Physically Based Rendering* significa que o material descreve as propriedades visuais de uma superfície de uma maneira realmente plausível, de modo que os resultados realistas sejam possíveis em todas as condições de iluminação.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-pbr.webp"
    alt="Figura: Material PBR."
    caption=" Physically Based Rendering."
%}

## 3. Estrutura do Material no Unreal Engine

A primeira e mais importante coisa a saber sobre os Materiais é que eles não são construídos por meio de código, mas por meio de uma rede de nós de script visual (chamados de Expressões de Material) dentro do Editor de Material. Cada nó contém um fragmento de código HLSL, designado para executar uma tarefa específica.

### 3.1. Criando um material

Para criar um material utilizamos o menu de contexto e a opção `Material`.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-menu-material.webp"
  alt="Figura: Context Menu > Material."
  caption="Utilizamos o menu de contexto para criar um material."
%}

Salve o material como `M_Base`.

### 3.2. Editor de Materiais

O Editor de Materiais consistem em uma barra de menu, toolbar e cinco regiões de propriedades [[Material Editor UI](https://docs.unrealengine.com/5.0/en-US/unreal-engine-material-editor-ui/)].

{% include image.html
  src="https://docs.unrealengine.com/5.0/Images/designing-visuals-rendering-and-graphics/materials/material-editor-user-guide/interface/material-editor-ui-full.webp"
  alt="Figura: Unreal Engine - Material Editor UI"
  caption=" O editor de materiais apresenta o gráfico de nós de material, código de implementação de materiais e os elementos necessários para a sua manipulação."
%}

1. Editor de materiais;

1. Barra de acesso rápido;

1. Pré-visualização do material;

1. Propriedades do nó selecionado;

1. Editor de lógica de nós;

1. Lista de funções ou nós disponíveis.

## 4. O que são Material expressions?

Os nós de Expressão de Material ou Material Expression contêm pequenos fragmentos de código HLSL que realizam tarefas muito específicas dentro de um Material. Os materiais são construídos usando combinações de nós de Expressão de Material que são combinados para realizar certas tarefas.

Conectando Material Expressions, abaixo um exemplo de conexão.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-connection.webp"
  alt="Figura: Exemplo de connection."
  caption=" Exemplo de connection."
%}

- Botão direito do mouse em qualquer área de trabalho (RMB) abre a lista de nós disponíveis;

- É possível fazer a busca de nós na aba `Palette` e arrastar com o mouse na área de trabalho.

Combinando `Material Expressions`, a área de trabalho é um modelo de programação visual que permite combinar variáveis e funções para construir a estrutura final. Cada nó apresenta uma saída para o próximo nó.

**Atenção:** Devemos considerar o tipo de valor de retorno do nó no momento da conexão para evitar erros de tipos conflitantes, por exemplo float3 * float2.
{: .notice--warning}

### 4.1. Valores que determinam a física

Existem variáveis ou nós específicos para determinar uma propriedade física do material, por exemplo um valor `float` com valores entre 0 e 1 que expressam a escala de tonalidades de cor, sombra e pedaços (pixels) de uma área.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-node-constant-1.webp"
  alt="Figura: Constant 1 - (Clicando 1 + RMB)."
  caption="Constant 1 ou valor escalar- Valor único."
%}

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-node-constant-2.webp"
  alt="Figura: Constant 2 - (Clicando 2 + RMB) para implementar o nó."
  caption="Constant 2 - Vetor de dois valores."
%}
  
{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-node-constant-3.webp"
  alt="Figura: Constant 3 - (Clicando 3 + RMB) para implementar o nó."
  caption="Constant 3 - Vetor de três valores."
%}

### 4.2. Texture samples

Texturas são imagens que são usadas em materiais e são representadas pelo nó abaixo.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-node-texture-sample.webp"
  alt="Figura: Material texture."
  caption="Clicando T + RMB."
%}

Considerações sobre texturas no **Unreal Engine**.

Tamanhos :

- 1x1, 2x2, 4x4, 1024x1024 e 8192x8192;
- As texturas serão importadas em qualquer tamanho, mas não serão mipmaps.

A seguir vamos abordar as características das texturas no **Unreal Engine**.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-texture.webp"
  alt="Figura: Base texture."
  caption="No exemplo utilizamos uma textura para determinar a cor base do objeto, utilizamos o canal vermelho (R) e o canal aplha (A) para alterar as propriedades do material."
%}

## 5. O Nó principal ou Node Result

O nó principal do material é responsável por exibir os resultados de todos os nós da *Expressão de Material* que são inseridos nele nas várias entradas. Cada entrada no nó Material Principal tem um efeito exclusivo sobre a aparência e o desempenho do Material.

Abaixo o nó principal e suas principais entradas.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-node-result-properties.webp"
  alt="Figura: Nó principal ou Node Result."
  caption="Nó que compila todos os parâmetros e valores e aplica no malha."
%}

### 5.1. Base color

A Cor Base define a cor geral do Material, tomando um valor Vector3 (RGB) onde cada canal é automaticamente fixado entre 0 e 1.

Se tirada do mundo real, esta é a cor quando fotografada usando um filtro polarizador (a polarização remove a especular dos não metais quando alinhada).

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/BaseColor_QS.webp"
  alt="Figura: Unreal Engine - Base color"
  caption="Propriedade Base color determina a cor base do material."
%}

### 5.2. Normal

O mapa Normal define em qual direção uma parte de uma superfície é voltada, que é usada para criar sombras e realces detalhados.

{% include image.html
  src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a8/Normal_vectors_on_a_curved_surface.svg/620px-Normal_vectors_on_a_curved_surface.svg.png"
  alt="Figura: Normal (geometry)"
  caption=" Normais de uma superfície."
%}

{% include image.html
  src="https://docs.unity3d.com/uploads/Main/BumpMapBumpShadingDiagram.svg"
  alt="Figura: Normal map (Bump mapping)"
  caption="Mapeamento normal em três polígonos, visto como um diagrama 2D."
%}

{% include image.html
  src="https://docs.unity3d.com/uploads/Main/BumpMapTexturePreview.png"
  alt="Figura: Normal map (Bump mapping)"
  caption="Exemplo de uma textura de mapa normal."
%}

### 5.3. Textura Normal

Usado para simular a maneira como a luz interage com a superfície do material para simular saliências e amassados menores.
É importante observar que um mapa normal não mudará sua geometria base (consulte os mapas de altura posteriormente neste artigo).

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-normal-rock-basalt.webp"
  alt="Figura: Texture Normal."
  caption="Exemplo de uma textura de mapa normal."
%}

A cor base de um mapa normal é roxo claro, esta é a “parte inferior” do mapa normal que representa a superfície de sua malha poligonal. A partir daí, os valores RGB são usados para produzir rachaduras, saliências ou poros em seu modelo. Os valores R, G e B são iguais às coordenadas X, Y e Z em sua malha base.

### 5.4. Metallic

O mapa Metálico define quais partes de um material são metálicas e quais não são. Seu valor será 0 ou 1, nada intermediário. Ao criar superfícies híbridas como metais corroídos, empoeirados ou enferrujados, você pode achar que precisa de algum valor entre 0 e 1.

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/metallic.png"
  alt="Figura: Physically Based Materials Metallic."
  caption="O valor para o parâmetro Metallic é 0 até 1."
%}

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/Metallic_1.jpg"
  alt="Figura: Metallic."
  caption="Exemplo de um vetor 3 e o valor escalar de 1 no parâmetro Metallic."
%}

### 5.5. Textura Metallic

Os mapas de metal também são em tons de cinza, mas a prática recomendada é usar apenas os valores de branco e preto e fazer as variações entre o uso de seus mapas de rugosidade.

Para exemplificar utilizaremos o canal R (Red) da textura *Rock Basalt*.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-chanel-r-rock-basalt.webp"
  alt="Figura: Texture Metallic."
  caption="Exemplo de uma textura que pode ser utilizada como base do parâmetro metallic, a textura é gradiente de negro e branco e representa a escala de 0 (negro) e 1 (branco)"
%}

### 5.6. Roughness

O mapa de rugosidade define a rugosidade de uma superfície. Uma rugosidade de 0 (suave) resulta em uma reflexão de espelho e rugosidade de 1 (áspera) resulta em uma superfície difusa (ou fosca).

`Roughness` (Aspereza e também chamada de brilho ou dispersão da micro-superfície) é um mapa semi-autoexplicativo. Eles definem como a luz é espalhada pela superfície do seu modelo.
Isso começa com um valor de zero, onde seu modelo não dispersará a luz, tornando os reflexos e a iluminação muito mais nítidos e brilhantes em seu material.
Por outro lado, se você aumentar a rugosidade ao máximo, a luz se espalhará mais pelo material. Isso faz com que a iluminação e os reflexos se espalhem pelo modelo, mas pareçam muito mais escuros.

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/roughness_nonmetal.png"
  alt="Figura: Physically Based Materials Roughness."
  caption="Rugosidade de 0 até 1."
%}

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/Roughness_1.jpg"
  alt="Figura: Roughness."
  caption="Exemplo da rugosidade, zero representa sem rugosidade."
%}

### 5.7. Textura Roughness

Para exemplificar utilizaremos o canal A (Alpha) da textura `Rock Basalt`.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-chanel-a-rock-basalt.webp"
  alt="Figura: Texture Roughness."
  caption="Esses mapas são em tons de cinza, com o branco sendo a aspereza máxima e o preto sendo uma superfície lisa e brilhante."
%}

### 5.8. Specular

Ao editar um material de superfície não metálico, há momentos em que você deseja ajustar sua capacidade de refletir a luz, especificamente, sua propriedade Specular. Para atualizar o Specular de um Material, insira um valor escalar entre 0 (não refletivo) e 1 (totalmente refletivo). Observe que o valor especular padrão de um material é 0,5.

Valores especulares medidos:

| Material | Valor |
| :------- | :---- |
| Grama    | 0.5   |
| Plástico | 0.5   |
| Quartz   | 0.570 |
| Gelo     | 0.224 |
| Água     | 0.255 |
| Pele     | 0.35  |

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/Specular_1.jpg"
  alt="Figura: Specular."
  caption="Parâmetro Specular."
%}

### 5.9. Ambient Occlusion

O mapa Ambient Occlusion (AO) pode ser usado para simular sombras suaves nas saliências de uma superfície. Não é realmente necessário criar materiais realistas no Blender (especialmente com Cycles), mas você ainda pode usá-lo para escurecer as pequenas sombras na superfície.

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/PostProcessEffects/AmbientOcclusion/ao_0.webp"
  alt="Figura: Ambient Occlusion 1 ."
  caption="Scene without Ambient Occlusion."
%}

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/PostProcessEffects/AmbientOcclusion/ao_1.webp"
  alt="Figura: Ambient Occlusion 2."
  caption="Ambient Occlusion Only."
%}

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/PostProcessEffects/AmbientOcclusion/ao_2.webp"
  alt="Figura: Ambient Occlusion 3."
  caption="Scene with Ambient Occlusion."
%}

## 6. Propriedades do nó principal

Nem todas as entradas serão úteis para cada tipo de material que você criar. Por exemplo, ao desenvolver uma Função de Luz - um Material que é aplicado a uma luz - você só pode usar a entrada Cor Emissiva no material e nada mais, visto que outras entradas, como Metálico ou Aspereza, não seriam aplicáveis. Por isso, é importante saber que tipo de material você está criando antes de começar a se preocupar muito com as entradas. As três propriedades de controle primárias são:

### 6.1. Blend Mode

Controla como o seu material se mesclará com os pixels por trás dele.

"Os modos de mesclagem descrevem como a saída do material atual se mesclará com o que já está sendo desenhado no fundo. Em termos mais técnicos, ele permite que você controle como o mecanismo combinará este Material (cor de origem) com o que já está no buffer de quadros (cor de destino) quando renderizado."

- `BLEND_Opaque` - Cor final = cor de origem. Isso significa que o material será desenhado na parte superior do fundo. Este modo de mesclagem é compatível com iluminação.

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/CameraObjectSetup.webp"
  alt="Figura: Material - Opaque."
  caption="BlendModes - Opaque"
  ref="https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/"
%}

- `BLEND_Masked` -  Cor final = cor de origem se `OpacityMask` > `OpacityMaskClipValue`, caso contrário, o pixel é descartado. Este modo de mesclagem é compatível com iluminação.

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/MaskedGridMaterial.webp"
  alt="Figura: Material - Masked."
  caption="Material com máscara."
%}

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/MaskedSetup.webp"
  alt="Figura: Masked 2."
  caption=" Material BlendModes - Masked <https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/)>."
%}
  
- `BLEND_Translucent` - Cor final = opacidade da cor de origem + cor de destino (1 - opacidade). Este modo de mistura NÃO é compatível com  iluminação dinâmica.

{% include imagelocal.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/TranslucentNetwork.webp"
  alt="Figura: Blueprint Material- Translucent."
%}
  
{% include imagelocal.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/TranslucentSetup.webp"
  alt="Figura: [Material BlendModes - Translucent](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/)"
%}
  
- `BLEND_Additive` - Cor final = cor de origem + cor de destino. Este modo de mistura NÃO é compatível com iluminação dinâmica.

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/AdditiveNetwork.webp"
  alt="Figura: Blueprint Material- Additive."
%}

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/AdditiveSetup.webp"
  alt="Figura: Additive 1."
  caption="Additive"
  ref="https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/"
%}

- `BLEND_Modulate` - Cor final = cor de origem x cor de destino. Este modo de mistura NÃO é compatível com iluminação dinâmica ou neblina, a menos que seja um material de decalque.

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/ModulateNetwork.webp"
  alt="Figura: Material- Modulate."
  caption="Modulate."
%}

{% include imagelocal.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/ModulateScene.webp"
  alt="Figura: Blueprint Material- Modulate 1."
  caption="Modulate"
  ref="https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/"
%}
  
### 6.2. Shading Model

Define como a luz é calculada para a superfície do material.

{% include imagelocal.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/LightingModels/LightingModelProperties.webp"
    alt="Figura: Shading Models."
    caption="Shading Models"
    ref="https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/LightingModels/"
%}

### 6.3. Material Domain

Controla como o material deve ser usado, por exemplo, se ele deve fazer parte de uma superfície, uma função leve ou um material pós-processamento.

> Esta configuração permite designar como este material será usado. Certos usos de materiais (como decalques) requerem instruções adicionais para o mecanismo de renderização considerar. Por isso, é importante designar o Material como sendo usado para esses casos

- `Surface` - Esta configuração define o Material como algo que será usado na superfície de um objeto; pense em metal, plástico, pele ou qualquer superfície física. Como tal, esta é a configuração que você usará na maioria das vezes;

- `Deferred Decal` -  Ao fazer um [Material de Decalque ou Decal Material](https://docs.unrealengine.com/4.26/en-US/Basics/Actors/DecalActor/), você usará esta configuração;

- `Light Function` - Usado ao criar um material para uso com uma função de luz;

- `Volume` - Usado ao descrever os atributos do material como um volume 3D;

- `Post-process` - Usado se o material for usado como um [Material de pós-processamento](https://docs.unrealengine.com/4.26/en-US/RenderingAndGraphics/PostProcessEffects/PostProcessMaterials/);

- `User Interface` - Usado quando este material é usado para interfaces de usuário UMG ou Slate;

- `Virtual Texture` - Usado ao fazer uma textura virtual em tempo de execução;

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-type-input.webp"
    alt="Figura: Blueprint Material- Type input."
    caption="Material Domain."
%}

## 7. Aplicando o material no objeto

Para aplicar o material em um objeto podemos selecionar o objeto e atualizamos a propriedade `MATERIALS` selecionando o material criando anteriormente.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-applying.webp"
    alt="Figura:  Applying Material."
    caption="Aplicando um material em um objeto."
%}

## 8. As propriedades e a lógica do material

Neste exemplo vamos combinar várias texturas e utilizar funções de manipulação para obter o resultado abaixo.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-combine-color.webp"
  alt="Figura: Objeto com mistura de texturas."
  caption="Exemplo de um objeto com diferentes texturas."
%}

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-node-combine.webp"
  alt="Figura: Lógica da combinação de texturas."
  caption="É possível criar comentários no diagrama, acima a lógica de construção de nós com comentários para facilitar a documentação."
%}

`Base Color 1` - Cada pixel do canal R da textura é multiplicado pela cor.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-chanel-r-wood-pine.webp"
  alt="Figura: Channel R Texture Wood Pine."
  caption="Na textura o valor 1 = branco e 0 = preto."
%}

`Base Color 2`

`Lerp` - Recebe o resultado da multiplicação e dos canais RGB da textura para do passo anterior. No parâmetro  Alpha é informado o canal G textura.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-chanel-g-ceramic-tile.webp"
  alt="Figura: Channel G Texture Ceramic Tile."
  caption="Neste passo o valores 0 (branco) e 1 (preto) são multiplicados."
%}

Podemos exemplificar o que está acontecendo utilizando uma expressão matemática de uma multiplicação entre vetores, pois os elementos são vetores de três dimensões (vector3).

```c++
  resul =  ( Vetor3(0.0664,0.0366,0.401) * Vetor3(0,1,0) );
  // Resultado
   (0,0.0366,0)
```

`Multiply` multiplica o canal R da textura com o resultado do Lerp.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-chanel-r-ceramic-tile.webp"
  alt="Figura: Channel R Texture Ceramic Tile."
  caption="O canal vermelho (R) da textura representa, nesta textura, os valores 0 e 1 com tons de cinza."
%}

- `Normal Map` - Mapa normal.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-mask-add-append.webp"
  alt="Figura: Texture Normal."
  caption=" Utilizamos texturas normais para distorcer o reflexo de luz."
%}

- `Mask` - Filtra os canais passados como parâmetro;

- `Append` - Combina dois canais juntos para criar um vetor com mais canais que o original.

```c++
resul =  ( Mask(Vetor3(64,36,40),1,1,0));
// Resultado 2 colunas
(64, 36)
resul = append(resul, 0);
// Resultado 3 colunas
(64, 36,0)
```

- `Add` - Adiciona os valores de dois parâmetros e retorna um novo vetor, por exemplo.

```c++
resul =  Add( vetor3(1,3,4) , vetor3(2,4,1)  );
// Resultado
(3,7,5)
```

## 9. Utilizando Panner e TextCoord

Neste exemplo será simulado o movimento da textura no objeto.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-panner.webp"
  alt="Figura: Function Panner."
  caption=" A função Panner adiciona velocidade e tempo nas coordenadas UV simulando movimento."
%}

Representação da lógica.

```c++
  M_Base =  ( TexturaSample( panner(TexCoord(),0.1,0) ) * Vetor3(0.0664,0.0366,0.401));
```

- `Panner` - Produz coordenadas de textura UV que podem ser usadas para criar texturas panorâmicas ou móveis;

- `Multiply` - Pega duas entradas, multiplica-as juntas e produz o resultado.
Se você passar valores com vários canais, cada canal será multiplicado separadamente. Por exemplo, se você passar valores de cor RGB para cada entrada, o canal R da primeira entrada é multiplicado pelo canal R da segunda entrada e o resultado é armazenado no canal R da saída; o canal G da primeira entrada é multiplicado pelo canal G da segunda entrada e o resultado é armazenado no canal G da saída e assim por diante.
Ambas as entradas devem ter o mesmo número de valores, a menos que um dos valores seja um único valor flutuante. Nesse caso, cada canal da entrada multicanal é multiplicado pelo valor flutuante único e armazenado em um canal separado do valor de saída;

- `TexCoord` - Gera coordenadas de textura UV na forma de um valor vetorial de dois canais, permitindo que os materiais usem diferentes canais UV, especifiquem ladrilhos e, de outra forma, operem nos UVs de uma malha.

## 10. Exemplo do nó Lerp

Interpola Linearmente entre A e B com base em Alfa (100% de A quando Alfa = 0 e 100% de B quando Alfa = 1)

{% include imagelocal.html
  src="unreal/materiais/ue4_material-lerp-exemplo.webp"
  alt="Figura: Exemplo de Lerp."
  caption=" A função learp interpola linearmente dois valores, ou seja cria vários valores entre os parâmetros inicial (A) e final (B)."
%}

## 11. World position Offset

Permite que os vértices de uma malha sejam manipulados no espaço do mundo pelo Material. Isso é útil para fazer objetos se moverem, mudarem de forma, girarem e uma variedade de outros efeitos. Isso é útil para coisas como animação ambiente.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-world_position-offset.webp"
  alt="Figura: World Position Offset."
  caption=" O parâmetro  World position Offset permite manipulação da malha."
%}

Os valores do nó Constant Vector 3, representam as coordenadas de posição do mundo (x,y,z) respectivamente.

Abaixo utilizamos variáveis para "animar" o material e simular movimento na malha.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-world_position_offset-panner.webp"
  alt="Figura: World Position offset."
  caption=" Utilizando a função Panner e uma textura em tons de cinza para alterar as coordenadas da malha."
%}

- `TexCoord` - U=0.15, V=0.15;

- `Panner` - Speed X =0.05, Speed Y= 0.1.

## 12. Unlit Shading Model

Produz apenas Emissivo para cores, tornando-o perfeito para efeitos especiais como fogo ou iluminação de objetos. Observe que, neste exemplo, o Material não está projetando luz na cena. Em vez disso, seu alto valor Emissivo resulta em um efeito de brilho, que também é captado pela Máscara de Sujeira aplicada à câmera. Parece iluminar, mas nenhuma luz ou sombra será projetada por este objeto.

{% include imagelocal.html
  src="unreal/materiais/ue4_material-properties_unlit.webp"
  alt="Figura: Properties Unlit Shading Model."
  caption=" Lógica utilizando Emissive Color com variáveis."
%}

{% include imagelocal.html
  src="unreal/materiais/ue4_material-properties-blend-mode-unlit-result.webp"
  alt="Figura: Material Properties blend Mode Unlit."
  caption=" Resultado do Unlit Shading Model."
%}

## 13. Masked Blend Mode

É usado para objetos nos quais você precisa controlar seletivamente a visibilidade de forma binária (liga / desliga). Por exemplo, considere um material que simula uma cerca de arame ou grade. Você terá algumas áreas que parecem sólidas, enquanto outras são invisíveis. Esses materiais são perfeitos para o modo de `Blend Masked` .

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-properties-blend-mode-masked.webp"
  alt="Figura: Properties blend mode masked."
  caption=" Lógica do material usando Opacity Mask."
%}

Parâmetros do scalar:

- `Roughness` - Valor 1.

Parâmetros do nó resultado:

- `Two Sided` - Valor `True`.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-properties-blend-mode-masked-result.webp "
  alt="Figura: Properties blend mode masked result."
  caption="Resultado do Blend Masked."
%}

## 14. Translucent Blend Mode

É usado para objetos que requerem alguma forma de transparência.

{% include imagelocal.html
  src="unreal/materiais/unreal-engine-material-properties-blend-mode-translucent.webp"
  alt="Figura: Properties blend mode Translucent."
  caption="Lógica do material utilizando Opacity e Translucent Blend Mode."
%}

Parâmetros do nó resultado:

- `Material Domain` - Surface;

- `Blend Mode` - Translucent;

- `Lighting Mode` - Surface TranslucencyVolume.

{% include imagelocal.html
  src="unreal/materiais/ue4_material-properties-blend-mode-translucent-result.webp"
  alt="Figura: Properties blend mode Translucent."
  caption="Resultado do Blend Mode Translucent."
%}
