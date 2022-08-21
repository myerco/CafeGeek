---
title: Game Instance, Game State e Game Mode
description: Neste capítulo iremos apresentar as classes GameMode e GameInstance com suas funcionalidades.
tags: [Unreal Engine,game mode,game instance,game state]
layout: page
---

***

<a name="8"></a>
## CAPÍTULO 8 - Estruturas de dados e Interface com usuário

Na estrutura do **Unreal Engine** existem classes para controlar regras do jogo (`GameMode`) e o personagem bem como classes com visibilidade global (`GameInstance`), neste capítulo iremos apresentar estas classes e suas funcionalidades.

&nbsp;&nbsp;[8.3 Como funciona Game Mode e Game State?](#8.3)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8.3.1 O que é PlayerController?](#8.3.1)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8.3.2 GameInstance](#8.3.2)    

***

<a name="8.3"></a>
## 8.3 Como funciona Game Mode e Game State?
O conceito de "jogo" é dividido em 2 classes. O modo de jogo e o estado são as definições do jogo, incluindo coisas como as regras do jogo e as condições de vitória.

- `GameMode` - Controla como os jogadores entram no jogo utilizando as classes:   
  `InitGame`, `PreLogin`, `PostLogin` e `Logout`.
- `GameState` - É responsável por permitir que os clientes monitorem o estado do jogo.  Ele pode controlar as propriedades do jogo, como a lista de jogadores conectados, pontuação da equipe no Capture The Flag, missões que foram concluídas em um jogo de mundo aberto e assim por diante.   

  >O **GameState** não é o melhor lugar para controlar coisas específicas do jogador, como quantos pontos um jogador específico marcou para o time em uma partida do Capture The Flag porque isso pode ser tratado de forma mais limpa pelo **PlayerState**. Em geral, o GameState deve rastrear propriedades que mudam durante o jogo e são relevantes e visíveis para todos. Embora o modo Jogo exista apenas no servidor, o **Game State** existe no servidor e é replicado para todos os clientes, mantendo todas as máquinas conectadas atualizadas conforme o jogo avança.

- `PlayerState` - É o estado de um participante do jogo, como um jogador humano ou um *bot* que está simulando um jogador. Os dados apropriados em um `PlayerState` incluem o nome do jogador, pontuação, nível de jogo ou se o jogador esta carregando a bandeira em um jogo CTF.

- `PlayerController` -
Jogadores humanos que entram no jogo são associados a `PlayerControllers`. Esses `PlayerControllers` permitem que os jogadores possuam peões no jogo para que possam ter representações físicas no nível. Os `PlayerControllers` também fornecem aos jogadores controles de entrada (teclado, mouse e etc), um HUD (*heads-up display* ou interface com o jogador) e um `PlayerCameraManager` para lidar com as visualizações da câmera.

**A organização de classes do Framework.**

O fluxograma abaixo apresenta como as principais classes de jogo se relacionam entre si.

![Figura: Game Framework - QuickReference Unreal Engine](imagens/gamemode/GameFramework.webp "Figura: Game Framework - QuickReference Unreal Engine")

> Figura: Game Framework - QuickReference Unreal Engine

**Implementando o GameMode.**

Existem duas formas de informar qual `GameMode` o jogo deve utilizar, por *Level* ou projeto, utilizando o menu de contexto escolhemos `Game Mode Base`.

![Figura: Blueprint - GameMode create.](imagens/gamemode/blueprint_gamemode_create.webp "Figura: Blueprint - GameMode create.")    

> Figura: Blueprint - GameMode create.

Podemos definir o `GameMode` por `Level` em `Word Settings`.

![Figura: Blueprint - GameMode em World Settigns GameMode.](imagens/gamemode/blueprint_world_settigns_gamemode.webp "Figura: Blueprint - GameMode em World Settigns GameMode.")   

> Figura: Blueprint - GameMode em World Settigns GameMode.

- `BP_Hero` - Objeto do tipo `Character`.
- `BP_PlayerController` - Objeto do tipo `PlayerController`.

Para definir um `GameMode` para o projeto inteiro utilizamos o Menu `Project` > `Maps & Modes`.     

![Figura: Blueprint - Project > Maps & Modes.](imagens/gamemode/blueprint_project_mapsmodes.webp "Figura: Blueprint - Project > Maps & Modes.")

> Figura: Blueprint - Project > Maps & Modes.

<a name="8.3.1"></a>
### 8.3.1 O que é PlayerController?
Um `PlayerController` é a interface entre o `Pawn` e o jogador humano que o controla. O `PlayerController` representa essencialmente a vontade do jogador humano é definido por *Level*.

**PlayerController vs  PlayerCharacter.**

Se você deseja implementar alguma funcionalidade de entrada complexa (por exemplo, se houver vários jogadores em um cliente de jogo ou houver uma necessidade de alterar os personagens dinamicamente em tempo de execução), é melhor (e às vezes necessário) usar `PlayerController`. Neste caso, o `PlayerController` lida com a entrada e emite comandos para o Pawn.

Por exemplo, em jogos *Deathmatch*, o `Pawn` pode mudar durante o jogo, mas o `PlayerController` geralmente permanece o mesmo.

A classe `Character` representa o jogador no mundo do jogo. Ele fornece funcionalidade para animação, colisão, movimento e rede básica e modos de entrada. Portanto, se sua entrada não for complicada e não houver necessidade de alterar o caractere dinamicamente em tempo de execução, a classe de caractere é mais adequada. Por exemplo, você pode usá-lo no jogo de tiro em primeira pessoa para um único jogador.   

![Figura: Blueprint - GetPlayerController e GetActorLocation para imprimir a localização do ator.](imagens/gamemode/blueprint_playercontroller_character.webp "Figura: Blueprint - GetPlayerController e GetActorLocation para imprimir a localização do ator.")

> Figura: Blueprint - GetPlayerController e GetActorLocation para imprimir a localização do ator.

- `GetPlayerController` - As coordenadas apresentadas no nó `Print String` serão as coordenadas iniciais do `Pawn`;

- `GetPlayerCharacter` - As coordenadas apresentadas no nó `Print String` variam conforme a movimentação do `Pawn`.

<a name="8.3.2"></a>
### 8.3.2 GameInstance

`GameInstance` é criada quando o jogo é inicializado e ela será válida durante todo o tempo do jogo, similarmente a uma classe GLOBAL para o projeto, permitindo o compartilhamento das variáveis, eventos e funções contidas na `GameInstance` por todos os Levels.   
Tem seu próprio `Event Graph` para permitir desenvolvimento.  

Então, para que GameInstance?

Para compartilhar variáveis, eventos e funções por todos os levels possibilitando uma programação mais otimizada evitando retrabalho.

**Criando GameInstance.**

Utilizando o menu de contexto escolhemos `Bluprint Class` e logo em seguida procuramos a classe `GameInstance` básica.   

![Figura: Blueprint - Create GameInstance.](imagens/gamemode/blueprint_gameinstance_classe.webp "Figura: Blueprint - Create GameInstance.")      

> Figura: Blueprint - Create GameInstance.

**Adicionando um evento dentro da GameInstance.**

Como explicado anteriormente, os eventos e objetos ficaram disponíveis para o projeto. Para este exemplo vamos utilizar um evento customizado `Add Custom Event` no `Event Graph` da `GameInstance`.    

![Figura: GameInstance - Implementando a chamada de um objeto Widget.](imagens/gamemode/blueprint_gameinstance_events.webp "Figura: GameInstance - Implementando a chamada de um objeto Widget.")            

> Figura: GameInstance - Implementando a chamada de um objeto Widget.

Vamos adicionar uma variável para exemplificar.   

![Figura: Blueprint - GameInstance Variáveis.](imagens/gamemode/blueprint_gameinstance_variable.webp "Figura: Blueprint - GameInstance Variáveis. ")            

> Figura: Blueprint - GameInstance Variáveis.

**Chamando a GameInstance para acessar os seus elementos.**

Para este exemplo criamos um Level Vazio e no `Open Level Blueprint` vamos executar a chamada da `GameInstance`.

1. Antes de executar a chamada da `GameInstance` dentro dos objetos é necessário informar para o projeto qual a `GameInstance` padrão.        
  ![Figura: Blueprint - GameInstance Project.](imagens/gamemode/blueprint_gameinstance_project.webp "Figura: Blueprint - GameInstance Project.")        

  >Figura: Blueprint - GameInstance Project.

2. Logo após podemos utilizar a função `GetGameInstance` que retorna a `GameInstance` definida anteriormente para o projeto.   
  ![Figura: Blueprint - Exemplo de GameInstance utilizando Cast.](imagens/gamemode/blueprint_gameinstance_cast.webp "Figura: Blueprint - Exemplo de GameInstance utilizando Cast.")

  >Figura: Blueprint - Exemplo de GameInstance utilizando Cast.
