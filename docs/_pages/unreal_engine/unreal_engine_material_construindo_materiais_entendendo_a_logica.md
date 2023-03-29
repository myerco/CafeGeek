---
title: Construindo Materiais e entendo a lógica
description: Neste capítulo vamos apresentar a lógica de construção de materiais, denomina Material Expressions no Unreal Engine e suas funções.
tags: [Unreal Engine,Materiais, material expressions, material, lógica]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
sidebar:  
  - title: "UNREAL ENGINE COM C++ E BLUEPRINT"
    image: /imagens/unreal/logos/unreal_engine.webp
    nav: "dev_unreal"
date: 2022-09-24 
---

***

- [1. As propriedades e a lógica do material](#1-as-propriedades-e-a-lógica-do-material)
- [2. Utilizando Panner e TextCoord](#2-utilizando-panner-e-textcoord)
- [3. Exemplo do nó Lerp](#3-exemplo-do-nó-lerp)
- [4. World position Offset](#4-world-position-offset)
- [5. Unlit Shading Model](#5-unlit-shading-model)
- [6. Masked Blend Mode](#6-masked-blend-mode)
- [7. Translucent Blend Mode](#7-translucent-blend-mode)

***

## 1. As propriedades e a lógica do material

***

Neste exemplo vamos combinar várias texturas e utilizar funções de manipulação para obter o resultado abaixo.

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_material_combine_color.webp"
  alt="Figura: Blueprint Material - Objeto com mistura de texturas."
  caption="Figura: Exemplo de um objeto com diferentes texturas."
%}

É possível criar comentários no diagrama, abaixo lógica de construção de nós com comentários para facilitar a documentação.

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_node_combine.webp"
  alt="Figura: Blueprint Material - Lógica da combinação de texturas."
  caption="Figura: Blueprint Material - Lógica da combinação de texturas."
%}

- `Base Color 1` - Cada pixel do canal R da textura é multiplicado pela cor.

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_material_chanel_r_wood_pine.webp"
  alt="Figura: Blueprint Material - Channel R Texture Wood Pine."
  caption="Figura: Na textura o valor 1 = branco e 0 = preto."
%}

- `Base Color 2`

- `Lerp` - Recebe o resultado da multiplicação e dos canais RGB da textura para do passo anterior. No parâmetro  Alpha é informado o canal G textura.

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_material_chanel_g_ceramic_tile.webp"
  alt="Figura: Blueprint Material - Channel G Texture Ceramic Tile."
  caption="Figura: Neste passo o valores 0 (branco) e 1 (preto) são multiplicados."
%}

Podems exemplificar o que está acontecento utilizando uma expressão matemática de uma multiplicação entre vetores, pois os elementos são vetores de três dimensões (vector3).

```c++
  resul =  ( Vetor3(0.0664,0.0366,0.401) * Vetor3(0,1,0) );
  // Resultado
   (0,0.0366,0)
```

- `Multiply` multiplica o canal R da textura com o resultado do Lerp.

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_material_chanel_r_ceramic_tile.webp"
  alt="Figura: Blueprint Material - Channel R Texture Ceramic Tile."
  caption="Figura: O canal vermelho (R) da textura representa, nesta textura, os valores 0 e 1 com tons de cinza."
%}

- `Normal Map` - Mapa normal.

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_material_mask_add_append.webp"
  alt="Figura: Blueprint Material - Texture Normal."
  caption="Figura: Utilizamos texturas normais para distorcer o reflexo de luz."
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

## 2. Utilizando Panner e TextCoord

***

Neste exemplo será simulado o movimento da textura no objeto.

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_material_panner.webp"
  alt="Figura: Blueprint Material - Function Panner."
  caption="Figura: A função Panner adiciona velocidade e tempo nas coordenadas UV simulando movimento."
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

## 3. Exemplo do nó Lerp

***

Interpola Linearmente entre A e B com base em Alfa (100% de A quando Alfa = 0 e 100% de B quando Alfa = 1)

{% include imagelocal.html
  src="unreal/materiais/ue4_material_lerp_exemplo.webp"
  alt="Figura: Blueprint Material - Exemplo de Lerp."
  caption="Figura: A função learp interpola linearmente dois valores, ou seja cria vários valores entre os parâmetros inicial (A) e final (B)."
%}

## 4. World position Offset

***

Permite que os vértices de uma malha sejam manipulados no espaço do mundo pelo Material. Isso é útil para fazer objetos se moverem, mudarem de forma, girarem e uma variedade de outros efeitos. Isso é útil para coisas como animação ambiente.

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_material_world_position_offset.webp"
  alt="Figura: Blueprint Material - World Position Offset."
  caption="Figura: O parâmetro  World position Offset permite manipulação da malha."
%}

Os valores do nó Constant Vector 3, representam as coordenadas de posição do mundo (x,y,z) respectivamente.

Abaixo utilizamos variáveis para "animar" o material e simular movimento na malha.

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_material_world_position_offset_panner.webp"
  alt="Figura: Blueprint Material - World Position offset."
  caption="Figura: Utilizando a função Panner e uma textura em tons de cinza para alterar as coordenadas da malha."
%}

