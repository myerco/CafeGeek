---
title: Delta time e sistema de coordenadas
description: Delta time e sistema de coordenadas
tags: [Unreal Engine,tempo, espaço]
categories: Unreal Engine
author: 
- Cafegeek
- KazeHiro1
layout: post
date: 2022-09-21 
---

## Índice

***

- [O que é Delta Time?](#o-que-é-delta-time)

- [Delta seconds](#delta-seconds)

- [Utilizando o Delta seconds com Event Tick](#utilizando-o-delta-seconds-com-event-tick)

- [Timeline](#timeline)

- [Acionando o evento para alterar a iluminação](#acionando-o-evento-para-alterar-a-iluminação)

- [Funções Blueprint para tratamento do Timeline](#funções-blueprint-para-tratamento-do-timeline)

- [Abrindo portas](#abrindo-portas)

- [Curves](#curves)

- [Exemplo de calculo de velocidade](#exemplo-de-calculo-de-velocidade)

- [Sistema de coordenadas](#sistema-de-coordenadas)

- [Verificando para onde o ator está apontando](#verificando-para-onde-o-ator-está-apontando)

- [Acompanhando o movimento de um objeto](#acompanhando-o-movimento-de-um-objeto)

***

Neste capítulo serão apresentados e implementados os elementos de controle de tempo (Delta Time) dentro do **Unreal Engine**, apresentaremos também funcionamento do sistema de coordenadas dos objetos.

## O que é Delta Time?

***

Delta Time é o tempo entre cada frame, onde um frame é um quadro ou imagem apresentada, uma animação é composta por vários frames.

|Time.deltafime = 0 |                                   |Tempo.DeltaTme = 0.05  | 
|:-:                |:-:                                |:-                     |
|Frame 1            |                                   |Frame 2                |
|                   | Tempo passado entre frames  é 0.05|                       |

Frame = 1

### Frames e Delta time

{% include imagebase.html
  src="unreal/tempoespaco/frame_walking.webp"
  alt="Figura: Walking Frame."
  caption="Figura: Vários quadros simulando uma animação."
%}

|       |   |   |   |   |   |   |   |   |   |   |
|:-:    |-  |-  |-  |-  |-  |-  |-  |-  |-  |-  |
|Frames | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10|
| Delta | 1 | 2 | 3 |4  | 5 | 6 | 7 | 8 | 9 |   |



Considerando a tabela acima podemos determinar o tempo em milissegundos de cada frame da seguinte forma:

- 10 Fps = 10 frames a cada segundo;

  - 1 segundo / 9 = 0,1 segundo ou 100ms;

- 100 FPS = 100 frames a cada segundo;

  - 1 segundo /99 = 0,01 segundo ou 10ms

- 30 FPS = 1/29 , 0.034 34ms;

- 60 FPS = 1/59 , 0.017 17ms;

### Utilizando comandos do console

O **Unereal Engine** permite visualizar e alterar os frames por segundo, *FPS*  utlizando o console de comandos *cmd*.

Para habilitar o console de comandos utilizamos `Menu` > `Project Settings` > `Engine Inputs` ou digitar na busca a palavra console, em seguida associe uma tecla ao console, o padrão é a tecla `´`.

{% include imagebase.html
  src="unreal/tempoespaco/unreal_engine_cmd_settings.webp"
  alt="Figura: Unreal Engine - Project Settings."
  caption="Figura: Unreal Engine - Project Settings configuração da tecla que acionará o comando para acessar o Console."
%}

Uma vez configurado podemos voltar para a tela principal ou `ViewPort` para acionar o console.

Pressione a tecla  `´`, configurada anteriormente, e o editor de comandos aparece na tela;

#### Apresentando o valor de FPS

{% include imagebase.html
  src="unreal/tempoespaco/unreal_engine_cmd_stat_fps.webp"
  alt="Figura: Unreal Engine - Project Cmd Stat fps."
  caption="Figura: Unreal Engine - Comando stat fps apresenta os valores do FPS atualizados."
%}

```bash
stat fps
```

#### Alterando o valor de FPS para 100

```bash
  t.MaxFPS 100
```

#### Exibindo informações de desempenho

```bash
stat unit
```

Valores:

- threads Frame;

- Game;

- Draw;

- GPU;

- RHIT;

- e DynRes do projeto.

> Para saber mais sobre cada elemento acesse o curso de Cafegeek > Computação Gráfica com Unreal Engine.

### Fornecendo feedback sobre quanto tempo os vários Ticks de jogo estão demorando

```bash
stat game
```

## Delta seconds

***

**Delta Seconds** é a quantidade de tempo decorrido desde o último evento `Tick`.

Ao multiplicar seu deslocamento por **Delta Seconds**, seu movimento será independente da taxa de quadros.

Por exemplo, seu peão tem uma velocidade máxima de 100. Se um segundo tivesse se passado desde o último tique de evento, seu peão moveria todas as 100 unidades. Se meio segundo tivesse passado, ele moveria 50 unidades.

### Tabela de velocidade

|Distância  | Velocidade  | Distância/Velocidade  |  FPS  | Delta Seconds | Y |
|:-:        |-            |-                      |-      |-              |-  |
|100        | 10          | 10                    | 100   | 0,1           | 1 |
|100        | 10          | 10                    | 60    | 0,166         |1,6|
|100        | 10          | 10                    | 30    | 0,333         | 3 |
|100        | 10          | 10                    | 20    | 0,5           | 5 |

`Delta seconds` - Intervalo entre os quadros;

`Y` - Deslocamento no eixo `Y`.

## Utilizando o Delta seconds com Event Tick

***

Para exemplificar vamos controlar o movimento do objeto independente do *FPS* utilizando o evento `Tick`.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_logic_simple.webp"
  alt="Figura: Blueprint - Event Tick com DeltaTime e SetWorldLocation."
  caption="Figura: Unreal Engine - Utilizamos GetWorldLocation e incrementamos o valor de Y a cada Tick para atualziar SetWordLocation, atualizando a posição do objeto."
%}

No exemplo acima se o *FPS* for um valor muito baixo o objeto vai se movimentar de forma lenta, por conseguinte percebemos que a movimentação será afetada pelo *FPS*.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_delta_seconds.webp"
  alt="Figura: Blueprint - Event Tick com DeltaTime e SetWorldLocation e calculando a velocidade"
  caption="Figura: Blueprint - Event Tick com DeltaTime e SetWorldLocation e calculando a velocidade"
%}

- *Distancia* - Valor = 1000;

- *Velocidade* - Valor = 10;

- O resultado esperado é que mesmo com um *FPS* baixo o movimento ainda se mantenha uniforme.

Quando multiplicamos o valor do `Delta Seconds` pela velocidade do objeto podemos ter um movimento mais fluido mesmo com valores de *FPS* baixos.

### Fixando o FPS do projeto

Podemos fixar o *FPS* do projeto utilizando o menu `Project settings` > `Use fixed frame rate`.  

{% include imagebase.html
  src="unreal/tempoespaco/unreal_engine_framerate_settings.webp"
  alt="Figura: Unreal Engine - General Settings Frame Rate"
  caption="Figura: Unreal Engine - Fixando FrameRate para todo o projeto"
%}

### Vídeo Delta time e sistema de coordenadas

{% include video.html
  link="https://youtu.be/gQdT8rah4CU"
  src="https://img.youtube.com/vi/gQdT8rah4CU/0.jpg"
  alt="Vídeo: Delta time e sistema de coordenadas  - Utilizando o Delta seconds 02  - Unreal Engine"
  caption="Vídeo: Delta time e sistema de coordenadas  - Utilizando o Delta seconds 02  - Unreal Engine."
%}

## Timeline

***

Os nós da linha de tempo são nós especiais dentro de **Blueprints** que permitem que uma animação simples baseada em tempo seja projetada e reproduzida rapidamente com base em eventos no jogo. As linhas do tempo são como sequências de matinê simples, pois permitem que valores simples sejam animados e que eventos sejam disparados ao longo do tempo.

Para adicionar um objeto Timeline utilizamos Click RMB no `Event Graph`, lógica do objeto, e no menu de contexto selecionamos `Add Timeline`.

{% include imagebase.html
  src="unreal/tempoespaco/unreal_engine_timeline_editor.webp"
  alt="Figura: Unreal Engine - Timeline Editor"
  caption="Figura: Unreal Engine - Timeline e a organização do editor de tempo."
%}

1. Parameters - Parâmetros do Timeline

2. Trilhas externas - Permite que você escolha uma curva externa no `Content Browser` em vez de criar sua própria curva.

3. Trilha do Timeline - Este é o gráfico de quadro-chave para esta trilha. Você colocará quadros-chave nisso e verá a curva de interpolação resultante.

### Entradas e Saídas

{% include imagebase.html
  src="unreal/tempoespaco/unreal_engine_timeline_object.webp"
  alt="Figura: Unreal Engine - Timeline Inputs and Outputs"
  caption="Figura: Unreal Engine - Entradas e Saídas do objeto TimeLine"
%}

`Play` -  Faz com que a Linha de tempo seja reproduzida a partir de sua hora atual.

`Play from start` -  Faz com que a linha de tempo seja reproduzida desde o início.

`Stop` - Congela a reprodução da Linha de tempo na hora atual.

`Reverse` - Reproduz a linha de tempo de trás para a hora atual.

`Reverse from End` - Reproduz a linha do tempo de trás para frente a partir do final.

`Set New Time` -  Define a hora atual para o valor definido (ou entrada) na entrada New Time.

`New Time` - Este pino de dados recebe um valor `float` representando o tempo em segundos, para o qual a Linha de tempo pode saltar quando a `Set New Time` é chamada.

### Parâmetros do TimeLine

`Length` - Permite definir a duração da reprodução para esta Linha de tempo.

`Use Last KeyFrame` - Se não estiver ativo, o último quadro-chave de uma sequência será ignorado. Isso pode ajudar a evitar pular quando uma animação está em loop.

`Autoplay` - Se ativo, este nó Timeline não requer uma entrada de execução para começar e começará a tocar assim que o nível começar.

`Loop` - Se estiver ativo, a animação da Linha de tempo será repetida indefinidamente, a menos que seja interrompida pelo pino de entrada Parar.

`Replicated` - Se ativo, a animação da Linha do tempo será replicada entre os clientes.

## Utilizando variáveis no Timeline

Para este exemplo vamos utilizar dois objetos, um objeto *Lamp* do tipo `Light Component`  para apresentar a estrutura de nó *TratamentoLuz* do tipo `TimeLine`, e outro objeto para controlar a *Lamp*, neste objeto utilizaremos um caixa de colisão.

A seguiur vamos criar o objeto *BP_ControlLight* do tipo `Box Trigger`.

{% include imagebase.html
  src="unreal/tempoespaco/unreal_engine_timeline_boxcolision.webp"
  alt="Figura: Blueprint - Box Trigger BP_ControlLight."
  caption="Figura: Blueprint - O objeto BP_ControlLight com seus componentes e variáveis."
%}

Em `BP_ControlLight` adicionamos a variável *Lampada* do tipo `PointLight` e a configuramos como publica, `Instance Editable`.

Adicionamos na cena um componente `PointLight`.

Em seguida adicionamos BP_ControlLight na cena e associamos o objeto `PointLight` na propriedade *Lamp*.

{% include imagebase.html
  src="unreal/tempoespaco/unreal_engine_timeline_variable.webp"
  alt="Figura: Blueprint - CollisionComponent e PointLight."
  caption="Figura: Componente BP_ControlLight associando a variável Lamp ao objeto na cena."
%}

Em *BP_ControlLight* adicionamos a seguinte lógica para tratamento de luz;

{% include imagebase.html
  src="unreal/tempoespaco/unreal_engine_timeline_logic.webp"
  alt="Figura: Blueprint - Lógica para tratamento da luz utilizando Set Light Color, Set Intensity e TimeLine."
  caption="Figura: Blueprint - Lógica para tratamento da luz utilizando Set Light Color, Set Intensity e TimeLine."
%}

A seguir vamos detalhar cada nó da lógica acima.

### Tipos de variáveis do objeto TimeLine

O Editor do TimeLine é um gráfico de tempo e valor, onde a linha horizontal representa os valores do tempo e a linha vertical a variação da variável.

O gráfico utiliza os tipos de dados: `Float`, `Vector`, `Event` e `Color`.

{% include imagebase.html
  src="unreal/tempoespaco/unreal_engine_timeline_type_variables.webp"
  alt="Figura: Blueprint - Variáveis do objeto Timeline."
  caption="Figura: Blueprint - Variáveis do objeto Timeline."
%}

#### FloatVariavel

Tipo `float` controla a intensidade da luz durante o tempo 1.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_float.webp"
  alt="Figura:   Blueprint - Exemplo de variável float do DeltaTime."
  caption="Figura:   Blueprint - Exemplo de variável float do DeltaTime."
%}

A seguir vamos criar variáveis para exemplicar cada tipo.

#### VetorVariavel

Tipo `Vector` altera o valor das coordenadas durante o tempo 4.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_vector.webp"
  alt="Figura:   Blueprint - Exemplo de variável Vector do DeltaTime."
  caption="Figura:   Blueprint - Exemplo de variável Vector do DeltaTime"
%}

#### CorVariavel

Tipo `color` altera as cores da luz conforme o tempo passa.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_color.webp"
  alt="Figura: Blueprint - Exemplo de variável Color do DeltaTime."
  caption="Figura: Blueprint - Exemplo de variável Color do DeltaTime."
%}

#### EventoVariavel

Tipo `Event` dispara um evento no tempo 2,4 e 6.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_event.webp"
  alt="Figura: Blueprint - Exemplo de um evento do DeltaTime."
  caption="Figura: Blueprint - Exemplo de variável Color do DeltaTime."
%}

## Acionando o evento para alterar a iluminação

***

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_call_event.webp"
  alt="Figura: Blueprint - Exemplo da lógica para alterar a iluminação."
  caption="Figura: Blueprint - Exemplo de variável Color do DeltaTime."
%}

## Funções Blueprint para tratamento do Timeline

- `SetLooping`;

- `SetTimeLength`;

- `GetTimeLength`;

- `GetPlaybackPosition`;

- `Auto play`;

- `Ignore time dilation`;

- `Set timer by event e clear timer`;

- `SetTimerbyEvent`;

- `ClearAndInvalidateTimerByHandle`;

- `SetTimerbyFunction`;

### Vídeo Delta time e sistema de coordenadas  - Timeline  03 Float

{% include video.html
  link="https://youtu.be/qOUYp-XWUtw"
  src="https://img.youtube.com/vi/qOUYp-XWUtw/0.jpg"
  alt="Vídeo: Delta time e sistema de coordenadas  - Timeline  03  Float - Unreal Engine."
  caption="Vídeo: Delta time e sistema de coordenadas  - Timeline  03  Float - Unreal Engine."
%}

### Vídeo Delta time e sistema de coordenadas  - Timeline  04 Color

{% include video.html
  link="https://youtu.be/EJQwXxjiS58"
  src="https://img.youtube.com/vi/EJQwXxjiS58/0.jpg"
  alt="Vídeo: Delta time e sistema de coordenadas  - Timeline  04  Color - Unreal Engine."
  caption="Vídeo: Delta time e sistema de coordenadas  - Timeline  04  Color - Unreal Engine."
%}

### Vídeo Delta time e sistema de coordenadas  - Timeline  05 Event

{% include video.html
  link="https://youtu.be/YkvP6tMMly0"
  src="https://img.youtube.com/vi/YkvP6tMMly0/0.jpg"
  alt="Vídeo: Delta time e sistema de coordenadas  - Timeline  05 Event - Unreal Engine."
  caption="Vídeo: Delta time e sistema de coordenadas  - Timeline  05 Event - Unreal Engine."
%}

### Vídeo Delta time e sistema de coordenadas  - Timeline  06 Vector

{% include video.html
  link="https://youtu.be/w5VpoM95B-Q"
  src="https://img.youtube.com/vi/w5VpoM95B-Q/0.jpg"
  alt="Vídeo: Delta time e sistema de coordenadas  - Timeline  06  Vector - Unreal Engine."
  caption="Vídeo: Delta time e sistema de coordenadas  - Timeline  06  Vector - Unreal Engine."
%}

## Abrindo portas

***

Nos exemplos a seguir vamos movimentar um objeto para simular a movimentação de abertura de uma porta de duas formas, deslizando e girando.  

### Deslizando a porta

Neste exemplo vamos implementar um movimento no eixo Y de abertura de uma porta.

Adicionando o elemento Movimentando `TimeLine` e alerando a posição do objeto.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_movement.webp"
  alt="Figura: Blueprint - Exemploo de movimentação deslizando a porta."
  caption="Figura: Blueprint - Exemplo de movimentação deslizando a porta."
%}

*Movimentando* utiliza a variável Movimento do tipo `Vector`. Somente o valor de Y é alterado.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_movement_vector.webp"
  alt="Figura: Blueprint - Exemplo de movimentação com vector somente com o eixo Y."
  caption="Figura: Blueprint - Exemplo de movimentação com vector somente com o eixo Y."
%}

Salvamos a posição inicial do objeto.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_save_pos.webp"
  alt="Figura: Blueprint - Salvando a posição de um objeto em um vetor."
  caption="Figura: Blueprint - Salvando a posição de um objeto em um vetor."
%}

### Girando a porta

Neste exemplo vamos implementar um movimento no eixo Z, girando e abrindo a porta.

Utilizamos a função `MakeRotator`.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_makerotator.webp"
  alt="Figura: Blueprint - Exemplo de movimentação girando a porta utilizando Make Rotator."
  caption="Figura: Blueprint - Exemplo de movimentação girando a porta utilizando Make Rotator."
%}

Movimentando utiliza a variável *Angulo* do tipo `Vector`.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_vector_angle.webp"
  alt="Figura: Blueprint - Exemplo de movimentação utilizando ângulo de abertura."
  caption="Figura: Blueprint - Exemplo de movimentação utilizando ângulo de abertura."
%}

