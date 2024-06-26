---
title: Lógica de movimentação
excerpt: Trabalhando com a lógica de movimentação do personagem utilizando Blueprint
permalink: /unreal-engine-capitulo-5/logica-de-movimentacao
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 501
tags:
  - movimentação
  - actions mappings
---

O **Unreal Engine** utiliza `Input Actions` e `Mappings` para associar teclas a ações e eixos de movimentação, separando a lógica da entrada física , neste capítulo vamos implementar a movimentação de objetos utilizando mapeamento de ações e controle de eixos de movimentação.

## 1. Mapeamento Input do projeto

Para associar teclas a eventos utilizamos o menu `Edit` > `Project Settings` > `Input`. O valores adicionados serão salvos automaticamente.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-input.webp"
    alt="Figura: Engine Input."
    caption="Figura: Menu principal Edit > Project Settings > Input."
%}

## 2. Actions Mappings

O mapeamento de ações permite vincular um evento a uma entrada de dados (teclado, mouse, Gamepad, etc) e determinar a ação que deve ser executada em código C++ ou Blueprint.  

{% include imagelocal.html
    src="unreal/actor/unreal-engine-mappings-actions.webp"
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

## 3. Axis Mappings

O Mapeamento de eixos permite associar uma tecla à movimentação do personagem, esse evento é atualizado constantemente.  

Registramos os seguintes valores:

`MoveForward` - Movimentação para a frente ou para trás :

- (-1) Para trás;

- (1) Para frente;

`MoveRight` - Movimentação para a direita e esquerda:

- (-1) Esquerda;

- (1) Direita;

**Infomração:** Para saber mais consulte o capítulo [Delta time e sistema de coordenadas](/unreal-engine-capitulo-5/delta-time-e-sistema-de-coordenadas).
{: .notice--info}

{% include imagelocal.html
    src="unreal/actor/unreal-engine-mappings-axis.webp"
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

## 4. Movimentação de peão Pawn com Blueprint

{% include imagelocal.html
    src="unreal/actor/unreal-engine-movimentacao-objeto.webp"
    alt="Figura: Objeto Pawn."
    caption="Figura: Lista de componentes do objeto."
%}

Para exemplificar a implementação utilizaremos uma classe do tipo Pawn que será o objeto que iremos controlar com os comandos de entrada

Vamos adicionar os seguintes componentes no objeto:

`FloatingPawnMovement` - Habilita lógica de movimentação do peão.

`SpringArm` - O componente Spring Arm é usado para controlar automaticamente como a câmera lida com situações em que fica obstruída.

`Camera`- Neste exemplo vamos utilizar o componente `Camera` para visualizar o objeto em terceira pessoa.

### 4.1. Habilitando a entrada de comandos de entrada

{% include imagelocal.html
    src="unreal/actor/unreal-engine-get-player-controller-enable-input.webp"
    alt="Figura : Exemplo Enabled Input."
    caption="Figura: O nó é chamado ao iniciar (BeginPlay) o objeto."
%}

É necessário habilitar a entrada de comandos para a classe Pawn com a função Enable Input que recebe como parâmetro o controlador de jogador atual ou Player controller

`PlayerController` - Implementa funcionalidade para pegar os dados de entrada do jogador e traduzi-los em ações, como movimento, uso de itens, armas de fogo, etc. O parâmetro `Player Index` define qual controlador iremos utilizar, para este exemplo temos somente um, parâmetro 0.

`Enable Input` - Habilita a entrada de comandos em um ator, você pode permitir que um jogador pressione um botão ou tecla e execute eventos que afetam o ator de alguma forma (seja acender ou apagar uma luz, abrir ou fechar uma porta, ativar algo, etc.) .

### 4.2. Implementando movimentação com teclado

{% include imagelocal.html
    src="unreal/actor/unreal-engine-pawn-inputaxis.webp"
    alt="Figura: Movimentação de teclado. "
    caption="Figura: Add Movement Input com InputAxis."
%}

Devemos executar a chamada dos eventos criados no mapeamento e associados aos inputs.

`GetActorRotation` - Retorna a rotação do `RootComponent` (Componente raiz que determina a posição do objeto)deste Ator;

`Get Right Vector` - Obtenha o vetor correto (Y)  desse componente, no espaço do mundo;

`Get Forward Vector` - Obtenha o vetor de direção da unidade para frente (X) deste componente, no espaço do mundo;

`Add Movement Input` - Adiciona entrada de movimento ao longo do vetor de direção do mundo dado (geralmente normalizado) escalado por 'ScaleValue'. Se ScaleValue <0, o movimento será na direção oposta. As classes base de peão não aplicam movimento automaticamente, cabe ao usuário fazer isso em um evento Tick. Subclasses como **Character** e `DefaultPawn` manipulam automaticamente essa entrada e se movem;

`Scale Value` - Escala para aplicar à entrada. Isso pode ser usado para entrada analógica, ou seja, um valor de 0,5 aplica-se à metade do valor normal, enquanto -1,0 inverteria a direção.

### 4.3. Capturando as coordenadas

{% include imagelocal.html
    src="unreal/actor/unreal-engine-pawn-consume-movement-input-vector.webp"
    alt="Figura: Exemplo Consume Movement Input Vector e AddActorWorldOffset."
    caption="Figura: O nó é chamado a cada tick do objeto, atualizando as coordenadas de localização."
%}

Vamos capturar as coordenadas do ator para que possamos utilizar os métodos de movimentação Turn e LookUp

`Consume Movement Input Vector` - Retorna o vetor de entrada pendente e o redefine para zero. Isso deve ser usado durante uma atualização de movimento (pelo Pawn ou PawnMovementComponent) para evitar o acúmulo de entrada de controle entre os quadros. Copia o vetor de entrada pendente para o vetor de entrada salvo (GetLastMovementInputVector()).

`AddActorWorldOffSet` - Adiciona um delta à localização deste ator no espaço do mundo.

### 4.4. Movimentação utilizando mouse

{% include imagelocal.html
    src="unreal/actor/unreal-engine-pawn-yaw-pitch.webp"
    alt="Figura: InputAxis associado ao nó Add Controller Yaw Input e Add Controller Pitch Input."
    caption="Figura: Atualiza constantemente o valor de Axis passando como parâmetro aos nós de controle de movimentação."
%}

Yaw e Pitch representam respectivamente as coordenadas :

- X = Roll;

- Y = Pitch;

- Z = Yaw;

### 4.5. Controle de movimentação do ator (Classe)

{% include imagelocal.html
    src="unreal/actor/unreal-engine-use-controller-rotation.webp"
    alt="Figura: Use Controller Rotation Pitch/Yaw."
    caption="Figura: Caso as opções Use controller rotation pitch/Yaw, parâmetros da raiz do objeto (Self), estiverem ativas (true) a cápsula do ator irá se movimentar no seu próprio eixo."
%}

{% include imagelocal.html
    src="unreal/actor/unreal-engine-pawn-use-pawn-control-rotation.webp"
    alt="Figura: Use Paw Controller Rotation."
    caption="Figura: Quando verdadeiro o parâmetro Use Pawn control Rotation do componente SpringArm somente o braço com a câmera são movimentados."
%}

## 5. Movimentação de objetos

Neste passo iremos implementar a Plataforma de Poder *PowerUp* para exemplificar a movimentação de objetos. Ao colidir com a plataforma a velocidade e o impulso do personagem **HP_Hero** aumentam.

A plataforma deverá se movimentar utilizando marcações (**TargetPoint**) para facilitar a level design.

Serão implementados objetos para disparar (Plataforma Trigger) a movimentação das plataformas.

### 5.1. Estrutura do objeto Plataforma

{% include imagelocal.html
    src="unreal/actor/unreal-engine-plataform-components.webp"
    alt="Figura: Exemplo estrutura da plataforma."
    caption="Figura: Lista de Componentes e variáveis."
%}

`StaticMeshActor` - Derivado da classe Actor;

`Box` - Do tipo `Box Collision`;

**Velocidade/Impulso** - Variáveis públicas para multiplicar as propriedades do personagem.

### 5.2. Aumentando a velocidade do Pawn

{% include imagelocal.html
    src="unreal/actor/unreal-engine-plataform-inc-velocity-char.webp"
    alt="Figura: Exemplo da lógica da movimentação."
    caption="Figura: Lógica para aumentar a velocidade de corrida e força de impulso do personagem do BP_Hero tipo Character."
%}

**Informação:** Ao colidir com a plataforma a lógica é acionada.
{: .notice--info}

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
    src="unreal/actor/unreal-engine-plataform-setactorlocarion-lerp-timeline.webp"
    alt="Figura: Exemplo utilizando Timeline em um Level Blueprint."
    caption="Figura: Nesta cena existe um objeto com dois objetos alvos (TargetPoint) para marcar as coordenadas de movimentação."
%}

Utilizando o Level Blueprint vamos implementar a lógica de movimentação usando TimeLine, seguindo os passos abaixo:

- Determinar o destino da movimentação;

- Implementar a lógica de movimentação usando `timeline`;

- Declarar a variável *Velocidade* para controle da velocidade de movimentação;  

- `Learp` - Interpola linearmente entre A e B com base em Alpha (100% de A quando Alpha = 0 e 100% de B quando Alpha = 1)

### 5.5. Implementação do controle de tempo

{% include imagelocal.html
    src="unreal/actor/unreal-engine-plataform-timeline-curve.webp"
    alt="Figura: TimeLine Curve para atualizar as coordenadas de movimentação."
    caption="Figura: Devemos definir uma curva de tempo para a variável Alpha para utilizar na interpolação de A com B (Learp)."
%}

### 5.6. Utilizando o evento Tick e TimeLine

{% include imagelocal.html
    src="unreal/actor/unreal-engine-plataform-timeline-tick.webp"
    alt="Figura: Blueprint - Passando como parâmetro a velocidade e alterando o movimento."
    caption="Figura: Com a finalidade de exemplificar podemos utilizar o evento Tick para alterar a velocidade da plataforma."
%}

**Informação:** Pode ser construída outra plataforma para acionar o evento, Plataforma de gatilho `Trigger Plataform`.
{: .notice--info}

## 6. Usando o evento Tick com Blueprint

Agora vamos usar o evento **Tick** para interpolar as coordenadas de origem e destino.

### 6.1. Declarando variáveis

{% include imagelocal.html
    src="unreal/movimentacao/unreal-engine-plataform-properties.webp"
    alt="Figura: Exemplo propriedades do objeto plataforma."
    caption="Figura: Variáveis do objeto."
%}

`TargetLocation` - Coordenadas do destino com `Widget`  ativo;

`GlobalStartLocation` - Coordenadas globais iniciais do ator;

`Location/Swap` - Variáveis auxiliares;

`GlobalTargetLocation` - Coordenadas globais iniciais do destino;

`Direction` - Vetor auxiliar que determina a direção do objeto.

### 6.2. Inicializando variáveis

{% include imagelocal.html
    src="unreal/movimentacao/unreal-engine-plataform-init-variables.webp"
    alt="Figura: Inicializando variáveis do objeto plataforma."
    caption="Figura: Usamos TransformLocation para converter o vetor TargetLocation em uma localização relativa a do jogador. Por exemplo, se T fosse a transformação de um objeto, isso transformaria uma posição do espaço local para o espaço mundial."
%}

### 6.3. Evento Tick da plataforma

{% include imagelocal.html
    src="unreal/movimentacao/unreal-engine-plataform-movement-with-tick.webp"
    alt="Figura: Lógica de movimentação usando Tick. "
    caption="Calculo de distância da trajetória inicial e final."
%}

{% include imagelocal.html
    src="unreal/movimentacao/unreal-engine-plataform-movement-with-tick-continue.webp"
    alt="Figura: Lógica de movimentação usando Tick - continuação. "
    caption="Figura: Alterna os vetores quando o objeto chega no destino final."
%}

## 7. Usando o evento Tick com C++

Neste passo vamos repetir a lógica anterior mas agora usaremos C++.

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

## 8. Movimentação de Characters

Um personagem ou `Character` é um `Pawn` que possui algumas funcionalidades básicas de movimento bípede por padrão.

Para este exemplo vamos criar o objeto **BP_Hero** do tipo `Character` com as seguintes propriedades.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-character-properties.webp"
    alt="Figura: Character class and properties."
    caption="Figura: Em SpringArm habilite a opção Use Pawn Control Rotation para que a cápsula do personagem não acompanhe o movimento do mouse."
%}

