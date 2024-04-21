---
title: Estrutura do Projeto
excerpt: Neste capítulo será apresentado a estrutura do projeto.
permalink: /docs/unreal-engine-estrutura-do-projeto
last_modified_at: 2023-03-28T08:48:05-04:00
author_profile: false
sidebar:
    nav: dev_unreal
toc: true  
tags:
  - Blueprint
  - Actors
  - Classes
  - Pastas
  - Estrutura
---

A seguir apresentaremos a estrutura de pastas do projeto de desenvolvimento do jogo, esta estrutura pode ser utilizada para diversos tipos de projetos que tenham personagens e jogadores.  

## 1. Pastas

```bash
└── Content
    ├── ExampleContent                # Pacotes de exemplo
    |   ├── AnimStarterPack           # Não devem estar no versionamento
    |   └── ThirdPerson               # Separados da lógica do projeto
    └── Projeto                       # Pasta principal do projeto
        ├── Art                       # Elementos do ambiente
        |   ├── Industrial            # Texturas e malhas
        |   |   ├── Ambient         
        |   |   ├── Machinery
        |   |   └── Pipes
        |   ├── Nature
        |   |   └── Ambient
        |   |       ├── Foliage
        |   |       ├── Rocks
        |   |       └── Trees
        |   └── Office
        ├── Models
        |   ├── Characters              # Estruturas dos personagens
        |   |   ├── Human               # Classe human
        |   |   |   ├── Mesh            # Malhas e esqueletos
        |   |   |   ├── Animations      # Animações
        |   |   |   └── Audio           # Sons
        |   |   ├── Mutant
        |   |   |   ├── Mesh            # Malha e texturas do personagem       
        |   |   |   └── Animations
        |   |   |       ├── Logic       # Animation Blueprint, Blend Space
        |   |   |       ├── Base        # Animações com movimento básico
        |   |   |       ├── Aim         # Animações usando uma arma e mirando
        |   |   |       └── Audio       # Sons do personagem
        |   |   └── NPC
        |   |       ├── Mesh            # Malha e texturas do personagem       
        |   |       └── Animations
        |   |           ├── Logic       # Animation Blueprint, Blend Space
        |   |           ├── Base        # Animações com movimento básico
        |   |           ├── Aim         # Animações usando uma arma e mirando
        |   |           └── Audio       # Sons do personagem
        |   ├── Chests                  # Baús
        |   |   ├── Materials     
        |   |   └── Mesh
        |   ├── Inventory               # Inventários
        |   ├── Itens                   # Itens
        |   └── Weapons                 # Armas
        ├── Core
        |   ├── Characters              # Classe principal dos personagens
        |   ├── Engine                  # Player Controller e Game Control
        |   ├── GameModes               # Game Mode e Game Instance
        |   ├── Interactables           # Classes de interação
        |   ├── Pickups                 # Classes básicas de objetos
        |   ├── DataSets                # Tabelas, enum e struct
        |   └── Weapons                 # Classe de armas
        ├── UI
        |   ├── Characters              # Interface vida, força e outros
        |   ├── SettingsMenu            # Configuração do jogo
        |   ├── ExitMenu                # Menu de saída 
        |   └── MainMenu                # Menu Principal
        └── Maps
            ├── Level1
            └── Level2

```

## 2. Classes

| Classe              | Pai                | Atributos          | Tipo          | Categoria          |
| :------------------ | :----------------- | :----------------- | :------------ | :----------------- |
| BP_CharacterBase    |                    | fHealth            | float         | Character          |
|                     |                    | sSound             | Sound Cue     |                    |
|                     |                    | tImage             | Texture 2D    |                    |
|                     |                    | cColor             | Color         |                    |
|                     |                    | nName              | Name          |                    |
|                     |                    | fWalkSpeed         | float         | Character\Movement |
|                     |                    | fCrouchSpeed       | float         |                    |
|                     |                    | fRunSpeed          | float         |                    |
|                     |                    | bRunning           | boolean       |                    |
|                     |                    | bCrouch            | boolean       |                    |
|                     |                    | bActionLeftAttack  | boolean       | Character\Action   |
|                     |                    | bActionRightAttack | boolean       |                    |
|                     |                    | bShooting          | boolean       |                    |
|                     |                    | bHoldingWeapon     | boolean       |                    |
|                     |                    | bAim               | boolean       |                    |
|                     |                    | bReloadWeapon      | boolean       |                    |
|                     |                    | Jump               | Event         |                    |
|                     |                    | Run                | Event         |                    |
|                     |                    | Attack Left        | Event         |                    |
|                     |                    | Attack Right       | Event         |                    |
|                     |                    | Weapon Take        | Event         |                    |
|                     |                    | Crouch             | Event         |                    |
|                     |                    | Weapon Aim         | Event         |                    |
|                     |                    | Weapon Reload      | Event         |                    |
|                     |                    | Weapon Shot        | Event         |                    |
|                     |                    | Died               | Event         |                    |
|                     |                    | Catch              | Event         |                    |
| ├── BP_Human        | BP_CharacterBase   |                    |               |                    |
| ├── BP_Mutant       | BP_CharacterBase   |                    |               |                    |
| └── BP_NPC          | BP_CharacterBase   |                    |               |                    |
| BP_PlayerController | APlayerController  |                    |               |                    |
| BP_AIController     | AIController       |                    |               |                    |
| BP_BotController    | APPlayerController |                    |               |                    |
| BP_GameMode         | UGameMode          |                    |               |                    |
| BP_GameInstance     | UGameInstance      | OpenMenuExit       |               |                    |
|                     |                    | OpenMenuMain       | Event         |                    |
|                     |                    | OpenMenPause       | Event         |                    |
| BP_Item             |                    | nName              | Name          |                    |
|                     |                    | sSound             | Sound Cue     |                    |
|                     |                    | tImage             | Texture 2D    |                    |
|                     |                    | cColor             | Color         |                    |
| └──BP_Weapon        | BP_Item            | WeaponShot         | Event         |                    |
|                     |                    | Magazine           | integer       |                    |
|                     |                    | Projectile         | BP_Projectile |                    |
| └──BP_Projectile    | BP_Item            | EventHit           | Event         |                    |
|                     |                    | Damage             | float         |                    |

```cpp
    class IMenuMainInterface : public UInterface {};
    class HUD_Player : public SWidget  {};
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