### Girando a porta utilizando C++

LearpDoor.h

```cpp
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "Components/BoxComponent.h"
#include "LerpDoor.generated.h"

UCLASS()
class TCMCPP_API ALerpDoor : public AActor
{
  GENERATED_BODY()
public:

  ALerpDoor();

protected:
  virtual void BeginPlay() override;

public:
  virtual void Tick(float DeltaTime) override;

  UPROPERTY(EditAnyWhere)
  UStaticMeshComponent* MyDoor;

  UPROPERTY(EditAnywhere)
  UBoxComponent* BoxComp;

  UFUNCTION()
    void OnOverlapBegin(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult);
  
  UFUNCTION()
  void OnOverlapEnd(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex);

  bool Open;
  float RotateValue;
  FRotator DoorRotation;
};
```

LearpDoor.cpp

```cpp
#include "LerpDoor.h"
#include "Kismet/KismetMathLibrary.h"
#include "Components/BoxComponent.h"

ALerpDoor::ALerpDoor()
{
  PrimaryActorTick.bCanEverTick = true;

  Open = false;

  BoxComp = CreateDefaultSubobject<UBoxComponent>(TEXT("My Box"));
  BoxComp->InitBoxExtent(FVector(50.0f, 50.0f, 50.0f));
  RootComponent = BoxComp;

  MyDoor = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("My Door"));
  MyDoor->SetRelativeLocation(FVector(0.0f, 50.0f, -50.0f));
  MyDoor->SetupAttachment(RootComponent);

  BoxComp->OnComponentBeginOverlap.AddDynamic(this, &ALerpDoor::OnOverlapBegin);
  BoxComp->OnComponentEndOverlap.AddDynamic(this, &ALerpDoor::OnOverlapEnd);
}

void ALerpDoor::BeginPlay()
{
  Super::BeginPlay();
}

void ALerpDoor::Tick(float DeltaTime)
{
  Super::Tick(DeltaTime);

  DoorRotation = MyDoor->GetRelativeRotation();

  if (Open)
  {
    MyDoor->SetRelativeRotation(FMath::Lerp(FQuat(DoorRotation), FQuat(FRotator(0.0f, RotateValue, 0.0f)),0.01));
  }
  else
  {
    MyDoor->SetRelativeRotation(FMath::Lerp(FQuat(DoorRotation), FQuat(FRotator(0.0f, 0.0f, 0.0f)), 0.01));
  }
}

void ALerpDoor::OnOverlapBegin(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult)
{

  if ((OtherActor != nullptr) && (OtherActor!= this) && (OtherComp != nullptr))
  {
    FVector PawnLocation = OtherActor->GetActorLocation();
    FVector Direction = GetActorLocation() - PawnLocation;
    Direction = UKismetMathLibrary::LessLess_VectorRotator(Direction, GetActorRotation());
    if (Direction.X > 0.0f)
    {
      RotateValue = 90.0f;
    }
    else
    {
      RotateValue = -90.0f;
    }
    Open = true;
}
}

void ALerpDoor::OnOverlapEnd(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex)
{
  if ((OtherActor != nullptr) && (OtherActor != this) && (OtherComp != nullptr))
  {
    Open = false;
  }

}
```

