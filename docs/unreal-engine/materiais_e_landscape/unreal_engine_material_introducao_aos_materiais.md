---
title: Introdução aos Materiais
description: Neste capítulo vamos apresentar o que são materiais e a sua estrutura.
tags: [Unreal Engine,Materiais, material Function, material]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
date: 2022-09-24 
---

## O que é um material?

Podemos definir como uma coleção de imagens e instruções computacionais que são adicionadas a superfícies poligonais. Contudo materiais não são somente cores mas representação de imperfeições da superfície a qual foram aplicadas, como por exemplo, rasuras, aspereza e transparência.

{% include image.html
    src="https://cdn2.unrealengine.com/Unreal+Engine%2Fonlinelearning-courses%2Fmaterials---exploring-essential-concepts%2FMaterialEssentialConcepts-1920x1080-1920x1080-2414bb5cf0b0c3bd7ac4b993e725d2acedd45334.png?resize=1&w=1400"
    alt="Figura: Material - Unreal Engine"
    caption="Figura: Unreal Engine - Material Essential Concepts."
%}

No exemplo acima podemos verificar uma esfera com diferentes tipos de materiais adicionados na sua superfície, onde cada um interage de forma diferente a iluminação.

## Materiais de base física - PBR

PBR *Physically Based Rendering* significa que o material descreve as propriedades visuais de uma superfície de uma maneira realmente plausível, de modo que os resultados realistas sejam possíveis em todas as condições de iluminação.

{% include image.html
    src="../imagens/materiais/material_pbr.webp"
    alt="Figura: Material PBR - <https://www.pikpng.com>."
    caption="Figura: Material PBR - <https://www.pikpng.com>."
%}

## Estrutura do Material no Unreal Engine

A primeira e mais importante coisa a saber sobre os Materiais é que eles não são construídos por meio de código, mas por meio de uma rede de nós de script visual (chamados de Expressões de Material) dentro do Editor de Material. Cada nó contém um fragmento de código HLSL, designado para executar uma tarefa específica.

### Criando um material

Para criar um material utilizamos o menu de contexto e a opção `Material`.

1. Utilize Menu de contexto para criar um material;
    {% include image.html
      src="../imagens/materiais/unreal_engine_menu_material.webp"
      alt="Figura: Contex Menu > Material."
      caption="Figura: Contex Menu > Material."
    %}
2. Salve o material como `M_Base`

### Editor de Materiais