- `TexCoord` - U=0.15, V=0.15;

- `Panner` - Speed X =0.05, Speed Y= 0.1.

## 5. Unlit Shading Model

***

Produz apenas Emissivo para cores, tornando-o perfeito para efeitos especiais como fogo ou iluminação de objetos. Observe que, neste exemplo, o Material não está projetando luz na cena. Em vez disso, seu alto valor Emissivo resulta em um efeito de brilho, que também é captado pela Máscara de Sujeira aplicada à câmera. Parece iluminar, mas nenhuma luz ou sombra será projetada por este objeto.

{% include imagelocal.html
  src="unreal/materiais/ue4_material_properties_unlit.webp"
  alt="Figura: Blueprint Material - Properties Unlit Shading Model."
  caption="Figura: Lógica utilizando Emissive Color com variáveis."
%}

{% include imagelocal.html
  src="unreal/materiais/ue4_material_properties_blend_mode_unlit_result.webp"
  alt="Figura: Material Properties blend Mode Unlit."
  caption="Figura: Resultado do Unlit Shading Model."
%}

## 6. Masked Blend Mode

***

É usado para objetos nos quais você precisa controlar seletivamente a visibilidade de forma binária (liga / desliga). Por exemplo, considere um material que simula uma cerca de arame ou grade. Você terá algumas áreas que parecem sólidas, enquanto outras são invisíveis. Esses materiais são perfeitos para o modo de `Blend Masked` .

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_material_properties_blend_mode_masked.webp"
  alt="Figura: Blueprint Material - Properties blend mode masked."
  caption="Figura: Lógica do material usando Opacity Mask."
%}

Parâmetros do scalar:

- `Roughness` - Valor 1.

Parâmetros do nó resultado:

- `Two Sided` - Valor `True`.

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_material_properties_blend_mode_masked_result.webp "
  alt="Figura: Blueprint Material - Properties blend mode masked result."
  caption="Figura: Resultado do Blend Masked."
%}

## 7. Translucent Blend Mode

***

É usado para objetos que requerem alguma forma de transparência.

{% include imagelocal.html
  src="unreal/materiais/unreal_engine_material_properties_blend_mode_translucent.webp"
  alt="Figura: Blueprint Material - Properties blend mode Translucent."
  caption="Figura: Lógica do material utilizando Opacity e Translucent Blend Mode."
%}

Parâmetros do nó resultado:

- `Material Domain` - Surface;

- `Blend Mode` - Translucent;

- `Lighting Mode` - Surface TranslucencyVolume.

{% include imagelocal.html
  src="unreal/materiais/ue4_material_properties_blend_mode_translucent_result.webp"
  alt="Figura: Blueprint Material - Properties blend mode Translucent."
  caption="Figura: Resultado do Blend Mode Translucent."
%}