Acionando a porta.
  
{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_open_door.webp"
  alt="Figura: Blueprint - Exemplo de abertura da porta utilizando CollisionComponent."
  caption="Figura: Blueprint - Exemplo de abertura da porta utilizando CollisionComponent."
%}  

## Curves

***

Podemos criar um tipo de objeto `Curve` para que possamos utilizar em vários Blueprints e determinar a variação dos valores.

Para criar um objeto do tipo `Curve` utilizamos o menu de contexto `Miscellaneous` > `Curve`.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_menu_curve.webp"
  alt="Figura: Blueprint - Menu de contexto Miscellaneous > Curve."
  caption="Figura: Blueprint - Menu de contexto Miscellaneous > Curve."
%}  

Criando o Objeto C_TempoPorta.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_icon_curve.webp"
  alt="Figura: Blueprint - Objeto C_TempoPorta."
  caption="Figura: Blueprint - Objeto C_TempoPorta."
%}  

Associando o objeto C_TempoPorta ao objeto Movimentando.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_timeline_curve.webp"
  alt="Figura: Blueprint - Associando a curva ao Timeline."
  caption="Figura: Blueprint - Associando a curva ao Timeline."
%}  

- `SetVectorCurve`;

## Exemplo de calculo de velocidade

***

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_velocity_exemple.webp"
  alt="Figura: Blueprint - Exemplo da lógica de calculo de velocidade."
  caption="Figura: Blueprint - Exemplo da lógica de calculo de velocidade."
