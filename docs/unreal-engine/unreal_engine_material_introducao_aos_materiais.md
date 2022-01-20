---
title: Introdução aos Materiais
description: Neste capítulo vamos apresentar o que são materiais e a sua estrutura.
tags: [Unreal Engine,Materiais, material Function, material]
layout: page
---

Neste capítulo vamos apresentar o que são materiais e a sua estrutura.

## Índice
1. [O que é um material?](#1)
1. [Materiais de base física - PBR](#2)
1. [Estrutura do Material no Unreal Engine](#3)
    1. [Criando um material](#3.1)
    1. [Editor de materiais](#3.2)
1. [O Nó principal ou Node Result](#4)
    1. [O nó principal e suas principais entradas](#4.1)    
    1. [Propriedades do nó principal](#4.2)    
        1. [Blend Mode](#4.2.1)    
        1. [Shading Model](#4.2.2)    
        1. [Material Domain](#4.2.3)    
1. [Valores que determinam a física](#5)
1. [Texture samples](#6)
    1. [Considerações sobre texturas no Unreal Engine](#6.1)    
1. [Atividades](#7)
    1. [O meu primeiro material no Unreal Engine](#7.1)    

<a name="1"></a>
## 1. O que é um material?
Podemos definir como uma coleção de imagens e instruções computacionais que são adicionadas a superfícies poligonais. Contudo materiais não são somente cores mas representação de imperfeições da superfície a qual foram aplicadas, como por exemplo, rasuras, aspereza e transparência.

![Unreal Material Concepts](https://cdn2.unrealengine.com/Unreal+Engine%2Fonlinelearning-courses%2Fmaterials---exploring-essential-concepts%2FMaterialEssentialConcepts-1920x1080-1920x1080-2414bb5cf0b0c3bd7ac4b993e725d2acedd45334.png?resize=1&w=1400)

*Figura: Material - Unreal Engine*

No exemplo acima podemos verificar uma esfera com diferentes tipos de materiais adicionados na sua superfície, onde cada um interage de forma diferente a iluminação.

<a name="2"></a>
## 2 Materiais de base física - PBR
PBR *Physically Based Rendering* significa que o material descreve as propriedades visuais de uma superfície de uma maneira realmente plausível, de modo que os resultados realistas sejam possíveis em todas as condições de iluminação.

![material_pbr](imagens/materiais/material_pbr.jpg)

*Figura: Material PBR - https://www.pikpng.com*

<a name="3"></a>
## 3. Estrutura do Material no Unreal Engine
A primeira e mais importante coisa a saber sobre os Materiais é que eles não são construídos por meio de código, mas por meio de uma rede de nós de script visual (chamados de Expressões de Material) dentro do Editor de Material. Cada nó contém um fragmento de código HLSL, designado para executar uma tarefa específica.

<a name="3.1"></a>
### 3.1 Criando um material
Vamos criar um material para que possamos exemplificar.
1. Menu de contexto para criar um material.     
  ![unreal_engine_menu_material](imagens/materiais/unreal_engine_menu_material.jpg)     

  *Figura: Contex Menu Material*

1. Salve o material como `M_Base`

<a name="3.2"></a>
### 3.2 Editor de Materiais

![Editor Material 4.26](https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/Materials/Editor/Interface/MaterialEditor_Windows.webp)

*Figura: Editor Material, Unreal Engine 4.26*

1. Editor de materiais.
1. Barra de acesso rápido.
1. Pré-visualização do material.
1. Propriedades do nó selecionado.
1. Editor de lógica de nós.
1. Lista de funções ou nós disponíveis.

<a name="4"></a>
## 4. O Nó principal ou Node Result
O nó principal do material é responsável por exibir os resultados de todos os nós da *Expressão de Material* que são inseridos nele nas várias entradas. Cada entrada no nó Material Principal tem um efeito exclusivo sobre a aparência e o desempenho do Material.

<a name="4.1"></a>
### 4.1 O nó principal e suas principais entradas     

![unreal_engine_node_result_properties](imagens/materiais/unreal_engine_node_result_properties.jpg)     

*Figura: Nó principal ou Node Result.*

- **Base Color**    

  A Cor Base define a cor geral do Material, obtendo um valor Vector3 (RGB) em que cada canal é automaticamente fixado entre 0 e 1.
- **Normal maps**     

  A entrada Normal leva em um mapa normal, que é usado para fornecer detalhes físicos significativos para a superfície, perturbando o "normal", ou direção de frente, de cada pixel individual.
- **Emissive**      

  Dá aos artistas uma maneira muito barata e eficaz de dar a ilusão de que um Material está lançando luz quando na verdade não está. Os materiais emissivos fazem isso permitindo que o artista empurre os valores da entrada emissiva acima de 1,0, o que empurrará o material para a faixa HDR, emitindo um efeito Bloom que você pode ver ao olhar para uma fonte de luz muito brilhante.   

<a name="4.2"></a>
### 4.2 Propriedades do nó principal
Nem todas as entradas serão úteis para cada tipo de material que você criar. Por exemplo, ao desenvolver uma Função de Luz - um Material que é aplicado a uma luz - você só pode usar a entrada Cor Emissiva no material e nada mais, visto que outras entradas, como Metálico ou Aspereza, não seriam aplicáveis. Por isso, é importante saber que tipo de material você está criando antes de começar a se preocupar muito com as entradas. As três propriedades de controle primárias são:

<a name="4.2.1"></a>
#### 4.2.1 Blend Mode
Controla como o seu material se mesclará com os pixels por trás dele.
>Os modos de mesclagem descrevem como a saída do material atual se mesclará com o que já está sendo desenhado no fundo. Em termos mais técnicos, ele permite que você controle como o mecanismo combinará este Material (cor de origem) com o que já está no buffer de quadros (cor de destino) quando renderizado.

  - `BLEND_Opaque` - Cor final = cor de origem. Isso significa que o material será desenhado na parte superior do fundo. Este modo de mesclagem é compatível com iluminação.
  - `BLEND_Masked` -  Cor final = cor de origem se OpacityMask > OpacityMaskClipValue, caso contrário, o pixel é descartado. Este modo de mesclagem é compatível com iluminação.
  - `BLEND_Translucent` - Cor final = opacidade da cor de origem + cor de destino (1 - opacidade). Este modo de mistura NÃO é compatível com  iluminação dinâmica.
  - `BLEND_Additive` - Cor final = cor de origem + cor de destino. Este modo de mistura NÃO é compatível com iluminação dinâmica.
  - `BLEND_Modulate` - Cor final = cor de origem x cor de destino. Este modo de mistura NÃO é compatível com iluminação dinâmica ou neblina, a menos que seja um material de decalque.

<a name="4.2.2"></a>
#### 4.2.2 Shading Model
Define como a luz é calculada para a superfície do material.

<a name="4.2.3"></a>
#### 4.2.3 Material Domain
Controla como o material deve ser usado, por exemplo, se ele deve fazer parte de uma superfície, uma função leve ou um material pós-processamento.
> Esta configuração permite designar como este material será usado. Certos usos de materiais (como decalques) requerem instruções adicionais para o mecanismo de renderização considerar. Por isso, é importante designar o Material como sendo usado para esses casos

- `Surface` - Esta configuração define o Material como algo que será usado na superfície de um objeto; pense em metal, plástico, pele ou qualquer superfície física. Como tal, esta é a configuração que você usará na maioria das vezes.
- `Deferred Decal` -  Ao fazer um [Material de Decalque ou Decal Material](https://docs.unrealengine.com/4.26/en-US/Basics/Actors/DecalActor/), você usará esta configuração.
- `Light Function` - Usado ao criar um material para uso com uma função de luz.
- `Volume` - Usado ao descrever os atributos do material como um volume 3D.
- `Post-process` - Usado se o material for usado como um [Material de pós-processamento](https://docs.unrealengine.com/4.26/en-US/RenderingAndGraphics/PostProcessEffects/PostProcessMaterials/).
- `User Interface` - Usado quando este material é usado para interfaces de usuário UMG ou Slate.
- `Virtual Texture` - Usado ao fazer uma textura virtual em tempo de execução.

![unreal_engine_material_type_input.jpg](imagens/materiais/unreal_engine_material_type_input.jpg)     

*Figura: Material Type input*

<a name="5"></a>
## 5. Valores que determinam a física
- Constant 1 ou valor escalar- Valor único.     
  ![unreal_engine_material_node_constant_1](imagens/materiais/unreal_engine_material_node_constant_1.jpg)         

  *Figura: Constant 1 -  1 + RMB*
- Constant 2 - Vetor de dois valores.      
  ![unreal_engine_material_node_constant_2](imagens/materiais/unreal_engine_material_node_constant_2.jpg)     

  *Figura: Constant 2 - 2 + RMB*
- Constant 3 - Vetor de três valores.     
  ![unreal_engine_material_node_constant_3](imagens/materiais/unreal_engine_material_node_constant_3.jpg)     

  *Figura: Constant 3 - 3 + RMB*

<a name="5"></a>
## 6. Texture samples
Texturas são imagens que são usadas em materiais e são representadas pelo nó abaixo.  

![unreal_engine_material_node_texture_sample](imagens/materiais/unreal_engine_material_node_texture_sample.jpg)       

*Figura: Material texture - T + RMB*

<a name="6.1"></a>
### 6.1 Considerações sobre texturas no Unreal Engine
Tamanhos :
  1x1, 2x2, 4x4, 1024x1024 e 8192x8192
- As texturas serão importadas em qualquer tamanho, mas não serão mipmaps.

<a name="7"></a>
## 7. Atividades
<a name="7.1"></a>
### 7.1 - O meu primeiro material no Unreal Engine
#### Regras
1. Utilize os parâmetros Base Color, Roughness e Metallic

#### Desafio      
1. Escolha um objeto da internet para tentar simular a sua textura com seguintes parâmetros: uma cor, reflexivo e que possa ser aplicado em superfícies simples.
1. Escolha um objeto qualquer para aplicar o material, exemplo: cadeira, mesa ou parede.

## Referências
- [Physically Based Materials](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Materials/PhysicallyBased/index.html)
- [Texture Import Guide](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Textures/Importing/index.html)
- [Curso Material Essential Concepts](https://www.unrealengine.com/en-US/onlinelearning-courses/materials---exploring-essential-concepts)
- [![Intro Material Unreal Engine](http://img.youtube.com/vi/lngF4VVNER4/0.jpg)](https://www.youtube.com/watch?v=lngF4VVNER4")
