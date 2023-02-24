---
title: Preparando o projeto
description: Neste capitulo vamos preparar e organizar os objetos e elementos necessários, como por exemplo, arquivos FBX, malhas e esqueletos e suas animações. Vamos também importar personagens do site Mixano.
tags: [Unreal Engine, Animação]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
date: 2022-09-25 
---

{% include imagebase.html
    src="unreal/animacao/unreal_engine_animation_project.webp"
    alt="Figura: Unreal Engine - Preparando o projeto de animação."
    caption="Figura: Unreal Engine - Preparando o projeto de animação."
%}

Neste capitulo vamos preparar e organizar os objetos e elementos necessários, como por exemplo, arquivos FBX, malhas e esqueletos e suas animações. Vamos também importar personagens do site Mixano.

***

- [1. Organizando pastas de bibliotecas](#1-organizando-pastas-de-bibliotecas)
  - [1.1. Classes do personagem Base](#11-classes-do-personagem-base)
  - [1.2. Classe do Humano](#12-classe-do-humano)
  - [1.3. Classe Mutante ou  Mutant](#13-classe-mutante-ou--mutant)
    - [1.3.1. Vídeo Classe do Mutant](#131-vídeo-classe-do-mutant)
- [2. Ambiente e controle](#2-ambiente-e-controle)
- [3. Animações e esqueleto do Mutant](#3-animações-e-esqueleto-do-mutant)
  - [3.1. Baixando o personagem Mutant](#31-baixando-o-personagem-mutant)
    - [3.1.1. Vídeo Baixando personagem](#311-vídeo-baixando-personagem)
  - [3.2. Importando Mesh e Skeletal](#32-importando-mesh-e-skeletal)
  - [3.3. Importando animações](#33-importando-animações)
  - [3.4. Vídeo Importando personagem](#34-vídeo-importando-personagem)

***

## 1. Organizando pastas de bibliotecas

***

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

### 1.1. Classes do personagem Base

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

### 1.2. Classe do Humano

Esta classe irá utilizar o esqueleto e animações do Mannequim (Unreal Mannequim) para representar um humano.

1. Criar a Classe `BP_Human` (Blueprint classe `BP_CharacterBase`) em `/Characters/Human`;

   - Menu Context > `Blueprint` > `All Classes` > `BP_CharacterBase`;

1. Atualize a `Mesh` para `Sk_Mannequim`;

### 1.3. Classe Mutante ou  Mutant

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

#### 1.3.1. Vídeo Classe do Mutant

{% include video.html
    link="https://youtu.be/obLJb4RBySA"
    src="https://img.youtube.com/vi/obLJb4RBySA/0.jpg"
    alt="Vídeo: Unreal Engine - Animation Classe do personagem."
    caption="Vídeo: Unreal Engine - Animation Classe do personagem."
%}

## 2. Ambiente e controle

Neste passo vamos implementar os controles do personagem e criar um level para testes.

1. Crie os seguintes objetos *Blueprint*:

   - BP_GameModeBase do tipo `Game Mode Base`;

   - BP_PlayerController do tipo `Player Controller`.

1. Crie um `Level` do tipo `Default` de nome **LevelTest** e salve na pasta `Projeto/Maps`.

1. Em `World Settings` configure:

   - `GameMode Override` - BP_GameModeBase;

   - `Default Pawn Class` - BP_PlayerBase.

## 3. Animações e esqueleto do Mutant

### 3.1. Baixando o personagem Mutant

Em este passo iremos utilizar o site [Mixano.com](https://www.mixamo.com/) para baixar o personagem Mutant.  

1. Character : Mutant

2. Animations:

   - Mutant Walking (In place = true)

   - Mutant Idle

   - Mutant Run (In place = true)

   - Mutant Jumping

Observação: Neste exemplo utilizaremos a opção `In Place = true` para exemplificar.  

#### 3.1.1. Vídeo Baixando personagem

{% include video.html
    link="https://youtu.be/G7c8DMdrsGY"
    src="http://img.youtube.com/vi/G7c8DMdrsGY/0.jpg"
    alt="Vídeo: Unreal Engine - Baixando personagem do Mixano."
    caption="Vídeo: Unreal Engine - Baixando personagem do Mixano."
%}

### 3.2. Importando Mesh e Skeletal

1. Crie a pasta `/Projeto/Characteres/Mutant/Mesh`;

1. Copie o arquivo `mutant.fbx` para a pasta criada no passo anterior;

1. Importe o arquivo com a opção `Import All`:

{% include imagebase.html
    src="unreal/animacao/unreal_engine_fbx_import_options.webp"
    alt="Figura: Unreal Engine - Blueprint FBX import options."
    caption="Figura: Unreal Engine - Blueprint FBX import options."
%}

### 3.3. Importando animações

1. Crie a pasta `/Projeto/Characteres/Mutant/animations`;

2. Copie os arquivos para pasta criada no passo anterior:

   - Mutant_Run.fbx;

   - Mutant_Idle.fbx;

   - Mutant_Walking.fbx.

3. Desmarque a opção `Import Mesh` para que a malha não seja importada novamente;

4. Escolha o esqueleto do personagem com `SKeleton`.

### 3.4. Vídeo Importando personagem

{% include video.html
    link="https://youtu.be/6ZLatHfD7P8"
    src="http://img.youtube.com/vi/6ZLatHfD7P8/0.jpg"
    alt="Vídeo: Unreal Engine - Importando personagem FBX baixado do Mixano."
    caption="Vídeo: Unreal Engine - Importando personagem FBX baixado do Mixano."
%}
