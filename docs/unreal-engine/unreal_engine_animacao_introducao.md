---
title: Animação - Introdução
description: Neste capitulo vamos apresentar o fluxo de trabalho e os elementos necessários para a animação de personagens.
tags: [Unreal Engine, Animação]
layout: page
---

Neste capitulo vamos apresentar o fluxo de trabalho e os elementos necessários para a animação de personagens.


## Índice
1. [Fluxo de trabalho](#1-fluxo-de-trabalho)
2. [Arquivo FBX](#2-arquivo-fbx)
3. [Skeleton](#3-skeleton)
    1. [Anim Graph](#31-anim-graph)
    1. [Sequence](#32-sequence)
4. [Skeletal Mesh](#4-skeletal-mesh)
5. [Atividades](#11-atividades)

## 1. Fluxo de trabalho
O *Unrel Engine* fornece um fluxo de trabalho simples para construção de animações utilizando Skeletal Mesh importadas de aplicativos 3D para uso em jogos. Atualmente, apenas uma única animação para cada *Skeletal Mesh* pode ser exportada / importada em um único arquivo.

Abaixo uma visão geral técnica do uso do pipeline de animações.

|Importar               | Malha            | Animação       | Classe       |
|:--                    |:-                |:-              |:-            |
|1. Arquivo FBX         |2. Skeletal Mesh  |4. Sequence     |7. Character  |         
|                       |3. Skeletal       |5. Anim Graph   |              |         

## 2. Arquivo FBX
Embora o formato FBX seja proprietário, muitos aplicativos de modelagem e animação que não são da Autodesk podem abrir arquivos FBX. Isso permite que os criadores compartilhem modelos 3D entre si usando o formato FBX, que é eficiente porque armazena modelos como dados binários. Os arquivos .OBJ, .DXF, .3DS e .DAE (COLLADA) podem ser convertidos em arquivos FBX, usando o Autodesk FBX Converter (disponível para Windows e Mac, mas sem suporte a partir de 2013) ou Autodesk Viewer (Web).[(fileinfo)](https://fileinfo.com/extension/fbx)

![Figura: File Autodesk FBX - fileinfo.com](https://cdn.fileinfo.com/img/ss/lg/fbx_2691.png)

*Figura: File Autodesk FBX - fileinfo.com*

## 3. Skeleton
Skeleton ou Esqueleto da malha importada no arquivo FBX contendo controle de movimentação e `Sockets` para colar outros objetos e ossos virtuais.
- `Sockets` - Ponto de controle do esqueleto, permitindo colar outros objetos no ponto;
- `Virtual Bones` - Adiciona um osso que não está na malha original;
- `Retargeting` - Permite que as animações sejam reutilizadas entre os personagens que usam o mesmo recurso `Skeleton`;
- `Physics` - Controle de física e animação dos ossos.

![Figura: Editor Skeleton](imagens/animacao/unreal_engine_skeleton_mannequim.jpg)

*Figura: Editor Skeleton*

### 3.1 Anim Graph
Editor para implementação das animações utilizando codificação visual.
- `Event Graph` - Código *Blueprint* onde deversão ser processadas todas as variáveis de inicialização para controle de fluxo das animações;  
- `Anim Graph` - Nós de representação de máquinas de estado do personagem, `State Machine`;
  - `Slots` - Permite adicionar uma camada de funcionalidade ao fluxo;
  - `Layerd Blend` por bone - Permite diversas formas de mixar animações no fluxo;
  - `Pose Caching` - Permite reutilizar a informação de um determinado "estado";
  - `Final posse` - `Sequence recorder` e `Animation Sharing manager`.

![Figura: Editor Skeleton](imagens/animacao/unreal_engine_animgraph.jpg)

*Figura: Editor Anim Graph*  

### 3.2 Sequence    
Editor que permite a edição de animações.                          
- `Blend Space` - Combina um grupo de animações com duas dimensões podendo usar variáveis;
- `Blend Space 1D` - Combina grupo de animações com uma dimensão podendo usar variáveis;
- `Montages` - Expõe a animação para o *Blueprint*;
- `Pose Assets` - Permite gravar uma nova posse do *Character*;
- `Notify Animations` - Adiciona uma etiqueta na `Timeline` da animação.

![Figura: Editor Blend Space 1D](imagens/animacao/unreal_engine_Blend_Space_1D.jpg)

*Figura: Editor Blend Space 1D*  


## 4. Skeletal Mesh
Skeletal Mesh ou Malha do esqueleto cobre os ossos para gerenciamento de `LOD` e `clothing` (roupas).

## 5. Atividades

***

## Referências
- [Importing Animations](https://docs.unrealengine.com/4.26/en-US/WorkingWithContent/Importing/FBX/Animations/)
- [Skeleton Editor](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/Skeleton/index.html)   
- [FBX Import Options Reference](https://docs.unrealengine.com/en-US/Engine/Content/Importing/FBX/ImportOptions/index.html)   
- [Animations Tools](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/index.html)  
- [AnimGraph](https://docs.unrealengine.com/en-US/Engine/Animation/AnimBlueprints/AnimGraph/index.html)
