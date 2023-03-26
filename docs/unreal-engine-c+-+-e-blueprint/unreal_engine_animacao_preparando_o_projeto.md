---
title: Projeto de animação
description: Neste capitulo vamos preparar e organizar os objetos e elementos necessários, como por exemplo, arquivos FBX, malhas e esqueletos e suas animações. Vamos também importar personagens do site Mixano.
tags: [Unreal Engine, Animação]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
sidebar:  
  - title: "UNREAL ENGINE COM C++ E BLUEPRINT"
    image: /imagens/unreal/logos/unreal_engine.webp- 
    nav: "dev_unreal"
date: 2022-09-25 
---

***

- [1. Introdução](#1-introdução)
- [2. Organizando pastas de bibliotecas](#2-organizando-pastas-de-bibliotecas)
  - [2.1. Classes do personagem Base](#21-classes-do-personagem-base)
  - [2.2. Classe do Humano](#22-classe-do-humano)
  - [2.3. Classe Mutante ou  Mutant](#23-classe-mutante-ou--mutant)
    - [2.3.1. Vídeo Classe do Mutant](#231-vídeo-classe-do-mutant)
- [3. Ambiente e controle](#3-ambiente-e-controle)
- [4. Animações e esqueleto do Mutant](#4-animações-e-esqueleto-do-mutant)
  - [4.1. Baixando o personagem Mutant](#41-baixando-o-personagem-mutant)
    - [4.1.1. Vídeo Baixando personagem](#411-vídeo-baixando-personagem)
  - [4.2. Importando Mesh e Skeletal](#42-importando-mesh-e-skeletal)
  - [4.3. Importando animações](#43-importando-animações)
  - [4.4. Vídeo Importando personagem](#44-vídeo-importando-personagem)

***

## 1. Introdução

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_project.webp"
    alt="Figura: Preparando o projeto de animação."
    caption="Neste capitulo vamos preparar e organizar os objetos e elementos necessários, como por exemplo, arquivos FBX, malhas e esqueletos e suas animações. Vamos também importar personagens do site Mixano."
%}

***

## 2. Organizando pastas de bibliotecas

Em este passo iremos preparar as pastas, configuração inicial do projeto e personagens.

1. Criar o projeto AulaAnimação com `Blueprint ThirdPerson`;

1. Adicione ao projeto `Animation Starter Pack`;

1. Criar as pastas para organização do projeto:

```bash
|--Projeto
      |--Core
          |--Character
             |--BP_CharacterBase
      |--Characters
          |--Human
             |--Mesh
             |--Animations                
             |--BP_Human<Child BP_CharacterBase>
          |--Mannequim
             |--Mesh
             |--Animations          
             |--BP_Mannequim<Child BP_CharacterBase>             
          |--Mutant
             |--Mesh
             |--Animations
             |--BP_Mutant<Child BP_CharacterBase>             
      |--Maps               
|--ExampleContent
      |-- AnimStarterPack
      |-- ThirdPerson      
```

Mova todas as pastas de bibliotecas externas para a pasta ExampleContent, como por exemplo ThirdPerson.

1. Mova os objetos:

```bash
cp /Mannequim/Character/Mesh/Sk_Mannequim  /Characteres/Mannequim/Mesh
cp /Mannequim/Character/Mesh/SK_Mannequin_PhysicsAsset  /Characteres/Mannequim/Mesh
cp /Mannequim/Character/Mesh/UE4_Mannequin_Skeleton  /Characteres/Mannequim/Mesh
cp /Mannequim/Animations/  /Character/Mannequim/Animations
 ```

### 2.1. Classes do personagem Base

Podemos utilizar um personagem base para servir de Referência ou classe pai para outros personagens.

1. Criar a Classe `BP_PlayerBase` (Blueprint classe `Character`) em `/Core/Character`;

2. Copiar todos elementos do `Eventh Graph` de `ThirdPersonCharacter` para `BP_PlayerBase`;

3. Adicionar e alinhar os componentes em `BP_PlayerBase`:

   - `Spring Arm` - (Location=0.0,0.0,8.4), habilite a opção `Use Pawn Control Rotation`

   - `Camera`.

   - `Mesh` - (Location=0.0,0.0,-89) (Rotation=-0,0,270).

4. Adicione as seguintes variáveis.

   - Category = Character

       - fHealth (float) = 100;

       - sSound (Sound Cue);

       - tImage (Texture 2D);

       - cColor (Color);

   - Category = Character\Movement
  
       - fWalkSpeed (float) = 300;
  
       - fCrouchSpeed (float) = 150;

       - fRunSpeed(float) = 600;

       - bIsRunning (Boolean) = false;

       - bIsCrouch (Boolean) = false;
  
   - Category = Character\Action

       - bActionLeftAttack (Boolean) = false;

       - bActionRightAttack (Boolean) = false;

       - bIsShooting (Boolean) = false;

       - bIsHoldingWeapon (Boolean) = false;

       - bIsAim (Boolean) = false;

       - bIsReloadWeapon (Boolean) = false;

### 2.2. Classe do Humano

Esta classe irá utilizar o esqueleto e animações do Mannequim (Unreal Mannequim) para representar um humano.

1. Criar a Classe `BP_Human` (Blueprint classe `BP_CharacterBase`) em `/Characters/Human`;

   - Menu Context > `Blueprint` > `All Classes` > `BP_CharacterBase`;

1. Atualize a `Mesh` para `Sk_Mannequim`;

### 2.3. Classe Mutante ou  Mutant

Para esta classe vamos importar o esqueleto e animações.

1. Crie o objeto BP_Mutant do tipo `BP_CharacterBase`;

1. Adicione a o esqueleto e animação do personagem criados anteriormente.

   - `Skeletal Mesh`: Mutant;

   - `Animation Mode`: Use Animation Bluerint;

   - `Anim Class`: ABP_Mutant_C;

1. Em `CharacterMomement` atualize os valores:

   - `Max Walk Speed`: 110;

   - `Max Walk Speed Crouched`: 110 ou

   - (Show InHerited Variables) > fWalkSpeed = 110;

   - (Show InHerited Variables) > fRunSpeed = 220;

1. Para testar a movimentação crie um level de teste e configure `World Settings` para:

   - `Default Pawn`: BP_Mutant;

#### 2.3.1. Vídeo Classe do Mutant

{% include video.html
    link="https://youtu.be/obLJb4RBySA"
    src="https://img.youtube.com/vi/obLJb4RBySA/0.jpg"
    alt="Vídeo: Classe do personagem."
    caption="Unreal Engine Animação - 06 A classe do personagem."
%}

## 3. Ambiente e controle

Neste passo vamos implementar os controles do personagem e criar um level para testes.

1. Crie os seguintes objetos *Blueprint*:

   - BP_GameModeBase do tipo `Game Mode Base`;

   - BP_PlayerController do tipo `Player Controller`.

1. Crie um `Level` do tipo `Default` de nome **LevelTest** e salve na pasta `Projeto/Maps`.

1. Em `World Settings` configure:

   - `GameMode Override` - BP_GameModeBase;

   - `Default Pawn Class` - BP_PlayerBase.

## 4. Animações e esqueleto do Mutant

A seguir vamos preparar o personagem Mutant, baixando e logo em seguida importando para dentro do Unreal Engine.

### 4.1. Baixando o personagem Mutant

Em este passo iremos utilizar o site [Mixano.com](https://www.mixamo.com/) para baixar o personagem Mutant.  

1. Character : Mutant

2. Animations:

   - Mutant Walking (In place = true)

   - Mutant Idle

   - Mutant Run (In place = true)

   - Mutant Jumping

Observação: Neste exemplo utilizaremos a opção `In Place = true` para exemplificar uma animação sem `root bone`.  

#### 4.1.1. Vídeo Baixando personagem

{% include video.html
    link="https://youtu.be/G7c8DMdrsGY"
    src="https://img.youtube.com/vi/G7c8DMdrsGY/0.jpg"
    alt="Vídeo: Baixando personagem do Mixano."
    caption="Unreal Engine Animação - 02 Baixando o personagem."
%}

### 4.2. Importando Mesh e Skeletal

1. Crie a pasta `/Projeto/Characteres/Mutant/Mesh`;

1. Copie o arquivo `mutant.fbx` para a pasta criada no passo anterior;

1. Importe o arquivo com a opção `Import All`:

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_fbx_import_options.webp"
    alt="Figura: FBX import options."
    caption="Opções para importar o objeto do tipo FBX."
%}

### 4.3. Importando animações

1. Crie a pasta `/Projeto/Characteres/Mutant/animations`;

2. Copie os arquivos para pasta criada no passo anterior:

   - Mutant_Run.fbx;

   - Mutant_Idle.fbx;

   - Mutant_Walking.fbx.

3. Desmarque a opção `Import Mesh` para que a malha não seja importada novamente;

4. Escolha o esqueleto do personagem com `SKeleton`.

### 4.4. Vídeo Importando personagem

{% include video.html
    link="https://youtu.be/6ZLatHfD7P8"
    src="https://img.youtube.com/vi/6ZLatHfD7P8/0.jpg"
    alt="Vídeo: Importando personagem FBX baixado do Mixano."
    caption="Unreal Engine Animação - 03 importando."
%}