%}  

## Sistema de coordenadas

***

O sistema de coordenadas descreve uma maneira de usar números para especificar a localização de um ponto (ou pontos) no espaço 2D ou 3D. Em um motor de jogo, é função do sistema de coordenadas define a localização de cada objeto e para qual **direção** ele está voltado. Com esses dados podemos calcular a distância entre objetos, rotação, velocidade e todos os tipos de outras informações úteis.

### Plano Cartesiano

Para demonstrar vamos utilizar um vetor de 2D (x,y).

|  |  |  |  |  | (Y) |  |  |  |  |  ||
|:-:|-|-|-|-|-|-|-|-|-|-|-|
|  |  |  |  |  |  **5**|  |  |  | D |  ||
|  |  |  |  |  |  **4**|  |  |  |  |  ||
|  |  |  | B |  |  **3**|  |  |  |  |  ||
|  |  |  |  |  | **2** |  |  | C |  |  ||
| |  |  |  |  | **1** |  |  |  |  |  |  |
|**-5** | **-4** | **-3** | **-2** | **-1** | **0** |  **1** | **2** |**3**  |**4**  | **5** |  **(X)**|
|  |  |  |  |  | **-1** |  |  |  |  |  |  |
| |  |  |  |  | **-2** |  |  |  |  |  |  |
|  |  |  |  |  | **-3** |  |  |  |  |  ||
|  | A |  |  |  | **-4** |  |  |  |  |  ||
|  |  |  |  |  | **-5** |  |  |  |  |  ||

