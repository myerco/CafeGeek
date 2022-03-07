---
title: Structure - Variáveis estruturadas
description: Structure, é um tipo de dados definido pelo usuário disponível no Unreal Engine em C++ e Blueprint, neste capitulo vamos explorar estes objetos.  
tags: [Unreal Engine,Structure]
layout: page
---

***

<a name="8"></a>
## CAPÍTULO 8 - Estruturas de dados e Interface com usuário

**Structure**, é um tipo de dados definido pelo usuário disponível no **Unreal Engine** em **C++** e **Blueprint**, neste capitulo vamos explorar estes objetos.

&nbsp;&nbsp;[8.1 O que são variáveis do tipo Structure?](#8.1)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8.1.1 Exemplo do uso de variáveis Structure](#8.1.1)    

***

<a name="8.1"></a>
## 8.1 O que são variáveis do tipo Structure?
**Structure**, são estruturas de dados também conhecidas como **registros**, permitem que um usuário combine itens de dados de (possivelmente) diferentes tipos de dados sob um único nome. Em outras palavras, é uma variável que contém outros variáveis de diferentes tipos.  

Podem ser utilizadas para definir propriedades de um elemento do jogo como por exemplo os personagens.

**Structure e Class.**

Em **C++**, uma estrutura é realmente a mesma coisa que uma **Class**, exceto por algumas diferenças sintáticas.  

Por exemplo, **Structs** em **C++** padronizam suas variáveis de membro como públicas por padrão, enquanto as classes têm variáveis privadas por padrão.

**C++ Struct.**

```cpp
struct Character {
    int velocidade;
    int forca;
    bool correndo;
};
```

**C++ Class**

```cpp
class Character {
    int Velocidade;
    int Forca;
    bool Correndo;
};
```

**C++ Struct Unreal**

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

**C++ Class Unreal**

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
<a name="8.1.1"></a>
### 8.1.1 Criando variáveis do tipo Structure com Blueprint

Neste passo vamos criar o objeto *SJogador* do tipo `Structure` para exemplificar o uso das variáveis utilizando o menu de contexto `Blueprints` > `Structure`.

![Figura: Blueprint - Menu de contexto Blueprints > Structure.](imagens/estruturas/blueprint_menu_structure.webp "Figura: Blueprint - Menu de contexto Blueprints > Structure.")

> Figura: Blueprint - Menu de contexto Blueprints > Structure.


**Definindo variáveis dentro da estrutura.**

A seguir vamos adicionar variáveis dentro do da estrutura criada.

![Figura: Blueprint - Editor de Structure.](imagens/estruturas/blueprint_variable.webp "Figura: Blueprint - Editor de Structure.")

> Figura: Blueprint - Editor de Structure.

1. Nome do tipo `Name` - Armazena o nome do jogador;

1. Vida do tipo `Float` - Total de vida do jogador.;

1. Forca do tipo `Float` - Total de força do jogador;

1. Nivel do tipo `Integer` - O Nível que o jogador se encontra;

1. Imagem do tipo `Texture2D/References` - Armazena imagem 2d que representa o jogador;

1. Personagem do tipo `Character/Class` - Armazena a classe de objeto do personagem do jogador.

**Acessando as variáveis.**

Para acessar as variáveis que estão dentro da objeto do tipo `Structure` vamos utilizar `Break Structure`.  

![Figura: Blueprint - Exemplo de Break Structure.](imagens/estruturas/blueprint_break_structure.webp "Figura: Blueprint - Exemplo de Break Structure.")

> Figura: Blueprint - Exemplo de Break Structure.

<a name="8.1.1"></a>
### 8.1.1 Exemplo do uso de variáveis Structure

Para exemplificar a utilização de variáveis `Structure` vamos implementar um level onde os elementos serão construídos dinamicamente, para tal vamos utilizar uma *Array* de objetos do tipo `Point Light Component` para que possam ser adicionados na cena no momento de construção do objeto.

**Criando o objeto SControleLuzes.**

![Figura: Blueprint - Exemplo do objeto SControleLuzes.](imagens/estruturas/blueprint_variable_2.webp "Figura: Blueprint - Exemplo do objeto SControleLuzes.")  

> Figura: Blueprint - Exemplo do objeto SControleLuzes.

**Lógica para construir os elementos na cena.**

1. Crie um `level` utilizando o modelo `default`.

2. Implemente um `Blueprint Actor` com o nome **BP_ControleLuzes**.

3. Adicionar as variáveis :
    - **Luzes** - *Array* de tipo `Point Light Component`;

    - **ControLuzes** - *Array* de tipo `SControleLuzes`;

    - **Total_luzes** : Integer.

4. Na construção do objeto (*Construction Script*) adicionamos elementos `Point light component` na cena e logo em seguida no array *Luzes*.  
  ![Figura: Blueprint - Lógica que adiciona os elementos em um array do mesmo tipo (PointLightComponent).](imagens/estruturas/blueprint_loop_array_structures.webp "Figura: Blueprint - Lógica que adiciona os elementos em um array do mesmo tipo (PointLightComponent).")  

  > Figura: Blueprint - Lógica que adiciona os elementos em um array do mesmo tipo (PointLightComponent).

5. Ao terminar o primeiro `loop` reconstruímos o *array* de controle *ControLuzes* e o percorremos em conjunto com o array *luzes* para configurar as propriedades dos elementos.  
  ![Figura: Blueprint - Lógica que altara as propriedades dos objetos do array.](imagens/estruturas/blueprint_loop_set_struct.webp "Figura: Blueprint - Lógica que altara as propriedades dos objetos do array.")  

  > Figura: Blueprint - Lógica que altara as propriedades dos objetos do array.

6. Adicione o elemento **BP_ControleLuzes** na cena para visualizar as luzes sendo construídas.