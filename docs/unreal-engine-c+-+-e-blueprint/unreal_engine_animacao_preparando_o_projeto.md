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

- [Organizando pastas de bibliotecas](#organizando-pastas-de-bibliotecas)
  - [Classes do personagem Base](#classes-do-personagem-base)
  - [Classe do Humano](#classe-do-humano)
  - [Classe Mutante ou  Mutant](#classe-mutante-ou--mutant)
    - [Vídeo Classe do Mutant](#vídeo-classe-do-mutant)
- [Ambiente e controle](#ambiente-e-controle)
- [Animações e esqueleto do Mutant](#animações-e-esqueleto-do-mutant)
  - [Baixando o personagem Mutant](#baixando-o-personagem-mutant)
    - [Vídeo Baixando personagem](#vídeo-baixando-personagem)
  - [Importando Mesh e Skeletal](#importando-mesh-e-skeletal)
  - [Importando animações](#importando-animações)
  - [Vídeo Importando personagem](#vídeo-importando-personagem)

***

## Organizando pastas de bibliotecas

***

Em este passo iremos preparar as pastas, configuração inicial do projeto e personagens.

1. Criar o projeto AulaAnimação com `Blueprint ThirdPerson`;

1. Adicione ao projeto `Animation Starter Pack`;

1. Criar as pastas para organização do projeto:

```bash
|--Projeto
      |--Core
          |--Character
      |--Characters
          |--Human
             |--Mesh
             |--Animations                
          |--Mannequim
             |--Mesh
             |--Animations          
          |--Mutant
             |--Mesh
             |--Animations
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

### Classes do personagem Base

Podemos utilizar um personagem base para servir de Referência ou classe pai para outros personagens.

1. Criar a Classe `BP_PlayerBase` (Blueprint classe `Character`) em `/Core/Character`;

2. Copiar todos elementos do `Eventh Graph` de `ThirdPersonCharacter` para `BP_PlayerBase`;

3. Adicionar e alinhar os componentes em `BP_PlayerBase`:

   - `Spring Arm` - (Location=0.0,0.0,8.4).

   - `Camera`.

   - `Mesh` - (Location=0.0,0.0,-89) (Rotation=-0,0,270).

### Classe do Humano

Esta classe irá utilizar o esqueleto e animações do Mannequim (Unreal Mannequim) para representar um humano.

1. Criar a Classe `BP_Human` (Blueprint classe `Character`) em `/Characters/Human`;

   - Menu Context > `Blueprint` > `Character`;

2. Adicione e alinhe os componentes em `BP_Human`:

   - `Spring Arm` - (Location=0.0,0.0,8.4);

   - `Camera` - Associe esse componente no `SpringArm`;

   - `Mesh` - (Location=0.0,0.0,-89) (Rotation=-0,0,270);

3. Atualize a `Mesh` para `Sk_Mannequim`;

### Classe Mutante ou  Mutant

Para esta classe vamos importar o esqueleto e animações.

1. Crie o objeto BP_Mutant do tipo `Character`;

2. Adicione os seguintes componentes e hierarquias:

   - `SpringArm` - Habilite a opção `Use Pawn Control Rotation`;

   - `Camera` - Componente câmera.

3. Adicione a o esqueleto e animação do personagem criados anteriormente.

   - `Skeletal Mesh`: Mutant;

   - `Animation Mode`: Use Animation Bluerint;

   - `Anim Class`: ABP_Mutant_C;

4. Em `CharacterMomement` atualize os valores:

   - `Max Walk Speed`: 110;

   - `Max Walk Speed Crouched`: 110;

5. Copiar todos os nós do `Event Graph` de `ThirdPersonCharacter` para componente criado e declare as variáveis não reconhecidas.

6. Para testar a movimentação crie um level de teste e configure `World Settings` para:

   - `Default Pawn`: BP_Mutant;

#### Vídeo Classe do Mutant

{% include video.html
    link="https://youtu.be/obLJb4RBySA"
    src="https://img.youtube.com/vi/obLJb4RBySA/0.jpg"
    alt="Vídeo: Unreal Engine - Animation Classe do personagem."
    caption="Vídeo: Unreal Engine - Animation Classe do personagem."
%}

## Ambiente e controle

Neste passo vamos implementar os controles do personagem e criar um level para testes.

1. Crie os seguintes objetos *Blueprint*:

   - BP_GameModeBase do tipo `Game Mode Base`;

   - BP_PlayerController do tipo `Player Controller`.

1. Crie um `Level` do tipo `Default` de nome **LevelTest** e salve na pasta `Projeto/Maps`.

1. Em `World Settings` configure:

   - `GameMode Override` - BP_GameModeBase;

   - `Default Pawn Class` - BP_PlayerBase.

## Animações e esqueleto do Mutant

### Baixando o personagem Mutant

Em este passo iremos utilizar o site [Mixano.com](https://www.mixamo.com/) para baixar o personagem Mutant.  

1. Character : Mutant

2. Animations:

   - Mutant Walking (In place = true)

   - Mutant Idle

   - Mutant Run (In place = true)

   - Mutant Jumping

Observação: Neste exemplo utilizaremos a opção `In Place = true` para exemplificar.  

#### Vídeo Baixando personagem

{% include video.html
    link="https://youtu.be/G7c8DMdrsGY"
    src="http://img.youtube.com/vi/G7c8DMdrsGY/0.jpg"
    alt="Vídeo: Unreal Engine - Baixando personagem do Mixano."
    caption="Vídeo: Unreal Engine - Baixando personagem do Mixano."
%}

### Importando Mesh e Skeletal

1. Crie a pasta `/Projeto/Characteres/Mutant/Mesh`;

1. Copie o arquivo `mutant.fbx` para a pasta criada no passo anterior;

1. Importe o arquivo com a opção `Import All`:

{% include imagebase.html
    src="unreal/animacao/unreal_engine_fbx_import_options.webp"
    alt="Figura: Unreal Engine - Blueprint FBX import options."
    caption="Figura: Unreal Engine - Blueprint FBX import options."
%}

### Importando animações

1. Crie a pasta `/Projeto/Characteres/Mutant/animations`;

2. Copie os arquivos para pasta criada no passo anterior:

   - Mutant_Run.fbx;

   - Mutant_Idle.fbx;

   - Mutant_Walking.fbx.

3. Desmarque a opção `Import Mesh` para que a malha não seja importada novamente;

4. Escolha o esqueleto do personagem com `SKeleton`.

### Vídeo Importando personagem

{% include video.html
    link="https://youtu.be/6ZLatHfD7P8"
    src="http://img.youtube.com/vi/6ZLatHfD7P8/0.jpg"
    alt="Vídeo: Unreal Engine - Importando personagem FBX baixado do Mixano."
    caption="Vídeo: Unreal Engine - Importando personagem FBX baixado do Mixano."
%}