Vamos adicionar e ajustar os componentes `SpringArm` e `Camera` para manipular a visualização do personagem em terceira pessoa.

`Capsule` - O `CapsuleComponent` é usado para colisão de movimento. Para calcular geometrias complicadas para o `CharacterMovementComponent`, supõe-se que o componente de colisão na classe Character seja uma cápsula orientada verticalmente.

`Arrow` - Um componente simples usado para indicar a direção do caminho do objeto.

`Skeletal Mesh` - Ao contrário dos `Pawn`, os Personagens vêm com um `SkeletalMeshComponent` para habilitar animações avançadas que usam um esqueleto. É possível adicionar outras `Skeletal Mesh` a classes derivadas de Personagens, mas esta é a `Skeletal Mesh` principal associada ao Personagem.

`Character Movement` - Permite que avatares que não usam física de corpo rígido se movam andando, correndo, pulando, voando, caindo e nadando. É específico para Personagens (`Characters`) e não pode ser implementado por nenhuma outra classe. As propriedades que podem ser definidas no `CharacterMovementComponent` incluem valores para atrito de queda e caminhada, velocidades de viagem pelo ar e água e pela terra, flutuabilidade, escala de gravidade e as forças físicas que o personagem pode exercer em objetos físicos. O CharacterMovementComponent também inclui parâmetros de movimento de raiz que vêm da animação e já estão transformados no espaço do mundo, prontos para uso pela física.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-character-skeletal-mesh.webp"
    alt="Figura: Inicializando variáveis do objeto plataforma."
    caption="Figura: Adicione e ajuste o componente Mesh para adicionar uma malha esquelética, no exemplo acima utilizamos o pacote ThirdPerson."