### Posição dos elementos

Consideramos o posição dos objetos com a seguinte expressão *v = v(x,y)*, por consequinte os valores para A,B,C e D são:

- A = a(-4,-4)

- B = b(-2,3)

- C = b(3,2)

- D = b(4,5)

### Movimento no sistema coordenadas X,Y

Uma direção nos diz como nos mover no sistema de coordenadas x, y. Um valor positivo nos diz para nos movermos na direção positiva e um valor negativo nos diz para nos movermos na direção negativa (com base no sistema de coordenadas).

### Movimentando o elemento B

- B = b(-2,3) **->** b(-1,4)

### Magnitude

A Magnitude nos diz o quanto nos movemos. A distância de um movimento provará ser muito útil e pode ser calculada apenas com o vetor. Isso é feito usando o Teorema de Pitágoras.

Assuma um objeto na posição (50, 25) e queremos movê-lo para (53, 23). Isso significa um Vetor de (3, -2).

- A = a(-4,-4) **->** a(2,-1)  
  O objeto se deslocou de (-4,-4) até a nova posição (2,1)  
  Andou 6 posições em X e 5 em Y

- Direção de A = (6,5)  

- Distância percorrida = raiz_quadrada(6 ^ *2* + 5 ^*2*) = **7.8**

> Você pode usar isso para calcular novas posições e movimentos. Suponha que você tenha um objeto na posição (12, 4) e deseja movê-lo na direção (3,2), mas deseja que a distância seja 4 vezes a distância normal. Para fazer isso funcionar e obter a nova posição, você multiplica o vetor pelo escalar V = (3*4,2*4) (12,8) A nova posição no sistema de coordenadas x / y é obtida adicionando este vetor para a posição original: (12 + 12, 4 + 8) (24, 12)

