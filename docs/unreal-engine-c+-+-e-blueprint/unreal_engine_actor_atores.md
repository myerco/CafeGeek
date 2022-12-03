---
title: Implementado Atores com Unreal Engine
description: Neste capitulo serão apresentados e implementados os atores *Actors* do seu projetos.
tags: [Unreal Engine,actor,atores]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
date: 2022-09-21 
---

***

- [O que são Actors?](#o-que-são-actors)
- [O que são Classes?](#o-que-são-classes)
  - [Exemplo de implementação utilizando C++](#exemplo-de-implementação-utilizando-c)
  - [Exemplo de implementação em Blueprint](#exemplo-de-implementação-em-blueprint)
  - [Utilizando classes com Blueprint](#utilizando-classes-com-blueprint)
- [Classe Actor](#classe-actor)
- [Classe Actor em C++ com uma Static Mesh](#classe-actor-em-c-com-uma-static-mesh)
  - [Arquivo CharacterBase.h](#arquivo-characterbaseh)
  - [Arquivo CharacterBase.cpp](#arquivo-characterbasecpp)
- [Classe Pawn](#classe-pawn)
- [Classe Character](#classe-character)
- [Componentes e Actors](#componentes-e-actors)
  - [Adicionando componentes](#adicionando-componentes)
  - [Static Mesh - Malhas estáticas](#static-mesh---malhas-estáticas)
  - [Componente StaticMesh](#componente-staticmesh)
  - [Propriedades do componente Static Mesh](#propriedades-do-componente-static-mesh)
  - [Skeletal Mesh - Malha Esquelética](#skeletal-mesh---malha-esquelética)
  - [A Estrutura](#a-estrutura)
  - [Componentes Mesh](#componentes-mesh)
  - [Detalhes do componente Mesh](#detalhes-do-componente-mesh)
- [O Editor Skeletal Mesh](#o-editor-skeletal-mesh)
- [Posição e coordenadas](#posição-e-coordenadas)
  - [Transform](#transform)
  - [Escrevendo na tela o posicionamento do ator no mundo](#escrevendo-na-tela-o-posicionamento-do-ator-no-mundo)
  - [Posição relativa no mundo](#posição-relativa-no-mundo)
  - [Escrevendo na tela o posição relativa do componente](#escrevendo-na-tela-o-posição-relativa-do-componente)
- [Trabalhando com herança com Blueprint](#trabalhando-com-herança-com-blueprint)
  - [Componente *ChildActor* implementa a ligação com outro ator](#componente-childactor-implementa-a-ligação-com-outro-ator)
  - [Herança de propriedades e métodos](#herança-de-propriedades-e-métodos)
  - [Referências de atores e componentes](#referências-de-atores-e-componentes)
- [Polimorfismo em C++](#polimorfismo-em-c)
- [Funções virtuais](#funções-virtuais)
  - [Exemplo de função virtual em C++ com Unreal Engine](#exemplo-de-função-virtual-em-c-com-unreal-engine)
  - [Exemplo de função virtual no C++](#exemplo-de-função-virtual-no-c)
- [Manipulando Actors](#manipulando-actors)
  - [Spawn e Destroy Actors - Criando e destruindo um Actor](#spawn-e-destroy-actors---criando-e-destruindo-um-actor)
  - [Listando Actors por classe](#listando-actors-por-classe)
  - [Listando Actors utilizando *tag* (etiquetas)](#listando-actors-utilizando-tag-etiquetas)
- [Colisões](#colisões)
  - [Trace Responses](#trace-responses)
  - [Interações](#interações)
  - [Exemplo de Colisão](#exemplo-de-colisão)
  - [Configuração de colisão de esfera](#configuração-de-colisão-de-esfera)
  - [Configuração de colisão de parede](#configuração-de-colisão-de-parede)
  - [Colisão e Simulação Geram Eventos de toque ou acerto](#colisão-e-simulação-geram-eventos-de-toque-ou-acerto)
  - [Configuração de colisão de esfera 1](#configuração-de-colisão-de-esfera-1)
  - [Configuração de colisão de parede 1](#configuração-de-colisão-de-parede-1)
  - [Sobrepor e ignorar](#sobrepor-e-ignorar)
  - [Configuração das propriedades de colisão de esfera](#configuração-das-propriedades-de-colisão-de-esfera)
  - [Configuração das propriedades colisão de parede](#configuração-das-propriedades-colisão-de-parede)
  - [Configuração das propriedades da colisão de esfera](#configuração-das-propriedades-da-colisão-de-esfera)
  - [Configuração das propriedades de colisão de parede](#configuração-das-propriedades-de-colisão-de-parede)
  - [Sobrepor e gerar eventos de sobreposição](#sobrepor-e-gerar-eventos-de-sobreposição)
  - [Colisão de esfera](#colisão-de-esfera)
  - [Colisão de parede](#colisão-de-parede)
  - [Colisão Simples versus Complexa](#colisão-simples-versus-complexa)
  - [Como usar](#como-usar)

***

Um ator é qualquer objeto que pode ser colocado em um nível, é uma classe de básica de objetos do **Unreal Engine**, neste capitulo serão apresentados e implementados os atores *Actors* do seu projeto.

## O que são Actors?

***

**Actors** ou Atores são uma classe genérica que oferece suporte a transformações 3D, como translação, rotação e escala. Atores podem ser criados (gerados) e destruídos por meio de código de jogo (**C++**  ou **Blueprints**). Em **C ++**, **AActor** é a classe base de todos os atores.

É composto por Atributos, componentes, eventos e permitem Herança.
Para entender melhor devemos conceituar e entender o que são classes.

## O que são Classes?

***

Classes são estruturas de dados que constituem a programação orientada a objetos. Contém seus próprios membros de dados e funções e podem ser acessados e usados criando uma instância de classe.

Classes determinam como os objetos serão quando criados.

Um objeto é uma instância de uma classe. Quando uma classe é definida, nenhuma memória é alocada, mas quando ela é instanciada (ou seja, um objeto é criado), a memória é alocada.

Abaixo vamos apresentar a estrutura hierarquia de classes.

```bash
|-- UObject C++
    |-- Actor C++
    |   |-- Pawn
    |   |   |-- Character
    |   |-- GameMode
    |   |-- GameController
    |   |   |-- PlayerController
    |   |   |-- IAController
|-- UObject C++
    |-- Actor BP
    |   |-- Pawn BP
    |   |   |-- Character BP
    |-- GameController BP
```

### Exemplo de implementação utilizando C++

```cpp
class Hero
{
    int iLife=100;

    void SendMessage()
    {
        std::cout << "Message in a Bottle";
    }
};
```

### Exemplo de implementação em Blueprint

Em **Blueprint** podemos obter os seguintes grupos de classes de atores:

- Actor;

- Pawn ;

- Character;

### Utilizando classes com Blueprint

Como citado anteriormente classes são estruturas de dados com eventos, variáveis e componentes.

Para criar uma classe utilizando **Blueprint** acesse o menu de contexto e selecione `Blueprint Class`.

{% include imagebase.html
    src="unreal/actor/blueprint_pick_class_resume.webp"
    alt="Figura: Pick Parent Class."
    caption="Figura: Pick Parent Class."
%}

## Classe Actor

***

A classe **Actor** compreende objetos básicos que podem ser adicionados a o mundo.  

{% include imagebase.html
    src="unreal/actor/blueprint_class_actor.webp"
    alt="Figura: Class Actor Details."
    caption="Figura: Class Actor Details."
%}

- `Parent Class` : Classe pai de Actor (Classe **C++**).

## Classe Actor em C++ com uma Static Mesh

***

### Arquivo CharacterBase.h

```cpp
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CharacterBase.generated.h"

UCLASS(Blueprintable)
class AULACPPV1_API ACharacterBase : public AActor
{
    GENERATED_BODY()

public:
    // Sets default values for this actor's properties
    ACharacterBase();

    /* Configurando propriedade para adicionar uma Static Mesh */
    UPROPERTY(VisibleAnywhere)
        UStaticMeshComponent* MeshMain;

protected:
    // Called when the game starts or when spawned
    virtual void BeginPlay() override;

public:
    // Called every frame
    virtual void Tick(float DeltaTime) override;

};
```

### Arquivo CharacterBase.cpp

```cpp
#include "CharacterBase.h"

// Sets default values
ACharacterBase::ACharacterBase()
{
    // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
    PrimaryActorTick.bCanEverTick = true;

    /*Construindo a malha na memória
    - CreateDefaultSubobject - Cria um componente ou subobjeto, permitindo criar uma classe filho e retornando a classe pai.
    Os objetos recém-iniciados podem ter alguns de seus valores padrão inicializados, mas o Mesh começará vazio.
    Você terá que carregar o malha mais tarde.
    */
    MeshMain = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh Main"));

    /*
    * ConstructorHelpers - No construtor, inicializamos os componentes e, em seguida, definimos seus valores usando FObjectFinder.
    Também configuramos a classe para gerar usando a função StaticClass para recuperar uma instância UStatic* de um tipo de classe.
    */
    static ConstructorHelpers::FObjectFinder<UStaticMesh> SphereVisualAsset(TEXT("/Game/ExampleContent/StarterContent/Shapes/Shape_Sphere.Shape_Sphere"));

    if (SphereVisualAsset.Succeeded()) {
        MeshMain->SetStaticMesh(SphereVisualAsset.Object);
        MeshMain->SetRelativeLocation(FVector(0.0f, 0.0f, -100.0f));
        MeshMain->SetWorldScale3D(FVector(0.8f));

    }
    MeshMain->SetupAttachment(RootComponent);
}

void ACharacterBase::BeginPlay()
{
    Super::BeginPlay();

    UE_LOG(LogTemp, Warning, TEXT("Teste 123..."));

}

void ACharacterBase::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);

}
```

## Classe Pawn

***

A classe **Pawn** ou peão é a classe base de todos os atores que podem ser controlados por jogadores ou IA. Um peão é a representação física de um jogador ou entidade de IA dentro do mundo. Isso não significa apenas que o peão determina a aparência visual do jogador ou entidade de IA, mas também como ele interage com o mundo em termos de colisões e outros aspectos físicos

>Isso pode ser confuso em certas circunstâncias, pois alguns tipos de jogos podem não ter uma malha de jogador ou avatar visível dentro do jogo. Independentemente disso, o peão, *pawn*, ainda representa a localização física, rotação, etc. de um jogador ou entidade dentro do jogo. Um personagem é um tipo especial de peão que tem a capacidade de andar.  

`Default Pawn`  

Enquanto a classe *Pawn* fornece apenas o essencial para a criação de uma representação física de um jogador ou entidade de IA no mundo, a subclasse `DefaultPawn` vem com alguns componentes e funcionalidades adicionais.

A classe `DefaultPawn` contém um componente `DefaultPawnMovementComponent` nativo, um `CollisionComponent` esférico e um `StaticMeshComponent`.

Para controlar o `DefaultPawnMovementComponent`, bem como a câmera, uma propriedade do tipo *Booleano* para adicionar ligações de movimento padrão também está presente na classe `DefaultPawn` e é definido como verdadeiro por padrão.

`Spectator Pawn`  

A classe `SpectatorPawn` é uma subclasse de `DefaultPawn`. Por meio de um **GameMode**, diferentes classes podem ser especificadas como padrões para *Pawn* e `SpectatorPawn`, e esta classe fornece uma estrutura simples ideal para a funcionalidade de espectador.

As Classes tem propriedades que definem a estrutura do objeto.

{% include imagebase.html
    src="unreal/actor/blueprint_class_properties.webp"
    alt="Figura: Details Class e estrutura."
    caption="Figura: Details Class e estrutura"
%}

- `Start with Tick Enabled` - Habilita o evento Tick na lógica. Pode ser desabilitado para ganhar performance;

- `Use Controller Rotation Pitch/Yaw` - Pode usar movimentação dos controladores;

- `Auto Possess Player/AI` - Faz com o **PlayerController** possua automaticamente o peão (*Pawn*);

- `Replication` : Opções para replicar o objeto pela rede.

- `Can be Damaged` : Habilita os eventos de dano do objeto.

{% include imagebase.html
    src="unreal/actor/blueprint_class_properties_damaged.webp"
    alt="Figura: Propriedade Collision."
    caption="Figura: Propriedade Collision."
%}

## Classe Character

***

Um personagem é um *Pawn* que tem algumas funcionalidades básicas de movimento bípede por padrão.  
Com a adição de um componente `CharacterMovementComponent`, um `CapsuleComponent` e um `SkeletalMeshComponent`, a classe *Pawn* é estendida para a classe *Character* com muitos recursos. Um personagem é projetado para uma representação do jogador orientada verticalmente que pode andar, correr, pular, voar e nadar pelo mundo. Esta classe também contém implementações de rede básica e modelos de entrada.

{% include imagebase.html
    src="unreal/actor/blueprint_character_properties.webp"
    alt="Figura: Classe Character Details."
    caption="Figura: Classe Character Details."
%}

- `Animation Mode` - Habilita uma animação simples ou um **Blueprint** de animação ao objeto;

- `Anim Class` - Blueprint de animação associado.

## Componentes e Actors

***

Os componentes são um tipo especial de objeto que os atores podem anexar a si próprios como subobjetos. Os componentes são úteis para compartilhar comportamentos comuns, como a capacidade de exibir uma representação visual e reproduzir sons. Eles também podem representar conceitos específicos do projeto, como a maneira como um veículo interpreta a entrada e muda sua própria velocidade e orientação. Por exemplo, um projeto com carros, aeronaves e barcos controláveis pelo usuário pode implementar as diferenças no controle e movimento do veículo, alterando qual componente um ator do veículo usa.

### Adicionando componentes

Na aba `Components`s podemos adicionar componentes para os objetos de forma hierarquia.

{% include imagebase.html
    src="unreal/movimentacao/blueprint_add_component_box.webp"
    alt="Figura: Blueprint Add Component."
    caption="Figura: Blueprint Add Component."
%}

Exemplo de Componentes que podemos adicionar a classe:  

- `Actor Child` - Componente associa outro ator a classe principal.

- `Static Mesh` - Adiciona um objeto de 3D;

- `Box Collsion` - Adiciona uma caixa de colisão;

Para editar os componentes utilizamos o Editor de objetos e componentes.

{% include imagebase.html
    src="unreal/actor/blueprint_view_components_objects.webp"
    alt="Figura: Editando componentes."
    caption="Figura: Editando componentes."
%}

### Static Mesh - Malhas estáticas

**Static Mesh** são a unidade básica usada para criar a geometria do mundo para níveis (*level*) criados no **Unreal Engine**. A grande maioria de qualquer mapa em um jogo feito com **Unreal** consistirá em Malhas Estáticas, geralmente na forma de Atores de Malha Estática.

Consistem em um conjunto de polígonos que podem ser armazenados em cache na memória de vídeo e renderizados pela placa de vídeo. Isso permite que eles sejam renderizados com eficiência, o que significa que podem ser muito mais complexos do que outros tipos de geometria, como **Brushes**. Como são armazenados em cache na memória de vídeo, as malhas estáticas podem ser traduzidas, giradas e dimensionadas, mas não podem ter seus vértices animados de nenhuma forma.

{% include imagebase.html
    src="unreal/movimentacao/blueprint_class_viewport.webp"
    alt="Figura: Statis Mesh ViewPort."
    caption="Figura: Statis Mesh ViewPort."
%}

### Componente StaticMesh

A aba `Components` apresenta uma lista hierarquia com os componentes associados ao objeto.

{% include imagebase.html
    src="unreal/movimentacao/blueprint_component_static_mesh.webp"
    alt="Figura: Componentes hierarquia."
    caption="Figura: Componentes hierarquia."
%}

### Propriedades do componente Static Mesh

{% include imagebase.html
    src="unreal/movimentacao/blueprint_component_properties.webp"
    alt="Figura: Propriedades do componente."
    caption="Figura: Propriedades do componente."
%}

- `Transform` - Propriedades de localização do componente;

- `Static Mesh` - Malha associada ao componente;

- `Material` - Material associado a malha;

- `Simulate Physcis` - Habilita a simulação de física do objeto.

**Editor de StaticMesh.**

Visualização da malha e suas propriedades (vértices, UV e modelo de colisão).

{% include imagebase.html
    src="unreal/movimentacao/blueprint_editor_static_mesh.webp"
    alt="Figura: Editor de StaticMesh."
    caption="Figura: Editor de StaticMesh."
%}

### Skeletal Mesh - Malha Esquelética

As **Skeletal mesh** são compostas por duas partes: Um conjunto de polígonos compostos para formar a superfície da Malha Esquelética e um conjunto hierárquico de ossos interconectados que podem ser usados para animar os vértices dos polígonos. **Skeletal mesh** são frequentemente usados no **Unreal Engine 4** para representar personagens ou outros objetos animados.

### A Estrutura

A baixo uma representação da hierarquia do Skeletal Mesh.

```bash
|-- Ator
    |-- Skeletal mesh
    |   |-- Mesh
    |   |-- Animation
    |   |-- Skeleton
    |   |-- Blueprint
    |   |-- Physics
    |-- Animation mode
    |   |-- Use Animation Bluprint
    |-- Anim Class
    |   |-- ThirdPerson_AnimBP_C
```

- `Mesh` - Malha do elemento;

- `Animation` - Animações associadas ao esqueleto;

- `Skeleton` - Estrutura de coordenadas alinhadas para marcar os ossos dos elementos;

- `Bluprint` - Lógica para sequenciamento de animações;

- `Physics` - Estrutura para gerenciamento da física da estruturas.

### Componentes Mesh

{% include imagebase.html
    src="unreal/movimentacao/blueprint_component_mesh.webp"
    alt="Figura: Bluprint Component Mesh."
    caption="Figura: Bluprint Component Mesh."
%}

- `Mesh` - Malha Esquelética;

- `CameraBoom` - Objeto do tipo `SpringArm` (Braço) para controlar a câmera;

- `FollowCamera` - Objeto do tipo `Camera`;

- `CharacterMovement` - Componente responsável pela lógica de movimentos do objeto.

### Detalhes do componente Mesh

{% include imagebase.html
    src="unreal/movimentacao/blueprint_component_mesh_details.webp"
    alt="Figura: Detalhes do componente Mesh."
    caption="Figura: Detalhes do componente Mesh."
%}

## O Editor Skeletal Mesh

{% include imagebase.html
    src="unreal/movimentacao/blueprint_editor_mesh.webp"
    alt="Figura: Editor Skeletal Mesh."
    caption="Figura: Editor Skeletal Mesh."
%}

Observe que o editor é divido em :

- `Skeleton` - Estrutura de conexões representando os ossos;

- `Mesh` - Malha o objeto;

- `Animation` - Sequencia de animações que determina os movimentos do objeto;

- `Blueprint` - Lógica de programação para sequenciamento de animações;

- `Physcis` - Estruturas para representar a física do esqueleto.

## Posição e coordenadas

***

Os objetos adicionados em uma cena possuem coordenadas de localização dentro do 'mundo', vamos apresentar como manipular coordenadas.

{% include imagebase.html
    src="unreal/actor/blueprint_coordinate_viewport.webp"
    alt="Figura: Coordenadas no ViewPort."
    caption="Figura: Coordenadas no ViewPort."
%}

### Transform

A seção **Transform** do painel Detalhes permite que você visualize e edite as transformações - Localização, Rotação e Escala - do (s) ator (es) selecionado (s). Além disso, quando aplicável, também contém as configurações para Mobilidade do Ator.

{% include imagebase.html
    src="unreal/actor/blueprint_transform.webp"
    alt="Figura: Transform - Coordenadas de posicionamento."
    caption="Figura: Transform - Coordenadas de posicionamento."
%}

### Escrevendo na tela o posicionamento do ator no mundo

{% include imagebase.html
    src="unreal/actor/blueprint_actor_print_location.webp"
    alt="Figura: Bluprint Print Location."
    caption="Figura: Bluprint Print Location."
%}

- `GetActorLocation` - Retorna um vetor contendo as coordenadas X,Y e Z da posição do ator no mundo. Utiliza o componente `RootComponent` para determinar os valores;

- `GetwordLocarion` - Retorna um vetor de coordenadas da posição do componente no mundo.

### Posição relativa no mundo

Os elementos associados a um ator, como por exemplo `StaticMeshes` tem posições relativas ao objeto ao qual estão associados.  

Considere o exemplo abaixo do objeto **BP_Ator**:

```bash
|-- BP_Ator
    |-- DefaultSceneRoot
    |   |-- StaticMesh
```

O objeto possui um componente `DefaultSceneRoot`.

{% include imagebase.html
    src="unreal/actor/blueprint_actor_add_component.webp"
    alt="Figura: DefaultSceneRoot."
    caption="Figura: DefaultSceneRoot."
%}

A posição do ator no mundo é calculada utilizando o componente `DefaultSceneRoot` do tipo `Scene`. O componente `StaticMesh` tem um vetor de coordenadas relativas ao objeto de hierarquia superior, sendo X=0,Y=0 e Z=0.

### Escrevendo na tela o posição relativa do componente

{% include imagebase.html
    src="unreal/actor/blueprint_actor_print_location_relative.webp"
    alt="Figura: Blueprint - Print Relative location."
    caption="Figura: Blueprint - Print Relative locationt."
%}

## Trabalhando com herança com Blueprint

***

Como apresentado no conceito de classes, a herança permite usar classes já definidas para derivar novas classes, a seguir vamos verificar como implementar utilizando **Blueprint**.  

Exemplo:  

```bash
|-- Character
    |-- BeginPlay()
    |-- Humanos
    |   |-- Vida (float) = 100    
    |   |-- Dano (float) = 100        
    |   |-- BeginPlay() (herdado)
    |   |-- Heroi
    |   |   |-- Vida = 100 (herdado)
    |   |   |-- Dano = 50 (herdado)
    |   |-- Vilao
    |   |   |-- Vida = 100 (herdado)
    |   |   |-- Dano = 80 (herdado)    
```

### Componente *ChildActor* implementa a ligação com outro ator

O componente **ChildActor** permite associar uma classe filha utilizando a lista de componentes.

{% include imagebase.html
    src="unreal/actor/blueprint_actor_childactor.webp"
    alt="Figura: Blueprint - ChildActor."
    caption="Figura: Blueprint - ChildActor."
%}

- `ChildActor` - É necessário informar a classe filho neste componente.

### Herança de propriedades e métodos

É possível sobrescrever os métodos da classe pai para adicionar uma nova lógica, vamos aos passos.

Criando um evento para sobrescrever o evento `Begin Play`.

{% include imagebase.html
    src="unreal/actor/blueprint_actor_event_inheritance_create.webp"
    alt="Figura: Blueprint  - Functions Override."
    caption="Figura: Blueprint  - Functions Override."
%}

Lógica adicionada no novo evento.

{% include imagebase.html
    src="unreal/actor/blueprint_actor_event_inheritance.webp"
    alt="Figura: Blueprint - Herança do evento Begin Play."
    caption="Figura: Blueprint - Herança do evento Begin Play."
%}

### Referências de atores e componentes

{% include imagebase.html
    src="unreal/actor/blueprint_view_class_inheritance.webp"
    alt="Figura: Blueprint - View Classy."
    caption="Figura: Blueprint - View Class."
%}

## Polimorfismo em C++

***

Polimorfismo em linguagens orientadas a objeto, é a capacidade de objetos se comportarem de forma diferenciada em face de suas características ou do ambiente ao qual estejam submetidos, mesmo quando executando ação que detenha, semanticamente, a mesma designação.

O polimorfismo em C++ se apresenta sob diversas formas diferentes, desde as mais simples, como funções com mesmo nome e lista de parâmetros diferentes, até as mais complexas como funções virtuais, cujas formas de execução são dependentes da classe a qual o objeto pertence e são identificadas em tempo de execução.

## Funções virtuais

"Uma função virtual é uma função de membro que é declarada dentro de uma classe base e é redefinida (Substituída) por uma classe derivada. Quando você se refere a um objeto de classe derivada usando um ponteiro ou uma referência à classe base, pode chamar uma função virtual para esse objeto e executar a versão da função da classe derivada."[Funções Virtuais](https://pt.wikipedia.org/wiki/Fun%C3%A7%C3%A3o_virtual "Funções Virtuais")

- As funções virtuais garantem que a função correta seja chamada para um objeto, independentemente do tipo de referência (ou ponteiro) usado para a chamada da função;

- Eles são usados principalmente para obter polimorfismo de tempo de execução;

- As funções são declaradas com uma palavra-chave virtual na classe base;

- A resolução da chamada de função é feita em tempo de execução.

### Exemplo de função virtual em C++ com Unreal Engine

```cpp
class WeaponBase {
  public: virtual void OnFire() {}
};
class WeaponRifle : public WeaponBase {
  public: void OnFire() override {}
};

...
WeaponRifle
void anotherFunction(WeaponBase *someWeapon) {
  someWeapon->OnFire();
}
```

- Na função anotherFunction o método chamado em OnFire é WeaponRifle::OnFire().

- O método WeaponBase::OnFire não é chamado pois foi sobreposto.

### Exemplo de função virtual no C++ 

```cpp
#include <iostream>

using std::cout;
using std::endl;

class Base {
public:
    // declaração da função virtual
    virtual void Quem_VIRTUAL()
    {
        cout << "Base\n";
    }
    // função comum
    void Quem_NAO_VIRTUAL()
    {
        cout << "Base\n";
    }
};

class Derivada : public Base {
public:
    // função virtual sobrescrita
    virtual void Quem_VIRTUAL()
    {
        cout << "Derivada\n";
    }
    // função comum sobrescrita
    void Quem_NAO_VIRTUAL()
    {
        cout << "Derivada\n";
    }
};

int main ()
{
    Base *ptr_base;
    Derivada derivada;

    ptr_base = &derivada;           // conversão implícita permissível
    ptr_base->Quem_VIRTUAL();       // chamada polimórfica (mostra: "Derivada")
    ptr_base->Quem_NAO_VIRTUAL();   // chamada comum, não-polimórfica (mostra: "Base")

    cout << endl;

    return 0;
}
```

## Manipulando Actors

***

Podemos adicionar, remover ou selecionar os atores que estão na cena do jogo, a seguir vamos implementar e entender esses comandos.

### Spawn e Destroy Actors - Criando e destruindo um Actor

O processo de criação de uma nova instância de um ator é conhecido como *spawning*. A geração de atores é realizada usando a função `SpawnActor`. Esta função cria uma nova instância de uma classe especificada e retorna um ponteiro para o Actor recém-criado. `SpawnActor` só pode ser usado para criar instâncias de classes que herdam da classe Actor em sua hierarquia.

{% include imagebase.html
    src="unreal/actor/blueprint_actor_spawn.webp"
    alt="Figura: Blueprint - Exemplo de SpawnActor e DestroyActor."
    caption="Figura: Blueprint - Exemplo de SpawnActor e DestroyActor."
%}

Utilizando o `Level Bluprint` podemos implementar o código acima.

1. Ao pressionar a tecla **H** o ator e criado na cena utilizando as coordenadas de um componente `targetPoint` adicionando na cena;

1. O comando `flip/flop` é utilizado para intercalar entre criar e destruir o ator, com os métodos `SpawnActor` e `DestroyActor` respectivamente;

1. Usamos `IsValid` para verificar se o ator existe na cena.

### Listando Actors por classe

Utilizando a função `GetAllActorOfClass` e o loop `For Each Loop` podemos listar todos os atores na cena.

{% include imagebase.html
    src="unreal/actor/blueprint_actor_get_all_actors.webp"
    alt="Figura: Blueprint - Exemplo de GetAllActorOfClass."
    caption="Figura: Blueprint - Exemplo de GetAllActorOfClass."
%}

### Listando Actors utilizando *tag* (etiquetas)

Adicionando uma *tag* (Etiqueta) na propriedade do ator podemos selecionar todos na cena que tenham a referida *tag*.

{% include imagebase.html
    src="unreal/actor/blueprint_actor_get_all_actors_tags.webp"
    alt="Figura: Blueprint - Exemplo de GetAllActorWithTag."
    caption="Figura: Blueprint - Exemplo de GetAllActorWithTag."
%}

## Colisões

***

**Collision Responses** e **Trace Responses** formam a base de como o Unreal Engine 4 lida com colisão e transmissão de raios durante o tempo de execução. Cada objeto que pode colidir recebe um tipo de objeto e uma série de respostas que definem como ele interage com todos os outros tipos de objeto. Quando ocorre um evento de colisão ou sobreposição, ambos (ou todos) os objetos envolvidos podem ser configurados para afetar ou serem afetados pelo bloqueio, sobreposição ou ignorando um ao outro. [Collision Overview](https://docs.unrealengine.com/4.27/en-US/InteractiveExperiences/Physics/Collision/Overview/)

### Trace Responses

Funcionam basicamente da mesma maneira, exceto que o próprio rastreamento (*ray cast*) pode ser definido como um dos tipos de resposta de rastreamento, permitindo assim que os atores o bloqueiem ou ignorem com base em suas respostas de rastreamento.

### Interações

Existem algumas regras a serem lembradas sobre como as colisões são tratadas:

- O bloqueio ocorrerá naturalmente entre dois (ou mais) Atores definidos como **Block** (Bloquear). No entanto, `Simulation Generates Hit Events` precisa ser habilitado para executar `Event Hit`, que é usado em Blueprints, `Destructible Actors`, `Triggers`, etc...

- Definir Atores para **Overlap** (Sobrepor) muitas vezes parecerá que eles Ignoram uns aos outros e, sem Gerar Eventos de Sobreposição, eles são essencialmente os mesmos.

- Para que dois ou mais objetos de simulação bloqueiem um ao outro, ambos precisam ser configurados para bloquear seus respectivos tipos de objeto.

- Para dois ou mais objetos de simulação: se um for configurado para sobrepor um objeto e o segundo objeto for configurado para bloquear o outro, a sobreposição ocorrerá, mas não o bloqueio.

- Eventos de sobreposição, **Overlap**, podem ser gerados mesmo que um objeto Bloqueie outro, especialmente se estiver viajando em alta velocidade.

- Não é recomendado que um objeto tenha eventos de colisão e sobreposição. Embora seja possível, é necessário  manuseio manual.

- Se um objeto for configurado para ignorar e o outro for configurado para sobrepor, nenhum evento de sobreposição será disparado.

### Exemplo de Colisão

>Essas interações pressupõem que todos os objetos tenham `Collision Enabled` definido como `Collision Enabled`, de modo que estejam configurados para colidir totalmente com tudo. Se a colisão estiver desabilitada, é como se ignorar tivesse sido definido para todas as `Collision Responses` .

Para a seção a seguir, abaixo a configuração usada para explicar o que está acontecendo:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_setup.png"
    alt="Figura: Exemplo de colisão."
    caption="Figura: Exemplo de colisão."
%}

A esfera é um **PhysicsBody** e a caixa é **WorldDynamic**, e alterando suas configurações de colisão podemos obter uma série de comportamentos.

Ao definir ambas as configurações de colisão para bloquear uma à outra, você obtém uma colisão, ótima para que os objetos interajam entre si:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent.png"
    alt="Figura: Collision Overview."
    caption="Figura: Collision Overview."
%}

### Configuração de colisão de esfera

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Sphere.png"
    alt="Figura: Configuração de colisão de esfera."
    caption="Figura: Configuração de colisão de esfera."
%}

Neste caso, a esfera é um `PhysicsBody` e está configurada para bloquear `WorldDynamic` (que é o que é a parede).

### Configuração de colisão de parede

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Configuração de colisão de parede."
    caption="Figura: Configuração de colisão de parede."
%}

A parede é uma `WorldDynamic` e está configurada para bloquear os Atores `PhysicsBody` (que é o que a esfera é).

Nesse caso, a esfera e a parede simplesmente colidirão; nenhuma outra notificação da colisão ocorrerá.

### Colisão e Simulação Geram Eventos de toque ou acerto

Apenas a colisão é útil e, em geral, o mínimo para interações físicas, mas se você quiser que algo relate, ele colidiu para que um **Blueprint** ou seção de código possa ser acionado:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideEvent.png"
    alt="Figura: Colisão de eventos."
    caption="Figura: Colisão de eventos."
%}

### Configuração de colisão de esfera 1

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideEvent_Sphere.png"
    alt="Figura: Configuração de Colisão de uma esfera."
    caption="Figura: Configuração de Colisão de uma esfera."
%}

Como no exemplo acima, a esfera é um `PhysicsBody` e está configurada para bloquear `WorldDynamic` (que é o que é a parede). No entanto, a esfera também habilitou `Simulation Generates Hit Event` para que acione um evento para si mesma sempre que colidir com algo.

### Configuração de colisão de parede 1

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Configuração de Colisão da Wall."
    caption="Figura: Configuração de Colisão da Wall."
%}

A parede é uma `WorldDynamic` e está configurada para bloquear os Atores `PhysicsBody` (que é o que a esfera é). Como a parede não está configurada para `Simulation Generates Hit Event` , ela não gerará um evento para si mesma.

Com a esfera definida como Simulação gera eventos de acerto, a esfera informará a si mesma que sofreu uma colisão. Ele irá disparar eventos como `ReceiveHit` ou `OnComponentHit` no **Blueprint** da esfera. Agora, se a caixa tivesse um evento de colisão, ela não dispararia porque nunca notificará a si mesma que aconteceu.

Além disso, um objeto que está relatando colisões rígidas relatará todas elas e relatórios de spam quando estiver apenas parado em algo, portanto, é melhor ter cuidado ao filtrar o que está colidindo em seu **Blueprint** ou no código.

### Sobrepor e ignorar

Para todos os efeitos, *Overlap* (Sobrepor) e *Ignore* (Ignorar) funcionam exatamente da mesma forma, supondo que Gerar eventos de sobreposição esteja desativado. Nesse caso, a esfera está configurada para sobrepor ou ignorar a caixa:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_ignore.png"
    alt="Figura: Overlap and Ignore."
    caption="Figura: Overlap and Ignore."
%}

### Configuração das propriedades de colisão de esfera

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_OverlapNoEvent_Sphere.png"
    alt="Figura: Configuração de Colisão da  esfera."
    caption="Figura: Configuração de Colisão da  esfera."
%}

Aqui a esfera está configurada para se sobrepor,`Overlap`, aos `WorldDynamic Actors` (como nossa parede), mas não tem a opção Gerar Eventos de Sobreposição habilitado. No que diz respeito à esfera, ela não colidiu ou se sobrepôs a nada, efetivamente ignorou a parede.

### Configuração das propriedades colisão de parede

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Configuração de colisão de parede."
    caption="Figura: Configuração de colisão de parede."
%}

A parede é uma `WorldDynamic` e está configurada para bloquear,`Block`, os Atores `PhysicsBody` (que é o que a esfera é). Como dito acima, ambos os Atores precisam ser configurados para bloquear os respectivos tipos de objetos um do outro. Se não o fizerem, não colidirão.

Ou:

### Configuração das propriedades da colisão de esfera

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_ignore_sphere.png"
    alt="Figura: Collide ignore Sphere."
    caption="Figura: Collide ignore Sphere."
%}

Aqui a esfera está configurada para ignorar, `Ignore`, os Atores `WorldDynamic` (como nossa parede), e ela passará pela parede.

### Configuração das propriedades de colisão de parede

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Collide No Event."
    caption="Figura: Collide No Event."
%}

A parede é uma `WorldDynamic` e está configurada para bloquear os Atores `PhysicsBody` (que é o que a esfera é). Como dito acima, ambos os Atores precisam ser configurados para bloquear, `Block`, os respectivos tipos de objetos um do outro. Se não o fizerem, não colidirão.

### Sobrepor e gerar eventos de sobreposição

Ao contrário das colisões que podem disparar todos os quadros, os eventos de sobreposição são `ReceiveBeginOverlap` e `ReceiveEndOverlap`, que são disparados apenas nesses casos específicos.

> Para que uma sobreposição ocorra, ambos os Atores precisam habilitar Gerar Eventos de Sobreposição. Isso é para desempenho. No caso em que tanto a Esfera quanto a Caixa desejam sobreposições quando movemos a Esfera ou a Caixa, fazemos uma consulta de sobreposição para ver se precisamos disparar algum evento.
>
>Se a caixa não quiser sobreposições, quando ela se mover, não faremos uma consulta de sobreposição. Mas agora poderíamos estar sobrepondo com a Esfera, e assim a Esfera precisaria marcar e verificar se há sobreposições em cada quadro caso alguém se movesse para eles.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_overlapEvent.png"
    alt="Figura: Evento overlap."
    caption="Figura: Evento overlap."
%}

### Colisão de esfera

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_OverlapEvent_Sphere.png"
    alt="Figura: Colisão da esfera."
    caption="Figura: Colisão da esfera."
%}

Aqui, a esfera está configurada para sobrepor, `Overlap`, os Atores `WorldDynamic` (como nossa parede), e ela gerará um evento para si mesma quando se sobrepuser a algo.

### Colisão de parede

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideOverLapEvent_Box.png"
    alt="Figura: Evento overlap no box."
    caption="Figura: Evento overlap no box."
%}

A parede é uma WorldDynamic e está configurada para bloquear, `Block`, os Atores `PhysicsBody` (que é o que a esfera é). Como dito acima, ambos os Atores precisam ser configurados para bloquear os respectivos tipos de objetos um do outro. Se não o fizerem, não colidirão. Mas, uma sobreposição ocorre aqui, e os eventos para a esfera e a caixa são disparados.

### Colisão Simples versus Complexa

No **Unreal Engine**, você tem acesso a formas de colisão simples e complexas. Colisão Simples, `Simplex Collision`, são primitivos como cubos, esferas, cápsulas e cascos convexos. Colisão Complexa, `Complex Collsion`, é o `trimesh` de um determinado objeto. Por padrão, o **Unreal Engine** cria formas simples e complexas, então, com base no que o usuário deseja (consulta complexa versus consulta simples), o solucionador de física usará a forma correspondente para consultas de cena e testes de colisão. [Simple versus Complex Collision](https://docs.unrealengine.com/5.0/en-US/simple-versus-complex-collision-in-unreal-engine/)

### Como usar

No painel `Static Mesh Editor > Details`, você pode encontrar as configurações de `Complex Collision` na categoria `Collision`.

{% include image.html
    src="https://docs.unrealengine.com/5.0/Images/making-interactive-experiences/Physics/collision/simple-vs-complex/StaticMeshSettingsCollisionComplexity.webp"
    alt="Figura: Staticmesh Settings Collision Complexity."
    caption="Figura: Staticmesh Settings Collision Complexity."
%}

- `Project Default` :  Usa as configurações físicas do projeto, isso fará com que solicitações de colisão simples usem colisão simples e solicitações complexas usem colisão complexa; o comportamento "padrão".

- `Simple and Complex`:  Esse sinalizador permite a criação de formas simples e complexas, usando formas simples para consultas de cena regulares e testes de colisão e usando formas complexas (por poli) para consultas de cena complexas.

- `Use Simple Collision As Complex`:  Isso significa que, se uma consulta complexa for solicitada, o mecanismo ainda consultará formas simples; basicamente ignorando o trimesh. Isso ajuda a economizar memória, pois não precisamos preparar o trimesh e pode melhorar o desempenho se a geometria de colisão for mais simples.

- `Use Complex Collision As Simple`:  Isso significa que, se uma consulta simples for solicitada, o mecanismo consultará formas complexas; basicamente ignorando a simples colisão. Isso nos permite usar o trimesh para a colisão de simulação de física. Observe que, se você estiver usando `UseComplexAsSimple`, não poderá simular o objeto, mas poderá usá-lo para colidir com outros objetos simulados (simples).

Por exemplo, na imagem abaixo a cadeira à esquerda tem colisão simples, e quando o peão acima dela cai sobre ela, ele desliza para fora da grande superfície angulada que cobre o assento. No entanto; a cadeira à direita está usando `Use Complex Collision As Simple`, e quando o peão acima dele cair, ele pousará no assento da cadeira e permanecerá lá.

{% include image.html
    src="https://docs.unrealengine.com/5.0/Images/making-interactive-experiences/Physics/collision/simple-vs-complex/exImage.webp"
    alt="Figura: Simple vs Complex."
    caption="Figura: Simple vs Complex."
%}
