---
title: Animação
description: Animação com Unreal Engine
tags: [Unreal Engine, Animação]
layout: page
---

Neste projeto serão apresentados as estruturas necessárias para construção de
animações, como por exemplo, importando arquivos FBX, malhas e esqueletos
e suas forma de animação e programação.

## Índice
1. [Preparando o projeto](#1-preparando-o-projeto)
1. [Estruturas básicas](#2-estruturas-basicas)
1. [Baixando o personagem](#3)
1. [Importando o personagem](#4)
1. [Animação - Animation Blend Space 1D](#5)
1. [Animação - Blueprint](#6)
1. [A Classe do personagem](#7)
1. [Animations tools](#8)
1. [Full Body](#9)
1. [Control Rig](#10)
1. [Motion Warping](#11)
1. [Animações](#12)
    1. [Animação com rifles](#12.1)
    1. [Animação com espadas](#12.2)
    1. [Animação livre](#12.3)

***

<a name="1"></a>
## 1. Preparando o projeto
Em este passo iremos preparar as pastas, configuração inicial do projeto e *Character* do
jogador.

1. Criar o projeto AulaAnimação;
1. Importar a pacote `ThirdPerson`
1. Criar as pastas para organização do projeto:
    ```bash
|--Maps  
|--Projeto
      |--Core
          |--Character
              |--Mesh
      |--Animations
|--ThirdPerson
|--ThirdPersonBP
|--Mannequim
```
1.  Mover os objetos    
  - `/Mannequim/Character/Mesh/Sk_Mannequim` para `/Core/Character/Mesh`.
  - `/Mannequim/Character/Mesh/SK_Mannequin_PhysicsAsset` para `/Core/Character/Mesh`.
  - `/Mannequim/Character/Mesh/UE4_Mannequin_Skeleton` para `/Core/Character/Mesh`.
1. Criar a Classe `BP_PlayerBase` (Blueprint classe `Character`) `/Core/Character`.
1. Copiar todos elementos do `Eventh Graph` de `ThirdPersonCharacter` para `BP_Jogador`.
1. Adicionor e alinhar os componentes em `BP_PlayerBase`:
    - `Spring Arm` - (Location=0.0,0.0,8.4).
    - `Camera`.
    - `Mesh` - (Location=0.0,0.0,-89) (Rotation=-0,0,270).
1. Crie os seguintes objetos Blueprint:
    - BP_GameModeBase do tipo `Game Mode Base`.
    - BP_PlayerController do tipo `Player Controller`.
1. Crie um `Level` do tipo `Default` de nome **LevelTest** e salve na pasta `Maps`.
1. Em `World Settings` configure:
    - `GameMode Override` - BP_GameModeBase.
    - `Default Pawn Class` - BP_PlayerBase.
***

<a name="2"></a>
## 2. Estruturas básicas
### Fluxo de trabalho
![Fluxo](https://docs.google.com/drawings/d/e/2PACX-1vRAIFvkSJ46inENVbULk7u8qCGvYNUKfOLNoRJ0GvJ0SD7AuNLae3BGyyDf7Jd_uoknXBJqMxUbEocb/pub?w=954&h=356)

### Arquivo FBX e as estruturas no Unreal Engine

|     Arquivo    | Editor           | Descrição                                            | Operações                                                                          |
| :-             |:-:               |:-                                                    |:-                                                                                  |
| FBX            |Skeleton          |Esqueleto da malha importada no arquivo FBX.          |`Sockets` - Ponto de controle do esqueleto, permitindo colar outros objetos no ponto|
|                |                  |Controle de movimentação.                             |`Virtual Bones` - Adiciona um osso que não está na malha original                   |
|                |                  |`Sockets` para colar outros objetos e ossos virtuais  |`Retargeting` - Permite que as animações sejam reutilizadas entre os personagens que usam o mesmo recurso `Skeleton`|
|                |                  |                                                                             |`Physics` - Controle de física e animação dos ossos          |
|                | Mesh             | Malha que cobre os ossos para gerenciamento de `LOD` e `clothing` (roupas)  |`LOD`                                                        |
|                |                  |                                                                             |`Clothing`                                                   |

### Skeleton (Esqueleto)

|     Estrutura    | Animação           |Descrição                                   | Operações                                                                                      |
| :-               |:-:                 |:-                                          |:-                                                                                              |
|Skeleton          |Anim Graph          |Implementação das animações utilizando codificação visual|`Event Graph` - Código *Blueprint* onde deversão ser processadas todas as variáveis de inicialização para controle de fluxo das animações|
|                  |                    |                                            |`Anim Graph` Nós de representação de máquinas de estado do personagem, `State Machine`|
|                  |Sequence            | Animador que permite a edição de animações |`Blend Space` - Combina um grupo de animações com duas dimensões podendo usar variáveis          |
|                  |                    |                                            |`Blend Space 1D` - Combina grupo de animações com uma dimensão podendo usar variáveis            |
|                  |                    |                                            |`Montages` - Expõe a animação para o *Blueprint*                                                 |
|                  |                    |                                            |`Pose Assets` - Permite gravar uma nova posse do `Character`                                     |
|                  |                    |                                            |`Notify Animations` - Adiciona uma etiqueta na `Timeline` da animação                            |

### AnimGraph
1. `Slots` - Permite adicionar uma camada de funcionalidade ao fluxo;
1. `Layerd Blend` por bone - Permite diversas formas de mixar animações no fluxo;
1. `Pose Caching` - Permite reutilizar a informação de um determinado "estado".

### Final posse
1. `Sequence recorder`
1. `Animation Sharing manager`


<a name="3"></a>
## 3. Baixando o personagem
Em este passo iremos utilizar o site [Mixano.com](https://www.mixamo.com/) para baixar o personagem Mutant  
1. `Characters` : **Mutant**
1. `Animations`:
  1. `Mutant Walking` (In place = true)
  1. `Mutant Idle`
  1. `Mutant Run` (In place = true)
  1. `Mutant Jumping`

> Neste exemplo utilizaremos a opção `In Place = true` para exemplificar.  

[![Aula 02](http://img.youtube.com/vi/G7c8DMdrsGY/0.jpg)](https://youtu.be/G7c8DMdrsGY "Aula 02")

*Vídeo: Aula 02 - Baixando personagem*

<a name="4"></a>
## 4. Importando o personagem
Importando personagem baixado anteriormente.

[![Aula 03](http://img.youtube.com/vi/6ZLatHfD7P8/0.jpg)](https://youtu.be/6ZLatHfD7P8 "Aula 03")

*Vídeo: Aula 03 - Importando personagem*

<a name="5"></a>
## 5. Animação - Animation Blend Space 1D
Em este passo iremos implementar a animação em um eixo de movimentação.
1. `Horizontal Axis`
  1. `Name` : Speed
  1. `Maximum axis value` : 220
  1. `Interpolation time`

[![Aula 04](http://img.youtube.com/vi/arRhm3KRUR0/0.jpg)](https://youtu.be/arRhm3KRUR0 "Aula 04")

<a name="6"></a>
## 6. Animação - Blueprint
Em este passo iremos implementar utilizando `Animation Blueprint`
1. Copiar todos os nos do `Event Graph` de `ThirdPerson_AnimBP` para componente criado.
1. Implementar `Anim Graph`

[![Aula 05](http://img.youtube.com/vi/a2JULC4-P1o/0.jpg)](https://youtu.be/a2JULC4-P1o "Aula 05")

<a name="7"></a>
## 7. A classe do personagem
Em este passo iremos implementar a classe do personagem.
1. Copiar todos os nós do `Event Graph` de `ThirdPersonCharacter` para componente criado.
1. Adicionar os seguintes componentes:
  1. Câmera
  1. Spring Arm
  1. Use Pawn Control Rotation=true
  1. Max Walk Speed (crouch) = 110
  1. Use animation Blueprint
  1. BP_Mutant

[![Aula 06](http://img.youtube.com/vi/obLJb4RBySA/0.jpg)](https://youtu.be/obLJb4RBySA "Aula 06")

<a name="8"></a>
## 8. Implementado a Corrida
Em este passo iremos implementar a corrida do personagem  

[![Aula 06](http://img.youtube.com/vi/k6tGHVm2BNQ/0.jpg)](https://youtu.be/k6tGHVm2BNQ "Aula 06")

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
- [Skeleton Editor](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/Skeleton/index.html)   
- [FBX Import Options Reference](https://docs.unrealengine.com/en-US/Engine/Content/Importing/FBX/ImportOptions/index.html)   
- [Animations Tools](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/index.html)  
- [AnimGraph](https://docs.unrealengine.com/en-US/Engine/Animation/AnimBlueprints/AnimGraph/index.html)
