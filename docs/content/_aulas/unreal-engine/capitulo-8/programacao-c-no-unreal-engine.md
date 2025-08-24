---
title: Programação C++ no Unreal Engine
excerpt: Neste capítulo, vamos conhecer como funciona a lógica de programação usando **C++** no **Unreal Engine**.
categories: 
  - "unreal-engine"
  - "capitulo-8"
date: 2024-09-01T07:48:05-04:00
order: 806
tags:
  - cpp
  - C++
---

## 1. O que é C++ no Unreal Engine?

O **C++** é uma linguagem poderosa, rápida e muito usada em jogos porque permite acessar recursos do computador de forma eficiente. O **Unreal Engine** usa o C++ para dar vida aos jogos, aproveitando tudo que a linguagem oferece: velocidade, controle de memória e a possibilidade de criar classes (ou seja, organizar o código em "caixinhas" com funções e dados).

Além disso, o Unreal facilita a vida do programador com várias ferramentas, como macros e tipos de objetos próprios da Engine, tornando o desenvolvimento mais prático.

## 2. Quando usar C++ no Unreal Engine?

Não existe uma resposta única, mas podemos comparar o uso de **Blueprints** (programação visual) e **C++** (programação por código):

### 2.1. Blueprints vs C++

- **Blueprints** são mais fáceis de entender e ótimos para quem está começando ou para equipes pequenas.
- **C++** é mais rápido e eficiente, ideal para partes do jogo que precisam de muita performance.
- Com **C++**, você pode usar sistemas de controle de versão como Git ou SVN.
- **Blueprints** precisam de ferramentas específicas para versionamento.
- Para jogos em plataformas mobile, geralmente o **C++** é recomendado.

### 2.2. Qual escolher?

Depende do seu projeto! Pense assim:

- Projetos pequenos ou equipes pequenas: **Blueprints** são ótimos.
- Projetos que precisam de mais desempenho ou equipes com experiência em programação: **C++** pode ser melhor.

## 3. Como criar classes C++ no Unreal Engine

Vamos ver como criar uma classe em **C++** no Unreal Engine. Basta ir em `Menu Tools` > `New C++ Class`.

{% include imagelocal.html
    src="unreal/cpp/unreal-engine-create-class-cpp.webp"
    alt="Figura: Create Class C++"
    caption="Figura: Criando a classe Actor em C++."
%}

{% include imagelocal.html
    src="unreal/cpp/unreal-engine-add-class-cpp.webp"
    alt="Figura: Add C++ Class"
    caption="Figura: Adicionando o nome da classe e informando a pasta de armazenamento do arquivo header e de código."
%}

O Unreal vai criar dois arquivos para você: um arquivo de cabeçalho (`.h`) e um arquivo de código (`.cpp`). Normalmente, eles ficam em pastas separadas: `Private` para o código e `Public` para os cabeçalhos.

### 3.1. Exemplo de arquivo header (.h)

```cpp
// Diretiva para garantir que o arquivo só seja incluído uma vez
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "ControlLight.generated.h"

// Macro que indica que essa classe faz parte do sistema do Unreal
UCLASS()
class CPP5_API AControlLight : public AActor
{
    GENERATED_BODY()

public:
    // Construtor da classe
    AControlLight();

protected:
    // Chamado quando o jogo começa ou o ator é criado
    virtual void BeginPlay() override;
public:
    // Chamado a cada frame
    virtual void Tick(float DeltaTime) override;
};
```

### 3.2. Exemplo de arquivo de implementação (.cpp)

```cpp
#include "ControlLight.h"

// Construtor da classe
AControlLight::AControlLight()
{
    // Faz o ator chamar Tick() a cada frame
    PrimaryActorTick.bCanEverTick = true;
}

void AControlLight::BeginPlay()
{
    Super::BeginPlay();
}

void AControlLight::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);
}
```

### 3.3. Exemplo de header com variáveis

Vamos criar uma classe chamada **Plataforma** para mostrar como declarar variáveis:

```cpp
#include "CoreMinimal.h"
#include "Engine/StaticMeshActor.h"
#include "Plataforma.generated.h"

UCLASS(ClassGroup=(Custom), meta=(BlueprintSpawnableComponent))
class PROJETOPLATAFORMA_API APlataforma : public AStaticMeshActor
{
    GENERATED_BODY()

public:
    APlataforma();

    virtual void Tick(float DeltaTime) override;
    virtual void BeginPlay() override;

    UPROPERTY(EditAnywhere, Meta = (MakeEditWidget = true))
    FVector TargetLocation;

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Plataforma")
    float SpeedPlataform = 20;

    UFUNCTION(BlueprintCallable, Category = "Plataforma")
    void AddActiveTrigger();

    UFUNCTION(BlueprintCallable, Category = "Plataforma")
    void RemoveActiveTrigger();

protected:
    FVector GlobalStartLocation;
    FVector GlobalTargetLocation;

    UPROPERTY(EditAnywhere)
    int ActiveTriggers = 1;
};
```

## 4. Entendendo a sintaxe e as macros do Unreal Engine

### 4.1. O que é um arquivo Include?

Quando você usa `#include`, está dizendo ao compilador para "colar" o conteúdo de outro arquivo no seu código. Assim, você pode usar funções e classes já prontas, sem precisar reescrever tudo do zero!

#### Exemplo:

```cpp
#include "CoreMinimal.h"
#include "Engine/StaticMeshActor.h"
#include "Plataforma.generated.h"
```

#### O que é o arquivo .generated.h?

O Unreal cria arquivos especiais chamados `.generated.h` para cada classe que usa as macros do sistema (como UCLASS). Eles ajudam o Unreal a entender e organizar seu código.

## 5. Encapsulamento: public, private e protected

- **public**: Qualquer um pode acessar.
- **private**: Só a própria classe pode acessar.
- **protected**: A própria classe e suas "filhas" (heranças) podem acessar.

## 6. UCLASS

Quando você coloca `UCLASS()` antes de uma classe, está dizendo ao Unreal: "Ei, essa classe faz parte do sistema do motor!". Assim, ela pode ser usada no editor, em Blueprints e muito mais.

### Exemplo:

```cpp
UCLASS(ClassGroup=(Custom), meta=(BlueprintSpawnableComponent))
```

- `BlueprintSpawnableComponent`: Permite criar o componente via Blueprint.
- `ClassGroup=GroupName`: Organiza a classe em grupos no editor.

## 7. UFUNCTION

Quando você coloca `UFUNCTION()` antes de uma função, ela pode ser usada em Blueprints e pelo sistema do Unreal.

### Exemplo:

```cpp
UFUNCTION(BlueprintCallable, Category = "Plataforma")
void AddActiveTrigger();
```

- `BlueprintCallable`: Permite chamar a função em Blueprints.

## 8. UPROPERTY

Quando você coloca `UPROPERTY()` antes de uma variável, ela pode ser editada no editor, lida ou modificada por Blueprints, e muito mais.

```cpp
UPROPERTY(EditAnywhere, Meta = (MakeEditWidget = true))
FVector TargetLocation;
```

- `EditAnywhere`: Pode ser editada em qualquer lugar no editor.
- `BlueprintReadWrite`: Pode ser lida e modificada em Blueprints.
- `MakeEditWidget`: Mostra um widget para editar a propriedade no editor.

### Exemplo prático: Classe Actor com Static Mesh

#### Arquivo CharacterBase.h

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
    // Construtor padrão
    ACharacterBase();

    // Propriedade para adicionar uma Static Mesh
    UPROPERTY(VisibleAnywhere)
    UStaticMeshComponent* MeshMain;

protected:
    virtual void BeginPlay() override;

public:
    virtual void Tick(float DeltaTime) override;

};
```

#### Arquivo CharacterBase.cpp

```cpp
#include "CharacterBase.h"

ACharacterBase::ACharacterBase()
{
    PrimaryActorTick.bCanEverTick = true;

    // Cria a malha na memória
    MeshMain = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh Main"));

    // Carrega uma malha padrão
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

- `CreateDefaultSubobject`: Cria um componente novo para o ator.
- `ConstructorHelpers`: Ajuda a carregar recursos do projeto, como malhas 3D.

---

**Dica final:**  
No Unreal Engine, você pode misturar Blueprints e C++ para aproveitar o melhor dos dois mundos. Use Blueprints para lógica simples e rápida, e C++ para partes que precisam de mais desempenho ou controle!

Divirta-se programando e criando seus jogos!
