---
title: Variáveis estruturadas
excerpt: Structure, é um tipo de dados definido pelo usuário disponível no Unreal Engine em C++ e Blueprint, neste capitulo vamos explorar estes objetos.  
permalink: /pages/unreal_engine/variaveis_estruturadas
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true  
---

**Structure**, é um tipo de dados definido pelo usuário disponível no **Unreal Engine** em **C++** e **Blueprint**, neste capitulo vamos explorar estes objetos.

## 1. O que são variáveis do tipo Structure?

***

**Structure**, são estruturas de dados também conhecidas como **registros**, permitem que um usuário combine itens de dados de (possivelmente) diferentes tipos de dados sob um único nome. Em outras palavras, é uma variável que contém outros variáveis de diferentes tipos.  

Podem ser utilizadas para definir propriedades de um elemento do jogo como por exemplo os personagens.

## 2. Structure e Class

***

Em **C++**, uma estrutura é realmente a mesma coisa que uma **Class**, exceto por algumas diferenças sintáticas.  

Por exemplo, **Structs** em **C++** padronizam suas variáveis de membro como públicas por padrão, enquanto as classes têm variáveis privadas por padrão.

### 2.1. C++ Struct

```cpp
struct Character {
    int velocidade;
    int forca;
    bool correndo;
};
```

### 2.2. C++ Class

```cpp
class Character {
    int Velocidade;
    int Forca;
    bool Correndo;
};
```

#### 2.2.1. C++ Struct Unreal

```cpp
USTRUCT([Specifier, Specifier, ...])
struct FStructName
{
    GENERATED_BODY()

    int32 Velocidade;
    int32 Forca;

    UPROPERTY()
    bool Correndo;
};
```

#### 2.2.2. C++ Class Unreal

```cpp
UCLASS()
class YOURMODULE_API APlayerCharacter: public ACharacter
{
  GENERATED_BODY()
public:
  UFUNCTION(BlueprintCallable, Category="Player")
  bool EstaCorrendo();

private:
        bool Correndo = false;
        int32 Velocidade=100;
        int32 Forca = 100;
};
```

## 3. Criando variáveis do tipo Structure com Blueprint

***

Neste passo vamos criar o objeto *SJogador* do tipo `Structure` para exemplificar o uso das variáveis utilizando o menu de contexto `Blueprints` > `Structure`.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_menu_structure.webp"
    alt="Figura: Blueprint - Menu de contexto Blueprints > Structure."
    caption="Figura: Blueprint - Menu de contexto Blueprints > Structure."
%}

### 3.1. Definindo variáveis dentro da estrutura

A seguir vamos adicionar variáveis dentro do da estrutura criada.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_variable.webp"
    alt="Figura: Blueprint - Editor de Structure.."
    caption="Figura: Blueprint - Editor de Structure."
%}

1. Nome do tipo `Name` - Armazena o nome do jogador;

1. Vida do tipo `Float` - Total de vida do jogador.;

1. Forca do tipo `Float` - Total de força do jogador;

1. Nível do tipo `Integer` - O Nível que o jogador se encontra;

1. Imagem do tipo `Texture2D/References` - Armazena imagem 2d que representa o jogador;

1. Personagem do tipo `Character/Class` - Armazena a classe de objeto do personagem do jogador.

### 3.2. Acessando as variáveis

Para acessar as variáveis que estão dentro da objeto do tipo `Structure` vamos utilizar `Break Structure`.  

{% include imagelocal.html
    src="unreal/estruturas/blueprint_break_structure.webp"
    alt="Figura: Blueprint - Exemplo de Break Structure."
    caption="Figura: Blueprint - Exemplo de Break Structure."
%}

### 3.3. Exemplo do uso de variáveis Structure

Para exemplificar a utilização de variáveis `Structure` vamos implementar um level onde os elementos serão construídos dinamicamente, para tal vamos utilizar uma *Array* de objetos do tipo `Point Light Component` para que possam ser adicionados na cena no momento de construção do objeto.

#### 3.3.1. Criando o objeto SControleLuzes

{% include imagelocal.html
    src="unreal/estruturas/blueprint_variable_2.webp"
    alt="Figura: Blueprint - Exemplo do objeto SControleLuzes."
    caption="Figura: Blueprint - Exemplo do objeto SControleLuzes."
%}

#### 3.3.2. Lógica para construir os elementos na cena

1. Crie um `level` utilizando o modelo `default`;

1. Implemente um `Blueprint Actor` com o nome `BP_ControleLuzes`;

1. Adicionar as variáveis :

    - **Luzes** - *Array* de tipo `Point Light Component`;

    - **ControLuzes** - *Array* de tipo `SControleLuzes`;

    - **Total_luzes** : Integer.

1. Na construção do objeto (*Construction Script*) adicionamos elementos `Point light component` na cena e logo em seguida no array *Luzes*.  

{% include imagelocal.html
    src="unreal/estruturas/blueprint_loop_array_structures.webp"
    alt="Figura: Blueprint - Lógica que adiciona os elementos em um array do mesmo tipo (PointLightComponent)."
    caption="Figura: Blueprint - Lógica que adiciona os elementos em um array do mesmo tipo (PointLightComponent)."
%}

1. Ao terminar o primeiro `loop` reconstruímos o *array* de controle *ControLuzes* e o percorremos em conjunto com o array *luzes* para configurar as propriedades dos elementos.  

{% include imagelocal.html
    src="unreal/estruturas/blueprint_loop_set_struct.webp"
    alt="Figura: Blueprint - Lógica que altara as propriedades dos objetos do array."
    caption="Figura: Blueprint - Lógica que altara as propriedades dos objetos do array."
%}

1. Adicione o elemento **BP_ControleLuzes** na cena para visualizar as luzes sendo construídas.