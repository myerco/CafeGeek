---
title: Animação
description: Animação com Unreal Engine
tags: [Unreal Engine, Animação]
---

[CafeGeek](http://CafeGeek.eti.br)  / [Desenvolvimento de jogos utilizando Unreal Engine](http://cafeGeek.eti.br/unreal_engine/index.html)

# Animação

Neste projeto serão apresentados as estruturas necessárias para construção de
animações, como por exemplo, importando arquivos FBX, malhas e esqueletos
e suas forma de animação e programação.

## Índice
1. [Preparando o projeto](#1)
1. [Estruturas básicas](#2)
1. [Baixando o personagem](#3)
1. [Importando o personagem](#4)
1. [Animação - Animation Blend Space 1D](#5)
1. [Animação - Blueprint](#6)
1. [A Classe do personagem](#7)

<a name="1"></a>
## 1 - Preparando o projeto
Em este passo iremos preparar as pastas, configuração inicial do projeto e *Character* do
jogador.

1. Criar o projeto AulaAnimação;
1. Criar as pastas para organização do projeto:
```bash
|--Maps  
|--Blueprints  
      |--Characters
      |--GameControls
|--Animations
|--Mesh
    ```
1.  Mover os objetos    
  - `/Mannequim/Mesh/Sk_Mannequim` para `/Mesh`
  - `/Mannequim/Mesh/SK_Mannequin_PhysicsAsset` para `/Mesh`
  - `/Mannequim/Mesh/UE4_Mannequin_Skeleton` para `/Mesh`
1. Criar a Classe `BP_Jogador` (Blueprint classe Character)
1. Copiar todos elementos do `Eventh Graph` de `ThirdPersonCharacter` para `BP_Jogador`.
1. Adicionor e alinhar os componentes em `BP_Jogador`
  - `Spring Arm` - (Location=0.0,0.0,8.4)
  - `Camera`
  - `Mesh` - (Location=0.0,0.0,-89) (Rotation=-0,0,270)
***

<a name="2"></a>
## 2. Estruturas básicas
### Fluxo de trabalho
![Fluxo](https://docs.google.com/drawings/d/e/2PACX-1vRAIFvkSJ46inENVbULk7u8qCGvYNUKfOLNoRJ0GvJ0SD7AuNLae3BGyyDf7Jd_uoknXBJqMxUbEocb/pub?w=954&h=356)

### Arquivo FBX e as estruturas no Unreal Engine

|     Arquivo    | Editor           | Descrição  | Operações|
| :-             |:-:               |:-          |:-        |
| FBX            | Skeleton         | **Esqueleto** da malha importada no arquivo FBX. Controle de movimentação, *sockets* para colar outros objetos e ossos virtuais|<ul><li>`Sockets` - Ponto de controle do esqueleto, permitindo colar outros objetos no ponto</li><li>Virtual Bones - Adiciona um osso que não está na malha original</li><li>Retargeting - Permite que as animações sejam reutilizadas entre os personagens que usam o mesmo recurso *Skeleton* </li><li>`Physics` - Controle de física e animação dos ossos</li></ul>|
|                | Mesh             |   **Malha** que cobre os ossos para gerenciamento de **LOD** e *clothing* (roupas) |<ul><li>**LOD**</li><li>Clothing</li></ul>|

### Skeleton (Esqueleto)

|     Estrutura    | Animação           |Descrição   | Operações|
| :-               |:-:                 |:-          |:-        |
|Skeleton          |Anim Graph          |Implementação das animações utilizando códificação visual|<ul><li>**Event Graph** - Código *blueprint* onde deversão ser processadas todas as variáveis de inicialização para controle de fluxo das animações </li><li>**Anim Graph** Nós de representação de máquinas de estado do personagem, *State Machine*</li></ul>|
||Sequence         | Animador que permite a edição de animações |<ul><li>`Blend Space` - Combina um grupo de animações com duas dimensões podendo usar variáveis</li><li>`Blend Space 1D` - Combina grupo de animações com uma dimensão podendo usar variáveis</li><li>`Montages` - Expõe a animação para o *Blueprint*</li><li>`Pose Assets` - Permite gravar uma nova posse do *Character*</li><li>`Notify Animations` - Adiciona uma etiqueta na *timeline* da animação</li></ul>|

### AnimGraph
1. `Slots` - Permite adicionar uma camada de funcionalidade ao fluxo;
1. `Layerd Blend` por bone - Permite diversas formas de mixar animações no fluxo;
1. `Pose Caching` - Permite reutilizar a informação de um determinado "estado".

### Final posse
1. Sequence recorder
1. Animation Sharing manager
***

<a name="3"></a>
## 3. Baixando o personagem
Em este passo iremos utilizar o site Mixano.com para baixar o personagem Mutant  
1. `Characters` : **Mutant**
1. `Animations`
  1. `Walk` (In place = true)
  1. `Breathing Idle`
  1. `Run` (In place = true)
  1. `Jumping`

[![Aula 02](http://img.youtube.com/vi/G7c8DMdrsGY/0.jpg)](https://youtu.be/G7c8DMdrsGY "Aula 02")

<a name="4"></a>
## 4. Importando o personagem
Importando personagem baixado anteriormente.

[![Aula 03](http://img.youtube.com/vi/6ZLatHfD7P8/0.jpg)](https://youtu.be/6ZLatHfD7P8 "Aula 03")

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
