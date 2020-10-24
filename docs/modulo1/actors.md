### Actors

Hierarquia

- UObject C++
 - Actor C++
    - Pawn
    - Character
    - GameController

- UObject C++
  - Actor BP
    - Pawn BP
    - Character BP
    - GameController BP

- Character
  - Movimentação
  - É controlado pelo PlayerController

- PlayerController
  - Character
- IAController
  - Character

- Actor
  - Actor Child
  - Component
  - Static Mesh

- Base - Andar, Correr e Pular
  - Mago
  - Guerreiro
  - Arqueiro

## Static Mesh
1. [Editor](https://docs.unrealengine.com/en-US/Engine/Content/Types/StaticMeshes/Editor/index.html)
1. [Static Mesh](https://www.youtube.com/watch?v=8WvwFPN1XNA)
1. [Static Mesh Actors](https://docs.unrealengine.com/en-US/Engine/Actors/StaticMeshActor/index.html)


## Skeletal mesh
1. [Skeletal Mesh Actors](https://docs.unrealengine.com/en-US/Engine/Actors/SkeletalMeshActors/index.html)

## Transformação
- Principal grupo de classes de atores.    
  ![Classes de atores](../actors/actor1.png)  

- A classe *Actor* .    
 ![Classe Actor](../actors/actor2.png)  

- Editor de objetos e componentes.   
 ![Editor](../actors/actor3.png)  

- Posicionamento do ator no mundo.  
 ![Posição](../actors/actor4.png)
- Posição relativa no mundo
 ![Posição Relativa](../actors/actor5.png)
- Janela de gerencimento.  
 ![Componentes](../actors/actor6.png)
 - o Componente *ChildActor* implementa a ligação com outro ator.
 [](https://www.youtube.com/watch?v=QM1QTQmvH-g)

## Adicionar atores na cena
spawn and destroy

## Isvalid

## Get All Actors

## Tag
Has Tag

## Game Mode
[Game mode](https://docs.unrealengine.com/en-US/Gameplay/Framework/GameMode/index.html)
## Default pawn

## Câmera

## Player input
1. [Spawned no cliente](https://docs.unrealengine.com/en-US/Gameplay/HowTo/SpawnAndDestroyActors/Blueprints/index.html)
1. [Enabled Input](https://docs.unrealengine.com/en-US/Gameplay/HowTo/ActorInput/Blueprints/index.html)
- Habilitando entradas de controles
1. [Mapeando de comandos](https://docs.unrealengine.com/en-US/Gameplay/Input/index.html)
- Action mapping
 - Mapeamento de um evento a um botão
 - Valores 0 e 1
 - Exemplo: Pulo = EventPulo(), Disparo = EventoDisparo(), Agachar = EventoDisparo()
- Axix mapping
 - Mapeamento de um evento a um botão ou a um eixo de controle
 - É atualizado constantemente
 - Escala de valores
 - Exemplo: MoverDireita = EventoDireita(), MoverEsquerda() = EventoEsquerda()
1. [Movimentação]([Unreal Engine CharacterMovement](https://docs.unrealengine.com/en-US/Gameplay/HowTo/CharacterMovement/Blueprints/index.html))
1.[PlayerInput](https://docs.unrealengine.com/en-US/Programming/Tutorials/PlayerInput/index.html)