O Editor de Materiais consistem em uma barra de menu, toolbar e cinco regiões de propriedades [Material Editor UI](https://docs.unrealengine.com/5.0/en-US/unreal-engine-material-editor-ui/).

{% include image.html
  src="https://docs.unrealengine.com/5.0/Images/designing-visuals-rendering-and-graphics/materials/material-editor-user-guide/interface/material-editor-ui-full.webp"
  alt="Figura: Unreal Engine - Material Editor UI"
  caption="Figura: O editor de materiais apresenta o gráfico de nós de material, código de implementação de materiais e os elementos necessários para a sua manipulação."
%}

1. Editor de materiais;

1. Barra de acesso rápido;

1. Pré-visualização do material;

1. Propriedades do nó selecionado;

1. Editor de lógica de nós;

1. Lista de funções ou nós disponíveis.

## O que são Material expressions?

Os nós de Expressão de Material ou Material Expression contêm pequenos fragmentos de código HLSL que realizam tarefas muito específicas dentro de um Material. Os materiais são construídos usando combinações de nós de Expressão de Material que são combinados para realizar certas tarefas.

Conectando Material Expressions, abaixo um exemplo de conexão.

{% include image.html
  src="../imagens/materiais/unreal_engine_material_connection.webp"
  alt="Figura: Blueprint Material - Exemplo de connection."
  caption="Figura: Blueprint Material - Exemplo de connection."
%}

- Botão direito do mouse em qualquer área de trabalho (RMB) abre a lista de nós disponíveis;

- É possível fazer a busca de nós na aba `Palette` e arrastar com o mouse na área de trabalho.

Combinando `Material Expressions`, a área de trabalho é um modelo de programação visual que permite combinar variáveis e funções para construir a estrutura final. Cada nó apresenta uma saída para o próximo nó.

> **Atenção** - Devemos considerar o tipo de valor de retorno do nó no momento da conexão para evitar erros de tipos conflitantes, por exemplo float3 * float2.

### Valores que determinam a física

Existem variáveis ou nós específicos para determinar uma propriedade física do material, por exemplo um valor `float` com valores entre 0 e 1 que expressam a escala de tonalidades de cor, sombra e pedaços (pixels) de uma área.

- Constant 1 ou valor escalar- Valor único.

    {% include image.html
      src="../imagens/materiais/unreal_engine_material_node_constant_1.webp"
      alt="Figura: Blueprint Material - Constant 1 - (Clicando 1 + RMB) para implementar o nó."
      caption="Figura: Blueprint Material - Constant 1 - (Clicando 1 + RMB) para implementar o nó."
    %}

- Constant 2 - Vetor de dois valores.

    {% include image.html
      src="../imagens/materiais/unreal_engine_material_node_constant_2.webp"
      alt="Figura: Blueprint Material - Constant 2 - (Clicando 2 + RMB) para implementar o nó."
      caption="Figura: Blueprint Material - Constant 2 - (Clicando 2 + RMB) para implementar o nó."
    %}
  
- Constant 3 - Vetor de três valores.

    {% include image.html
      src="../imagens/materiais/unreal_engine_material_node_constant_3.webp"
      alt="Figura: Blueprint Material - Constant 3 - (Clicando 3 + RMB) para implementar o nó."
      caption="Figura: Blueprint Material - Constant 3 - (Clicando 3 + RMB) para implementar o nó."
    %}

### Texture samples

Texturas são imagens que são usadas em materiais e são representadas pelo nó abaixo.

{% include image.html
  src="../imagens/materiais/unreal_engine_material_node_texture_sample.webp"
  alt="Figura: Blueprint Material texture - (Clicando T + RMB)."
  caption="Figura: Blueprint Material texture - (Clicando T + RMB)."
%}

Considerações sobre texturas no **Unreal Engine**.

Tamanhos :

- 1x1, 2x2, 4x4, 1024x1024 e 8192x8192;
- As texturas serão importadas em qualquer tamanho, mas não serão mipmaps.

A seguir vamos abordar as características das texturas no **Unreal Engine**.

{% include image.html
  src="../imagens/materiais/unreal_engine_material_texture.webp"
  alt="Figura: Blueprint Material - Base texture."
  caption="Figura: Blueprint Material, no exemplo utilizamos uma textura para determinar a cor base do objeto, utilizamos o canal vermelho (R) e o canal aplha (A) para alterar as propriedades do material."
%}

## O Nó principal ou Node Result

O nó principal do material é responsável por exibir os resultados de todos os nós da *Expressão de Material* que são inseridos nele nas várias entradas. Cada entrada no nó Material Principal tem um efeito exclusivo sobre a aparência e o desempenho do Material.

Abaixo o nó principal e suas principais entradas.

{% include image.html
  src="../imagens/materiais/unreal_engine_node_result_properties.webp"
  alt="Figura: Blueprint Material - Nó principal ou Node Result."
  caption="Figura: Blueprint Material e nó principal, nó que compila todos os parâmetros e valores e aplica no malha."
%}

### Base color

A Cor Base define a cor geral do Material, tomando um valor Vector3 (RGB) onde cada canal é automaticamente fixado entre 0 e 1.

Se tirada do mundo real, esta é a cor quando fotografada usando um filtro polarizador (a polarização remove a especular dos não metais quando alinhada).

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/BaseColor_QS.webp"
  alt="Figura: Unreal Engine - Base color"
  caption="Figura: Unreal Engine - Propriedade Base color determina a cor base do material."
%}

