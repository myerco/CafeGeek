---
title: Inteligência Artificial
excerpt: Trabalhando com Inteligência Artificial
permalink: /pages/unreal-engine/inteligencia-artificial
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal_5
toc: true 
categories:
  - Unreal Engine
tags:
  - IA
  - IA MoveTO
  - inteligência artificial
---

[Avançado](/collection-archive/){: .btn .btn--danger}

Neste projeto serão apresentados os elementos necessários para a construção de simulação de comportamentos, como por exemplo, busca e detecção de jogadores bem como configurar o personagem controlado pela IA em diferentes estados de comportamento.

## 1. Preparando o projeto

Em este passo iremos preparar as pastas, configuração inicial do projeto e *Character* do jogador. Vamos criar o projeto AulaIA, considere a estrutura de pastas [Estrutura do Projeto](/docs/unreal-engine-estrutura-do-projeto).

Crie um novo *level* de nome **LevelTeste** e salvar na pasta **Maps**, logo em seguida configure o projeto para que o **levelTeste** seja inicializado ao abrir o projeto usando `Project Settings` > `Maps & Mods`.

A seguir vamos criar os personagens e os controles.

- **BP_PlayerController** do tipo `PlayerController`;
- **BP_GameMode** do tipo `GameMode`;
- **BP_PlayerBase** do tipo *Character* (vamos duplicar e utilizar o já existente no projeto);  
- **BP_AIController** do tipo `AIController`;
- **BP_HumanBase** do tipo `BP_PlayerBase`.

Configure `World Settings` adicionando as classes de controle de jogador **BP_PlayerController**, modo do jogo **BP_GameMode** e o personagem **BP_PlayerBase**;

### 1.1. Vídeo preparando o projeto de IA

{% include video id="XNGknrCy4JM" provider="youtube" %}

## 2. NPC básico

Em este passo iremos implementar a classe *Character* para o NPC (Personagem não jogável que será controlado pelo *Engine*).  

A classe Blueprint **BP_NPC** do tipo *Character* e logo em seguida adicionar a malha do esqueleto (*Skeletal mesh*) e as animações do manequim padrão do *Engine*.

{% include imagelocal.html
  src="unreal/ia/unreal-engine-ia-class-properties.webp"
  alt="Figura: AutoPossesAI."
  caption=" Determina quando o Peão é criado e possuído por um Controlador AI (no início do nível, quando gerado, etc)."
%}

- `Placed in World` - Apenas possuído por um AI Controller se o Pawn for colocado no mundo;
- `Placed in World  or Spawned` - O peão é automaticamente possuído por um AI Controller sempre que é criado;
- `Spawner` - Possuir apenas por um controlador AI se o peão for gerado após o carregamento do mundo.

`AI Controller Class` - É a classe base de controladores para peões controlados por IA. Os controladores são atores não físicos que podem ser anexados a um peão para controlar suas ações. AIControllers gerenciam a inteligência artificial para os peões que controlam.
{: .notice--info}

Em jogos em rede, eles existem apenas no servidor.

{% include imagelocal.html
  src="unreal/ia/unreal-engine-ia-npc-move-ia.webp"
  alt="Figura: AI MoveTO"
  caption="Movimenta o peão com AIController para um local específico."
%}

Adicione o componente **NavMeshBoundVolume** para definir fronteiras de movimentação do NPC.

{% include imagelocal.html
    src="unreal/ia/unreal-engine-ia-navmeshboundsvolume.webp"
    alt="Figura: NavMeshBoundsVolume "
    caption="Permite que os peões encontrem seu caminho através de obstáculos, rampas ou saltos de saliências. Enquanto estiver no editor e com um NavMeshBoundsVolume colocado no nível, pressionar a tecla P mostrará/ocultará a área que o NavMesh cobre."
%}

{% include imagelocal.html
    src="unreal/ia/unreal-engine-ia-npc-update-walk-speed.webp"
    alt="Figura: Função : NPC > Update Walk Speed "
    caption="Podemos implementação uma função para alterar a velocidade do NPC."
%}
  
### 2.1. Vídeo implementando o NPC

{% include video id="3i5omWI6r-U" provider="youtube" %}
