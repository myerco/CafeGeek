---
title: HUD - Interface com o jogador
tags: [Unreal Engine,HUD,user interface]
---

[CafeGeek](https://myerco.github.io/unreal-engine)  / [Desenvolvimento de jogos utilizando Unreal Engine 4](https://myerco.github.io/unreal-engine/ue4_blueprint/index.html)

# HUD - Interface com o jogador
HUD (Heads-up Display) ou UI (Use Interface) é um objeto especial da **Unreal Engine** para apresentar informações sobrepostas na tela e interagir com o jogador.

## Índice
>1. [Como interagir com o jogador?](#1)
>1. [Implementando menu](#1)
>1. [Componentes do menu](#1)
>1. [HUD do jogador](#1)
>1. [Quit game](#1)
>1. [Salvando o jogo](#1)
>1. [Organizando a estrutura do menu](#1)

<a name="1"></a>
## 1. Como interagir com o jogador?
Durante o tempo do jogo é necessário interagir com o jogador de diversas formas, informando status de jogo, personagem e até mesmo guias de missões. Geralmente são informações em formatado texto e imagens 2D que se sobrepõe a tela para informar o jogador.       

De outra forma, o comunicação de ações globais do jogo como por exemplo iniciar uma missão, salvar o jogo, sair do jogo e controlar de opções são formas de interação jogo vs player que utilizam menus através de botões, caixas rolantes e outros componentes.

<a name="11"></a>
## 1.1 Menos é Melhor!
Uma dica simples, segundo as boas práticas de IHC (Interface Homem Computador), é **"Menos é melhor"**, onde apresentar somente o necessário para o jogador e deixar a maior parte da experiência do jogador para o Gameplay.

<a name="2"></a>
## 2. Editor de de Widget

### 2.1 Entendo alinhamento e o objeto Anchors
Para gerenciar melhor o posicionamento de objetos no **Widget Designer** vamos entender a hierarquia de elmentos na tela e o objeto **Anchor** (Âncora).

<a name="2"></a>
## 1. Implementando o Menu do jogo

![](../imagens/hud/blueprint_anchor_alinhamento_separado.jpg)

![](../imagens/hud/blueprint_anchor_alinhamento.jpg)

![](../imagens/hud/blueprint_grid_panel.jpg)

![](../imagens/hud/blueprint_horizontal_box.jpg)

![](../imagens/hud/blueprint_horizontal_box_fill.jpg)

***
## Referências
- [1.1 - HUD Example](https://docs.unrealengine.com/en-US/Resources/ContentExamples/Blueprints_HUD/1_1/index.html)
- [User Interfaces & HUDs](https://docs.unrealengine.com/en-US/InteractiveExperiences/Framework/UIAndHUD/index.html)
-[Anchors](https://docs.unrealengine.com/en-US/InteractiveExperiences/UMG/UserGuide/Anchors/index.html)

***
## Tags
[Blueprint](https://myerco.github.io/unreal-engine/ue4_blueprint/blueprint.html), [Unreal Engine](https://myerco.github.io/unreal-engine/ue4_blueprint/index.html), [CafeGeek](https://myerco.github.io/unreal-engine/)
