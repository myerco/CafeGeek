---
title: Trabalhando com Materiais
description: Trabalhando com Materiais
tags: [Unreal Engine,Materiais, material Function,material]
---

[CafeGeek](https://myerco.github.io/CafeGeek)  / [Desenvolvimento de jogos utilizando Unreal Engine 4](https://myerco.github.io/CafeGeek/ue4_blueprint/index.html)

# Trabalhando com Materiais

## Índice
1. Editor de materiais;
1. Material Instance;
1. Materiais e Blueprint;
1. Material Function;


<a name="1"></a>
## 1. O que é um material?
Podemos definir como uma coleção de imagens e instruções computacionais que são adicionadas a superfícies poligonais.

![Unreal Material Concepts](https://cdn2.unrealengine.com/Unreal+Engine%2Fonlinelearning-courses%2Fmaterials---exploring-essential-concepts%2FMaterialEssentialConcepts-1920x1080-1920x1080-2414bb5cf0b0c3bd7ac4b993e725d2acedd45334.png?resize=1&w=1400)

No exemplo acima podemos verificar uma esfera com diferentes tipos de materiais adicionados na sua superfície, onde cada um interage de forma diferente a iluminação.
Podemos definir o material como uma pintura que é aplicada em superfícies.
Contudo materiais não são somente cores mas representação de imperfeições da superfície a qual foram aplicadas, como por exemplo, rasuras, aspereza e transparência.
Atualmente os materiais são baseados em simulações físicas do mundo.

<a name="2"></a>
## 2 Materiais de base física - PBR
PBR significa P hysically B ased R endering e significa que o material descreve as propriedades visuais de uma superfície de uma maneira realmente plausível, de modo que os resultados realistas sejam possíveis em todas as condições de iluminação. A maioria dos mecanismos de jogo e ferramentas de criação de conteúdo modernos dão suporte aos materiais do PBR porque eles são considerados a melhor aproximação de cenários do mundo real para renderização em tempo real.

<a name="2"></a>
## 2. Estrutura do Material no Unreal Engine 4
A primeira e mais importante coisa a saber sobre os Materiais é que eles não são construídos por meio de código, mas por meio de uma rede de nós de script visual (chamados de Expressões de Material) dentro do Editor de Material. Cada nó contém um fragmento de código HLSL, designado para executar uma tarefa específica. Isso significa que, conforme você constrói um Material, está criando código HLSL por meio de scripts visuais.

<a name="3"></a>
## 3. Atributos importantes
Abaixo citamos os mais importantes atributos dos materiais.
- Base Color
- Metallic   Valores entre 0 e 1
- Roughness   Valores entre 0.1 e 0.9
- Emissive     Valores entre 0 e 1
- Normals

<a name="4"></a>
## 4. Valores que determinam a física
- Constant 3
- Constant 1

<a name="5"></a>
## 5. Texture samples
## Texturas
- Tamanhos :
  1x1, 2x2, 4x4, 1024x1024 e 8192x8192
  - As texturas serão importadas em qualquer tamanho, mas não serão mipmaps.
- Formatos
- Importando
- Compressão

## 6. Material expressions
Os nós de Expressão de Material contêm pequenos fragmentos de código HLSL que realizam tarefas muito específicas dentro de um Material. Os materiais são construídos usando combinações de nós de Expressão de Material que são combinados para realizar certas tarefas.
Exemplos:
- Planner
- Multiply
- Lerp
- TextCoord

## 7. Conectando material Expressions

## 8. Material Inputs

## 9. Material propriedades





## 3. Editor de materiais;
## 4. Material Instance;
## 5. Materiais e Blueprint;
## 6. Material Function;

***

## Referências
- [Shaders: o que são e para que servem?](https://www.tecmundo.com.br/voxel/especiais/182970-shaders-o-que-sao-e-para-que-servem-.htm)
- [Physically Based Materials](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Materials/PhysicallyBased/index.html)
- [Texture Import Guide](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Textures/Importing/index.html)
- [Material Expression Reference](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Materials/ExpressionReference/index.html)
