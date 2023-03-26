---
title: Lógica de movimentação
description: Trabalhando com a lógica de movimentação do personagem utilizando Blueprint
tags: [Unreal Engine,eventos,events,funções,functions,macro]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
sidebar:  
  - title: "UNREAL ENGINE COM C++ E BLUEPRINT"
    nav: "dev_unreal"
date: 2022-09-21 
---

***

- [1. Mapeamento Input do projeto](#1-mapeamento-input-do-projeto)
- [2. Actions Mappings](#2-actions-mappings)
  - [2.1. Exemplo em C++ associando mapeamento a eventos](#21-exemplo-em-c-associando-mapeamento-a-eventos)
- [3. Axis Mappings](#3-axis-mappings)
  - [3.1. Exemplo em C++ associando um evento ao método MoveForward](#31-exemplo-em-c-associando-um-evento-ao-método-moveforward)
- [4. Movimentação de peão Pawn com Blueprint](#4-movimentação-de-peão-pawn-com-blueprint)
  - [4.1. Habilitando a entrada de comandos de entrada](#41-habilitando-a-entrada-de-comandos-de-entrada)
  - [4.2. Implementando movimentação com teclado](#42-implementando-movimentação-com-teclado)
  - [4.3. Capturando as coordenadas](#43-capturando-as-coordenadas)
  - [4.4. Movimentação utilizando mouse](#44-movimentação-utilizando-mouse)
  - [4.5. Controle de movimentação do ator (Classe)](#45-controle-de-movimentação-do-ator-classe)
- [5. Movimentação de objetos](#5-movimentação-de-objetos)
  - [5.1. Estrutura do objeto Plataforma](#51-estrutura-do-objeto-plataforma)
  - [5.2. Aumentando a velocidade do Pawn](#52-aumentando-a-velocidade-do-pawn)
  - [5.3. Movimentação da plataforma](#53-movimentação-da-plataforma)
  - [5.4. Lógica usando Level Blueprint](#54-lógica-usando-level-blueprint)
  - [5.5. Implementação do controle de tempo](#55-implementação-do-controle-de-tempo)
  - [5.6. Utilizando o evento Tick e TimeLine](#56-utilizando-o-evento-tick-e-timeline)
- [6. Usando o evento Tick com Blueprint](#6-usando-o-evento-tick-com-blueprint)
  - [6.1. Declarando variáveis](#61-declarando-variáveis)
  - [6.2. Inicializando variáveis](#62-inicializando-variáveis)
  - [6.3. Evento Tick da plataforma](#63-evento-tick-da-plataforma)
- [7. Usando o evento Tick com C++](#7-usando-o-evento-tick-com-c)
  - [7.1. Inicializando variáveis da plataforma](#71-inicializando-variáveis-da-plataforma)
  - [7.2. Lógica do evento Tick](#72-lógica-do-evento-tick)
- [8. Movimentação de Characters](#8-movimentação-de-characters)
  - [8.1. Utilizando Enumeration para registro de poses do personagem](#81-utilizando-enumeration-para-registro-de-poses-do-personagem)
    - [8.1.1. Variável Enumeration](#811-variável-enumeration)
    - [8.1.2. Atualizando a variável com os eventos Jump e Crouch](#812-atualizando-a-variável-com-os-eventos-jump-e-crouch)

***

O **Unreal Engine** utiliza `Input Actions` e `Mappings` para associar teclas a ações e eixos de movimentação, separando a lógica da entrada física , neste capítulo vamos implementar a movimentação de objetos utilizando mapeamento de ações e controle de eixos de movimentação.

## 1. Mapeamento Input do projeto

***

Para associar teclas a eventos utilizamos o menu `Edit` > `Project Settings` > `Input`. O valores adicionados serão salvos automaticamente.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_input.webp"
    alt="Figura: Engine Input."
    caption="Menu principal Edit > Project Settings > Input."
%}

***

## 2. Actions Mappings

Mapeamento de ações permite vincular um evento a uma entrada de dados (teclado, mouse, Gamepad, etc) e determinar a ação que deve ser executada em código C++ ou Blueprint.  

{% include imagebase.html
    src="unreal/actor/unreal_engine_mappings_actions.webp"
    alt="Figura: Actions Mappings."
    caption="Figura: Podemos adicionar novos mapeamentos de ações configurando os parâmetros do projeto."
%}

### 2.1. Exemplo em C++ associando mapeamento a eventos

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

***

## 3. Axis Mappings

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

### 3.1. Exemplo em C++ associando um evento ao método MoveForward

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

***

## 4. Movimentação de peão Pawn com Blueprint

{% include imagelocal.html
    src="unreal/actor/unreal_engine_movimentacao_objeto.webp"
    alt="Figura: Objeto Pawn."
    caption="Para exemplificar a implementação utilizaremos uma classe do tipo Pawn que será o objeto que iremos controlar com os comandos de entrada."
%}

Vamos adicionar os seguintes componentes no objeto:

- `FloatingPawnMovement` - Habilita lógica de movimentação do peão.

- `SpringArm` - O componente Spring Arm é usado para controlar automaticamente como a câmera lida com situações em que fica obstruída.

- `Camera`- Neste exemplo vamos utilizar o componente `Camera` para visualizar o objeto em terceira pessoa.

### 4.1. Habilitando a entrada de comandos de entrada

{% include imagelocal.html
    src="unreal/actor/blueprint_get_player_controller_enable_input.webp"
    alt="Figura : Exemplo Enabled Input."
    caption="É necessário habilitar a entrada de comandos para a classe Pawn com a função Enable Input que recebe como parâmetro o controlador de jogador atual ou Player controller."
%}

- `PlayerController` - Implementa funcionalidade para pegar os dados de entrada do jogador e traduzi-los em ações, como movimento, uso de itens, armas de fogo, etc. O parâmetro `Player Index` define qual controlador iremos utilizar, para este exemplo temos somente um, parâmetro 0.

- `Enable Input` - Habilita a entrada de comandos em um ator, você pode permitir que um jogador pressione um botão ou tecla e execute eventos que afetam o ator de alguma forma (seja acender ou apagar uma luz, abrir ou fechar uma porta, ativar algo, etc.) .

### 4.2. Implementando movimentação com teclado

{% include imagelocal.html
    src="unreal/actor/unreal_engine_pawn_inputaxis.webp"
    alt="Figura: Movimentação de teclado Add Movement Input com InputAxis."
    caption="Devemos executar a chamada dos eventos criados no mapeamento e associados aos inputs."
%}

- `GetActorRotation` - Retorna a rotação do `RootComponent` (Componente raiz que determina a posição do objeto)deste Ator;

- `Get Right Vector` - Obtenha o vetor correto (Y)  desse componente, no espaço do mundo;

- `Get Forward Vector` - Obtenha o vetor de direção da unidade para frente (X) deste componente, no espaço do mundo;

- `Add Movement Input` - Adiciona entrada de movimento ao longo do vetor de direção do mundo dado (geralmente normalizado) escalado por 'ScaleValue'. Se ScaleValue <0, o movimento será na direção oposta. As classes base de peão não aplicam movimento automaticamente, cabe ao usuário fazer isso em um evento Tick. Subclasses como **Character** e `DefaultPawn` manipulam automaticamente essa entrada e se movem;

- `Scale Value` - Escala para aplicar à entrada. Isso pode ser usado para entrada analógica, ou seja, um valor de 0,5 aplica-se à metade do valor normal, enquanto -1,0 inverteria a direção.

### 4.3. Capturando as coordenadas

{% include imagelocal.html
    src="unreal/actor/blueprint_pawn_consume_movement_input_vector.webp"
    alt="Figura: Exemplo Consume Movement Input Vector e AddActorWorldOffset."
    caption="Vamos capturar as coordenadas do ator para que possamos utilizar os métodos de movimentação Turn e LookUp."
%}

- `Consume Movement Input Vector` - Retorna o vetor de entrada pendente e o redefine para zero. Isso deve ser usado durante uma atualização de movimento (pelo Pawn ou PawnMovementComponent) para evitar o acúmulo de entrada de controle entre os quadros. Copia o vetor de entrada pendente para o vetor de entrada salvo (GetLastMovementInputVector()).

- `AddActorWorldOffSet` - Adiciona um delta à localização deste ator no espaço do mundo.

### 4.4. Movimentação utilizando mouse

{% include imagelocal.html
    src="unreal/actor/unreal_engine_pawn_yaw_pitch.webp"
    alt="Figura: InputAxis e Add Controller Yaw Input e Add Controller Pitch Input."
    caption="Yaw e Pitch representam respectivamente as coordenadas : "
%}

- X = Roll;

- Y = Pitch;

- Z = Yaw;

### 4.5. Controle de movimentação do ator (Classe)

{% include imagelocal.html
    src="unreal/actor/unreal_engine_use_controller_rotation.webp"
    alt="Figura: Use Controller Rotation Pitch/Yaw."
    caption="Caso as opções Use controller rotation pitch/Yaw, parâmetros da raiz do objeto (Self), estiverem ativas (true) a cápsula do ator irá se movimentar no seu próprio eixo."
%}

{% include imagelocal.html
    src="unreal/actor/blueprint_pawn_use_pawn_control_rotation.webp"
    alt="Figura: Use Paw Controller Rotation."
    caption="Quando verdadeiro o parâmetro Use Pawn control Rotation do componente SpringArm somente o braço com a câmera são movimentados."
%}

***

## 5. Movimentação de objetos

Neste passo iremos implementar a Plataforma de Poder *PowerUp* para exemplificar a movimentação de objetos. Ao colidir com a plataforma a velocidade e o impulso do personagem **HP_Hero** aumentam.

A plataforma deverá se movimentar utilizando marcações (**TargetPoint**) para facilitar a level design.

Serão implementados objetos para disparar (Plataforma Trigger) a movimentação das plataformas.

### 5.1. Estrutura do objeto Plataforma

{% include imagelocal.html
    src="unreal/actor/blueprint_plataform_components.webp"
    alt="Figura: Exemplo estrutura da plataforma."
    caption="Lista de Componentes e variáveis."
%}

- `StaticMeshActor` - Derivado da classe Actor;

- `Box` - Do tipo `Box Collision`;

- **Velocidade/Impulso** - Variáveis públicas para multiplicar as propriedades do personagem.

### 5.2. Aumentando a velocidade do Pawn

{% include imagelocal.html
    src="unreal/actor/blueprint_plataform_inc_velocity_char.webp"
    alt="Figura: Exemplo da lógica da movimentação."
    caption="Lógica para aumentar a velocidade de corrida e força de impulso do personagem do BP_Hero tipo Character."
%}

- Ao colidir com a plataforma a lógica é acionada.

### 5.3. Movimentação da plataforma

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

### 5.4. Lógica usando Level Blueprint

{% include imagelocal.html
    src="unreal/actor/blueprint_plataform_setactorlocarion_lerp_timeline.webp"
    alt="Figura: Exemplo utilizando Timeline em um Level Blueprint."
    caption="Utilizando o Level Blueprint vamos implementar a lógica de movimentação usando TimeLine."
%}

- Determinar o destino da movimentação;

- Implementar a lógica de movimentação usando `timeline`;

- Declarar a variável *Velocidade* para controle da velocidade de movimentação;  

- `Learp` - Interpola linearmente entre A e B com base em Alpha (100% de A quando Alpha = 0 e 100% de B quando Alpha = 1)

### 5.5. Implementação do controle de tempo

{% include imagelocal.html
    src="unreal/actor/blueprint_plataform_timeline_curve.webp"
    alt="Figura: TimeLine Curve para atualizar as coordenadas de movimentação."
    caption="Devemos definir uma curva de tempo para a variável Alpha para utilizar na interpolação de A com B (Learp)."
%}

### 5.6. Utilizando o evento Tick e TimeLine

{% include imagelocal.html
    src="unreal/actor/blueprint_plataform_timeline_tick.webp"
    alt="Figura: Blueprint - Passando como parâmetro a velocidade e alterando o movimento."
    caption="Com a finalidade de exemplificar podemos utilizar o evento Tick para alterar a velocidade da plataforma."
%}

Pode ser construída outra plataforma para acionar o evento, Plataforma de gatilho `Trigger Plataform`.

***

## 6. Usando o evento Tick com Blueprint

Agora vamos usar o evento **Tick** para interpolar as coordenadas de origem e destino.

### 6.1. Declarando variáveis

{% include imagelocal.html
    src="unreal/movimentacao/blueprint_plataform_properties.webp"
    alt="Figura: Exemplo propriedades do objeto plataforma."
    caption="Variáveis do objeto."
%}

- `TargetLocation` - Coordenadas do destino com `Widget`  ativo;

- `GlobalStartLocation` - Coordenadas globais iniciais do ator;

- `Location/Swap` - Variáveis auxiliares;

- `GlobalTargetLocation` - Coordenadas globais iniciais do destino;

- `Direction` - Vetor auxiliar que determina a direção do objeto.

### 6.2. Inicializando variáveis

{% include imagelocal.html
    src="unreal/movimentacao/blueprint_plataform_init_variables.webp"
    alt="Figura: Inicializando variáveis do objeto plataforma."
    caption="Usamos TransformLocation para converter o vetor TargetLocation em uma localização relativa a do jogador. Por exemplo, se T fosse a transformação de um objeto, isso transformaria uma posição do espaço local para o espaço mundial."
%}

### 6.3. Evento Tick da plataforma

{% include imagelocal.html
    src="unreal/movimentacao/blueprint_plataform_movement_with_tick.webp"
    alt="Figura: Lógica de movimentação usando Tick. "
    caption="Calculo de distância da trajetória inicial e final."
%}

{% include imagebase.html
    src="unreal/movimentacao/blueprint_plataform_movement_with_tick_continue.webp"
    alt="Figura: Lógica de movimentação usando Tick - continuação. "
    caption="Alterna os vetores quando o objeto chega no destino final."
%}

***

## 7. Usando o evento Tick com C++

### 7.1. Inicializando variáveis da plataforma

```cpp
void APlataforma::BeginPlay()
{
  Super::BeginPlay();
  GlobalStartLocation = GetActorLocation();
  GlobalTargetLocation = GetTransform().TransformPosition(TargetLocation);
}
```

### 7.2. Lógica do evento Tick

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

***

## 8. Movimentação de Characters

Um personagem ou `Character` é um `Pawn` que possui algumas funcionalidades básicas de movimento bípede por padrão.

Para este exemplo vamos criar o objeto **BP_Hero** do tipo `Character` com as seguintes propriedades.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_character_properties.webp"
    alt="Figura: Character class and properties."
    caption="Em SpringArm habilite a opção Use Pawn Control Rotation para que a cápsula do personagem não acompanhe o movimento do mouse."
%}

Vamos adicionar e ajustar os componentes `SpringArm` e `Camera` para manipular a visualização do personagem em terceira pessoa.

- `Capsule` - O `CapsuleComponent` é usado para colisão de movimento. Para calcular geometrias complicadas para o `CharacterMovementComponent`, supõe-se que o componente de colisão na classe Character seja uma cápsula orientada verticalmente.

- `Arrow` - Um componente simples usado para indicar a direção do caminho do objeto.

- `Skeletal Mesh` - Ao contrário dos `Pawn`, os Personagens vêm com um `SkeletalMeshComponent` para habilitar animações avançadas que usam um esqueleto. É possível adicionar outras `Skeletal Mesh` a classes derivadas de Personagens, mas esta é a `Skeletal Mesh` principal associada ao Personagem.

- `Character Movement` - Permite que avatares que não usam física de corpo rígido se movam andando, correndo, pulando, voando, caindo e nadando. É específico para Personagens (`Characters`) e não pode ser implementado por nenhuma outra classe. As propriedades que podem ser definidas no `CharacterMovementComponent` incluem valores para atrito de queda e caminhada, velocidades de viagem pelo ar e água e pela terra, flutuabilidade, escala de gravidade e as forças físicas que o personagem pode exercer em objetos físicos. O CharacterMovementComponent também inclui parâmetros de movimento de raiz que vêm da animação e já estão transformados no espaço do mundo, prontos para uso pela física.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_character_skeletal_mesh.webp"
    alt="Figura: Inicializando variáveis do objeto plataforma."
    caption="Adicione e ajuste o componente Mesh para adicionar uma malha esquelética, no exemplo acima utilizamos o pacote ThirdPerson."
%}

### 8.1. Utilizando Enumeration para registro de poses do personagem

Podemos utilizar uma variável `Enumeration` para registrar os estados do objeto.

#### 8.1.1. Variável Enumeration

{% include imagelocal.html
    src="unreal/actor/unreal_engine_enum_state_char_basics.webp"
    alt="Figura: Enumeration e Estados do jogador."
    caption="Implemente a variável EN_State_Hero do tipo Enumeration, utilize o menu de contexto Blueprints > Enumerations."
%}

Adicione as linhas no objeto, `AddEnumerator`:

- Running - Correndo;

- Crouch - Agachado;

- Normal - Para o estado normal;

- Aiming - Mirando;

#### 8.1.2. Atualizando a variável com os eventos Jump e Crouch

{% include imagelocal.html
    src="unreal/actor/unreal_engine_enum_jump_crouch.webp"
    alt="Figura: Atualizando o estado do jogador utilizando Enumeration."
    caption="Atualizamos as variáveis Enumeration para o estado associado ao comando Input."
%}

- `Input Action Crouch` - Este evento deve ser definido em `Project Settings` > `Input`, escolha a tecla `D` para este exemplo;

- `Can crouch` - Habilite este parâmetro em `Character Movement` para possibilitar o personagem agachar.