### Normal

O mapa Normal define em qual direção uma parte de uma superfície é voltada, que é usada para criar sombras e realces detalhados.

{% include image.html
  src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a8/Normal_vectors_on_a_curved_surface.svg/620px-Normal_vectors_on_a_curved_surface.svg.png"
  alt="Figura: Normal (geometry)"
  caption="Figura: Normais de uma superfície."
%}

{% include image.html
  src="https://docs.unity3d.com/uploads/Main/BumpMapBumpShadingDiagram.svg"
  alt="Figura: Normal map (Bump mapping)"
  caption="Figura: Mapeamento normal em três polígonos, visto como um diagrama 2D."
%}

{% include image.html
  src="https://docs.unity3d.com/uploads/Main/BumpMapTexturePreview.png"
  alt="Figura: Normal map (Bump mapping)"
  caption="Figura: Exemplo de uma textura de mapa normal."
%}

### Textura Normal

Usado para simular a maneira como a luz interage com a superfície do material para simular saliências e amassados menores.
É importante observar que um mapa normal não mudará sua geometria base (consulte os mapas de altura posteriormente neste artigo).

{% include image.html
  src="../imagens/materiais/unreal_engine_material_normal_rock_basalt.webp"
  alt="Figura: Blueprint Material - Texture Normal."
  caption="Figura: Exemplo de uma textura de mapa normal."
%}

A cor base de um mapa normal é roxo claro, esta é a “parte inferior” do mapa normal que representa a superfície de sua malha poligonal. A partir daí, os valores RGB são usados para produzir rachaduras, saliências ou poros em seu modelo. Os valores R, G e B são iguais às coordenadas X, Y e Z em sua malha base.

### Metallic

O mapa Metálico define quais partes de um material são metálicas e quais não são. Seu valor será 0 ou 1, nada intermediário. Ao criar superfícies híbridas como metais corroídos, empoeirados ou enferrujados, você pode achar que precisa de algum valor entre 0 e 1.

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/metallic.png"
  alt="Figura: Physically Based Materials Metallic."
  caption="Figura: O valor para o parâmetro Metallic é 0 até 1."
%}

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/Metallic_1.jpg"
  alt="Figura: Blueprint Material - Metallic."
  caption="Figura: Exemplo de um vetor 3 e o valor escalar de 1 no parâmetro Metallic."
%}

### Textura Metallic

Os mapas de metal também são em tons de cinza, mas a prática recomendada é usar apenas os valores de branco e preto e fazer as variações entre o uso de seus mapas de rugosidade.

Para exemplificar utilizaremos o canal R (Red) da textura *Rock Basalt*.

{% include image.html
  src="../imagens/materiais/unreal_engine_material_chanel_r_rock_basalt.webp"
  alt="Figura: Blueprint Material - Texture Metallic."
  caption="Figura: Exemplo de uma textura que pode ser utilizada como base do parâmetro metallic, a textura é gradiente de negro e branco e representa a escala de 0 (negro) e 1 (pranco)"
%}

### Roughness

O mapa de rugosidade define a rugosidade de uma superfície. Uma rugosidade de 0 (suave) resulta em uma reflexão de espelho e rugosidade de 1 (áspera) resulta em uma superfície difusa (ou fosca).

`Roughness` (Aspereza e também chamada de brilho ou dispersão da micro-superfície) é um mapa semi-autoexplicativo. Eles definem como a luz é espalhada pela superfície do seu modelo.
Isso começa com um valor de zero, onde seu modelo não dispersará a luz, tornando os reflexos e a iluminação muito mais nítidos e brilhantes em seu material.
Por outro lado, se você aumentar a rugosidade ao máximo, a luz se espalhará mais pelo material. Isso faz com que a iluminação e os reflexos se espalhem pelo modelo, mas pareçam muito mais escuros.

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/roughness_nonmetal.png"
  alt="Figura: Blueprint Material - Physically Based Materials Roughness."
  caption="Figura: Rugosidade de 0 até 1."
