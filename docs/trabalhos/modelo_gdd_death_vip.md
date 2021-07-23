---
title: Death VIP
description: Modelo de GDD do jogo Death VIP
tags: [Unreal Engine, Death VIP, roteiro,GDD]
---

[CafeGeek](http://cafegeek.eti.br)  / [Trabalhos](http://cafegeek.eti.br/trabalhos/index.html)

# DEATH VIP
“Rescue or die trying”

>All work Copyright ©2018 by CafeGeek
Written by Nostromo    
Version # 1.00    

## 2.Plataforma
PC
## 3.Faixa Etária
14
## 4.Classificação
SEM RESTRIÇÃO

## 5. Características gerais
- Mapas grandes (KM)
- 3D gráficos
- 32-Bit color
- 3ª Pessoa

## 6.Características multiplayer
Salas de até 16 jogadores

## 7.Resumo da história
Quando o comandante das milícias descobriu a tentativa de resgate de um alvo considerado por ele de extrema importância, mandou todos os seus soldados fazer de tudo para MATAR O VIP para servir de exemplo.

Equipe de resgate (EAS - Esquadrão Aeroterrestre de Salvamento)  de 3 jogadores tenta resgatar um VIP (Very Important Person) em uma região dominada por milícias fortemente armadas em um país da América do Sul. A equipe conta com arsenal leve de combate e resgate, como por exemplo metralhadoras M4, espingardas e pistolas.
Quanto ao VIP, não está armado e nem consegue segurar uma arma mas pode curar os membros da sua equipe, também conta com a capacidade de visualizar o mapa e procurar itens que podem  auxiliar no resgate.

Durante o trajeto até o resgate deverão ser cumpridos três (3) objetivos, obrigando toda a equipe  a se envolver em combates.

A equipe EAS com auxílio do VIP pode localizar outras equipes de resgate e seus VIPS´s para tentar sobreviver juntos.

Os itens espalhados no mapa podem ser armas pesadas e rifles de precisão bem como itens que alteram o modo de jogo, como por exemplo  o “TREINO VIP” que transforma o VIP em um membro da equipe EAS por alguns minutos.

## 8.Diferenciais de vendas
- Explore o mapa para encontrar itens que auxiliam na sobrevivência e resgate do VIP;
- Esteja preparado para a missão mudar durante o jogo, alterando totalmente a sua tática de resgate;
- Tente sobreviver ouvindo ROCK INDIE das melhores bandas de garagem;
- Encontre outras equipes e seus VIP´s para tentar sobreviver em um grande modo cooperativo de 16 jogadores, modo *Kill House*;
- Múltiplos modo de gameplay, incluindo cooperativo de 4 jogadores, cooperativo de 16 jogadores e multiplayer onde as equipes tentam eliminar o VIP do adversário;

## 9.Produtos concorrentes
- Left for dead
- COD Zumbi

## 10.Objetivos
- Não deixar o VIP morrer, caso morra o jogo acaba;
- Alcançar o ponto de resgate com toda a sua equipe;
- Explorar o mapa para coletar itens auxiliares;
- Cumprir os 3 objetivos durante o resgate;

## 11.Personagens

|Class        |Aggressive         | Defensive         |Support          |VIP            |
|:-           |:-:                |:-:                |:-:              |:-:            |
|Type         |Lieutenant         |Destructive        |Sniper           |VIP            |
|**Details**  |                   |                   |                 |               |
|Health       |80                 |100                |80               |100            |
|Speed        |100                |80                 |90               |90             |
|**Skill**    |                   |                   |                 |               |
|Weapons      |                   |                   |                 |               |
|             |M4A1               | M60               |Rifle Scout      |Maps           |
|             |Shotgun            | M4A1              |Pistol 1914      |               |
|Extras       |                   |                   |                 |               |
|             |knife              |knife              |knife            |Medical Kit    |
|             |grenade            | grenade           |grenade          |resurrect and cure friends     |
|             |interact itens     |provides ammunition|Prepare C4       |find items     |

>Observação:    
>Interação com itens :
> - Abrir portas codificadas;
> - Chamar o resgate quando chegar no local marcado;

###  11.2. Movimentação Controle


## 10. O Mundo do jogo
- Florestas tropicais;
- Favelas da América latina;
- Vilarejos;

## 11. Interface (HUB)
- Medidor de Saúde do personagem
- Lista de membros da equipe com medidor de saúde
- Tipo da arma com informação de munição (Atual/Total)
- Quantidade de Granadas;
- Mini Mapa com localização de objetivos e itens (somente o VIP)

## 12. Câmera
Movimentação em 180º ;
Na altura do ombro do jogador e distante o suficiente para visualizar os pés do jogador;
Ao mirar com arma leve a câmera dá zoom do alvo (2x) visualizando o ombro do jogador
Ao mirar com rifle de precisão o zoom é de 4x e somente é apresentado a lente da arma;

## 13. Inimigos

|Class        |Aggressive         | Shooter           |Boss             |Boss           |Boss         |Boss       |Boss         |Boss       |
|:-           |:-:                |:-:                |:-:              |:-:            |:-:          |:-:        |:-:          |:-:        |
|Type         |Soldier            |demolisher         |Sniper           |Hell           |Mercenary    |Armored    |Bomb         |Captain    |
|**Details**  |                   |                   |                 |               |             |           |             |           |
|Health       |40                 |100                |200              |100            |100          |250        |40           |400        |
|Speed        |100                |80                 |90               |90             |150          |90         |50           |50         |
|**Skill**    |                   |                   |                 |               |             |           |             |           |
|Weapons      |                   |                   |                 |               |             |           |             |           |
|             |AL 47              | M60               |Rifle Scout      |throw flames   |AK 47        |AK 47+     |RPG          | AK 74     |
|             |Shotgun            | M4A1              |Pistol 1914      |               |             |           |             |           |  
|Objective    |                   |                   |                 |               |             |           |             |           |
|             |Não tem alvo       |Não tem alvo       |Alvo VIP         |Não tem alvo   |Não tem alvo | Alvo VIP  |Não tem alvo | VIP       |
|             |Ataca jogador      |Ataca VIP e prox.  |Foco 2s          |Ataca jogador  |Ataca VIP    | Foco 2s   |Foco 2s      |Foco 2s    |


## 14. Armas
|Weapon       |Bullet for loader  | Max Loader    |
|:-           |:-:                |:-:            |
|M4A1         |15                 |40             |
|M60          |15                 |40             |
|AK 47        |15                 |30             |
|Granada      |                   |               |
|Rifle scout  |10                 |5              |
|Barret .40   |7                  |2              |


## 15. Músicas e efeitos de som
- Rock indie (procurar lista sem direitos autorais)
- Link das músicas

## 16. Multiplayer
- 4 Jogadores
- Cooperativo
- Competitivo
- Chat aberto
- Estimativa de jogadores online ( > 100 )

## 17. GamePlay
### 17.1.    Objetivos

|Objetivo               | Ação            |
|:-                     |:-               |
| A casa da morte- Casa protegida por todas classes de inimigos - Casa onde eram realizada torturas | Abrir uma porta (2s) - Recolher a peça do rádio 1 (2s) - Procurar item especial, provas do massacre - Recolher o item especial (2s)     |
|A central de planejamento - Casa protegida por todas as classes- Casa onde estão os mapas e as provas de crimes| Entrar no prédio, arrombar Uma porta (2s) - Entrar na sala de planejamento, Arrombar 2 portas (2s cada uma) - Recolher a peça de rádio 2 (2s) - Procurar itens especiais, relatórios - Recolher o item especial (2s)   |
| A central de comunicação -Central de comunicações das milícias |Entrar no prédio, arrombar uma porta (2s) - Entrar na sala de planejamento, Arrombar 4 portas (2s cada uma) - Recolher a peça de rádio 3 (2s)- Subir no terraço do prédio para melhorar a comunicação Chamar Resgate (2s)          |
|O ponto de resgate - Campo aberto com poucas áreas de cobertura  |Sinalizar o local de resgate (2s) - Aguardar o resgate (60s)  |
|A prisão | O jogador preso fica sem armas- Quando a porta da prisão abrir o jogador recebe as armas e pode sair - A prisão é protegida por 2 snipers, 4 infernos, 4 bomba e 3 mercenários |

### 17.2. Mapas
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

### 17.3. Experiência e Level
Não definido.

### 17.4. Características especiais do Capitão
- O capitão aparece quando os jogadores passam por algumas áreas ou quando um objetivo é alcançado. Ele sempre aparece com 100% de vida;
- Se o capitão ficar perto de um jogador (5 metros) o jogador é sequestrado e enviado para “A prisão”. Essa ação é repetida até o capitão prender todos os membros do time e/ou matar o VIP ;
- O capitão desaparece quando o nível de vida chega em 20%, joga fumaça e some.;
- Quando o resgate é chamado o capitão não desaparece mais;
- Quanto aparece ele grita provocações e xingamentos;
- Quando captura um membro da equipe ri de forma sinistra;

### 17.5. Modelos
- EAS - Equipe principal com uniformes do exército brasileiro
- SEAL - Uniformes de SEAL USA
- Milicianos - Sem uniformes, roupas da região;
- VIP - Roupa casual, jeans e camiseta;


## Estrutura do modelo
```cpp

|-- Content
  |-- ProjetoAula
    |-- Art
    | |-- Industrial
    | | |-- Ambient
    | |	|-- Machinery
    | |	|-- Pipes
    | |-- Nature
    | | | |-- Ambient
    | | | | |-- Foliage
    | | | | |-- Rocks
    | | | | |-- Trees
    |	|-- Office
    |-- Characters
    | |-- lieutenant
            class BP_PlayerBase Lieutenant {};
    | |-- vip
    | |-- sniper
    | |-- destructive						
    | |-- Common
    | |  |-- Animations
              class AAnimation BP_PlayerAnimations {};
              class AAnimation BP_BotAnimation {};
    | |  |  |-- Audio
              class audio voice {};
              class audio walkstep {};
    |-- Bots                    
    | |-- bSoldier
            class BP_BotBase BP_bSoldier {};
            class ABehaviortreee BHT_bSoldier {};
    | |-- bDestructive                  
            class BP_BotBase BP_bDestructive {};
            class ABehaviortreee BHT_bDestructive {}
    | |-- bHell                  
    | |-- bSniper                  
    |-- Core
    | |-- Characters
            struct sInventory {
              Vector class BP_Item
            }
            struct sPlayer {
              float Health; float MaxHealth;
              float Armor; float MaxArmor;
              float Speed; float MaxSpeed;
              Name NameCharacter;
              Name NamePlayer;
              sProfile ListProfile;  
              2Dimage image;
              Text ClassPlayer <Aggressive,Defensive,Support>;
              Text TypePlayer <Lieutenant,Sniper, Vip,destructive>;
            };
            struct sBot {
              float Health; float MaxHealth;
              float Armor;  float MaxArmor;
              Name NameBot;
              2Dimage image;
              Text ClassBot <Aggressive,Defensive,Support>;
              Text TypePlayer <Lieutenant,Sniper, Vip,destructive>;
              Char TypeEnemy  <Boss,Normal>;
            };
            class ACharacter CharacterBase{
              void Died();
              void Run();
              void Crouching();
              void Walk();
              void Talk();
            };
            class BP_CharacterBase BP_PlayerBase {
              sPlayer PlayerInfo;
              void catch();
              void changeWeapon();
              void Amni();
              void Shoot();
            };
            class BP_CharacterBase BP_BotBase {
              sBot BotInfo;
              void Amni();
              void Shoot();
            };
            class APlayerController BP_PlayerControllerBase {};
            class APPlayerControler BP_BotControllerBase {};
    |	|-- Engine
            class UGameInstance BP_GameInstanceBase  {
              void openMenuMain();
              void openMenuPause();
            };
            class UInterface UMenuMainInterface {
            };
    |	|-- GameModes
            class UGameMode BP_GameModeBase {};
    |	|-- Interactables
            struct sItem {
              Name    NameItem;
              2Dimage image;
              Text  Type <Weapon, Life, Damage, collectible>;
              integer Magazine;                 // Max Bullet magazine
              integer MaxMagazine;              // Numbers of magazine;
              float Damage;   float MaxDamage;
              float Life; float MaxLife;
              USound  soundItem;
            };
            class UActor Item {
              sItem InfoItem
            };
            class Item BP_Item {
              void PlaySound();
            };  
      |	|-- Pickups
      |	|-- Weapons
            class Item WeaponBase {
              sItem itemInfo;
            };
            class Item BP_M4A1 {};
            class Item BP_M4A1 {};
    |-- Maps
    |	|-- Level1
    |	|-- Level2      
    |-- UI
    |	|-- HUD    
            class UUserWidget HUD_Player {};
    |	|-- Menu
            class UUserWidget MenuMain {};
            class UUserWidget MenuLobbySinglePlayer {};            
            class UUserWidget MenuLobbyMultiPlayer {};                        
            class UUserWidget MenuConfig {};            
            class UUserWidget MenuPause {};                        
            class UUserWidget MenuExit {};
            class MenuMain IMenuInterface {};                                     
            class UMenuMainInterface IMenuMainInterface {};
            class UGameInstance, IMenuMainInterface UProjectGameInstance {};
```


### Equipe

|Requisito                      | Responsável           | Perfil      |
|:--                            |:--                    |:--          |
|Core                           | Equipe 1              | Programação |
|Art (mesh/material)            | Equipe 2              | Arte        |
|Character & Animations         | Equipe 3              | Programação |
|Menus                          | Equipe 1              | Programação |
|Infraestrutura                 | Equipe 4              | Programação |
|Músicas e sons                 | Equipe 5              | Áudio e som |
|Gerencia e comunicação         | Equipe 4              | Gerente     |
