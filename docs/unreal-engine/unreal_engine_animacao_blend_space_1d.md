---
title: Animação - Blend Space 1D
description: Neste capitulo vamos usar o editor Blend Space 1D para construir uma animação horizontalmente para simular uma corrida por exemplo.
tags: [Unreal Engine, Animação,Blend Space 1D]
layout: page
---

Em este capítulo iremos implementar a animação em um eixo de movimentação utilizando o elemento e editor `Blend space 1D`.

## Índice
1. [Animação - Animation Blend Space 1D](#5)

## 1. Carregando o editor
Usando o menu de contexto `Animation > Blend Space 1D`

![Figura: Menu de contexto Animation > Blend Space 1D](imagens/animacao/unreal_engine_animation_blend_1d.jpg)

*Figura: Menu de contexto Animation > Blend Space 1D*

## 2. Configurando a animação
Vamos renomear a variável de controle do eixo horizontal para *Speed* e alterar os seus valores como exemplificado abaixo:
- `Horizontal Axis`
  - `Name` : Speed
  - `Maximum axis value` : 220
  - `Interpolation time` : 0.5

1. Para criar a movimentação no eixo horizontal vamos arrastar os elementos apresentados em `Asset Browser` para a linha do tempo.
  1. Mutant_Idle em tempo 0;  
  1. Mutant_Walking em tempo 110;  
  1. Mutant_Run em tempo 220;  
1. Para acompanhar o movimentação pressione Shift + LMB e arrastre o mouse.   

## 3. Vídeo Animation Blend Space 1D
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
- [Skeleton Editor](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/Skeleton/index.html)   
- [FBX Import Options Reference](https://docs.unrealengine.com/en-US/Engine/Content/Importing/FBX/ImportOptions/index.html)   
- [Animations Tools](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/index.html)  
- [AnimGraph](https://docs.unrealengine.com/en-US/Engine/Animation/AnimBlueprints/AnimGraph/index.html)
