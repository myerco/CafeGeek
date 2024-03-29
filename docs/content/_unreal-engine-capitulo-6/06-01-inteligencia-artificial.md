---
title: Inteligência Artificial
excerpt: Trabalhando com Inteligência Artificial
permalink: /unreal-engine-capitulo-6/inteligencia-artificial
date: 2024-03-01T08:48:05-04:00
show_date: true
read_time: true
last_modified_at: 2023-03-28T08:48:05-04:00
layout: single
order: 601
sidebar:
    nav: dev_unreal_6
toc: true 
categories:
  - Unreal Engine
tags:
  - IA
  - IA MoveTO
---

Neste projeto serão apresentados os elementos necessários para a construção de simulação de comportamentos, como por exemplo, busca e detecção de jogadores bem como configurar o personagem controlado pela IA em diferentes estados de comportamento.

## 1. Preparando o projeto

Em este passo iremos preparar as pastas, configuração inicial do projeto e *Character* do jogador. Vamos criar o projeto AulaIA, considere a estrutura de pastas [Estrutura do Projeto](/docs/unreal-engine-estrutura-do-projeto).

Crie um novo *level* de nome **LevelTeste** e salvar na pasta **Maps**, logo em seguida configure o projeto para que o **levelTeste** seja inicializado ao abrir o projeto usando `Project Settings` > `Maps & Mods`.

A seguir vamos criar os Blueprints dos personagens e os controles.

- **BP_PlayerController** do tipo `PlayerController`;
- **BP_GameMode** do tipo `GameMode`;
- **BP_CharacterBase** do tipo *Character* (vamos duplicar e utilizar o existente no projeto);  
- **BP_NPC_Controller** do tipo `AIController`;
- **BP_HumanBase** do tipo `BP_CharacterBase`.
- **BP_NPC** do tipo `BP_CharacterBase`.
- **BH_NPC do tipo** `Behaivor Tree`;
- **BB_NPC** do tipo `Blackboard`;  

Configure `World Settings` adicionando as classes de controle de jogador **BP_PlayerController**, modo do jogo **BP_GameMode** e o personagem **BP_HumanBase**;

### 1.1. Vídeo preparando o projeto de IA

{% include video id="XNGknrCy4JM" provider="youtube" %}

## 2. NPC básico

A classe Blueprint **BP_NPC** do tipo *Character/BP_CharacterBase* e logo em seguida adicionar a malha do esqueleto (*Skeletal mesh*) e as animações do manequim padrão do *Engine*.

{% include imagelocal.html
  src="unreal/ia/unreal-engine-ia-npc-class-properties.webp"
  alt="Figura: AutoPossessAI e AI Controller Class - "
  caption="Alterando os parâmetros da classe em Details."
%}

**`AutoPossesAI`** - Determina quando o Peão é criado e possuído por um Controlador AI (no início do nível, quando gerado, etc).

| Opções                        | Descrição                                                                               |
| :---------------------------- | :-------------------------------------------------------------------------------------- |
| `Placed in World`             | Apenas possuído por um AI Controller se o Pawn for colocado no mundo;                   |
| `Placed in World  or Spawned` | O peão é automaticamente possuído por um AI Controller sempre que é criado;             |
| `Spawner`                     | Possuir apenas por um controlador AI se o peão for gerado após o carregamento do mundo. |

**`AI Controller Class`** - É a classe base de controladores para peões controlados por IA. Os controladores são atores não físicos que podem ser anexados a um peão para controlar suas ações. AIControllers gerenciam a inteligência artificial para os peões que controlam.

**Informação**: Em jogos em rede, eles existem apenas no servidor.
{: .notice--info}

### 2.1. Vídeo implementando o NPC

{% include video id="3i5omWI6r-U" provider="youtube" %}

### 2.2. Alterando velocidade

Implementando uma função para alterar a velocidade do NPC.

{% include imagelocal.html
    src="unreal/ia/unreal-engine-ia-npc-update-walk-speed.webp"
    alt="Figura: Função : NPC > Update Walk Speed - "
    caption="Lógica para alterar a movimentação."
%}

## 3. AI MoveTo

O "AI Move To" é uma função projetada para permitir que personagens controlados por inteligência artificial (AI) naveguem pelo ambiente do jogo até um destino específico.

{% include imagelocal.html
  src="unreal/ia/unreal-engine-ia-npc-move-ia.webp"
  alt="Figura: AI MoveTo - "
  caption="Movimenta o peão com AIController para um local específico."
%}

## 4. NavMesh

Permite que os peões encontrem seu caminho através de obstáculos, rampas ou saltos de saliências. Enquanto estiver no editor e com um NavMeshBoundsVolume colocado no nível, pressionar a tecla P mostrará/ocultará a área que o NavMesh cobre.

{% include imagelocal.html
    src="unreal/ia/unreal-engine-ia-navmeshboundsvolume.webp"
    alt="Figura: NavMeshBoundsVolume - "
    caption="Adicione o componente NavMeshBoundVolume para definir fronteiras de movimentação do NPC."
%}

Você pode pressionar a tecla **P** para apresentar a `NavMesh` no ViewPort (áreas verdes indicam os locais de navegação).

## 5. Movimentação

Neste passo iremos suavizar a movimentação do NPC configurando os controles de rotação.

Na classe principal **BP_NPC** configure :

- `Use Controller Rotation Yaw` = *False* para que o personagem não utilize o controlador na rotação ;

- No Componente `CharacterMovement` configure `Rotation Rate` Z=540

Aumenta a taxa de rotação;

- Em `Orient Rotation to Movement` = *true*;  

Seu personagem se volta para a direção da viagem. Não importa para que lado a câmera esteja.

### 5.1. Vídeo Implementando a movimentação do NPC

{% include video id="Q5F0Vr4t0mg" provider="youtube" %}