%}

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/Roughness_1.jpg"
  alt="Figura: Blueprint Material - Roughness."
  caption="Figura: Exemplo da rugosidade, zero representa sem rugossidade."
%}

### Textura Roughness

Para exemplificar utilizaremos o canal A (Alpha) da textura `Rock Basalt`.

{% include image.html
  src="../imagens/materiais/unreal_engine_material_chanel_a_rock_basalt.webp"
  alt="Figura: Blueprint Material - Texture Roughness."
  caption="Figura: Esses mapas são em tons de cinza, com o branco sendo a aspereza máxima e o preto sendo uma superfície lisa e brilhante."
%}

### Specular

Ao editar um material de superfície não metálico, há momentos em que você deseja ajustar sua capacidade de refletir a luz, especificamente, sua propriedade Specular. Para atualizar o Specular de um Material, insira um valor escalar entre 0 (não refletivo) e 1 (totalmente refletivo). Observe que o valor especular padrão de um material é 0,5.

Valores especulares medidos:

|Material   |Valor    |
|:-         |:-       |
|Grama      |0.5      |
|Plástico   |0.5      |
|Quartz     |0.570    |
|Gelo       |0.224    |
|Água       |0.255    |
|Leie       |0.277    |
|Pele       |0.35     |

{% include image.html
  src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/PhysicallyBased/Specular_1.jpg"
  alt="Figura: Blueprint Material - Specular."
  caption="Figura: Parâmetro Specular."
%}

### Ambient Occlusion

O mapa Ambient Occlusion (AO) pode ser usado para simular sombras suaves nas saliências de uma superfície. Não é realmente necessário criar materiais realistas no Blender (especialmente com Cycles), mas você ainda pode usá-lo para escurecer as pequenas sombras na superfície.

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/PostProcessEffects/AmbientOcclusion/ao_0.webp"
  alt="Figura: Blueprint Material - Ambient Occlusion 1 ."
  caption="Figura: Scene without Ambient Occlusion."
%}

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/PostProcessEffects/AmbientOcclusion/ao_1.webp"
  alt="Figura: Blueprint Material - Ambient Occlusion 2."
  caption="Figura:Ambient Occlusion Only."
%}

{% include image.html
  src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/PostProcessEffects/AmbientOcclusion/ao_2.webp"
  alt="Figura: Blueprint Material - Ambient Occlusion 3."
  caption="Figura:Scene with Ambient Occlusion."
%}

## Propriedades do nó principal

Nem todas as entradas serão úteis para cada tipo de material que você criar. Por exemplo, ao desenvolver uma Função de Luz - um Material que é aplicado a uma luz - você só pode usar a entrada Cor Emissiva no material e nada mais, visto que outras entradas, como Metálico ou Aspereza, não seriam aplicáveis. Por isso, é importante saber que tipo de material você está criando antes de começar a se preocupar muito com as entradas. As três propriedades de controle primárias são:

### Blend Mode

Controla como o seu material se mesclará com os pixels por trás dele.

"Os modos de mesclagem descrevem como a saída do material atual se mesclará com o que já está sendo desenhado no fundo. Em termos mais técnicos, ele permite que você controle como o mecanismo combinará este Material (cor de origem) com o que já está no buffer de quadros (cor de destino) quando renderizado."

- `BLEND_Opaque` - Cor final = cor de origem. Isso significa que o material será desenhado na parte superior do fundo. Este modo de mesclagem é compatível com iluminação.

  {% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/CameraObjectSetup.webp"
    alt="Figura: Blueprint Material - Opaque."
    caption="Figura: [Material Blen Modes - Opaque](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/)."
  %}