%}

### 8.1. Utilizando Enumeration para registro de poses do personagem

Podemos utilizar uma variável `Enumeration` para registrar os estados do objeto.

#### 8.1.1. Variável Enumeration

{% include imagelocal.html
    src="unreal/actor/unreal-engine-enum-state-char-basics.webp"
    alt="Figura: Enumeration e Estados do jogador."
    caption="Figura: Implemente a variável EN_State_Hero do tipo Enumeration, utilize o menu de contexto Blueprints > Enumerations."
%}

Adicione as linhas no objeto, `AddEnumerator`:

- Running - Correndo;

- Crouch - Agachado;

- Normal - Para o estado normal;

- Aiming - Mirando;

#### 8.1.2. Atualizando a variável com os eventos Jump e Crouch

{% include imagelocal.html
    src="unreal/actor/unreal-engine-enum-jump-crouch.webp"
    alt="Figura: Atualizando o estado do jogador utilizando Enumeration."
    caption="Figura: Atualizamos as variáveis Enumeration para o estado associado ao comando Input."
%}

`Input Action Crouch` - Este evento deve ser definido em `Project Settings` > `Input`, escolha a tecla `D` para este exemplo;

`Can crouch` - Habilite este parâmetro em `Character Movement` para possibilitar o personagem agachar.