### Normalização

Aprendemos que um vetor é um par de números que contém uma direção e que pode ser usado para derivar uma magnitude. Quando um vetor contém um par de números, como (10, 5), ele indica que o movimento será de 10 unidades na direção X positiva e 5 unidades na direção Y positiva. Este vetor especifica quantas unidades mover, mas também indica uma direção geral em porcentagens. Essa é a proporção de movimento de 10 por 5. O cálculo dessa porcentagem de movimento é chamado de Normalização de um vetor.  
O vetor normalizado é um par de números, cada um deles menor que um. Você pode criar um vetor normalizado obtendo a magnitude de um vetor e dividindo cada valor do Vetor pela magnitude. Com um vetor de (3,4) a magnitude é 5.

- 5 = raiz_quadrada(3 ^ *2* + 4 ^*2*)

- (.6,.8) = (3/5, 4/5)

*Resultado.*

O vetor normalizado das coordenadas (3,4) é (-.6,.8).

#### Calculando distância

Usando a função `GetActorLocation` podemos determinar a distância entre dois objetos, no exemplo a segueir vamos calcular a distância dos objetos Cube e Cube2 .

- **Cube**  

  **a**=GetActorLocation(0,-600,70)

- **Cube2**  

  **b**=GetActorLocation(600,600,70)

