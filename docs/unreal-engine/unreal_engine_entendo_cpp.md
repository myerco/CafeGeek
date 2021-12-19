---
title: Entendendo a lógica de programação com C++ com Unreal Engine
description: Neste capítulo será apresentado o modelo da lógica de programação utilizando **C++** com Unreal Engine
unreal_engine: Unreal Engine 5
tags: [Unreal Engine,Blueprint]
cover-img: "/imagens/cafegeek_small.png"
layout: unreal_engine
---

Neste capítulo será apresentado o modelo da lógica de programação utilizando **C++** com Unreal Engine.


## Índice
1. **[O que são Blueprints e Visual Scripting?](#1)**  
    1. [Características](#1.1)  
    1. [Representação da construção do projeto no Unreal Engine](#1.2)
1. **[Trabalhando com Levels](#2)**      
1. [Atividades](#8)

***

Neste capítulo vamos utilizar a linguagem **C++** para o desenvolvimento.

<a name="1"></a>
## 1. Unreal e C++
O C++ por ter como base de desenvolvimento o C tem o benefício da rapidez e da portabilidade para diversas plataformas e ainda permite a implementação de classes, tornando a linguagem em uma boa candidata para o desenvolvimento de projetos com necessidade de velocidade acessando recursos de baixo nível e construção de classes.

O Unreal Egine utiliza a linugagem C++ aproveitando todas as funcionalidades que a linguagem fornece, como por exemplo o gerenciamento otimizado de memória, quanto a implementação a Engine fornece muitos elementos para auxiliar a codificação tornando-a mais fácil, entre eles a utilização de macros e objetos primitivos próprios da Engine.

**[⬆ Volta para o início](#índice)**
<a name="2"></a>
## 2. Mas quanto usar a linguagem  C++?
Não há uma resposta definitiva dessa questão mas podemos considerar algumas diferenças entre **Blueprint** e o **C++**.

<a name="2.1"></a>
### 2.1 Blueprints vs C++
- Blueprints são mais fáceis de ser lidos e entendidos pelos membros da equipe;
- C++ evitam sobrecarga de chamadas de função economizando ciclos de CPU;
- C++ Conseguem acesso a `Library Math`;
- É possível utilizar um sistema de versionamento como por exemplo o Git ou SVN com **C++**;
- Blueprints necessitam de ferramenta específica para versionamento;
- Para projetos em plataformas mobile o recomendado é **C++**.

<a name="2.2"></a>
### 2.2 O que é ideal?
- Depende do problema;
- Para equipes pequenas e projetos pequenos é recomendado Blueprints;
- Para equipes pequenas com cultura de desenvolvimento e necessidade de processamento é recomendado **C++**.

**[⬆ Volta para o início](#índice)**
<a name="3"></a>
## 3. O fluxo de desenvolvimento e Herança
Um modelo de desenvolvimento utilizando C++ pode ser visto abaixo onde primeiro criamos a classe do objeto A em C++ e depois uma classe Blueprint B filha da classe A. Fazendo isso pode-se aproveitar as características de ambas linguagens, como por exemplo: lógica em C++ e parametrização de componentes visuais usando o Editor Blueprint.  

Exemplo:

1. Vamos Criar uma Blueprint *BP_Plataforma* do tipo `static_mesh_actor`;
1. Depois Criar a classe **C++** `Plataforma` do tipo `AStaticMeshActor`;
1. Alterar classe pai do *BP_Plataforma* para *Plataforma*.

Onde :

| Origem      | Destino       |       |
|:-           |:-             |:-     |
|Classe C++   |Blueprints     |Certo  |
|Blueprints   |Classe C++     | Errado|

*Tabela: Representação do desenvolvimento descrito anteriormente.*

**[⬆ Volta para o início](#índice)**
<a name="4"></a>
## 4. Uma breve história sobre Herança.
A Herança em linguagem de programação permitem usar classes já definidas para derivar classes novas onde a nova classe herda as propriedades da classe base.

Exemplo:

**C++.**

```cpp
// Classe Pessoa
class Pessoa {
  int32 iVida;
  FString sNome;
}

class Heroi: public Pessoa {
  float fForca = 100;
}

void main() {
   // instânciando o objeto Nostromo do tipo Heroi
    Heroi nostromo;
}
```

**Blueprint.**

```cpp
class Hugo: Pessoa
      // iVida -- Herdada
      // movimentacao() - Herdada  

      AddActiveTrigger()  
      float SpeedPlataforma  
      int32 Vida #Error  
```

**[⬆ Volta para o início](#índice)**
<a name="5"></a>
## 5.Tipos de variáveis
A seguir vamos apresentar os tipos de variáveis em ambas as linguagens.

| Blueprint | C++     |
|:-:        |:-       |
|integer    |int32    |
|Vector     |FVector  |
|String     |FString  |
|Float      |float  |

**[⬆ Volta para o início](#índice)**
<a name="6"></a>
## 6. Construindo classes C++ no Unreal Engine
A seguir vamos implementar uma classe C++ no Unreal Engine para tal utilizamos o `Menu Tools` > `New C++ Class`

![Figura: Create Class C++](imagens/cpp/unreal_engine_create_class_cpp.jpg "Figura: Create Class C++")

*Figura: Create Class C++*

![Figura: Add C++ Class](imagens/cpp/unreal_engine_add_class_cpp.jpg "Figura: Add C++ Class")

*Figura: Add C++ Class*

O Unreal ira cria dois arquivos, o arquivo header (.h) e o de implementação (.cpp), sugerindo separar ambos nas pastas private e header.

<a name="6.1"></a>
### 6.1 Pasta privada com os arquivos header das classes
```bash
<Projeto>/Private/ControlLight.h
```

```cpp
// Diretiva de compilação que serve para fazer com que o arquivo seja
// incluído somente uma vez durante o processo de compilação.
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
// Arquivo criado durante a compilação
#include "ControlLight.generated.h"

// Macro utilizada para indicar que uma C++ fará parte do Unreal
// Reflection system. Isto é necessário para
//que a classe seja reconhecida pelo editor do Unreal Engine.

UCLASS()
class CPP5_API AControlLight : public AActor
{
	GENERATED_BODY()

public:
	// Construtor da classe
	AControlLight();

protected:
	// Método chamado quando o jogo inicia ou quando a classe
  // é adicionada na cena.
  virtual void BeginPlay() override;
public:
	// Método chamado a cada quadro.
	virtual void Tick(float DeltaTime) override;
};
```

Pasta publica com a implementação das classes :
```bash
<Projeto>/Public/ControlLight.cpp
```

```cpp
#include "ControlLight.h"

// Método construtor da classe
AControlLight::AControlLight()
{
  // Configura este ator para chamar o evento Tick() a cada frame.
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
<a name="6.2"></a>
### 6.2 Exemplo de um arquivo header com variáveis
Abaixo vamos construir uma classe em C++ chamado plataforma para exemplificar a declaração de variáveis.

```cpp

#include "CoreMinimal.h"
#include "Engine/StaticMeshActor.h"
#include "Plataforma.generated.h"

UCLASS(ClassGroup=(Custom),meta=(BlueprintSpawnableComponent) )
class PROJETOPLATAFORMA_API APlataforma : public AStaticMeshActor
{
	GENERATED_BODY()

public:
  // Construtor da classe
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

**[⬆ Volta para o início](#índice)**
<a name="7"></a>
## 7. Sintaxe da linguagem e C++ e macros do Unreal Engine
A seguir vamos apresentar algumas características de linguagem e as macros que facilitam a implementação em C++.

<a name="7.1"></a>
### 7.1 Include
É uma forma de incluir um arquivo padrão ou definido pelo usuário no programa e é principalmente escrito no início de qualquer programa C / C ++.  
Esta diretiva é lida pelo pré-processador e ordena que ele insira o conteúdo de um arquivo de cabeçalho do sistema ou definido pelo usuário no programa a seguir. Esses arquivos são importados principalmente de uma fonte externa para o programa atual. O processo de importação de tais arquivos que podem ser definidos pelo sistema ou pelo usuário é conhecido como Inclusão de Arquivo. Este tipo de diretiva de pré-processador diz ao compilador para incluir um arquivo no programa de código-fonte.

Exemplo:

```cpp
#include "CoreMinimal.h"
#include "Engine/StaticMeshActor.h"
#include "Plataforma.generated.h"
```

#### O arquivo <Classe>.generated.h
O Unreal Engine faz uso extensivo de macros de pré-processador, e algumas dessas macros são definidas (#defined) no arquivo `genrated.h` que acompanha cada `UCLASS`. Se você criar uma `UCLASS` *MyClass*, o arquivo MyClass.h irá incluir (#include) MyClass.generated.h. O cabeçalho gerado, MyClass.generated.h, é feito na parte inicial do processo de construção do Unreal Engine.

<a name="7.2"></a>
### 7.2 Encapsulamento
`Public` – Quando precede uma lista de membros de classe, o  *public*  palavra-chave especifica que esses membros são acessíveis a partir de qualquer função. Isso se aplica a todos os membros declarados até o próximo especificador de acesso ou o fim da classe. Ou seja visível a todos.

`Private` – Quando precede uma lista de membros de classe, o *private* palavra-chave especifica que esses membros são acessíveis somente dentro de funções de membro e amigos da classe.  Isso se aplica a todos os membros declarados até o próximo especificador de acesso ou o fim da classe. Ou seja visível somente para membros dentro da classe.

`Protected` – O *Protected* palavra-chave especifica o acesso a membros de classe no lista de membros até o próximo especificador de acesso (pública ou private) ou no final da definição de classe.  O *Protected* é mistura entre *Public* e *Private* ou seja é visível somente para membros da classe e visível para subclasses.

<a name="7.3"></a>
###  7.3 UCLASS
Você também pode declarar classes C ++ personalizadas, que se comportam como classes UE4, declarando seus objetos C ++ personalizados como UCLASS. UCLASS usa *Smart Pointers* do UE4 e rotinas de gerenciamento de memória para alocação e desalocação de acordo com as regras do Smart Pointer, podem ser carregados e lidos pelo *UE4 Editor* e opcionalmente acessados a partir de Blueprints.

Exemplo:

```cpp
UCLASS(ClassGroup=(Custom),meta=(BlueprintSpawnableComponent) )
```
Os parâmetros descritos no exemplo são os [especificadores](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/GameplayArchitecture/Classes/Specifiers/ "Class Specifiers") da classe que irão determinar o seu comportamento.

- `BlueprintSpawnableComponent` - Se estiver presente, o componente Class pode ser gerado por um Blueprint.
- `ClassGroup=GroupName` - Indica que o Navegador de ator do Unreal Editor deve incluir esta classe e qualquer subclasse dessa classe dentro do GroupName especificado quando a Visualização de grupo estiver ativada no Navegador de ator.

<a name="7.4"></a>
### 7.4 UFUNCTION
Um **UFunction** é uma função C ++ que é reconhecida pelo sistema de reflexão Unreal Engine 4 (UE4). Qualquer **UObject** ou biblioteca de função Blueprint pode declarar uma função de membro como um **UFunction**, colocando a macro UFUNCTION na linha acima da declaração da função no arquivo de cabeçalho. A macro oferecerá suporte a Especificadores de Função para alterar como o UE4 interpreta e usa uma função.

Ao declarar funções, os especificadores de função podem ser adicionados à declaração para controlar como a função se comporta com vários aspectos do mecanismo e do editor.

Exemplo:
```cpp
UFUNCTION(BlueprintCallable, Category = "Plataforma")
void AddActiveTrigger();
```
- `BlueprintAuthorityOnly` - Esta função só será executada a partir do código Blueprint se for executada em uma máquina com autoridade de rede (um servidor, servidor dedicado ou jogo para um único jogador).
- `BlueprintCallable` - A função pode ser executada em um gráfico Blueprint ou Level Blueprint.

<a name="7.4"></a>
### 7.5 UPROPERTY
As propriedades são declaradas usando a sintaxe de variável C ++ padrão, precedida pela macro UPROPERTY que define metadados de propriedade e especificadores de variável.

Ao declarar propriedades, os Especificadores de Propriedade podem ser adicionados à declaração para controlar como a propriedade se comporta com vários aspectos do Motor e do Editor.

```cpp
UPROPERTY(EditAnywhere, Meta = (MakeEditWidget = true))
  FVector TargetLocation;
```
- `BlueprintReadOnly` - Esta propriedade pode ser lida pelo Blueprints, mas não modificada. Este especificador é incompatível com o especificador BlueprintReadWrite.
- `BlueprintReadWrite` - Esta propriedade pode ser lida ou escrita a partir de um Blueprint. Este especificador é incompatível com o especificador BlueprintReadOnly.
- `EditAnywhere` - Indica que esta propriedade pode ser editada por janelas de propriedades, em arquétipos e instâncias. Este especificador é incompatível com qualquer um dos especificadores "visíveis".
- `MakeEditWidget` - Usado para propriedades *Transform* ou *Rotator*, ou Matrizes de *Transforms* ou *Rotators*. Indica que a propriedade deve ser exposta na janela de visualização como um *widget* móvel.

**[⬆ Volta para o início](#índice)**
<a name="8"></a>
## 8. Funções Virtuais - virtual
> Uma função virtual é uma função de membro que é declarada dentro de uma classe base e é redefinida (Substituída) por uma classe derivada. Quando você se refere a um objeto de classe derivada usando um ponteiro ou uma referência à classe base, pode chamar uma função virtual para esse objeto e executar a versão da função da classe derivada.

[Funções Virtuais](https://pt.wikipedia.org/wiki/Fun%C3%A7%C3%A3o_virtual "Funções Virtuais")

- As funções virtuais garantem que a função correta seja chamada para um objeto, independentemente do tipo de referência (ou ponteiro) usado para a chamada da função.
- Eles são usados principalmente para obter polimorfismo de tempo de execução.
- As funções são declaradas com uma palavra-chave virtual na classe base.
- A resolução da chamada de função é feita em tempo de execução.

Exemplo:
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

Na função anotherFunction o método chamado em OnFire é WeaponRifle::OnFire().
O método WeaponBase::OnFire não é chamado pois foi sobreposto.


***

## Referências
- [Unreal Property System (Reflection)](https://www.unrealengine.com/en-US/blog/unreal-property-system-reflection?sessionInvalidated=true)
- [The UCLASS() macro ](https://romeroblueprints.blogspot.com/2020/10/the-uclass-macro.html)
- [Exposing Gameplay Elements to Blueprints](https://docs.unrealengine.com/en-US/Engine/Blueprints/TechnicalGuide/ExtendingBlueprints/index.html)
- [Macros](
https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Macros/index.html)
- [UFunctions](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Reference/Functions/index.html)
- [UPROPERTY](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Reference/Properties/index.html)
- [Access modifiers in C++](https://www.geeksforgeeks.org/access-modifiers-in-c/)
- [Virtual Function in C++](https://www.geeksforgeeks.org/virtual-function-cpp/)
- [Inheritance](https://www.youtube.com/watch?v=X8nYM8wdNRE&list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb&index=27)
- [Virtual Functions in C++](https://www.youtube.com/watch?v=oIV2KchSyGQ&list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb&index=28)
- [Default IntelliSense and UE4](https://docs.wholetomato.com/default.asp?W805)
