---
title: Enums
excerpt: Neste capítulo serão descritos objetos do tipo Enum.
permalink: /pages/unreal-engine/enums
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true  
categories:
  - Unreal Engine
tags:
  - Blueprint
  - enum
---

[Intermediário](/collection-archive/){: .btn .btn--warning}

## 1. O que são Enums?

Uma enumeração é um tipo definido pelo usuário que consiste em um conjunto de constantes integrais nomeadas que são conhecidas como enumeradores.

Exemplo:

```cpp
enum cores = { vermelho,amarelo, azul, verde = 20, preto}
```

### 1.1. Criando Enums no Unreal Engine e Blueprint

{% include imagelocal.html
    src="unreal/enum/unreal-engine-enum-declare.webp"
    alt="Figura: Blueprint e Enum."
    caption="Podemos adicionar e remover vários valores."
%}

Execute o comando no menu de contexto `Blueprints` > `Enumeration` e logo depois preencha os valores conforme a tela abaixo.  

{% include imagelocal.html
    src="unreal/enum/unreal-engine-enum.webp"
    alt="Figura: Blueprint Enum no Context Browser."
    caption="Objeto criado EN_Estado e EN_Pedra."
%}

### 1.2. Criando Enums no Unreal Engine e C++

Arquivo header.

`Visual Studio` > `Arquivo` > `Novo` > `Arquivo` > Escolha Visual C++, Arquivo de Cabeçalho (.h)

```cpp
// EnumName.h
UENUM(BlueprintType)
namespace EStatusEnum {
// Definimos namespace para que não existam conflitos no acesso aos elementos.
    enum Status
    {
        Ligada     UMETA(DisplayName = "Ligada"),
        Desligada      UMETA(DisplayName = "Desligada"),
    };

}
```

Arquivo de implementação.

```cpp
// Hero.cpp
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = Status)
  TEnumAsByte < EStatusEnum::Status > status;
```

### 1.3. Exemplos de uso - A lâmpada

Vamos verificar e alterar o estado de uma lâmpada utilizando uma variável do tipo `boolean`.  

{% include imagelocal.html
    src="unreal/enum/unreal-engine-enum-example-lamp-state.webp"
    alt="Figura: Blueprint Verificando o estado de uma lâmpada."
    caption="Lógica para determinar se a lâmpada está ligada ou desligada."
%}

### 1.4. A lâmpada em C++

```cpp
void AFirstPersonBaseCodeCharacter::SetupPlayerInputComponent(class UInputComponent* InputComponent)
  {
          // set up gameplay key bindings
          check(InputComponent);
          ...
          InputComponent->BindAxis("AnyKey", this, &AFirstPersonBaseCodeCharacter::AnyKey);
          ...
  }   
void AFirstPersonBaseCodeCharacter::AnyKey(float Value)
  {
    if bLigado
    {
      UE_LOG(LogTemp, Warning, TEXT("Lâmpada ligada."));  
    }    
    else
      UE_LOG(LogTemp, Warning, TEXT("Lâmpada desligada."));
  }    
```

Alterando o componente `PointLight` para ligar e desligar a iluminação.

{% include imagelocal.html
    src="unreal/enum/unreal-engine-enum-example-lamp-offon.webp"
    alt="Figura: Blueprint Ligando e desligando o PointLight."
    caption="Utilizando Flip Flop podemos mudar a propriedade Set Intensity e configurando a variável Ligado para falso ou verdadeiro."
%}

### 1.5. Arquivo Header da lâmpada em C++

```cpp
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "ControlLight.generated.h"

UCLASS()
class CPP5_API AControlLight : public AActor
{
    GENERATED_BODY()

public:
    UPROPERTY()
        USceneComponent* Root;

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Parameters")
        bool bLigado;

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Parameters")
        float fIntensidade;

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Parameters")
        class UPointLightComponent* PointLight;

    UPROPERTY(EditAnywhere, Meta = (MakeEditWidget = true))
        FVector TargetLocation;

    AControlLight();

protected:

    virtual void BeginPlay() override;

    void AnyKey();

public:
    virtual void Tick(float DeltaTime) override;
    void InitControl();

    class APlayerController* PlayerControllControlLight;

};
```