- **Resultado**  

  Resultado =  a - b
  > (600,1200,0)  

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_distancia_com_vetores.webp"
  alt="Figura: Blueprint - Exemplo de lógica para calculo da distância de dois objetos."
  caption="Figura: Blueprint - Exemplo de lógica para calculo da distância de dois objetos."
%}  

### VectorLength

Calcula o comprimento do vetor, onde Comprimento = VectorLength(Resultado) (1341.64078);

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_vector_lenght.webp"
  alt="Figura: Blueprint - Exemplo de VectorLength."
  caption="Figura: Blueprint - Exemplo de VectorLength."
%}  

### GetDistanceTo

Calcula a distância de dois objetos, onde Distancia = GetDistanceTo(Cubo,Cubo2) (1341.64078);

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_getdistanceto.webp"
  alt="Figura: Blueprint - Exemplo de GetDistanceTo."
  caption="Figura: Blueprint - Exemplo de GetDistanceTo."
%}  
  
### Normalize  

**a** = Cubo.GetActorLocation(0,-600,70)

Resultado = Normalize(**a**,0)

> (0,0.99,0.16)
>
> Os valores variam entre 0 e 1.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_normalize.webp"
  alt="Figura: Blueprint - Exemplo de Normalize."
  caption="Figura: Blueprint - Exemplo de Normalize."
%}  

## Verificando para onde o ator está apontando

***

Usaremos várias funções para verificar a direção que o ator está apontando.

- `GetActorForwardVector`

  **a** = Cubo.GetActorForwardVector()
  > 1,0,0

- `GetActorUpVector`  
    **a** = Cubo.GetActorUpVector()
    > 0,0,1

- `GetActorRightVector`  
  **a** = Cubo.GetActorRightVector()
  > 0,1,0

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_forward_up_right_vector.webp"
  alt="Figura: Blueprint - Exemplo de GetActorForwardVector para definir onde o ator esta apontando."
  caption="Figura: Blueprint - Exemplo de GetActorForwardVector para definir onde o ator esta apontando."
%}  

## Acompanhando o movimento de um objeto

***

Usaremos a função `FindLookAtRotation` para que um objeto se movimente no seu próprio eixo baseado na posição de outro objeto, no exemplo o **Cubo3** do tipo `Character` vai *apontar* para a face de outro objeto.

{% include imagebase.html
  src="unreal/tempoespaco/blueprint_find_look_rotation.webp"
  alt="Figura: Blueprint - Exemplo de FindLookAtRotation."
  caption="Figura: Blueprint - Exemplo de FindLookAtRotation."
%}
