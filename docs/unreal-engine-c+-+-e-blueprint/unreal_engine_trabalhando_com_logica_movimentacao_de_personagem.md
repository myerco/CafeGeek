---
title: Implementando a movimentação do personagem
description: Trabalhando com a lógica de movimentação do personagem utilizando Blueprint
tags: [Unreal Engine,eventos,events,funções,functions,macro]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
date: 2022-09-21 
---

## Índice

***

- [Actions Mappings](#actions-mappings)

- [Axis Mappings](#axis-mappings)

- [Mapeamento Input do projeto](#mapeamento-input-do-projeto)

- [Movimentação de peão Pawn com Blueprint](#movimentação-de-peão-pawn-com-blueprint)

- [Movimentação de objetos](#movimentação-de-objetos)

- [Usando o evento Tick com Blueprint](#usando-o-evento-tick-com-blueprint)

- [Usando o evento Tick com C++](#usando-o-evento-tick-com-c)

- [Movimentação de Characters](#movimentação-de-characters)

***

O **Unreal Engine** utiliza `Input Actions` e `Mappings` para associar teclas a ações e eixos de movimentação, separando a lógica da entrada física , neste capítulo vamos implementar a movimentação de objetos utilizando mapeamento de ações e controle de eixos de movimentação.

## Mapeamento Input do projeto

***

Para associar teclas a eventos utilizamos o menu `Edit` > `Project Settings` > `Input`. O valores adicionados serão salvos automaticamente.

{% include imagebase.html
    src="unreal/actor/unreal_engine_input.webp"
    alt="Figura: Engine Input."
    caption="Figura: Edit > Project Settings > Input."
%}

## Actions Mappings

***

Mapeamento de ações permite vincular um evento a uma entrada de dados (teclado, mouse, Gamepad, etc) e determinar a ação que deve ser executada em código C++ ou Blueprint.  

{% include imagebase.html
    src="unreal/actor/unreal_engine_mappings_actions.webp"
    alt="Figura: Actions Mappings."
    caption="Figura: Podemos adicionar novos mapeamentos de ações configurando os parâmetros do projeto."
%}

### Exemplo em C++ associando mapeamento a eventos

```cpp

// SetupPlayerInputComponent permite associar a entrada mapeada a uma função passada como parâmetro

void AProjetoMPCharacter::SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent)
{
    // Set up gameplay key bindings
    check(PlayerInputComponent);

    // Exemplos de parâmetros
    //      MoveForward = Nome definido no mapeamento do projeto.
    //      &AProjetoMPCharacter::MoveForward = Aqui é passado como referência (endereço de memória) o nome do método.
    PlayerInputComponent->BindAxis("MoveForward", this, &AProjetoMPCharacter::MoveForward);
    PlayerInputComponent->BindAxis("MoveRight", this, &AProjetoMPCharacter::MoveRight);

    PlayerInputComponent->BindAxis("Turn", this, &APawn::AddControllerYawInput);
    PlayerInputComponent->BindAxis("TurnRate", this, &AProjetoMPCharacter::TurnAtRate);
    PlayerInputComponent->BindAxis("LookUp", this, &APawn::AddControllerPitchInput);
    PlayerInputComponent->BindAxis("LookUpRate", this, &AProjetoMPCharacter::LookUpAtRate);

}

void AProjetoMPCharacter::TurnAtRate(float Rate)
{
    AddControllerYawInput(Rate * BaseTurnRate * GetWorld()->GetDeltaSeconds());
}

void AProjetoMPCharacter::LookUpAtRate(float Rate)
{
    AddControllerPitchInput(Rate * BaseLookUpRate * GetWorld()->GetDeltaSeconds());
}

// Método para controlar a movimentação para a frente e para trás
void AProjetoMPCharacter::MoveForward(float Value)
{
    if ((Controller != NULL) && (Value != 0.0f))
    {
        const FRotator Rotation = Controller->GetControlRotation();
        const FRotator YawRotation(0, Rotation.Yaw, 0);

        const FVector Direction = FRotationMatrix(YawRotation).GetUnitAxis(EAxis::X);
        AddMovementInput(Direction, Value);
    }
}

// Método para controlar a movimentação lateral, direita e equerda
void AProjetoMPCharacter::MoveRight(float Value)
{
    if ( (Controller != NULL) && (Value != 0.0f) )
    {
        const FRotator Rotation = Controller->GetControlRotation();
        const FRotator YawRotation(0, Rotation.Yaw, 0);
        const FVector Direction = FRotationMatrix(YawRotation).GetUnitAxis(EAxis::Y);
        AddMovementInput(Direction, Value);
    }
}
```

## Axis Mappings

***

O Mapeamento de eixos permite associar uma tecla para a movimentação do personagem, esse é atualizado constantemente.  

Registramos os seguintes valores:

`MoveForward` - Movimentação para a frente ou para trás :

- (-1) Para trás;

- (1) Para frente;

`MoveRight` - Movimentação para a direita e esquerda:

- (-1) Esquerda;

- (1) Direita;

> Para saber mais consulte o capítulo **Delta time e sistema de coordenadas**.

{% include imagebase.html
    src="unreal/actor/unreal_engine_mappings_axis.webp"
    alt="Figura: Axis Mappings."
    caption="Figura: Podemos associar teclas de movimentação para um método."
%}

### Exemplo em C++ associando um evento ao método MoveForward

```cpp
void AProjetoMPCharacter::SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent)
{

    check(PlayerInputComponent);
    PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &ACharacter::Jump);
    PlayerInputComponent->BindAction("Jump", IE_Released, this, &ACharacter::StopJumping);
    ...
}    
void AProjetoMPCharacter::Jump(ETouchIndex::Type FingerIndex, FVector Location)
{
    Jump();
}

void AProjetoMPCharacter::StopJumping(ETouchIndex::Type FingerIndex, FVector Location)
{
    StopJumping();
}
```

## Movimentação de peão Pawn com Blueprint

***

Para exemplificar a implementação utilizaremos uma classe do tipo `Pawn` que será o objeto que iremos controlar com os comandos de entrada.

### Componentes do objeto Pawn

{% include imagebase.html
    src="unreal/actor/unreal_engine_movimentacao_objeto.webp"
    alt="Figura: Blueprint - FloatingPawnMovement."
    caption="Figura: Blueprint - FloatingPawnMovement."
%}

Vamos adicionar os seguintes componentes no objeto:

- `FloatingPawnMovement` - Habilita lógica de movimentação do peão.

- `SpringArm` - O componente Spring Arm é usado para controlar automaticamente como a câmera lida com situações em que fica obstruída.

- `Camera`- Neste exemplo vamos utilizar o componente `Camera` para visualizar o objeto em terceira pessoa.

### Habilitando a entrada de comandos de entrada

É necessário habilitar a entrada de comandos para a classe **Pawn** com a função `Enable Input` que recebe como parâmetro o controlador de jogador atual ou `Player controller`.  

{% include imagebase.html
    src="unreal/actor/blueprint_get_player_controller_enable_input.webp"
    alt="Figura : Blueptint - Exemplo Enabled Input."
    caption="Figura : Blueptint - Exemplo Enabled Input."
%}

- `PlayerController` - Implementa funcionalidade para pegar os dados de entrada do jogador e traduzi-los em ações, como movimento, uso de itens, armas de fogo, etc. O parâmetro `Player Index` define qual controlador iremos utilizar, para este exemplo temos somente um, parâmetro 0.

- `Enable Input` - Habilita a entrada de comandos em um ator, você pode permitir que um jogador pressione um botão ou tecla e execute eventos que afetam o ator de alguma forma (seja acender ou apagar uma luz, abrir ou fechar uma porta, ativar algo, etc.) .

### Implementando movimentação com teclado

Devemos executar a chamada dos eventos criados no mapeamento e associados aos *inputs*.

{% include imagebase.html
    src="unreal/actor/unreal_engine_pawn_inputaxis.webp"
    alt="Figura: Blueprint - Movimentação de teclado Add Movement Input com InputAxis."
    caption="Figura: Blueprint - Movimentação de teclado Add Movement Input com InputAxis."
%}

- `GetActorRotation` - Retorna a rotação do `RootComponent` (Componente raiz que determina a posição do objeto)deste Ator;

- `Get Right Vector` - Obtenha o vetor correto (Y)  desse componente, no espaço do mundo;

- `Get Forward Vector` - Obtenha o vetor de direção da unidade para frente (X) deste componente, no espaço do mundo;

- `Add Movement Input` - Adiciona entrada de movimento ao longo do vetor de direção do mundo dado (geralmente normalizado) escalado por 'ScaleValue'. Se ScaleValue <0, o movimento será na direção oposta. As classes base de peão não aplicam movimento automaticamente, cabe ao usuário fazer isso em um evento Tick. Subclasses como **Character** e `DefaultPawn` manipulam automaticamente essa entrada e se movem;

- `Scale Value` - Escala para aplicar à entrada. Isso pode ser usado para entrada analógica, ou seja, um valor de 0,5 aplica-se à metade do valor normal, enquanto -1,0 inverteria a direção.

### Capturando as coordenadas

A seguir vamos capturar as coordenadas do ator para que possamos utilizar os métodos de movimentação **Turn** e **LookUp**  

{% include imagebase.html
    src="unreal/actor/blueprint_pawn_consume_movement_input_vector.webp"
    alt="Figura: Blueprint - Exemplo Consume Movement Input Vextor e AddActorWorldOffset."
    caption="Figura: Blueprint - Exemplo Consume Movement Input Vextor e AddActorWorldOffset."
%}

- `Consume Movement Input Vector` - Retorna o vetor de entrada pendente e o redefine para zero. Isso deve ser usado durante uma atualização de movimento (pelo Pawn ou PawnMovementComponent) para evitar o acúmulo de entrada de controle entre os quadros. Copia o vetor de entrada pendente para o vetor de entrada salvo (GetLastMovementInputVector()).

- `AddActorWorldOffSet` - Adiciona um delta à localização deste ator no espaço do mundo.

### Movimentação utilizando mouse

{% include imagebase.html
    src="unreal/actor/unreal_engine_pawn_yaw_pitch.webp"
    alt="Figura: Blueprint - InputAxis e Add Controller Yaw Input e Add Controller Pitch Input."
    caption="Figura: Blueprint - InputAxis e Add Controller Yaw Input e Add Controller Pitch Input."
%}

`Yaw e Pitch` - Representam respectivamente as coordenadas:  

- X = Roll;

- Y = Pitch;

- Z = Yaw;

### Controle de movimentação do ator (Classe)

{% include imagebase.html
    src="unreal/actor/unreal_engine_use_controller_rotation.webp"
    alt="Figura: Blueprint - Use Controller Rotation Pitch/Yaw."
    caption="Figura: Blueprint - Use Controller Rotation Pitch/Yaw."
%}

Caso as opções `Use controller rotation pitch/Yaw`, parâmetros da raiz do objeto (`Self`), estiverem ativas (`true`) a cápsula do ator irá se movimentar no seu próprio eixo.

{% include imagebase.html
    src="unreal/actor/blueprint_pawn_use_pawn_control_rotation.webp"
    alt="Figura: Blueprint - Use Paw Controller Rotation."
    caption="Figura: Blueprint - Use Paw Controller Rotation."
%}

Quando verdadeiro o parâmetro `Use Pawn control Rotation` do componente `SpringArm` somente o braço com a câmera são movimentados.

## Movimentação de objetos

***

Neste passo iremos implementar a Plataforma de Poder *PowerUp* para exemplificar a movimentação de objetos. Ao colidir com a plataforma a velocidade e o impulso do personagem **HP_Hero** aumentam.

A plataforma deverá se movimentar utilizando marcações (**TargetPoint**) para facilitar a level design.

Serão implementados objetos para disparar (Plataforma Trigger) a movimentação das plataformas.

### Estrutura do objeto Plataforma

{% include imagebase.html
    src="unreal/actor/blueprint_plataform_components.webp"
    alt="Figura: Blueprint - Exemplo de componentes da estutura da plataforma."
    caption="Figura: Blueprint - Exemplo de componentes da estrutura da plataforma."
%}

- `StaticMeshActor` - Derivado da classe Actor;

- `Box` - Do tipo `Box Collision`;

- **Velocidade/Impulso** - Variáveis públicas para multiplicar as propriedades do personagem.

### Aumentando a velocidade do Pawn

Lógica para aumentar a velocidade de corrida e força de impulso do personagem do *BP_Hero* tipo **Character**.

{% include imagebase.html
    src="unreal/actor/blueprint_plataform_inc_velocity_char.webp"
    alt="Figura: Blueprint - Exemplo da lógica da movimentação."
    caption="Figura: Blueprint - Exemplo da lógica da movimentação."
%}

- Ao colidir com a plataforma a lógica é acionada.

### Movimentação da plataforma

A movimentação tem que ser interpolada, quer dizer que as coordenadas tem que ser atualizadas a cada passo.  

Exemplos de interpolação de coordenadas:  

|       | X     |Y      |Z  |
|:-:    |:-:    |:-:    |:-:|
|Início |1      | 1     | 1 |
|       | 1     | **2** | 1 |
|       | 1     | **3** | 1 |
|       | 1     | **4** | 1 |
|Fim    | 1     | 5     | 1 |  

- Destino : 1,5.1
- Origem : 1,1,1

Perceba que o valor de `Y` varia até alcançar o valor final.

### Lógica usando Level Blueprint

Utilizando o `Level Blueprint` vamos implementar a lógica de movimentação usando `TimeLine`.

{% include imagebase.html
    src="unreal/actor/blueprint_plataform_setactorlocarion_lerp_timeline.webp"
    alt="Figura: Blueprint - Exemplo utilizando Timeline em um Level Blueprint."
    caption="Figura: Blueprint - Exemplo utilizando Timeline em um Level Blueprint."
%}

- Determinar o destino da movimentação;

- Implementar a lógica de movimentação usando `timeline`;

- Declarar a variável *Velocidade* para controle da velocidade de movimentação;  

- `Learp` - Interpola linearmente entre A e B com base em Alpha (100% de A quando Alpha = 0 e 100% de B quando Alpha = 1)

### Implementação do controle de tempo

Devemos definir uma curva de tempo para a variável **Alpha** para utilizar na interpolação de A com B (**Learp**).

{% include imagebase.html
    src="unreal/actor/blueprint_plataform_timeline_curve.webp"
    alt="Figura: Blueprint - TimeLine Curve para atualizar as coordenadas de movimentação."
    caption="Figura: Blueprint - TimeLine Curve para atualizar as coordenadas de movimentação."
%}

### Utilizando o evento Tick e TimeLine

Com a finalidade de exemplificar podemos utilizar o evento **Tick** para alterar a velocidade da plataforma.

{% include imagebase.html
    src="unreal/actor/blueprint_plataform_timeline_tick.webp"
    alt="Figura: Blueprint - Passando como parâmetro a velocidade e alterando o movimento."
    caption="Figura: Blueprint - Passando como parâmetro a velocidade e alterando o movimento."
%}

Pode ser construída outra plataforma para acionar o evento, Plataforma de gatilho `Trigger Plataform`.

## Usando o evento Tick com Blueprint

***

Agora vamos usar o evento **Tick** para interpolar as coordenadas de origem e destino.

### Declarando variáveis

{% include imagebase.html
    src="unreal/movimentacao/blueprint_plataform_properties.webp"
    alt="Figura: Blueprint - Exemplo propriedades do objeto plataforma."
    caption="Figura: Blueprint - Exemplo propriedades do objeto plataforma."
%}

- `TargetLocation` - Coordenadas do destino com `Widget`  ativo;

- `GlobalStartLocation` - Coordenadas globais iniciais do ator;

- `Location/Swap` - Variáveis auxiliares;

- `GlobalTargetLocation` - Coordenadas globais iniciais do destino;

- `Direction` - Vetor auxiliar que determina a direção do objeto.

### Inicializando variáveis

{% include imagebase.html
    src="unreal/movimentacao/blueprint_plataform_init_variables.webp"
    alt="Figura: Blueprint - Inicializando variáveis do objeto plataforma."
    caption="Figura: Blueprint - Inicializando variáveis do objeto plataforma."
%}

### Evento Tick da plataforma

{% include imagebase.html
    src="unreal/movimentacao/blueprint_plataform_movement_with_tick.webp"
    alt="Figura: Blueprint - Lógica de movimentação usando Tick."
    caption="Figura: Blueprint - Lógica de movimentação usando Tick."
%}

{% include imagebase.html
    src="unreal/movimentacao/blueprint_plataform_movement_with_tick_continue.webp"
    alt="Figura: Blueprint - Lógica de movimentação usando Tick - continuação."
    caption="Figura: Blueprint - Lógica de movimentação usando Tick - continuação."
%}

## Usando o evento Tick com C++

***

### Inicializando variáveis da plataforma

```cpp
void APlataforma::BeginPlay()
{
  Super::BeginPlay();
  GlobalStartLocation = GetActorLocation();
  GlobalTargetLocation = GetTransform().TransformPosition(TargetLocation);
}
```

### Lógica do evento Tick

```cpp
void APlataforma::Tick(float DeltaTime)
{
  {
    Super::Tick(DeltaTime);

    if (ActiveTriggers > 0)
      {
        FVector Location = GetActorLocation();

        float JourneyLength = (GlobalTargetLocation - GlobalStartLocation).Size();
        float JourneyTravelled = (Location - GlobalStartLocation).Size();

        if (JourneyTravelled >= JourneyLength)
          {
            FVector Swap = GlobalStartLocation;
            GlobalStartLocation = GlobalTargetLocation;
            GlobalTargetLocation = Swap;
        }

        FVector Direction = (GlobalTargetLocation - GlobalStartLocation).GetSafeNormal();
        Location += DeltaTime * SpeedPlataform * Direction;
        SetActorLocation(Location);
     }
  }
}
```

## Movimentação de Characters

***

Um personagem ou `Character` é um `Pawn` que possui algumas funcionalidades básicas de movimento bípede por padrão.

Para este exemplo vamos criar o objeto **BP_Hero** do tipo `Character` com as seguintes propriedades.

{% include imagebase.html
    src="unreal/movimentacao/unreal_engine_character_properties.webp"
    alt="Figura: Blueprint - Character class and properties."
    caption="Figura: Blueprint - A classe Character e suas propriedades básicas."
%}

Vamos adicionar e ajustar os componentes `SpringArm` e `Camera` para manipular a visualização do personagem em terceira pessoa.

Em `SpringArm` habilite a opção `Use Pawn Control Rotation` para que a cápsula do personagem não acompanhe o movimento do mouse.

- `Capsule` - O `CapsuleComponent` é usado para colisão de movimento. Para calcular geometrias complicadas para o `CharacterMovementComponent`, supõe-se que o componente de colisão na classe Character seja uma cápsula orientada verticalmente.

- `Arrow` - Um componente simples usado para indicar a direção do caminho do objeto.

- `Skeletal Mesh` - Ao contrário dos `Pawn`, os Personagens vêm com um `SkeletalMeshComponent` para habilitar animações avançadas que usam um esqueleto. É possível adicionar outras `Skeletal Mesh` a classes derivadas de Personagens, mas esta é a `Skeletal Mesh` principal associada ao Personagem.

- `Character Movement` - Permite que avatares que não usam física de corpo rígido se movam andando, correndo, pulando, voando, caindo e nadando. É específico para Personagens (`Characters`) e não pode ser implementado por nenhuma outra classe. As propriedades que podem ser definidas no `CharacterMovementComponent` incluem valores para atrito de queda e caminhada, velocidades de viagem pelo ar e água e pela terra, flutuabilidade, escala de gravidade e as forças físicas que o personagem pode exercer em objetos físicos. O CharacterMovementComponent também inclui parâmetros de movimento de raiz que vêm da animação e já estão transformados no espaço do mundo, prontos para uso pela física.

{% include imagebase.html
    src="unreal/movimentacao/unreal_engine_character_skeletal_mesh.webp"
    alt="Figura: Blueprint - Inicializando variáveis do objeto plataforma."
    caption="Figura: Blueprint - Inicializando variáveis do objeto plataforma."
%}

Adicione e ajuste o componente `Mesh` para adicionar uma malha esquelética, no exemplo acima utilizamos o pacote `ThirdPerson`.

### Utilizando Enumeration para registro de poses do personagem

Podemos utilizar uma variável `Enumeration` para registrar os estados do objeto.

#### Variável Enumeration

Implemente a variável **EN_State_Hero** do tipo `Enumeration`, utilize o menu de contexto `Blueprints` > `Enumerations`.

{% include imagebase.html
    src="unreal/actor/unreal_engine_enum_state_char_basics.webp"
    alt="Figura: Blueprint - Enumeration e Estados do jogador."
    caption="Figura: Blueprint - Enumeration e Estados do jogador."
%}

Adicione as linhas no objeto, `AddEnumerator`:

- Running - Correndo;

- Crouch - Agachado;

- Normal - Para o estado normal;

- Aiming - Mirando;

#### Atualizando a variável com os eventos Jump e Crouch

{% include imagebase.html
    src="unreal/actor/unreal_engine_enum_jump_crouch.webp"
    alt="Figura: Blueprint - Atualizando o estado do jogador utilizando Enumeration."
    caption="Figura: Blueprint - Atualizando o estado do jogador utilizando Enumeration."
%}

- `Input Action Crouch` - Este evento deve ser definido em `Project Settings` > `Input`, escolha a tecla `D` para este exemplo;

- `Can crouch` - Habilite este parâmetro em `Character Movement` para possibilitar o personagem agachar.
