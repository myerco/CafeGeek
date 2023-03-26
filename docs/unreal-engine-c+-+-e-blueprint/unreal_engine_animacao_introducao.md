---
title: Introdução a animação de personagens
description: Neste capitulo vamos apresentar o fluxo de trabalho e os elementos necessários para a animação de personagens.
tags: [Unreal Engine, Animação]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
sidebar:  
  - title: "MOVIMENTAÇÃO E ANIMAÇÃO DE PERSONAGENS"
    nav: "dev_unreal_movimentacao"
date: 2023-03-25 
---

***

- [1. Fluxo de trabalho para animação utilizando Unreal Engine](#1-fluxo-de-trabalho-para-animação-utilizando-unreal-engine)
- [2. Arquivo FBX](#2-arquivo-fbx)
- [3. Skeleton](#3-skeleton)
  - [3.1. Animation Editors](#31-animation-editors)
- [4. Skeletal Mesh](#4-skeletal-mesh)
  - [4.1. Skeletal Mesh Editor](#41-skeletal-mesh-editor)
- [5. Anim Graph](#5-anim-graph)
  - [5.1. Animation Blueprint Editor](#51-animation-blueprint-editor)
- [6. Sequence](#6-sequence)
  - [6.1. Animation Sequence Editor](#61-animation-sequence-editor)

***

## 1. Fluxo de trabalho para animação utilizando Unreal Engine

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation.webp"
    alt="Figura: Unreal Engine e Animação de personagens."
    caption=""
%}

A animação de personagens consiste em associar um esqueleto com pontos de controle a uma malha 3D, o objeto então pode ser adicionado a uma sequencia de animações.

{% include imagelocal.html
    src="unreal/animacao/Skeleton-over-a-mesh.webp"
    alt="Figura: Skeleton over a Mesh."
    caption="A malha envolve a estrutura do esqueleto."
%}

{% include imagelocal.html
    src="unreal/animacao/Animation-pose-keyframes-and-timeline.webp"
    alt="Figura: Animation pose keyframes and timeline."
    caption="Adicionamos uma pose a uma linha de tempo para simular movimento."
%}

{% include image.html
    src="https://www.researchgate.net/profile/Santiago-Moreno-Diaz-2/publication/337228005/figure/fig1/AS:824881293836293@1573678434329/Walk-cycle-https-rustyanimatorcom-walk-cycle-animation.jpg"
    alt="Figura: Walk Cycle."
    caption="Motion Matching in Unreal Engine."
    ref="https://www.researchgate.net/publication/337228005_Motion_Matching_in_Unreal_Engine/"
%}

O **Unreal Engine** fornece um fluxo de trabalho simples para construção de animações utilizando Skeletal Mesh importadas de aplicativos 3D para uso em jogos. Atualmente, apenas uma única animação para cada `Skeletal Mesh` pode ser exportada / importada em um único arquivo.

Abaixo uma visão geral técnica do uso do processo de construção de animações.

| Importar       | Malha            | Animação      | Classe       |
| :------------- | :--------------- | :------------ | :----------- |
| 1. Arquivo FBX | 2. Skeletal Mesh | 4. Sequence   | 7. Character |
|                | 3. Skeletal      | 5. Anim Graph |              |

***

## 2. Arquivo FBX

Embora o formato FBX seja proprietário, muitos aplicativos de modelagem e animação que não são da Autodesk podem abrir arquivos FBX. Isso permite que os criadores compartilhem modelos 3D entre si usando o formato FBX, que é eficiente porque armazena modelos como dados binários. Os arquivos .OBJ, .DXF, .3DS e .DAE (COLLADA) podem ser convertidos em arquivos FBX, usando o Autodesk FBX Converter (disponível para Windows e Mac, mas sem suporte a partir de 2013) ou Autodesk Viewer (Web).[(fileinfo)](https://fileinfo.com/extension/fbx "Fileinfo")

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_fbx_export_unreal.webp"
    alt="Figura: Arquivo FBX."
    caption="Exportando um modelo 3D do Autodesk Maya para o Unreal."
%}

***

## 3. Skeleton

Skeleton ou Esqueleto da malha importada no arquivo FBX contendo controle de movimentação e `Sockets` para colar outros objetos e ossos virtuais.

- `Sockets` - Ponto de controle do esqueleto, permitindo colar outros objetos no ponto;

- `Virtual Bones` - Adiciona um osso que não está na malha original;

- `Retargeting` - Permite que as animações sejam reutilizadas entre os personagens que usam o mesmo recurso `Skeleton`;

- `Physics` - Controle de física e animação dos ossos.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_skeleton_mannequim.webp"
    alt="Figura: Editor de esqueleto ou Skeleton."
    caption="Ao abrir um objeto do tipo esqueleto é fornecido um editor específico para a manipulação esse tipo de objeto."
%}

### 3.1. Animation Editors

{% include image.html
    src="https://docs.unrealengine.com/5.1/Images/animating-characters-and-objects/SkeletalMeshAnimation/Persona/AnimationEditorOverview.png"
    alt="Figura: Animation Editors."
    caption="O Skeletal Mesh Animation System no Unreal Engine é composto por editores de recursos de animação especializados que apresentam ferramentas de animação robustas que você pode usar ao trabalhar com Skeletal Meshes e outros recursos de animação. Com esses editores de animação, você pode criar animações de personagens, interações dentro dos níveis e outros comportamentos processuais."
    ref="https://docs.unrealengine.com/5.1/en-US/animation-editors-in-unreal-engine/"
%}

***

## 4. Skeletal Mesh

Skeletal Mesh ou Malha do esqueleto cobre os ossos para gerenciamento de `LOD` e `clothing` (roupas).

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_skeletal_mesh_editor.webp"
    alt="Figura: Skeletal Mesh."
    caption="Com este editor podemos manipular a malha do esqueleto."
%}

### 4.1. Skeletal Mesh Editor

{% include image.html
    src="https://docs.unrealengine.com/5.1/Images/animating-characters-and-objects/SkeletalMeshAnimation/Persona/MeshDetails/SkeletalMeshEditorOverview.png"
    alt="Figura: Skeletal Mesh Editor."
    caption="O modo Skeletal Mesh Editor é onde você pode encontrar as ferramentas para manipular e visualizar os ativos do Skeletal Mesh. É semelhante ao Static Mesh Editor. No Editor de malha esquelética, você pode fazer alterações na malha poligonal atribuindo materiais, adicionando elementos de vestuário, configurando LODs (nível de detalhe) e visualizando quaisquer Alvos Morph aplicados à malha."
    ref="https://docs.unrealengine.com/5.1/en-US/skeletal-mesh-editor-in-unreal-engine/"
%}

***

## 5. Anim Graph

Editor para implementação das animações utilizando codificação visual.

- `Event Graph` - Código *Blueprint* onde deverão ser processadas todas as variáveis de inicialização para controle de fluxo das animações;  

- `Anim Graph` - Nós de representação de máquinas de estado do personagem, `State Machine`;

  - `Slots` - Permite adicionar uma camada de funcionalidade ao fluxo;

  - `Layerd Blend` por bone - Permite diversas formas de mixar animações no fluxo;

  - `Pose Caching` - Permite reutilizar a informação de um determinado "estado";

  - `Final posse` - `Sequence recorder` e `Animation Sharing manager`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animgraph.webp"
    alt="Figura: Editor Anim Graph."
    caption="Adicionamos toda a lógica de animação dos objetos utilizando um apresentação um fluxo de estados ou poses."
%}

### 5.1. Animation Blueprint Editor

{% include image.html
    src="https://docs.unrealengine.com/5.1/Images/animating-characters-and-objects/SkeletalMeshAnimation/AnimBlueprints/animation-blueprint-editor/EditorOverview.png"
    alt="Figura: Animation Blueprint Editor."
    caption="O Animation Blueprint Editor compartilha funcionalidade semelhante ao Blueprint Editor, mas contém recursos, ferramentas e janelas diferentes para auxiliar na criação de scripts de animação de personagens."
    ref="https://docs.unrealengine.com/5.1/en-US/skeletal-mesh-editor-in-unreal-engine/"
%}

***

## 6. Sequence

Editor que permite a edição de animações.

- `Blend Space` - Combina um grupo de animações com duas dimensões podendo usar variáveis;

- `Blend Space 1D` - Combina grupo de animações com uma dimensão podendo usar variáveis;

- `Montages` - Expõe a animação para o *Blueprint*;

- `Pose Assets` - Permite gravar uma nova posse do *Character*;

- `Notify Animations` - Adiciona uma etiqueta na `Timeline` da animação.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_Blend_Space_1D.webp"
    alt="Figura: Blueprint - Editor Blend Space 1D."
    caption="Podemos sequenciar animações associadas a variáveis possibilitando um fluxo de animações."
%}

### 6.1. Animation Sequence Editor

{% include image.html
    src="https://docs.unrealengine.com/5.1/Images/animating-characters-and-objects/SkeletalMeshAnimation/Persona/AssetEditor/AnimationSequenceEditorOverview.png"
    alt="Figura: Animation Sequence Editor."
    caption="O Animation Sequence Editor fornece acesso a vários recursos centrados em animação disponíveis para Skeletal Meshes no Unreal Engine. No Animation Sequence Editor, você pode editar e visualizar sequências de animação, montagens, curvas e muito mais."
    ref="https://docs.unrealengine.com/5.1/en-US/animation-sequence-editor-in-unreal-engine/"
%}
