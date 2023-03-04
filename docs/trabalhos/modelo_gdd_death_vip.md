---
title: Death VIP
description: Modelo de GDD do jogo Death VIP
tags: [Unreal Engine, Death VIP, roteiro,GDD]
categories: Trabalhos
author: 
- Cafegeek
layout: post
---


“Rescue or die trying”

- [1. Introdução](#1-introdução)
  - [1.1. Plataforma](#11-plataforma)
  - [1.2. Faixa Etária](#12-faixa-etária)
  - [1.3. Classificação](#13-classificação)
  - [1.4. Gênero](#14-gênero)
  - [1.5. Publico Alvo](#15-publico-alvo)
  - [1.6. Características gerais](#16-características-gerais)
  - [1.7. Características multiplayer](#17-características-multiplayer)
  - [1.8. Resumo da história](#18-resumo-da-história)
- [2. Marketing](#2-marketing)
  - [2.1. Diferenciais de vendas](#21-diferenciais-de-vendas)
  - [2.2. Produtos concorrentes](#22-produtos-concorrentes)
- [3. Objetivos](#3-objetivos)
- [4. Personagens](#4-personagens)
  - [4.1. Movimentação Controle](#41-movimentação-controle)
  - [4.2. Inimigos](#42-inimigos)
  - [4.3. Armas](#43-armas)
- [5. O Mundo do jogo](#5-o-mundo-do-jogo)
- [6. Estruturas](#6-estruturas)
  - [6.1. Interface (HUD)](#61-interface-hud)
  - [6.2. Câmera](#62-câmera)
  - [6.3. Músicas e efeitos de som](#63-músicas-e-efeitos-de-som)
- [7. GamePlay](#7-gameplay)
  - [7.1. Objetivos e Ação](#71-objetivos-e-ação)
  - [7.2. Mapas](#72-mapas)
  - [7.3. Experiência e Level](#73-experiência-e-level)
  - [7.4. Características especiais do Capitão](#74-características-especiais-do-capitão)
  - [7.5. Modelos](#75-modelos)
  - [7.6. Multiplayer](#76-multiplayer)
- [8. Estrutura do modelo](#8-estrutura-do-modelo)
- [9. Projeto](#9-projeto)
  - [9.1. Equipe](#91-equipe)
  - [9.2. Tarefas](#92-tarefas)

****

## 1. Introdução

### 1.1. Plataforma

Distribuição : PC.

Desenvolvimento: Unreal Engine.

### 1.2. Faixa Etária

14

### 1.3. Classificação

SEM RESTRIÇÃO

### 1.4. Gênero

FPS (First-person shooter) Cooperativo - Os jogadores devem cumprir os objetivos e levar o VIP (Classe de Jogador) até a área de resgate.

### 1.5. Publico Alvo

- Jogadores de tiro e trabalho cooperativo;

- Jogadores que visam maiores desafios pois para vencer tentem levar o VIP para a área de resgate;

- O VIP é membro da equipe sem armas mas com habilidades especiais permitindo outro tipo de perfil de jogador com habilidades de fuga e rapidez na tomada de decisões.

### 1.6. Características gerais

- Mapas grandes (KM);

- 3D gráficos;

- 32-Bit color;

- 3ª Pessoa;

### 1.7. Características multiplayer

Salas de até 16 jogadores

### 1.8. Resumo da história

Quando o comandante das milícias descobriu a tentativa de resgate de um alvo considerado por ele de extrema importância, mandou todos os seus soldados fazer de tudo para MATAR O VIP para servir de exemplo.

Equipe de resgate (EAS - Esquadrão Aeroterrestre de Salvamento)  de 3 jogadores tenta resgatar um VIP (Very Important Person) em uma região dominada por milícias fortemente armadas em um país da América do Sul. A equipe conta com arsenal leve de combate e resgate, como por exemplo metralhadoras M4, espingardas e pistolas.
Quanto ao VIP, não está armado e nem consegue segurar uma arma mas pode curar os membros da sua equipe, também conta com a capacidade de visualizar o mapa e procurar itens que podem  auxiliar no resgate.

Durante o trajeto até o resgate deverão ser cumpridos três (3) objetivos, obrigando toda a equipe  a se envolver em combates.

A equipe EAS com auxílio do VIP pode localizar outras equipes de resgate e seus VIPS´s para tentar sobreviver juntos.

Os itens espalhados no mapa podem ser armas pesadas e rifles de precisão bem como itens que alteram o modo de jogo, como por exemplo  o “TREINO VIP” que transforma o VIP em um membro da equipe EAS por alguns minutos.

## 2. Marketing

### 2.1. Diferenciais de vendas

- Explore o mapa para encontrar itens que auxiliam na sobrevivência e resgate do VIP;

- Esteja preparado para a missão mudar durante o jogo, alterando totalmente a sua tática de resgate;

- Tente sobreviver ouvindo ROCK INDIE das melhores bandas de garagem;

- Encontre outras equipes e seus VIP´s para tentar sobreviver em um grande modo cooperativo de 16 jogadores, modo *Kill House*;

- Múltiplos modo de gameplay, incluindo cooperativo de 4 jogadores, cooperativo de 16 jogadores e multiplayer onde as equipes tentam eliminar o VIP do adversário;

### 2.2. Produtos concorrentes

- Left for dead;

- COD Zumbi.

## 3. Objetivos

- Não deixar o VIP morrer, caso morra o jogo acaba;

- Alcançar o ponto de resgate com toda a sua equipe;

- Explorar o mapa para coletar itens auxiliares;

- Cumprir os 3 objetivos durante o resgate;

## 4. Personagens

| Class       |   Aggressive   |      Defensive      |   Support   |            VIP             |
| :---------- | :------------: | :-----------------: | :---------: | :------------------------: |
| Type        |   Lieutenant   |     Destructive     |   Sniper    |            VIP             |
| **Details** |                |                     |             |                            |
| Health      |       80       |         100         |     80      |            100             |
| Speed       |      100       |         80          |     90      |             90             |
| **Skill**   |                |                     |             |                            |
| Weapons     |                |                     |             |                            |
|             |      M4A1      |         M60         | Rifle Scout |            Maps            |
|             |    Shotgun     |        M4A1         | Pistol 1914 |                            |
| Extras      |                |                     |             |                            |
|             |     knife      |        knife        |    knife    |        Medical Kit         |
|             |    grenade     |       grenade       |   grenade   | resurrect and cure friends |
|             | interact itens | provides ammunition | Prepare C4  |         find items         |

>Observação
>
>Interação com itens :
>
> - Abrir portas codificadas;
> - Chamar o resgate quando chegar no local marcado;

### 4.1. Movimentação Controle

|           Controle            | Teclado |           Mouse            | Ação                       |
| :---------------------------: | :-----: | :------------------------: | :------------------------- |
|                               |         |                            |                            |
| Direcional Analógico Esquerda | A,S,D,W |                            | Character movement         |
| Direcional Analógico Direita  |         | Movimentação + Click Right | Camera movement (180º)     |
| Analógico Direita pressionado |    F    |    Pressionando Rolagem    | knife                      |
|               Y               |   1,2   |          Rolagem           | Change Weapon              |
|               X               |    R    |                            | Reload                     |
|               B               |    E    |                            | **Defensive**              |
|                               |         |                            | provides ammunition        |
|                               |         |                            | **Sniper**                 |
|                               |         |                            | Prepare C4                 |
|                               |         |                            | **Aggressive**             |
|                               |         |                            | interact itens             |
|                               |         |                            | **VIP**                    |
|                               |         |                            | Medical Kit                |
|               A               |    X    |                            | **VIP**                    |
|                               |         |                            | Find items                 |
|                               |         |                            | resurrect and cure friends |
|            L2 + X             | G+Mouse |        Click Right         | grenade                    |
|              L1               |         |  Movimentação +Click Left  | Aim                        |

### 4.2. Inimigos

| Class       |  Aggressive   |      Shooter      |    Boss     |     Boss      |     Boss     |   Boss   |     Boss     |  Boss   |
| :---------- | :-----------: | :---------------: | :---------: | :-----------: | :----------: | :------: | :----------: | :-----: |
| Type        |    Soldier    |    demolisher     |   Sniper    |     Hell      |  Mercenary   | Armored  |     Bomb     | Captain |
| **Details** |               |                   |             |               |              |          |              |         |
| Health      |      40       |        100        |     200     |      100      |     100      |   250    |      40      |   400   |
| Speed       |      100      |        80         |     90      |      90       |     150      |    90    |      50      |   50    |
| **Skill**   |               |                   |             |               |              |          |              |         |
| Weapons     |               |                   |             |               |              |          |              |         |
|             |     AL 47     |        M60        | Rifle Scout | throw flames  |    AK 47     |  AK 47+  |     RPG      |  AK 74  |
|             |    Shotgun    |       M4A1        | Pistol 1914 |               |              |          |              |         |
| Objective   |               |                   |             |               |              |          |              |         |
|             | Não tem alvo  |   Não tem alvo    |  Alvo VIP   | Não tem alvo  | Não tem alvo | Alvo VIP | Não tem alvo |   VIP   |
|             | Ataca jogador | Ataca VIP e prox. |   Foco 2s   | Ataca jogador |  Ataca VIP   | Foco 2s  |   Foco 2s    | Foco 2s |

### 4.3. Armas

| Weapon      | Bullet for loader | Max Loader |
| :---------- | :---------------: | :--------: |
| M4A1        |        15         |     40     |
| M60         |        15         |     40     |
| AK 47       |        15         |     30     |
| Granada     |                   |            |
| Rifle scout |        10         |     5      |
| Barret .40  |         7         |     2      |

## 5. O Mundo do jogo

- Florestas tropicais;

- Favelas da América latina;

- Vilarejos;

## 6. Estruturas

### 6.1. Interface (HUD)

- Medidor de Saúde do personagem;

- Lista de membros da equipe com medidor de saúde;

- Tipo da arma com informação de munição (Atual/Total);

- Quantidade de Granadas;

- Mini Mapa com localização de objetivos e itens (somente o VIP).

### 6.2. Câmera

- Movimentação em 180º;

- Na altura do ombro do jogador e distante o suficiente para visualizar os pés do jogador;

- Ao mirar com arma leve a câmera dá zoom do alvo (2x) visualizando o ombro do jogador

- Ao mirar com rifle de precisão o zoom é de 4x e somente é apresentado a lente da arma;

### 6.3. Músicas e efeitos de som

- Rock indie (procurar lista sem direitos autorais);

- Link das músicas;

## 7. GamePlay

### 7.1. Objetivos e Ação

| Objetivo                                                                                                        | Ação                                                                                                                                                                                                                      |
| :-------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| A casa da morte- Casa protegida por todas classes de inimigos - Casa onde eram realizada torturas               | Abrir uma porta (2s) - Recolher a peça do rádio 1 (2s) - Procurar item especial, provas do massacre - Recolher o item especial (2s)                                                                                       |
| A central de planejamento - Casa protegida por todas as classes- Casa onde estão os mapas e as provas de crimes | Entrar no prédio, arrombar Uma porta (2s) - Entrar na sala de planejamento, Arrombar 2 portas (2s cada uma) - Recolher a peça de rádio 2 (2s) - Procurar itens especiais, relatórios - Recolher o item especial (2s)      |
| A central de comunicação -Central de comunicações das milícias                                                  | Entrar no prédio, arrombar uma porta (2s) - Entrar na sala de planejamento, Arrombar 4 portas (2s cada uma) - Recolher a peça de rádio 3 (2s)- Subir no terraço do prédio para melhorar a comunicação Chamar Resgate (2s) |
| O ponto de resgate - Campo aberto com poucas áreas de cobertura                                                 | Sinalizar o local de resgate (2s) - Aguardar o resgate (60s)                                                                                                                                                              |
| A prisão                                                                                                        | O jogador preso fica sem armas- Quando a porta da prisão abrir o jogador recebe as armas e pode sair - A prisão é protegida por 2 snipers, 4 infernos, 4 bomba e 3 mercenários                                            |

### 7.2. Mapas

- A Selva
  - Selva tropical
    - Áreas para se abrigar
    - MAPA GRANDE
- A Vila
  - Vilarejo pequeno
    - Combate nas ruas do vilarejo
    - MAPA GRANDE - área fora do vilarejo
- A favela
  - Favela
  - Combate urbano
    - MAPA GRANDE

### 7.3. Experiência e Level

Não definido.

### 7.4. Características especiais do Capitão

- O capitão aparece quando os jogadores passam por algumas áreas ou quando um objetivo é alcançado. Ele sempre aparece com 100% de vida;
- Se o capitão ficar perto de um jogador (5 metros) o jogador é sequestrado e enviado para “A prisão”. Essa ação é repetida até o capitão prender todos os membros do time e/ou matar o VIP ;
- O capitão desaparece quando o nível de vida chega em 20%, joga fumaça e some.;
- Quando o resgate é chamado o capitão não desaparece mais;
- Quanto aparece ele grita provocações e xingamentos;
- Quando captura um membro da equipe ri de forma sinistra;

### 7.5. Modelos

- EAS - Equipe principal com uniformes do exército brasileiro

- SEAL - Uniformes de SEAL USA

- Milicianos - Sem uniformes, roupas da região;

- VIP - Roupa casual, jeans e camiseta;

### 7.6. Multiplayer

- 4 Jogadores;

- Cooperativo;

- Competitivo;

- Chat aberto;

- Estimativa de jogadores online ( > 100 ).

## 8. Estrutura do modelo

- `Content` \ `ProjetoAula`
- `Content` \ `ProjetoAula` \ `Art`
- `Content` \ `ProjetoAula` \ `Art` \ `Industrial`
- `Content` \ `ProjetoAula` \ `Art` \ `Industrial` \ `Ambient`
- `Content` \ `ProjetoAula` \ `Art` \ `Industrial` \ `Machinery`
- `Content` \ `ProjetoAula` \ `Art` \ `Industrial` \ `Pipes`
- `Content` \ `ProjetoAula` \ `Art` \ `Nature`
- `Content` \ `ProjetoAula` \ `Art` \ `Nature` \ `Ambient`
- `Content` \ `ProjetoAula` \ `Art` \ `Nature` \ `Foliage
- `Content` \ `ProjetoAula` \ `Art` \ `Nature` \ `Rocks`
- `Content` \ `ProjetoAula` \ `Art` \ `Nature` \ `Trees`
- `Content` \ `ProjetoAula` \ `Art` \ `Office`
- `Content` \ `ProjetoAula` \ `Characters`
- `Content` \ `ProjetoAula` \ `Characters` \ `Lieutenant`

```cpp
class Lieutenant : public BP_PlayerBase {};
```

- `Content` \ `ProjetoAula` \ `Characters` \ `VIP`
- `Content` \ `ProjetoAula` \ `Characters` \ `Sniper`
- `Content` \ `ProjetoAula` \ `Characters` \ `Destructive`
- `Content` \ `ProjetoAula` \ `Characters` \ `Common`
- `Content` \ `ProjetoAula` \ `Characters` \ `Common` \ `Animations`

```cpp
class BP_PlayerAnimations : public AAnimation {};
class BP_BotAnimation : public AAnimation {};
```

- `Content` \ `ProjetoAula` \ `Characters` \ `Common` \ `Audio`  

```cpp
    class UVoice : public USoundCLass {};
    class UWalkstep : public USoundCLass {};
```

- `Content` \ `ProjetoAula` \ `Bots`  
- `Content` \ `ProjetoAula` \ `Bots` \ `bSoldier` \

```cpp
    class  BP_bSoldier : public BP_BotBase {};
    class  BHT_bSoldier : public ABehaviortreee public {};
```

- `Content` \ `ProjetoAula` \ `Bots` \ `bDestructive` \

```cpp
class BP_BotBase BP_bDestructive {};
class ABehaviortreee BHT_bDestructive {};
```  

- `Content` \ `ProjetoAula` \ `Bots` \ `bHell` \
- `Content` \ `ProjetoAula` \ `Bots` \ `bSniper` \
- `Content` \ `ProjetoAula` \ `Core` \ `Characters`

```cpp
  struct FInventory {
    Vector class BP_Item;
  };

  struct FPlayer {
  float Health; float MaxHealth;
  float Armor; float MaxArmor;
  float Speed; float MaxSpeed;
  FName NameCharacter;
  FName NamePlayer;
  sProfile ListProfile;  
  UImage ImagePlayer;
  FText ClassPlayer <Aggressive,Defensive,Support>;
  FText TypePlayer <Lieutenant,Sniper, Vip,destructive>;
};

  struct sBot {
  float Health; float MaxHealth;
  float Armor;  float MaxArmor;
  Name NameBot;
  UImage ImageBot;
  FText ClassBot <Aggressive,Defensive,Support>;
  FText TypePlayer <Lieutenant,Sniper, Vip,destructive>;
  Char TypeEnemy  <Boss,Normal>;
};

  class ACharacterBase : public ACharacter
{
    void Died();
    void Run();
    void Crouching();
    void Walk();
    void Talk();
};

  class BP_PlayerBase : public ACharacterBase {
  FPlayer PlayerInfo;
  void Catch();
  void ChangeWeapon();
  void Amni();
  void Shoot();
};

  class BP_BotBase : public ACharacterBase {
  sBot BotInfo;
  void Amni();
  void Shoot();
};

  class BP_PlayerControllerBase : public APlayerController  {};
  class BP_BotControllerBase : public APPlayerControler  {};
```

- `Content` \ `ProjetoAula` \ `Core` \ `Engine`

```cpp
class BP_GameInstanceBase : public UGameInstance  {
  void openMenuMain();
  void openMenuPause();
};
class UMenuMainInterface : public UInterface {};
```

- `Content` \ `ProjetoAula` \ `Core` \ `GameModes`

```cpp
    class BP_GameModeBase : public UGameMode {};
```

- `Content` \ `ProjetoAula` \ `Interactables`

```cpp
    struct sItem {
      Name    NameItem;
      UImage ImageItem;
      FText  Type <Weapon, Life, Damage, collectible>;
      integer Magazine;                 
      integer MaxMagazine;              
      float Damage;   float MaxDamage;
      float Life; float MaxLife;
      USound  SoundItem;
    };

  class Item : public UObject{
    sItem InfoItem;
  };
  class BP_Item : public Item {
  void PlaySound();
};
```  

- `Content` \ `ProjetoAula` \ `Interactables` \ `Pickups`
- `Content` \ `ProjetoAula` \ `Interactables` \ `Weapons`

```cpp
    class WeaponBase : public Item  {
      sItem itemInfo;
    };

    class BP_M4A1 : public Item {};
    class BP_M4A1 : public Item{};
```

- `Content` \ `ProjetoAula` \ `Maps`
- `Content` \ `ProjetoAula` \ `Maps` \ `Level1`
- `Content` \ `ProjetoAula` \ `Maps` \ `Level2`
- `Content` \ `ProjetoAula` \ `UI`
- `Content` \ `ProjetoAula` \ `UI` \ `HUD`

```cpp
    class HUD_Player : public SWidget  {};
```

- `Content` \ `ProjetoAula` \ `UI` \ `HUD` \ `Menu`

```cpp
    class MenuMain : public SWidget {};
    class MenuLobbySinglePlayer : public SWidget {};            
    class MenuLobbyMultiPlayer : public SWidget {};                        
    class MenuConfig : public SWidget {};            
    class MenuPause : public SWidget {};                        
    class MenuExit : public SWidget {};
    class MenuMain : public IMenuInterface {};                                     
    class UMenuMainInterface : public IMenuMainInterface {};
    class UProjectGameInstance : public UGameInstance, IMenuMainInterface  {};
```

## 9. Projeto

### 9.1. Equipe

| Requisito                   | Responsável                               | Perfil      |
| :-------------------------- | :---------------------------------------- | :---------- |
| Art (mesh/material)         | Equipe 2                                  | Arte        |
| Músicas e sons              | <span style="color:green">Equipe 5</span> | Áudio e som |
| Character & Animations      | Equipe 3                                  | Programação |
| Menus                       | <span style="color:red">Equipe 1</span>   | Programação |
| Core                        | <span style="color:red">Equipe 1 </span>  | Programação |
| Gerenciamento e comunicação | <span style="color:blue">Equipe 4</span>  | Gerente     |
| Infraestrutura              | <span style="color:blue">Equipe 4</span>  | Programação |

### 9.2. Tarefas

| Tarefas                 | Responsável |   Início   |    Fim     |   %   |
| :---------------------- | :---------- | :--------: | :--------: | :---: |
| **Planjamento**         |             |            |            |       |
| - Preparação do projeto | Nostromo    | 01/01/2021 | 01/02/2021 |  0%   |
| **Desenvolvimento**     |             |            |            |       |
| - Storyline             | Nostromo    |            |            |       |
| - Protótipo             | Ripley      |            |            |       |
| - Arte conceitual       | Dallas      |            |            |       |
| - Mecânica 1            | Dallas      |            |            |       |
| **Testes**              |             |            |            |       |
| - Teste de Cena 1       | Xenomorfo   |            |            |       |

- D1 - Definição de tema
- D2 - Estrutura do projeto
- D3 - Desenvolvimento
- D4 - Testes
- Ano base 2023

| Tarefas                | Responsável |   1   |   2   |   3   |   4   |   5   |   6   |     7     |   8   |   9   |  10   |  11   |  12   |  13   |    14     |
| :--------------------- | :---------- | :---: | :---: | :---: | :---: | :---: | :---: | :-------: | :---: | :---: | :---: | :---: | :---: | :---: | :-------: |
|                        |             |  D1   |  D1   |  D1   |  D2   |  D2   |  D2   |    D3     |  D3   |  D3   |  D3   |  D3   |  D3   |  D3   |    D3     |
|                        |             | 24/02 | 03/03 | 10/03 | 17/03 | 24/03 | 31/03 | **14/04** | 28/04 | 05/05 | 12/05 | 19/05 | 26/05 | 02/06 | **16/06** |
| Nome do jogo           | Aluno 1     |   X   |       |       |       |       |       |           |       |       |       |       |       |       |           |
| Gênero                 |             |   X   |       |       |       |       |       |           |       |       |       |       |       |       |           |
| Características gerais |             |   X   |   X   |   X   |       |       |       |           |       |       |       |       |       |       |           |
| - Objetivos            |             |       |       |   X   |   X   |       |       |           |       |       |       |       |       |       |           |
| - Storyline            |             |       |       |   X   |   X   |   X   |       |           |       |       |       |       |       |       |           |
| GDD                    |             |       |       |   X   |   X   |   X   |       |           |       |       |       |       |       |       |           |
| Protótipo v1           |             |       |       |       |       |       |   x   |           |       |       |       |       |       |       |           |
| - Arte conceitual      |             |       |       |       |       |   X   |   x   |     x     |       |       |       |       |       |       |           |
| Character base         |             |       |       |       |       |       |       |           |   x   |       |       |       |       |       |           |
| - Character player     |             |       |       |       |       |       |       |           |       |   x   |       |       |       |       |           |
| - Character Outros     |             |       |       |       |       |       |       |           |       |   x   |       |       |       |       |           |
| Assets                 |             |       |       |       |       |       |       |           |       |       |   x   |   x   |   x   |       |           |
| - Itens básicos        |             |       |       |       |       |       |       |           |       |       |   x   |   x   |   x   |       |           |
| - Itens interativos    |             |       |       |       |       |       |       |           |       |       |   x   |   x   |   x   |       |           |
| - Itens Armas          |             |       |       |       |       |       |       |           |       |       |   x   |   x   |   x   |       |           |
| Level Design 1         |             |       |       |       |       |       |       |           |       |       |       |       |   x   |   x   |           |
| - Desafios             |             |       |       |       |       |       |       |           |       |       |       |       |   x   |   x   |           |
| - Montagem de ambiente |             |       |       |       |       |       |       |           |       |       |       |       |   x   |   x   |     x     |
| HUD                    |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| - Menus                |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| - HuD do player        |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| IA                     |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| - Perseguição          |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| - Ataque               |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| - Patrulha             |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| Sistema de pontos      |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| - Atributos(+)         |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| - Evolução             |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| Level Design Lv1       |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| Level Design lv2       |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| Level Design Lv3       |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| Testes                 |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| Correção               |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
| Apresentação           |             |       |       |       |       |       |       |           |       |       |       |       |       |       |           |