- `BLEND_Masked` -  Cor final = cor de origem se `OpacityMask` > `OpacityMaskClipValue`, caso contrário, o pixel é descartado. Este modo de mesclagem é compatível com iluminação.

  {% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/MaskedGridMaterial.webp"
    alt="Figura: Blueprint Material - Masked."
    caption="Figura: Material com máscara."
  %}

  {% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/MaskedSetup.webp"
    alt="Figura: Blueprint Material - Masked 2."
    caption="Figura: [Material Blen Modes - Masked](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/)."
  %}
  
- `BLEND_Translucent` - Cor final = opacidade da cor de origem + cor de destino (1 - opacidade). Este modo de mistura NÃO é compatível com  iluminação dinâmica.

  {% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/TranslucentNetwork.webp"
    alt="Figura: Blueprint Material- Translucent."
  %}
  
  {% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/TranslucentSetup.webp"
    alt="Figura: [Material Blen Modes - Translucent](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/)"
  %}
  
- `BLEND_Additive` - Cor final = cor de origem + cor de destino. Este modo de mistura NÃO é compatível com iluminação dinâmica.

  {% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/AdditiveNetwork.webp"
    alt="Figura: Blueprint Material- Additive."
  %}

  {% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/AdditiveSetup.webp"
    alt="Figura: Blueprint Material- Additive 1."
    caption="Figura: [Material Blen Modes - Additive](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/)."
  %}

- `BLEND_Modulate` - Cor final = cor de origem x cor de destino. Este modo de mistura NÃO é compatível com iluminação dinâmica ou neblina, a menos que seja um material de decalque.

  {% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/ModulateNetwork.webp"
    alt="Figura: Blueprint Material- Modulate."
    caption="Figura Blueprint Metarial - Modulate".
  %}

  {% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/ModulateScene.webp"
    alt="Figura: Blueprint Material- Modulate 1."
    caption="Figura: [Material Blen Modes - Modulate](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/)."
  %}
  
### Shading Model

Define como a luz é calculada para a superfície do material.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/Materials/MaterialProperties/LightingModels/LightingModelProperties.webp"
    alt="Figura: Blueprint Material- Shading Models."
    caption="Figura: [Shading Models](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Materials/MaterialProperties/LightingModels/)."
%}

### Material Domain

Controla como o material deve ser usado, por exemplo, se ele deve fazer parte de uma superfície, uma função leve ou um material pós-processamento.

> Esta configuração permite designar como este material será usado. Certos usos de materiais (como decalques) requerem instruções adicionais para o mecanismo de renderização considerar. Por isso, é importante designar o Material como sendo usado para esses casos

- `Surface` - Esta configuração define o Material como algo que será usado na superfície de um objeto; pense em metal, plástico, pele ou qualquer superfície física. Como tal, esta é a configuração que você usará na maioria das vezes;

- `Deferred Decal` -  Ao fazer um [Material de Decalque ou Decal Material](https://docs.unrealengine.com/4.26/en-US/Basics/Actors/DecalActor/), você usará esta configuração;

- `Light Function` - Usado ao criar um material para uso com uma função de luz;

- `Volume` - Usado ao descrever os atributos do material como um volume 3D;

- `Post-process` - Usado se o material for usado como um [Material de pós-processamento](https://docs.unrealengine.com/4.26/en-US/RenderingAndGraphics/PostProcessEffects/PostProcessMaterials/);

- `User Interface` - Usado quando este material é usado para interfaces de usuário UMG ou Slate;

- `Virtual Texture` - Usado ao fazer uma textura virtual em tempo de execução;

{% include image.html
    src="../imagens/materiais/unreal_engine_material_type_input.webp"
    alt="Figura: Blueprint Material- Type input."
    caption="Figura: Material Domain."
%}

## Aplicando o material no objeto

Para aplicar o material em um objeto podemos selecionar o objeto e atualizamos a propriedade `MATERIALS` selecionando o material criando anteriormente.

{% include image.html
    src="../imagens/materiais/unreal_engine_material_applying.webp"
    alt="Figura: Blueprint Material -  Applying Material."
    caption="Figura: Aplicando um material em um objeto."
%}
