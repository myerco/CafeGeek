---
title: Estruturas de programação no Unreal Engine
description: Neste capítulo serão descritas as estruturas de armazenamento, manipulação e fluxo da lógica de programação.
tags: [Unreal Engine,blueprint,programação,estruturas,variáveis,c++]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
date: 2022-09-21 
---

***

- [O que são variáveis?](#o-que-são-variáveis)
- [Variáveis no Unreal Engine](#variáveis-no-unreal-engine)
  - [Tipos de Variáveis](#tipos-de-variáveis)
  - [Declarando variáveis](#declarando-variáveis)
- [Variáveis em C++](#variáveis-em-c)
  - [Declarando variáveis em C++](#declarando-variáveis-em-c)
  - [Expondo variáveis para o Editor](#expondo-variáveis-para-o-editor)
- [Métodos Get e Set](#métodos-get-e-set)
  - [Métodos Get e Set Blueprint](#métodos-get-e-set-blueprint)
  - [Métodos Get e Set em C++](#métodos-get-e-set-em-c)
- [Tratamento e armazenamento de texto no Unreal Engine](#tratamento-e-armazenamento-de-texto-no-unreal-engine)
  - [Strings em Blueprint](#strings-em-blueprint)
  - [String em C++](#string-em-c)
    - [Concatenando textos usando a função Append](#concatenando-textos-usando-a-função-append)
    - [Procurando texto dentro de uma string em Blueprint](#procurando-texto-dentro-de-uma-string-em-blueprint)
    - [Procurando texto com C++](#procurando-texto-com-c)
- [Variáveis do tipo numéricas Integer e Float](#variáveis-do-tipo-numéricas-integer-e-float)
  - [Inteiro em Blueprint](#inteiro-em-blueprint)
  - [Inteiro em C++](#inteiro-em-c)
- [Armazenando valores lógicos com Boolean](#armazenando-valores-lógicos-com-boolean)
- [Controle de acesso a variáveis](#controle-de-acesso-a-variáveis)
  - [Variáveis Privadas](#variáveis-privadas)
  - [Variáveis Públicas](#variáveis-públicas)
- [O que são estruturas de controle ou fluxo?](#o-que-são-estruturas-de-controle-ou-fluxo)
  - [Exemplo de fluxo de execução em C++](#exemplo-de-fluxo-de-execução-em-c)
  - [Exemplo de fluxo condicional](#exemplo-de-fluxo-condicional)
  - [Exemplo de fluxo de repetição](#exemplo-de-fluxo-de-repetição)
- [Estruturas de fluxo condicional](#estruturas-de-fluxo-condicional)
  - [Controle de fluxo com Branch (if)](#controle-de-fluxo-com-branch-if)
    - [IF em Blueprint](#if-em-blueprint)
    - [IF em C++](#if-em-c)
  - [Switch Nodes](#switch-nodes)
    - [Switchs node em Blueprint](#switchs-node-em-blueprint)
    - [Switchs node em C++](#switchs-node-em-c)
  - [Referências](#referências)
  - [Sequenciamento de fluxo com Sequence](#sequenciamento-de-fluxo-com-sequence)
    - [Sequence em Blueprint](#sequence-em-blueprint)
    - [Sequence em C++](#sequence-em-c)
  - [Flip Flop em Blueprint](#flip-flop-em-blueprint)
  - [Flip Flop em C++](#flip-flop-em-c)
  - [Gate e Multi Gate em Blueprint](#gate-e-multi-gate-em-blueprint)
  - [Gate e Multi Gate em C++](#gate-e-multi-gate-em-c)
- [Estruturas de repetição](#estruturas-de-repetição)
  - [For Loop em Blueprint](#for-loop-em-blueprint)
  - [For Loop em C++](#for-loop-em-c)
  - [While Loop em Blueprint](#while-loop-em-blueprint)
  - [While Loop em C++](#while-loop-em-c)
  - [Do N em Blueprint](#do-n-em-blueprint)
  - [Do N em C++](#do-n-em-c)
  - [Do once em Blueprint](#do-once-em-blueprint)
  - [Do once em C++](#do-once-em-c)
- [O que são variáveis do tipo array?](#o-que-são-variáveis-do-tipo-array)
- [Declarando arrays e acessando os seus elementos](#declarando-arrays-e-acessando-os-seus-elementos)
  - [Array em Blueprint](#array-em-blueprint)
  - [Método Get para arrays com Blueprint](#método-get-para-arrays-com-blueprint)
  - [Método Get para arrays com C++](#método-get-para-arrays-com-c)
  - [Get utilizando uma variável como índice com Blueprint](#get-utilizando-uma-variável-como-índice-com-blueprint)
  - [Get utilizando uma variável como índice com C++](#get-utilizando-uma-variável-como-índice-com-c)
  - [Último índice e a quantidade de elementos do array em Blueprint](#último-índice-e-a-quantidade-de-elementos-do-array-em-blueprint)
- [Percorrendo arrays](#percorrendo-arrays)
  - [Listando todos os elementos utilizando For usando Blueprint](#listando-todos-os-elementos-utilizando-for-usando-blueprint)
  - [Listando todos os elementos utilizando For usando C++](#listando-todos-os-elementos-utilizando-for-usando-c)
  - [Usando o comando Find com Blueprint](#usando-o-comando-find-com-blueprint)
  - [Usando o comando Find com C++](#usando-o-comando-find-com-c)
  - [Contando elementos dentro de um array com Blueprint](#contando-elementos-dentro-de-um-array-com-blueprint)
  - [Contando elementos dentro de um array com C++](#contando-elementos-dentro-de-um-array-com-c)
  - [Percorrendo e atualizando dados com Blueprint](#percorrendo-e-atualizando-dados-com-blueprint)
  - [Percorrendo e atualizando dados com C++](#percorrendo-e-atualizando-dados-com-c)
- [Removendo elementos do array](#removendo-elementos-do-array)
  - [Removendo utilizando Remove com Blueprint](#removendo-utilizando-remove-com-blueprint)
  - [Removendo utilizando Remove com C++](#removendo-utilizando-remove-com-c)
  - [Removendo passando uma variável como parâmetro com Blueprint](#removendo-passando-uma-variável-como-parâmetro-com-blueprint)
  - [Removendo passando uma variável como parâmetro com C++](#removendo-passando-uma-variável-como-parâmetro-com-c)
  - [Removendo utilizando nó Remove Index com Blueprint](#removendo-utilizando-nó-remove-index-com-blueprint)
  - [Removendo utilizando nó Remove Index com C++](#removendo-utilizando-nó-remove-index-com-c)
  - [Limpando o array com Clear com Blueprint](#limpando-o-array-com-clear-com-blueprint)
  - [Limpando o array com Clear com C++](#limpando-o-array-com-clear-com-c)
- [O que são Enums?](#o-que-são-enums)
  - [Criando Enums no Unreal Engine e Blueprint](#criando-enums-no-unreal-engine-e-blueprint)
  - [Criando Enums no Unreal Engine e C++](#criando-enums-no-unreal-engine-e-c)
  - [Exemplos de uso - A lâmpada](#exemplos-de-uso---a-lâmpada)
  - [A lâmpada em C++](#a-lâmpada-em-c)
  - [Arquivo Header da lâmpada em C++](#arquivo-header-da-lâmpada-em-c)
  - [Verificando o estado utilizando o Enum com Blueprint](#verificando-o-estado-utilizando-o-enum-com-blueprint)
  - [Verificando o estado utilizando o Enum com C++](#verificando-o-estado-utilizando-o-enum-com-c)
  - [Ligando e desligando utilizando o Enum com Blueprint](#ligando-e-desligando-utilizando-o-enum-com-blueprint)
  - [Ligando e desligando utilizando o Enum com C++](#ligando-e-desligando-utilizando-o-enum-com-c)
  - [Exemplos de uso - A pedra das emoções](#exemplos-de-uso---a-pedra-das-emoções)

***

{% include logo.html
    src="unreal/variaveis/unreal_engine_variables.webp"
    alt="Blueprint Variables."
    caption="Blueprint Variables."
%}

## O que são variáveis?

***

Variáveis são estruturas que são utilizadas para armazenar um valor de um determinado tipo na memória do computador.

Estrutura de memória.

| Variável |  Tipo   |   Valor   |
| :------- | :-----: | :-------: |
| iSoma    | Integer |     0     |
| fValor   |  Float  |    6.5    |
| tName    | String  | "Gandalf" |
| bRunnig  | Boolean |   false   |
| vLista   | FVector |  (1,2,4)  |

Abaixo um exemplo em C++:

```cpp
// Variável do tipo inteiro
int iSoma = 0;

// Variável do tipo ponto flutuante
float fValor = 6.5;
```

## Variáveis no Unreal Engine

***

Variáveis no **Unreal Engine** são propriedades que contêm um valor ou fazem referência a um objeto ou ator no mundo. Essas propriedades podem ser acessíveis internamente ao **Blueprint** que as contém, ou podem ser tornadas acessíveis externamente para que seus valores possam ser modificados por designers que trabalham com instâncias do **Blueprint** colocadas em um nível.

### Tipos de Variáveis

Para armazenar qualquer informação na memória devemos definir um tipo de dados primitivo ou mesmo uma estrutura de dados, a seguir alguns tipos de dados:

- `Boolean` - Armazena valores falso ou verdadeiro (true e false).

    ```cpp
    bool VariavelBoolean;
    VariavelBoolean = true;
    ```

- `Integer` - Valores inteiros entre −2.147.483.648 e 2.147.483.647

    ```cpp
    int32 VariavelInt;
    VariavelInt = 1;
    ```

    Utilize int32, uint8, uint32 para representar números inteiros.

- `Float` - Valores com casas decimais tal como 0,0553, 101,2887 e -78,322 .

    ```cpp
    float VariavelFloat;
    VariavelFloat = 2.4;
    ```

- `String`- Grupo de caracteres alfanuméricos.

    ```cpp
    FString VariavelString ;
    VariavelString = TEXT("Alo mundo!!");
    ```

### Declarando variáveis

Declarando variáveis informamos ao computador que estamos reservando um espaço de memória temporário.  

{% include imagelocal.html
    src="unreal/variaveis/unreal_engine_variable.webp"
    alt="Figura: Blueprint Variables."
    caption="Variáveis no Editor de Blueprint."
%}

{% include imagelocal.html
    src="unreal/variaveis/unreal_engine_variable_details.webp"
    alt="Figura: Details ou propriedades das variáveis."
    caption="As variáveis tem tipos e propriedades que determinam o sua utilização."
%}

Observe que a propriedade `Category` agrupa as variáveis por uma categoria.

## Variáveis em C++

***

### Declarando variáveis em C++

```cpp
    int32 Count;
```

### Expondo variáveis para o Editor

```cpp
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Parâmetros")
    int32 iLife = 10;
```

## Métodos Get e Set

***

Para acessar o conteúdo das variáveis utilizamos os métodos `Get` e `Set`, onde:

- `Get`: Obtém o valor de uma variável.

- `Set`: Atualiza o valor da variável.

### Métodos Get e Set Blueprint

{% include imagelocal.html
    src="unreal/variaveis/unreal_engine_get_set.webp"
    alt="Figura: Métodos Get e Set."
    caption="Get se Set, obtém e atualiza respectivamente a variável Life."
%}

- `BeginPlay` - Ao iniciar o jogo a lista de comandos conectados a estes nó deve ser acionado.

- `Print String` - Escreve um texto na cena do jogo.

- `Add +` - Variáveis numéricas podem ser manipuladas com operadores matemáticos.

- `Converts` - Converte tipos de variáveis, neste caso converte um valor do tipo `integer` em um do tipo `String`.

### Métodos Get e Set em C++

Arquivo Header.

```cpp
// MyHero.h
UPROPERTY()
virtual void BeginPlay() override;
```

Arquivo de implementação.

```cpp
// Myhero.cpp
void AMyHeroClass::BeginPlay()
 {
    Super::BeginPlay();
    int32 iLifeLocal = 5;
    float fSpeed = 3.7f;
    FString fsName = TEXT("O nome do personagem é Nostromo");
    iLifeLocal = iLifeLocal + iLife;
    // iLife é uma variável global
    UE_LOG(LogTemp, Warning, TEXT("O resultado é =, %d %f %s"), iLife, fSpeed, *fsName );
 }
 ```

## Tratamento e armazenamento de texto no Unreal Engine

***

No **Unreal Engine** são definidos alguns tipos de dados para manipulação e armazenamento de caracteres alfanuméricos, entre elas estão os tipos de variáveis a seguir.

| Variável | Tamanho  | Considerações                                                                                                                                      |
| :------: | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
|  `Text`  | 40 Bytes | Podemos adicionar opções avançadas como exemplo `String Table`, ideal para textos longos que podem variar conforme a lingua definida pelo jogador. |
| `String` | 16 Bytes | Armazenamento e consumo de memória mediano                                                                                                         |
|  `Name`  | 8 Bytes  | Cadeias de caracteres  curtas que ocupam pouca memória.                                                                                            |

Podemos realizar as seguintes operações em `strings`:

- Atribuir o valor de uma `string` para outra;

- Acessar caracteres individualmente;

- Adicionar uma `string` no final de outra;

- Concatenar `strings`;

- Procurar uma determinada letra ou Substring dentro da `string`.

### Strings em Blueprint

{% include imagelocal.html
    src="unreal/variaveis/unreal_engine_string_functions.webp"
    alt="Figura: String functions."
    caption="Append - Concatena tuas ou mais strings, Contains- Retorna falso ou verdadeiro se encontra um string dentro de outra."
%}

### String em C++

Arquivo header.

```cpp
// myHero.h
UPROPERTY()
virtual void BeginPlay() override;

UPROPERTY()
FString NomeCharacter;

UPROPERTY()
FString ClassCharacter;

```

Arquivo de implementação.

```cpp
// myHero.cpp
void AMyHeroClass::BeginPlay()
 {
    Super::BeginPlay();

    FString fsMessage = TEXT("Procurando a classe do personagem");
    FString fsResultado;

    fsResultado.append("O nome é ",*NomeCharacter)

    // ou
    fsResultado =TEXT("O nome é ");
    fsResultado += *NomeCharacter;

    UE_LOG(LogTemp, Warning, TEXT("O resultado é =,  %s"), *fsResultado );

    // Procurando uma Substring
    if (fsMessage.Contains("class"))
    {
      UE_LOG(LogTemp, Warning, TEXT("Encontrei!!"));
    }
    else
        UE_LOG(LogTemp, Warning, TEXT("Não encontrei"));
 }

```

#### Concatenando textos usando a função Append

A função `Append` concatena duas ou mais `strings`, passamos como parâmetros os textos que gostaríamos de concatenar e tendo como resultado um novo texto contendo os dois textos.

```cpp

FString sTexto = TEXT("Alo mundo...");
sTexto.append("Cruel");

// Resultado: Alo mundo...Cruel
```

#### Procurando texto dentro de uma string em Blueprint

A função `Contains` procura uma sequencia de caracteres dentro de uma `string`, passamos os seguintes parâmetros para a função.

- `Search In` - Texto passado como parâmetro.
- `Substring` - Texto que deve ser localizado.
- `Use Case` - Diferencia maiúsculas e minúsculas.
 `Search from end` - Inicia a busca pelo fim do texto.

#### Procurando texto com C++

```cpp

FString sTexto = TEXT("Procurando o texto escondido.");

if (sTexto.Contains(TEXT("texto")))
{
  return true;
}
else
  return false;

// Resultado: Alo mundo...Cruel
```

## Variáveis do tipo numéricas Integer e Float

***

### Inteiro em Blueprint

Valores numéricos utilizam operadores matemáticos para a sua manutenção, como veremos a seguir.  

{% include imagelocal.html
    src="unreal/variaveis/unreal_engine_variable_division.webp"
    alt="Figura: Utilizando Divisão com inteiros."
    caption="A exemplo acima divide um inteiro por 2 e trunca o resultado."
%}

{% include imagelocal.html
    src="unreal/variaveis/unreal_engine_variable_multiplication.webp"
    alt="Figura: Multiplicação valores."
    caption="Neste exemplo multiplicamos o valor por 100."
%}

### Inteiro em C++

***

```cpp
void AMyCharacterClass::BeginPlay()
{
    Super::BeginPlay();
    Float fStrength = 10;
    int32 iLife = 0;

    iLife = int(fStrength / 2);
}
```

- (+) - soma;

- (*) - Multiplicação;

- (/) - Divisão.

## Armazenando valores lógicos com Boolean

***

Variáveis Boolean armazenam dois valores : falso `false` ou verdadeiro `true`.

{% include imagelocal.html
    src="unreal/variaveis/unreal_engine_variable_boolean.webp"
    alt="Figura: Variável Boolean."
    caption="No exemplo acima se o valor de life for maior que 50 então o valor é atualizado para true."
%}

## Controle de acesso a variáveis

***

Como especificar quais variáveis de um objeto um usuário pode acessar e quais estão fora dos limites? - usando os especificadores de controle de acesso público e privado.

### Variáveis Privadas

Variáveis privadas só podem ser acessadas por membros da mesma classe.

Variavel private usando Blueprint.

{% include imagelocal.html
    src="unreal/variaveis/unreal_engine_variable_private_details.webp"
    alt="Figura: Private details."
    caption="Com a opção Privada marcada em uma variável, isso evita que a variável seja modificada por módulos externos."
%}

Variáveis Privadas em C++.

```cpp
private:
   bool Running = false;
```

### Variáveis Públicas

Para permitir que uma variável seja modificada de fora de seu módulos, torne-a pública.  

Variavel públicas em Blueprint.

{% include imagelocal.html
    src="unreal/variaveis/unreal_engine_variable_public.webp"
    alt="Figura: Public."
    caption="Expondo a variável."
%}

{% include imagelocal.html
    src="unreal/variaveis/unreal_engine_variable_public_details.webp"
    alt="Figura: Public details."
    caption="Expõe a variável no Editor ViewPort."
%}

Variáveis Públicas com C++

```cpp
public:

  float Damage;

  UPROPERTY(BlueprintCallable, Category="Player")
  bool IsRunning;

```

## O que são estruturas de controle ou fluxo?

***

Em linguagens de programação existem métodos de tomada de decisão para tarefas corriqueiras que os programas podem executar, por exemplo a escolha de qual caminho ou instrução executar. Em **Blueprints** utilizamos nós específicos para controle de fluxo como por exemplo o `Branch`.

### Exemplo de fluxo de execução em C++

Considere a sequencia de comandos abaixo:

```cpp
int32 i, x, resultado=0;
i = 2;
x = 10;
resultado = i + x;
UE_LOG(LogTemp, Warning, TEXT("O resultado é %d"), resultado);

```

O resultado desse código é o valor 12 sendo apresentado na tela.

Agora vamos alterar o fluxo de execução:

```cpp
int i, x, resultado=0;
i = 2;
x = 10;
if ( i > x )
  resultado = i + x;

UE_LOG(LogTemp, Warning, TEXT("O resultado é %d"), resultado);
```

O resultado será 0 pois a condição de controle de fluxo **if** provocou um desvio do fluxo de instruções.

### Exemplo de fluxo condicional

|           | t1                                  | t2                                  | t3                                  | t4                                  | t5                                 | t6                                 | t7                                  | t8                                  | t9                                  |
| :-------- | :---------------------------------- | :---------------------------------- | :---------------------------------- | :---------------------------------- | :--------------------------------- | :--------------------------------- | :---------------------------------- | :---------------------------------- | :---------------------------------- |
| Principal | <span style="color:blue">--></span> | <span style="color:blue">--></span> | <span style="color:blue">--></span> | <span style="color:blue">-D-</span> |                                    |                                    | <span style="color:blue">-O-</span> | <span style="color:blue">--></span> | <span style="color:blue">--></span> |
| Desvio    |                                     |                                     |                                     | <span style="color:red">--></span>  | <span style="color:red">--></span> | <span style="color:red">--></span> | <span style="color:red">--></span>  |                                     |                                     |

### Exemplo de fluxo de repetição

|           | t1                                  | t2                                  | t3                                  | t4                                  | t5                                 | t6                                 | t7                                  | t8                                  | t9                                  |
| :-------- | :---------------------------------- | :---------------------------------- | :---------------------------------- | :---------------------------------- | :--------------------------------- | :--------------------------------- | :---------------------------------- | :---------------------------------- | :---------------------------------- |
| Principal | <span style="color:blue">--></span> | <span style="color:blue">--></span> | <span style="color:blue">--></span> | <span style="color:blue">-D-</span> | <span style="color:red"><--</span> | <span style="color:red"><--</span> | <span style="color:blue">-O-</span> | <span style="color:blue">--></span> | <span style="color:blue">--></span> |
| Desvio    |                                     |                                     |                                     | <span style="color:blue">--></span> | <span style="color:red">--></span> | <span style="color:red">--></span> | <span style="color:red">--></span>  |                                     |                                     |

## Estruturas de fluxo condicional

***

A seguir vamos entender como é fluxo condicional é descrito com programação visual usando **Blueprint**.

### Controle de fluxo com Branch (if)

`Branch` é uma estrutura condicional que testa uma variável utilizando uma expressão lógica e redireciona o fluxo da lógica.

#### IF em Blueprint

{% include imagelocal.html
    src="unreal/estruturascontrole/blueprint_example_if.webp"
    alt="Figura: Blueprint e branch ou if."
    caption="O teste acima verifica se um valor é maior que o outro e redireciona o fluxo."
%}

#### IF em C++

```cpp
if ( 2 >= 4)
{
  UE_LOG(LogTemp, Warning, TEXT("Escreve a mensagem caso a condição for verdadeira."));
}
else
{
  UE_LOG(LogTemp, Warning, TEXT("Escreve a mensagem caso a condição for falso."));
}
```

### Switch Nodes

O nó `Switch` lê uma entrada de dados e, com base no valor dessa entrada, envia o fluxo de execução para fora da saída de execução correspondente (ou padrão opcional). Existem vários tipos de opções disponíveis: `Int`, `String`, `Name` e `Enum`.

#### Switchs node em Blueprint

{% include imagelocal.html
    src="unreal/estruturascontrole/blueprint_exemple_switch.webp"
    alt="Figura: Blueprint e Switch ou Case."
    caption="Este comando verifica qual valor adente é igual ao parâmetro de entrada."
%}

#### Switchs node em C++

```cpp

switch (VariavelInt)
{
  case 0:
  {
    UE_LOG(LogTemp, Warning, TEXT("O valor é zero."));
    break;
  }  
  case 1:
  {
    UE_LOG(LogTemp, Warning, TEXT("O valor é um."));
  }    
  default:
  {
    UE_LOG(LogTemp, Warning, TEXT("O valor padrão."));
  }      
}

```

Em geral, os `switches` têm uma entrada de execução e uma entrada de dados para o tipo de dados que avaliam. As saídas são todas as saídas de execução. Os switches `Enum` geram automaticamente os pinos de execução de saída das propriedades do `Enum`, enquanto os `switches` `Int`, `String` e `Name` possuem pinos de execução de saída personalizáveis.

### Referências

- Unreal Engine, 2022. Flow Control - Nodes that allow for controlling the flow of execution based on conditions.  [https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/Blueprints/UserGuide/FlowControl/](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/Blueprints/UserGuide/FlowControl/ "Unreal Engine, 2022. Flow Control - Nodes that allow for controlling the flow of execution based on conditions")
- Couch Learn. (2019,Dezembro 27). Switch Statements in Unreal Engine 4. [https://couchlearn.com/switch-statements-in-unreal-engine-4/](https://couchlearn.com/switch-statements-in-unreal-engine-4/ "https://couchlearn.com/switch-statements-in-unreal-engine-4/")

### Sequenciamento de fluxo com Sequence

O nó `Sequence` permite que um único pulso de execução acione uma série de eventos em ordem. O nó pode ter qualquer número de saídas, todas chamadas assim que o nó Sequência receber uma entrada. Eles sempre serão chamados em ordem, mas sem qualquer demora. Para um usuário típico, as saídas provavelmente parecerão ter sido disparadas simultaneamente.

#### Sequence em Blueprint

{% include imagelocal.html
    src="unreal/estruturascontrole/blueprint_example_sequence.webp"
    alt="Figura: Blueprint Sequence."
    caption="A sequencia começa no 0 e podemos adicionar outros fluxos."
%}

#### Sequence em C++

```cpp
// Não tem similar em C++, deve ser implementado
```

### Flip Flop em Blueprint

O nó `Flip Flop` obtém uma saída de execução e alterna entre duas saídas de execução. Na primeira vez que é chamado, a saída A é executada. Na segunda vez, B. Depois A, B e assim por diante. O nó também possui uma saída booleana que permite rastrear quando a Saída A foi chamada.

{% include imagelocal.html
    src="unreal/estruturascontrole/blueprint_example_flip_flop.webp"
    alt="Figura: Blueprint Flip FLop."
    caption="Alterna entre aberto e fechado a medida que se pressiona a tecla H."
%}

### Flip Flop em C++

```cpp
// Não tem similar em C++, deve ser implementado
```

### Gate e Multi Gate em Blueprint

O nó `MultiGate` recebe um único pulso de dados e o encaminha para qualquer número de saídas potenciais. Isso pode ocorrer sequencialmente, aleatoriamente e pode ou não ser executado em loop.

{% include imagelocal.html
    src="unreal/estruturascontrole/blueprint_example_multigate.webp"
    alt="Figura: Blueprint MultiGate."
    caption="Quando é pressionada tecla H pela primeira vez é apresentado o texto "zero" na tela, na próxima vez que pressionar o texto será "Um" e assim sucessivamente. Se pressionado J a sequencia é reiniciada. Caso a opção Is Ramdon esteja assinalada a sequencia será aleatória."
%}

### Gate e Multi Gate em C++

```cpp
// Não tem similar em C++, deve ser implementado
```

## Estruturas de repetição

***

Podemos utilizar estruturas de repetição para repetir instruções ou nós, a seguir vamos entender algumas dessas estruturas.

### For Loop em Blueprint

O nó `For Loop` funciona como um loop de código padrão, disparando um pulso de execução para cada índice entre o início e o fim.

{% include imagelocal.html
    src="unreal/estruturascontrole/blueprint_example_forloop.webp"
    alt="Figura: Blueprint for loop."
    caption="Iniciando em zero e terminando em 4 será apresentado a cada passo o texto correspondente ao contador (índice)."
%}

### For Loop em C++

```cpp
for (int i = 0; i < 4; i++ ){
      cout << "Contanto: ";
      cout << i;
    }

UE_LOG(LogTemp, Warning, TEXT("Terminei de contar"));

```

### While Loop em Blueprint

Uma condição de teste e um corpo são tudo o que constitui um *loop While*. Antes de executar a (s) instrução (ões) em seu corpo, o **Blueprint** avalia a condição de teste `While Loops` para determinar se ela é verdadeira.

{% include imagelocal.html
    src="unreal/estruturascontrole/blueprint_example_whileloop.webp"
    alt="Figura: Blueprint While loop."
    caption="O loop será executado enquanto o valor for menor que 4."
%}

### While Loop em C++

```cpp
int32 valor = 0;
while ( valor <= 4) {
    i++;
    cout << i;
    }
UE_LOG(LogTemp, Warning, TEXT("Terminei de contar"));
```

### Do N em Blueprint

O nó `Do N` disparará um pulso de execução N vezes. Depois que o limite for atingido, ele interromperá todas as execuções de saída até que um pulso seja enviado para sua entrada Reset.

{% include imagelocal.html
    src="unreal/estruturascontrole/blueprint_example_do_n.webp"
    alt="Figura: Blueprint Do N."
    caption="No exemplo acima toda vez que a tecla H for pressionada um valor vai ser apresentado. Quanto o valor 10 for atingido a instrução Print String não será executada. Pressionando a tecla J a contagem será reiniciada."
%}

### Do N em C++

```cpp
// Não tem similar em C++, deve ser implementado
```

### Do once em Blueprint

O nó `Do Once` - como o nome sugere - disparará um pulso de execução apenas uma vez. Desse ponto em diante, ele interromperá toda a execução de saída até que um pulso seja enviado para sua entrada Reset. Este nó é equivalente a um nó `Do N` onde N = 1.

{% include imagelocal.html
    src="unreal/estruturascontrole/blueprint_example_do_once.webp"
    alt="Figura: Blueprint Do Once."
    caption="Se pressionada a tecla H é acionado evento Print String, caso for pressionada novamente nada acontece até que seja pressionada a tecla J para reiniciar o fluxo."
%}

### Do once em C++

```cpp
// Não tem similar em C++, deve ser implementado.
```

## O que são variáveis do tipo array?

***

É um conjunto de variáveis do mesmo tipo agrupadas dentro de uma estrutura e acessíveis por um índice. Podemos representar os *arrays* como uma tabela onde os dados são acessados por um índice que indica a posição do elemento, a seguir um exemplo.

| s          | s[0] | s[1] | s[2] | s[3]  |
| ---------- | ---- | ---- | ---- | ----- |
| **Valor**  | Ana  | José | Hugo | Hulda |
| **Índice** | 0    | 1    | 2    | 3     |

- s[0] - O valor entre colchetes indica a posição (índice) do elemento no *array*;
- O índice em C++ inicia com o valor 0.

A seguir alguns exemplos utilizando **C++**.

Exemplo de números inteiros.  

```cpp
TArray<int32> IntArray;
IntArray.Init(10, 5);
// IntArray == [10,10,10,10,10]  
```

Exemplo de números float.  

```cpp
TArray<float> floatArray[5];
floatArray.Init(10.0f, 5);
```

Exemplo com String.  

```cpp
TArray<FString> StrArr;
StrArr.Add    (TEXT("Hello"));
StrArr.Emplace(TEXT("World"));
// StrArr == ["Hello","World"]
```

## Declarando arrays e acessando os seus elementos

***

Para declarar variáveis do tipo *array* devemos primeiro escolher um tipo de variável primitivo, como por exemplo um tipo `String`, e logo em seguida determinar que será um *array*, vamos aos exemplos.

### Array em Blueprint

{% include imagebase.html
    src="unreal/array/blueprint_array_declare.webp"
    alt="Figura: Blueprint array details."
    caption="Figura: Blueprint array details."
%}

- `Nomes` - É uma variável *array*, como o ícone de mini grid informa,do tipo `String`;

- `Default Value` - Contem a lista de valores contidos inicialmente no `array`.

Em **Blueprint** a variável é representada por um ícone 3x3.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/ProgrammingAndScripting/Blueprints/UserGuide/Arrays/array_selected.webp"
    alt="Figura: Blueprint Arrays."
    caption="Figura: Blueprint Arrays."
%}

### Método Get para arrays com Blueprint

Para acessar qualquer elemento dentro *array* é necessários utilizar o índice, como no exemplo abaixo.  

{% include imagebase.html
    src="unreal/array/blueprint_array_get.webp"
    alt="Figura: Blueprint Get para Array."
    caption="Figura: Blueprint Get para Array."
%}

### Método Get para arrays com C++

```cpp
FString s = pessoa[0];
UE_LOG(LogTemp,Warning,TEXT("O nome é %s",*s));
```

### Get utilizando uma variável como índice com Blueprint

Podemos utilizar uma variável para substituir o índice e acessar elementos do *array*.

{% include imagebase.html
    src="unreal/array/blueprint_array_get_string.webp"
    alt="Figura: Blueprint Get utilizando uma variável como índice."
    caption="Figura: Blueprint Get utilizando uma variável como índice."
%}

No exemplo acima definimos o valor de Índice igual a 1 para acessar o elemento de mesma posição.

### Get utilizando uma variável como índice com C++

```cpp
int32 indice = 4;
FString s = pessoa[indice];
UE_LOG(LogTemp,Warning,TEXT("O nome é %s",*s));
```

### Último índice e a quantidade de elementos do array em Blueprint

Podemos determinar a quantidade de elementos ou valor do último índice do *array* utilizando os nós abaixo.

{% include imagebase.html
    src="unreal/array/blueprint_array_last_index.webp"
    alt="Figura: Blueprint Last Index."
    caption="Figura: Blueprint Last Index."
%}

- `Last Index` - Retorna o valor do último índice e o comando;

- `Length` - Retorna a quantidade de elementos do *array*.

**C++.**

```cpp
FString Nome  = StrArr.Last();
UE_LOG(LogTemp,Warning,TEXT("O último nome é %s",nome));

int32 Tamanho = StrArr.Num();
UE_LOG(LogTemp,Warning,TEXT("O tamanho do array é %d",Tamanho));

```

## Percorrendo arrays

***

Percorrer **array** implica em ler todos ou alguns elementos da estrutura, para tal usamos vários nós ou funções que permitem dependendo da necessidade facilitar a lógica.

### Listando todos os elementos utilizando For usando Blueprint

Na lógica abaixo percorremos todo *array* e listamos cada elemento.

{% include imagebase.html
    src="unreal/array/blueprint_array_with_forloop.webp"
    alt="Figura: Blueprint  Array com loop."
    caption="Figura: Blueprint  Array com loop."
%}

### Listando todos os elementos utilizando For usando C++

Podemos iterar utilizando a sintaxe padrão do C++.

```cpp
FString StrResultado;
for (auto& StrItem : Nomes)
{
    StrResultado += StrItem;
    StrResultado += TEXT(" ");
}
// StrResultado == "Nome1 Nome2"
```

Ou utilizar uma variável como índice.

```cpp
for (int32 Index = 0; Index != Nomes.Num(); ++Index)
{
    StrResultado += Nomes[Index];
    StrResultado += TEXT(" ");
}
```

Finalmente, array tem seu próprio tipo de elemento para iterar. Existem duas funções chamadas `CreateIterator` e `CreateConstIterator`, que podem ser usados para acesso de leitura e gravação ou somente leitura aos elementos, respectivamente:

```cpp
for (auto It = StrArr.CreateConstIterator(); It; ++It)
{
    StrResultado += *It;
    StrResultado += TEXT(" ");
}
```

- `For Each Loop` - Para cada elemento do *array* é processada uma interação.
- `For Loop` - Para cada elemento do *array*, dentro dos parâmetros `First Index` e `Last Index` é processada uma interação.

### Usando o comando Find com Blueprint

`Find` procura um elemento dentro do *array* e se encontra retorna o valor do índice do elemento, caso não encontre retorna -1.

{% include imagebase.html
    src="unreal/array/blueprint_array_search_string.webp"
    alt="Figura: Blueprint Find e Array."
    caption="Figura: Blueprint Find e Array."
%}

### Usando o comando Find com C++

```cpp
int32 Index;
if (StrArr.Find(TEXT("Hello"), Index))
{
    // Index == 3
}
```

### Contando elementos dentro de um array com Blueprint

O exemplo abaixo conta todos os elementos do *array* `Nomes` que são iguais a variável `NomeBusca`.

{% include imagebase.html
    src="unreal/array/blueprint_array_write_total_occurrence.webp"
    alt="Figura: Blueprint for para escrever o total de ocorrências."
    caption="Figura: Blueprint for para escrever o total de ocorrências."
%}

### Contando elementos dentro de um array com C++

```cpp
FString NomeBusca = TEXT("Nome 3");
int32 iTotal = 0;

for (int32 Index = 0; Index != Nomes.Num(); ++Index)
{
    StrResultado += Nomes[Index];
    if StrResultado.Equals(NomeBusca)
      iTotal++;
}
UE_LOG(LogTemp, Warning, TEXT("O Total é %d"),iTotal);
```

### Percorrendo e atualizando dados com Blueprint

O exemplo abaixo vamos percorrer o *array* utilizando uma instrução `for` e atualizar outro *array*.

{% include imagebase.html
    src="unreal/array/blueprint_array_fill_string.webp"
    alt="Figura: Blueprint preenchendo o array com strings."
    caption="Figura: Blueprint preenchendo o array com strings."
%}

### Percorrendo e atualizando dados com C++

```cpp
TArray<FString> StrArrayResultado;

FString StrResultado;


for (int32 Index = 0; Index != Nomes.Num(); ++Index)
{
    StrResultado += Nomes[Index];
    if StrResultado.Equals(TEXT("Ana"))
      StrArrayResultado.Add(StrResultado);
}
UE_LOG(LogTemp, Warning, TEXT("O Total é %d"),iTotal);

```

## Removendo elementos do array

***

É possível remover elementos de dentro de um *array*, após a remoção a quantidade e índice final da estrutura vai ser atualizada, a seguir vamos apresentar algumas funções.

### Removendo utilizando Remove com Blueprint

A função `Remove` exclui um elemento do *array*, o valor a ser removido tem que ser informado como parâmetro.

{% include imagebase.html
    src="unreal/array/blueprint_array_remove.webp"
    alt="Figura: Blueprint Remove Array."
    caption="Figura: Blueprint Remove Array."
%}

### Removendo utilizando Remove com C++

```cpp

TArray<FString> Nomes;
...
Nomes.Remove(TEXT("Ana"));
```

### Removendo passando uma variável como parâmetro com Blueprint

O comando `Remove`executa uma busca utilizando um parâmetro, **NomeBusca** no exemplo abaixo, e o remove do *array*.

{% include imagebase.html
    src="unreal/array/blueprint_array_remove_index.webp"
    alt="Figura: Blueprint Remove array com index."
    caption="Figura: Blueprint Remove array com index."
%}

### Removendo passando uma variável como parâmetro com C++

```cpp
FString StrNomeBusca = TEXT("Ana");

TArray<FString> Nomes;
...
Nomes.Remove(StrNomeBusca);
```

### Removendo utilizando nó Remove Index com Blueprint

`Remove Index` exclui um elemento do *array* utilizando o índice do *array*.

{% include imagebase.html
    src="unreal/array/blueprint_array_find.webp"
    alt="Figura: Blueprint Find e remove."
    caption="Figura: Blueprint Find e remove."
%}

### Removendo utilizando nó Remove Index com C++

```cpp
int32 Index;
if (Nomes.Find(TEXT("Hello"), Index))
{
    Nomes.RemoveAt(Index);
}

```

### Limpando o array com Clear com Blueprint

`Clear` remove todos os elementos do *array*.

{% include imagebase.html
    src="unreal/array/blueprint_array_clear.webp"
    alt="Figura: Blueprint Clear Array."
    caption="Figura: Blueprint Clear Array."
%}

### Limpando o array com Clear com C++

```cpp

Nomes.Empty();

```

## O que são Enums?

***

Uma enumeração é um tipo definido pelo usuário que consiste em um conjunto de constantes integrais nomeadas que são conhecidas como enumeradores.

Exemplo:

```cpp
enum cores = { vermelho,amarelo, azul, verde = 20, preto}
```

### Criando Enums no Unreal Engine e Blueprint

{% include imagebase.html
    src="unreal/enum/blueprint_enum_declare.webp"
    alt="Figura: Blueprint e Enum."
    caption="Figura: Blueprint e Enum."
%}

Execute o comando no menu de contexto `Blueprints` > `Enumeration` e logo depois preencha os valores conforme a tela abaixo.  

Objeto criado `EN_Estado` e `EN_Pedra`.

{% include imagebase.html
    src="unreal/enum/blueprint_enum.webp"
    alt="Figura: Blueprint Enum no Context Browser."
    caption="Figura: Blueprint Enum no Context Browser."
%}

### Criando Enums no Unreal Engine e C++

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

### Exemplos de uso - A lâmpada

Vamos verificar e alterar o estado de uma lâmpada utilizando uma variável do tipo `boolean`.  

{% include imagebase.html
    src="unreal/enum/blueprint_enum_example_lamp_state.webp"
    alt="Figura: Blueprint Verificando o estado de uma lâmpada."
    caption="Figura: Blueprint Verificando o estado de uma lâmpada."
%}

### A lâmpada em C++

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

{% include imagebase.html
    src="unreal/enum/blueprint_enum_example_lamp_offon.webp"
    alt="Figura: Blueprint Ligando e desligando o PointLight."
    caption="Figura: Blueprint Ligando e desligando o PointLight."
%}

### Arquivo Header da lâmpada em C++

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

### Verificando o estado utilizando o Enum com Blueprint

{% include imagebase.html
    src="unreal/enum/blueprint_enum_example_lamp_read_state.webp"
    alt="Figura: Blueprint Lendo Enum."
    caption="Figura: Blueprint Lendo Enum."
%}

### Verificando o estado utilizando o Enum com C++

```cpp
// Definindo um status no enum.
status = EStatusEnum::Ligada;

UE_LOG(LogTemp, Warning,TEXT("O enum é = %s"), *UEnum::GetValueAsString(status));
```

### Ligando e desligando utilizando o Enum com Blueprint

{% include imagebase.html
    src="unreal/enum/blueprint_enum_example_lamp_off.webp"
    alt="Figura: Blueprint Ligando e desligando usando Enum."
    caption="Figura: Blueprint Ligando e desligando usando Enum."
%}

### Ligando e desligando utilizando o Enum com C++

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

### Exemplos de uso - A pedra das emoções

Vamos verificar e alterar o estado de emocional de uma pedra.

1. Alterando o estado emocional da pedra.

{% include imagebase.html
    src="unreal/enum/blueprint_enum_example_rock.webp"
    alt="Figura: Blueprint alterando Enum."
    caption="Figura: Blueprint alterando Enum."
%}

1. Apresentando o estado emocional da pedra.

{% include imagebase.html
    src="unreal/enum/blueprint_enum_example_rock_state.webp"
    alt="Figura: Blueprint escrevendo o conteúdo do Enum."
    caption="Figura: Blueprint escrevendo o conteúdo do Enum."
%}
  
1. Alterando as cores da pedra conforme a emoção.  

{% include imagebase.html
    src="unreal/enum/blueprint_enum_example_rock_set_material.webp"
    alt="Figura: Blueprint alterando o material de uma malha utilizando um Enum como parâmetro."
    caption="Figura: Blueprint alterando o material de uma malha utilizando um Enum como parâmetro."
%}
