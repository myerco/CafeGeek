---
title: Usando Structs
excerpt: Neste capítulo vamos explorar o tipo de variável Struct.  
permalink: /unreal-engine-capitulo-2/usando-structs
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 203
tags:
  - variáveis estruturadas
---

## 1. O que são variáveis do tipo Structure?

**Structure**, são estruturas de dados também conhecidas como **registros**, permitem que um usuário combine itens de dados de (possivelmente) diferentes tipos de dados sob um único nome. Em outras palavras, é uma variável que contém outros variáveis de diferentes tipos.  

Podem ser utilizadas para definir propriedades de um elemento do jogo como por exemplo os personagens.

## 2. Structure e Class

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

### 2.3. C++ Struct Unreal

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

### 2.4. C++ Class Unreal

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

Neste passo vamos criar o objeto *SJogador* do tipo `Structure` para exemplificar o uso das variáveis utilizando o menu de contexto `Blueprints` > `Structure`.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-blueprint-structure.webp"
    alt="Figura: Menu de contexto Blueprints > Structure."
    caption="Cria o objeto do tipo Structure."
%}

### 3.1. Definindo variáveis dentro da estrutura

A seguir vamos adicionar variáveis dentro do da estrutura criada.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-blueprint-structure-variables.webp"
    alt="Figura: Editor de Structure."
    caption="Podemos adicionar e salvar novos tipos de dados."
%}

| Nome      | Tipo                   | Descrição                                            |
| :-------- | :--------------------- | :--------------------------------------------------- |
| Nome      | `Name`                 | Armazena o nome do jogador                           |
| Life      | `Float`                | Total de vida do jogador                             |
| Strength  | `Float`                | Total de força do jogador                            |
| Level     | `Integer`              | O Nível que o jogador se encontra                    |
| Image     | `Texture2D/References` | Armazena imagem 2d que representa o jogador          |
| Character | `Character/Class`      | Armazena a classe de objeto do personagem do jogador |

### 3.2. Acessando as variáveis

Para acessar as variáveis que estão dentro da objeto do tipo `Structure` vamos utilizar `Break Structure`.  

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-blueprint-structure-break.webp"
    alt="Figura: Exemplo de Break Structure."
    caption="Usamos esse nó para acessar as variáveis dentro da estrutura."
%}

### 3.3. Atualizando as variáveis

Quanto necessitamos atualizar as variáveis que estão contidas dentro de uma estrutura, podemos selecionar o variável e arrastar a conexão para abrir a lista de seleção de objetos e funções relacionados e selecionamos `Set Members`.

{% include iframe.html
    src="https://blueprintue.com/render/3hzx4m-2/"
    title="Cafegeek - Usando e atualizando variáveis do tipo Struct"
    caption="Para atualizar a variável usamos Set Members in."
    ref="https://blueprintue.com/render/3hzx4m-2/"
%}

**Info** - Variável SLights do tipo `Struct`;

**Info.Status** - Variável `enum` com os valores LightOn e LightOff;

**Set Members in SLights** - Função para atualização as variáveis membro de uma estrutura, SLights.

### 3.4. Exemplo do uso de variáveis Structure

Para exemplificar a utilização de variáveis `Structure` vamos implementar um level onde os elementos serão construídos dinamicamente, para tal vamos utilizar uma *Array* de objetos do tipo `Point Light Component` para que possam ser adicionados na cena no momento de construção do objeto.

#### 3.4.1. Criando o objeto SControleLuzes

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-variable-2.webp"
    alt="Figura: Exemplo do objeto SControleLuzes."
    caption=""
%}

#### 3.4.2. Lógica para construir os elementos na cena

**1.** Crie um `level` utilizando o modelo `default`;

**2.** Implemente um `Blueprint Actor` com o nome `BP_ControleLuzes`;

**3.** Adicionar as variáveis :

**Luzes** - *Array* de tipo `Point Light Component`;

**ControLuzes** - *Array* de tipo `SControleLuzes`;

**Total_luzes** : Integer.

**4.** Na construção do objeto (*Construction Script*) adicionamos elementos `Point light component` na cena e logo em seguida no array *Luzes*.  

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-loop-array-structures.webp"
    alt="Figura: Lógica que adiciona os elementos em um array do mesmo tipo (PointLightComponent)."
    caption=""
%}

**5.** Ao terminar o primeiro `loop` reconstruímos o *array* de controle *ControLuzes* e o percorremos em conjunto com o array *luzes* para configurar as propriedades dos elementos.  

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-loop-set-struct.webp"
    alt="Figura: Lógica que altara as propriedades dos objetos do array."
    caption=""
%}

**6.** Adicione o elemento **BP_ControleLuzes** na cena para visualizar as luzes sendo construídas.