Arquivo de implementação.

```cpp
#include "ControlLight.h"
#include "Components/PointLightComponent.h"
#include "Kismet/GameplayStatics.h"
#include "Components/InputComponent.h"

// Sets default values
AControlLight::AControlLight()
{
    PrimaryActorTick.bCanEverTick = true;
    Root = CreateDefaultSubobject<USceneComponent>("Root");
    RootComponent = Root;
    PointLight = CreateDefaultSubobject<UPointLightComponent>(TEXT("Ponto de Luz"));
    PointLight->SetRelativeTransform(FTransform(FRotator(0, 0, 0), FVector(250, 0, 0),FVector(0.1f)));
    fIntensidade = 10000;
    bLigado = true;
}

void AControlLight::InitControl()
{
    FVector GlobalLocation = GetTransform().TransformPosition(TargetLocation);
    PointLight->SetWorldLocation(GlobalLocation);
    PointLight->SetIntensity(fIntensidade);
}

// Called when the game starts or when spawned
void AControlLight::BeginPlay()
{
    Super::BeginPlay();
    PlayerControllControlLight = UGameplayStatics::GetPlayerController(this, 0);
    EnableInput(PlayerControllControlLight);
    AControlLight::InitControl();
}

// Called every frame
void AControlLight::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);
    if (PlayerControllControlLight != NULL)
    {
        if (PlayerControllControlLight->WasInputKeyJustPressed(EKeys::T))
        {
        AnyKey();
        }
    }
}

void AControlLight::AnyKey()
{
    if (bLigado)
    {
        fIntensidade = 0;
        bLigado = false;

    }
    else
    {
        fIntensidade = 10000;
        bLigado = true;
    }
    PointLight->SetIntensity(fIntensidade);
}

```

### 1.6. Verificando o estado utilizando o Enum com Blueprint

{% include imagelocal.html
    src="unreal/enum/unreal-engine-enum-example-lamp-read-state.webp"
    alt="Figura: Blueprint Lendo Enum."
    caption="Podemos ler o valor corrente de um Enum acessando diretamente a variável."
%}

### 1.7. Verificando o estado utilizando o Enum com C++

```cpp
// Definindo um status no enum.
status = EStatusEnum::Ligada;

UE_LOG(LogTemp, Warning,TEXT("O enum é = %s"), *UEnum::GetValueAsString(status));
```

### 1.8. Ligando e desligando utilizando o Enum com Blueprint

{% include imagelocal.html
    src="unreal/enum/unreal-engine-enum-example-lamp-off.webp"
    alt="Figura: Blueprint Ligando e desligando usando Enum."
    caption="Usamos agora a variável Estado do tipo Enum para configurar o estado da lâmpada."
%}

### 1.9. Ligando e desligando utilizando o Enum com C++

```cpp
...
if (status = EStatusEnum::Ligada) {
  fIntensidade = 0;
  bLigado = false;
  status = EStatusEnum::Desligada;
}
else {
  fIntensidade = 10000;
  bLigado = true;
  status = EStatusEnum::Ligada;
}
```

### 1.10. Exemplos de uso - A pedra das emoções

Vamos verificar e alterar o estado de emocional de uma pedra.

Alterando o estado emocional da pedra.

{% include imagelocal.html
    src="unreal/enum/unreal-engine-enum-example-rock.webp"
    alt="Figura: Blueprint alterando Enum."
    caption="Altera o estado para Feliz, triste, pulando e pensando."
%}

{% include imagelocal.html
    src="unreal/enum/unreal-engine-enum-example-rock-state.webp"
    alt="Figura: Blueprint escrevendo o conteúdo do Enum."
    caption="Apresentando o estado da pedra."
%}
  
{% include imagelocal.html
    src="unreal/enum/unreal-engine-enum-example-rock-set-material.webp"
    alt="Figura: Blueprint alterando o material de uma malha utilizando um Enum como parâmetro."
    caption="Alterando o material de uma malha utilizando um Enum como parâmetro."
%}
