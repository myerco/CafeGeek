---
title: Animação - Preparando o projeto
description: Neste capitulo vamos preparar e organizar os objetos e elementos necessários, como por exemplo, arquivos FBX, malhas e esqueletos e suas animações. Vamos também importar personagens do site Mixano.
tags: [Unreal Engine, Animação]
layout: page
---

Neste capitulo vamos preparar e organizar os objetos e elementos necessários, como por exemplo, arquivos FBX, malhas e esqueletos e suas animações. Vamos também importar personagens do site Mixano.

## Índice
1. [Fluxo de trabalho](#1-fluxo-de-trabalho)
1. [Preparando o projeto](#1-preparando-o-projeto)
2. [Estruturas básicas](#2-estruturas-basicas)
3. [Baixando o personagem](#3-baixando)
4. [Importando o personagem](#4)
5. [Atividades](#5-atividades)

***

## 1. Fluxo de trabalho
O *Unrel Engine* fornece um fluxo de trabalho simples para construção de animações utilizando Skeletal Mesh importadas de aplicativos 3D para uso em jogos. Atualmente, apenas uma única animação para cada *Skeletal Mesh* pode ser exportada / importada em um único arquivo.

Abaixo uma visão geral técnica do uso do pipeline de animações.

|Importar               | Malha         | Animação    | Classe    |
|:--                    |:-             |:-           |:-         |
| Arquivo FBX           |Skeletal Mesh  |Anim Graph   |Character  |         
|                       |Skeletal       |Sequence     |           |         


## 2. Arquivo FBX
Embora o formato FBX seja proprietário, muitos aplicativos de modelagem e animação que não são da Autodesk podem abrir arquivos FBX. Isso permite que os criadores compartilhem modelos 3D entre si usando o formato FBX, que é eficiente porque armazena modelos como dados binários. Os arquivos .OBJ, .DXF, .3DS e .DAE (COLLADA) podem ser convertidos em arquivos FBX, usando o Autodesk FBX Converter (disponível para Windows e Mac, mas sem suporte a partir de 2013) ou Autodesk Viewer (Web).[(fileinfo)](https://fileinfo.com/extension/fbx)

![Figura: File Autodesk FBX - fileinfo.com](https://cdn.fileinfo.com/img/ss/lg/fbx_2691.png)

*Figura: File Autodesk FBX - fileinfo.com*

## 3. Skeleton (Esqueleto)
Esqueleto da malha importada no arquivo FBX contendo controle de movimentação e `Sockets` para colar outros objetos e ossos virtuais.
- `Sockets` - Ponto de controle do esqueleto, permitindo colar outros objetos no ponto;
- `Virtual Bones` - Adiciona um osso que não está na malha original;
- `Retargeting` - Permite que as animações sejam reutilizadas entre os personagens que usam o mesmo recurso `Skeleton`;
- `Physics` - Controle de física e animação dos ossos.

### 3.1 Anim Graph
Editor para implementação das animações utilizando codificação visual.
- `Event Graph` - Código *Blueprint* onde deversão ser processadas todas as variáveis de inicialização para controle de fluxo das animações;  
- `Anim Graph` - Nós de representação de máquinas de estado do personagem, `State Machine`;
  - `Slots` - Permite adicionar uma camada de funcionalidade ao fluxo;
  - `Layerd Blend` por bone - Permite diversas formas de mixar animações no fluxo;
  - `Pose Caching` - Permite reutilizar a informação de um determinado "estado".
  -  `Final posse`
    - `Sequence recorder`
    - `Animation Sharing manager`

### 3.2 Sequence    
Animador que permite a edição de animações.                          
- `Blend Space` - Combina um grupo de animações com duas dimensões podendo usar variáveis;
- `Blend Space 1D` - Combina grupo de animações com uma dimensão podendo usar variáveis;
- `Montages` - Expõe a animação para o *Blueprint*;
- `Pose Assets` - Permite gravar uma nova posse do `Character`;
- `Notify Animations` - Adiciona uma etiqueta na `Timeline` da animação.

## 4. Skeletal Mesh (Malha do esqueleto)
Malha que cobre os ossos para gerenciamento de `LOD` e `clothing` (roupas).


## 1. Preparando o projeto
Em este passo iremos preparar as pastas, configuração inicial do projeto e *Character* do
jogador.

1. Criar o projeto AulaAnimação;
1. Importar a pacote `ThirdPerson`
1. Criar as pastas para organização do projeto:
    ```bash
|--Projeto
      |--Core
          |--Character
      |--Characters
          |--Mannequim
             |--Mesh
             |--Animations          
          |--Mutant
             |--Mesh
             |--Animations
      |--Maps               
```
1.  Mover os objetos    
 - `/Mannequim/Character/Mesh/Sk_Mannequim` para `/Core/Character/Mannequim/Mesh`.
 - `/Mannequim/Character/Mesh/SK_Mannequin_PhysicsAsset` para `/Core/Character/Mannequim/Mesh`.
 - `/Mannequim/Character/Mesh/UE4_Mannequin_Skeleton` para `/Core/Character/Mannequim/Mesh`.
 - `/Mannequim/Character/Mesh/UE4_Mannequin_Skeleton` para `/Core/Character/Mannequim/Mesh`.
1. Criar a Classe `BP_PlayerBase` (Blueprint classe `Character`) `/Core/Character`.
1. Copiar todos elementos do `Eventh Graph` de `ThirdPersonCharacter` para `BP_Jogador`.
1. Adicionor e alinhar os componentes em `BP_PlayerBase`:
 - `Spring Arm` - (Location=0.0,0.0,8.4).
 - `Camera`.
 - `Mesh` - (Location=0.0,0.0,-89) (Rotation=-0,0,270).
1. Crie os seguintes objetos Blueprint:
 - BP_GameModeBase do tipo `Game Mode Base`.
 - BP_PlayerController do tipo `Player Controller`.
1. Crie um `Level` do tipo `Default` de nome **LevelTest** e salve na pasta `Projeto/Maps`.
1. Em `World Settings` configure:
 - `GameMode Override` - BP_GameModeBase.
 - `Default Pawn Class` - BP_PlayerBase.




<a name="3"></a>
## 3. Baixando o personagem
Em este passo iremos utilizar o site [Mixano.com](https://www.mixamo.com/) para baixar o personagem Mutant  
1. `Characters` : **Mutant**
1. `Animations`:
  - `Mutant Walking` (In place = true)
  - `Mutant Idle`
  - `Mutant Run` (In place = true)
  - `Mutant Jumping`

> Neste exemplo utilizaremos a opção `In Place = true` para exemplificar.  

[![Vídeo: Aula 02 - Baixando personagem](http://img.youtube.com/vi/G7c8DMdrsGY/0.jpg)](https://youtu.be/G7c8DMdrsGY "Aula 02")

*Vídeo: Aula 02 - Baixando personagem*

<a name="4"></a>
## 4. Importando o personagem
Neste passo vamos importar personagem baixado anteriormente.

### 4.1 Importando Mesh e Skeletal
1. Crie a pasta `/Core/Characteres/Mutant/Mesh`;
1. Copie o arquivo mutant.fbx para a pasta criada no passo anterior;
1. Importe o arquivo com a opção `Import All`:

  ![Figura: FBX import options](imagens/animacao/unreal_engine_fbx_import_options.jpg)

  *Figura: FBX import options*

### 4.2 Importando animações
1. Crie a pasta `/Core/Character/Mutant/animations`;
1. Copie os arquivos para pasta criada no passo anterior:
 - Mutant_Run.fbx, Mutant_Idle.fbx e Mutant_Walking.fbx

### 4.3 Vídeo Importando personagens
[![Importando personagem](http://img.youtube.com/vi/6ZLatHfD7P8/0.jpg)](https://youtu.be/6ZLatHfD7P8 "Aula 03")

*Vídeo: Aula 03 - Importando personagem*

<a name="5"></a>
## 5. Animação - Animation Blend Space 1D
Em este passo iremos implementar a animação em um eixo de movimentação utilizando o elemento e editor `Blend space 1D`.

1. Usando o menu de contexto `Animation > Blend Space 1D`

  ![Figura: Menu de contexto Animation > Blend Space 1D](imagens/animacao/unreal_engine_animation_blend_1d.jpg)

  *Figura: Menu de contexto Animation > Blend Space 1D*

1. Vamos renomear a variável de controle do eixo horizontal para *Speed* e alterar os seus valores como exemplificado abaixo:
   - `Horizontal Axis`
     - `Name` : Speed
     - `Maximum axis value` : 220
     - `Interpolation time` : 0.5

1. Para criar a movimentação no eixo horizontal vamos arrastar os elementos apresentados em `Asset Browser` para a linha do tempo.
  1. Mutant_Idle em tempo 0;  
  1. Mutant_Walking em tempo 110;  
  1. Mutant_Run em tempo 220;  
1. Para acompanhar o movimentação pressione Shift + LMB e arrastre o mouse.   

### 5.1 Vídeo Animation Blend Space 1D
[![Vídeo: Animation Blend Space 1D](http://img.youtube.com/vi/arRhm3KRUR0/0.jpg)](https://youtu.be/arRhm3KRUR0 "Aula 04")

*Vídeo: Animation Blend Space 1D*

<a name="6"></a>
## 6. Animação - Blueprint
Em este passo iremos implementar utilizando `Animation Blueprint` para criar um fluxo de animação.

1. Usando o menu de contexto `Animation > Animation Blueprint`;
   ![Figura: Menu contexto Animation > Blend Space 1D](imagens/animacao/unreal_engine_animation_animation_blueprint.jpg)  

   *Figura Menu contexto Animation > Animation Blueprint*

1. Copiar todos os nos do `Event Graph` de `ThirdPerson_AnimBP` para componente criado;
1. Arrastre o elemento BS_Mutant para AnimGraph;
   ![Figura: AnimGraph BS_Mutant](imagens/animacao/unreal_engine_animations_bs_mutant_graph.jpg)

   *Figura: AnimGraph BS_Mutant*
1. Implementar `Anim Graph`

### 6.1 Vídeo Animation Bluerint
[![Vídeo: Animation Bluerint](http://img.youtube.com/vi/a2JULC4-P1o/0.jpg)](https://youtu.be/a2JULC4-P1o "Aula 05")

*Vídeo: Animation Bluerint*

<a name="7"></a>
## 7. A classe do personagem
Em este passo iremos implementar a classe do personagem.
1. Crie o objeto BP_Mutant do tipo `Character`;
1. Adicione os seguintes componentes e hierarquias:
   - `SpringArm` - Habilite a opção `Use Pawn Control Rotation`
   - `Camera` - Componente câmera.
1. Adicione a o esqueleto e animação do personagem criados anteriormente.
   - `Skeletal Mesh`: Mutant  
   - `Animation Mode`: Use Animation Bluerint
   - `Anim Class`: ABP_Mutant_C
1. Em `CharacterMomement` atualize os valores:
   - `Max Walk Speed`: 110
   - `Max Walk Speed Crouched`: 110
1. Copiar todos os nós do `Event Graph` de `ThirdPersonCharacter` para componente criado e declare as variáveis não reconhecidas.
1. Para testar a movimentação crie um level de teste e configure `World Settings` para:
   - `Default Pawn`: BP_Mutant

### 7.1 Vídeo Classe do personagem
[![Vídeo: Animation Classe do personagem](http://img.youtube.com/vi/obLJb4RBySA/0.jpg)](https://youtu.be/obLJb4RBySA "Aula 06")

*Vídeo: Animation Classe do personagem*

<a name="8"></a>
## 8. Implementado a Corrida
Em este passo iremos implementar a corrida do personagem.

Vamos configura o evento `Left Shift` para alterar a propriedade `Max Walk Speed` do componente `CharacterMomement` com os valores 220 para velocidade máxima e 110 para caminhada.

![Figura: Bluerint running](imagens/animacao/unreal_engine_animation_blueprint_running.jpg)

*Figura: Bluerint running*

### 7.1 Vídeo Implementando a corrida
[![Vídeo: Implementando a corrida](http://img.youtube.com/vi/k6tGHVm2BNQ/0.jpg)](https://youtu.be/k6tGHVm2BNQ "Aula 06")

*Vídeo: Implementando a corrida*



<a name="9"></a>
## 9. Montando a animação de ataque
Em este passo utilizaremos o `Animation Montage` para montar as animações de ataque esquerda e direita.
1. Componente `Animation Montage`.

[![Aula 06](http://img.youtube.com/vi/Kufu78tu9EE/0.jpg)](https://youtu.be/Kufu78tu9EE "Aula 06")

<a name="10"></a>
## 10. Lógica de animação com AnimGraph
Em este passo utilizaremos a lógica de programação com AnimGraph.
[![Aula 06](http://img.youtube.com/vi/Ss22A7xrtCQ/0.jpg)](https://youtu.be/Ss22A7xrtCQ "Aula 06")

<a name="11"></a>
## 11. Lógica de animação com AnimGraph
Em este iremos continuar com com a programação AnimGraph para fazer o personagem correr e atacar ao mesmo tempo.

[![Aula 06](http://img.youtube.com/vi/1gjkcrU7pmA/0.jpg)](https://youtu.be/1gjkcrU7pmA "Aula 06")


#### Referências
https://docs.unrealengine.com/4.26/en-US/WorkingWithContent/Importing/FBX/Animations/
- [Skeleton Editor](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/Skeleton/index.html)   
- [FBX Import Options Reference](https://docs.unrealengine.com/en-US/Engine/Content/Importing/FBX/ImportOptions/index.html)   
- [Animations Tools](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/index.html)  
- [AnimGraph](https://docs.unrealengine.com/en-US/Engine/Animation/AnimBlueprints/AnimGraph/index.html)
