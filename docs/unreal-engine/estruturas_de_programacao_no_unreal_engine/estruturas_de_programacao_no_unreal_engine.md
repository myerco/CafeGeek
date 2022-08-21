---
title: Estruturas de programação no Unreal Engine
description: Neste capítulo serão descritas as estruturas de armazenamento, manipulação e fluxo da lógica de programação.
tags: [Unreal Engine,blueprint,programação,estruturas,variáveis,c++]
layout: page
---

![Blueprint Variables](imagens/variaveis/unreal_engine_variables.webp "Blueprint Variables")

> Figura: Blueprint Variáveis.

## O que são variáveis?

Variáveis são estruturas que são utilizadas para armazenar um valor de um determinado tipo na memória do computador.

Estrutura de memória.

|Variável       |Tipo     | Valor       |
|:-             |:-:      |:-:          |
|iSoma          |Integer  |0            |
|fValor         |Float    |6.5          |
|tName          |String   |"Gandalf"    |
|bRunnig        |Boolean  |false        |

Abaixo um exemplo em C++:

```cpp
// Variável do tipo inteiro
int iSoma = 0;

// Variável do tipo ponto flutuante
float fValor = 6.5;
```

## Variáveis no Unreal Engine

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

**Blueprint.**

- Variáveis no Editor de Blueprint.

    ![Figura: Blueprint Variables.](imagens/variaveis/unreal_engine_variable.webp "Figura: Blueprint Variables.")

    > Figura: Blueprint Variables.

- As variáveis tem tipos e propriedades que determinam o sua utilização.  

    ![Figura: Details ou properiedades das variáveis.](imagens/variaveis/unreal_engine_variable_details.webp "Figura: Details ou properiedades das variáveis.")

    > Figura: Details ou properiedades das variáveis.

    Observe que a propriedade `Category` agrupa as variáveis por uma categoria.

**C++.**

```cpp
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Parâmetros")
    int32 iLife = 10;
```

## Métodos Get e Set

Para acessar o conteúdo das variáveis utilizamos os métodos `Get` e `Set`, onde:

- `Get`: Obtém o valor de uma variável.

- `Set`: Atualiza o valor da variável.

**Blueprint.**

![Figura: Métodos Get e Set.](imagens/variaveis/unreal_engine_get_set.webp "Figura: Métodos Get e Set.")

> Figura: Métodos Get e Set.

- `BeginPlay` - Ao iniciar o jogo a lista de comandos conectados a estes nó deve ser acionado.

- `Print String` - Escreve um texto na cena do jogo.

- `Add +` - Variáveis numéricas podem ser manipuladas com operadores matemáticos.

- `Converts` - Converte tipos de variáveis, neste caso converte um valor do tipo `integer` em um do tipo `String`.

**C++.**

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

No **Unreal Engine** são definidos alguns tipos de dados para manipulação e armazenamento de caracteres alfanuméricos, entre elas estão os tipos de variáveis a seguir.

| Variável          |Tamanho    | Considerações               |
|:-:                |-          |-                            |
| `Text`            | 40 Bytes  | Podemos adicionar opções avançadas como exemplo `String Table`, ideal para textos longos que podem variar conforme a lingua definida pelo jogador.  |
| `String`          | 16 Bytes  | Armazenamento e consumo de memória mediano |
| `Name`            | 8 Bytes   |  Cadeias de caracteres  curtas que ocupam pouca memória.|

Podemos realizar as seguintes operações em `strings`:

- Atribuir o valor de uma `string` para outra;

- Acessar caracteres individualmente;

- Adicionar uma `string` no final de outra;

- Concatenar `strings`;

- Procurar uma determinada letra ou Substring dentro da `string`.

**Blueprint.**

![Figura: String functions.](imagens/variaveis/unreal_engine_string_functions.webp "Figura: String functions.")

> Figura: String functions.

**C++.**

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

### Concatenando textos usando a função Append

A função `Append` concatena duas ou mais `strings`, passamos como parâmetros os textos que gostaríamos de concatenar e tendo como resultado um novo texto contendo os dois textos.

**C++**

```cpp

FString sTexto = TEXT("Alo mundo...");
sTexto.append("Cruel");

// Resultado: Alo mundo...Cruel
```

### Procurando texto dentro de uma string

A função `Contains` procura uma sequencia de caracteres dentro de uma `string`, passamos os seguintes parâmetros para a função.

**Blueprint.**

- `Search In` - Texto passado como parâmetro.
- `Substring` - Texto que deve ser localizado.
- `Use Case` - Diferencia maiúsculas e minúsculas.
 `Search from end` - Inicia a busca pelo fim do texto.

**C++.**

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

Valores numéricos utilizam operadores matemáticos para a sua manutenção, como veremos a seguir.  

**Blueprint.**

![Figura: Utilizando Divisão.](imagens/variaveis/unreal_engine_variable_division.webp "Figura: Utilizando Divisão.")

> Figura: Utilizando Divisão.

**C++.**

```cpp
void AMyCharacterClass::BeginPlay()
{
    Super::BeginPlay();
    Float fStrength = 10;
    int32 iLife = 0;

    iLife = int(fStrength / 2);
}
```

![Figura: Multiplicação valores.](imagens/variaveis/unreal_engine_variable_multiplication.webp "Figura: Multiplicação valores.")

> Figura: Multiplicação valores.

- (+) - soma;

- (*) - Multiplicação;

- (/) - Divisão.

## Armazenando valores lógicos com Boolean

Armazena dois valores : falso `false` ou verdadeiro `true`.

![Figura: Variável Boolean.](imagens/variaveis/unreal_engine_variable_boolean.webp "Figura: Variável Boolean.")

> Figura: Variável Boolean.

No exemplo acima se o valor de `life` for maior que 50 então o valor é atualizado para `true`.

## Controle de acesso a variáveis

Como especificar quais variáveis de um objeto um usuário pode acessar e quais estão fora dos limites? - usando os especificadores de controle de acesso público e privado.

### Variáveis Privadas

Com a opção Privada marcada em uma variável, isso evita que a variável seja modificada por módulos externos.  

**Blueprint.**

![Figura: Private details.](imagens/variaveis/unreal_engine_variable_private_details.webp "Figura: Private details.")

> Figura: Private details.

**C++.**

```cpp
private:
   bool Running = false;
```

### Variáveis Públicas

Para permitir que uma variável seja modificada de fora de seu módulos, torne-a pública.  

**Blueprint.**

![Figura: Public.](imagens/variaveis/unreal_engine_variable_public.webp "Figura: Public.")

> Figura: Public.

![Figura: Public details.](imagens/variaveis/unreal_engine_variable_public_details.webp "Figura: Public details.")

> Figura: Public details.

**C++.**

```cpp
public:
  UFUNCTION(BlueprintCallable, Category="Player")
  bool IsRunning();

```

## 6.8 O que são estruturas de controle ou fluxo?

Em linguagens de programação existem métodos de tomada de decisão para tarefas corriqueiras que os programas podem executar, por exemplo a escolha de qual caminho ou instrução executar. Em **Bluprints** utilizamos nós específicos para controle de fluxo como por exemplo o `Branch`.

Exemplo de fluxo de execução, considere a sequencia de comandos abaixo:

**C++.**

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

**Exemplo de fluxo condicional.**

|           |t1 |t2 |t3 |t4 |t5 |t6 |t7 |t8 |t9 |
|:-         |:- |:- |:- |:- |:- |:- |:- |:- |:- |
|Principal  |<span style="color:blue">--></span> |<span style="color:blue">--></span> |<span style="color:blue">--></span> |<span style="color:blue">-D-</span>|   |   |<span style="color:blue">-O-</span>|<span style="color:blue">--></span> |<span style="color:blue">--></span> |
|Desvio     |   |   |   |<span style="color:red">--></span> |<span style="color:red">--></span> |<span style="color:red">--></span> |<span style="color:red">--></span> |   |   |

**Exemplo de fluxo de repetição.**

|           |t1 |t2 |t3 |t4 |t5 |t6 |t7 |t8 |t9 |
|:-         |:- |:- |:- |:- |:- |:- |:- |:- |:- |
|Principal  |<span style="color:blue">--></span> |<span style="color:blue">--></span> |<span style="color:blue">--></span> |<span style="color:blue">-D-</span>|<span style="color:red"><--</span>|<span style="color:red"><--</span> |<span style="color:blue">-O-</span>|<span style="color:blue">--></span> |<span style="color:blue">--></span> |
|Desvio     |   |   |   |<span style="color:blue">--></span> |<span style="color:red">--></span> |<span style="color:red">--></span> |<span style="color:red">--></span> |   |   |

## Estruturas de fluxo condicional

A seguir vamos entender como é fluxo condicional é descrito com programação visual usando **Blueprint**.

### Controle de fluxo com Branch (if)

`Branch` é uma estrutura condicional que testa uma variável utilizando uma expressão lógica e redireciona o fluxo da lógica.

**Blueprint.**

![Figura: Blueprint e branch ou if.](imagens/estruturascontrole/blueprint_example_if.webp "Figura: Blueprint e branch ou if.")

> Figura: Blueprint e branch ou if.

**C++.**

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

**Blueprint.**

![Figura: Blueprint e Switch ou Case.](imagens/estruturascontrole/blueprint_exemple_switch.webp "Figura: Blueprint e Switch ou Case.")

> Figura: Blueprint e Switch ou Case

**C++.**

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

**Referências:**

- Unreal Engine, 2022. Flow Control - Nodes that allow for controlling the flow of execution based on conditions.  [https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/Blueprints/UserGuide/FlowControl/](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/Blueprints/UserGuide/FlowControl/ "Unreal Engine, 2022. Flow Control - Nodes that allow for controlling the flow of execution based on conditions")
- Couch Learn. (2019,Dezenbro 27). Switch Statements in Unreal Engine 4. [https://couchlearn.com/switch-statements-in-unreal-engine-4/](https://couchlearn.com/switch-statements-in-unreal-engine-4/ "https://couchlearn.com/switch-statements-in-unreal-engine-4/")

### Sequenciamento de fluxo com Sequence

O nó `Sequence` permite que um único pulso de execução acione uma série de eventos em ordem. O nó pode ter qualquer número de saídas, todas chamadas assim que o nó Sequência receber uma entrada. Eles sempre serão chamados em ordem, mas sem qualquer demora. Para um usuário típico, as saídas provavelmente parecerão ter sido disparadas simultaneamente.

**Blueprint.**

![Figura: Blueptint Sequence.](imagens/estruturascontrole/blueprint_example_sequence.webp "Figura: Blueptint Sequence.")

> Figura: Blueptint Sequence.

**C++.**

```cpp
// Não tem similar em C++, deve ser implementado
```

### Flip Flop

O nó `Flip Flop` obtém uma saída de execução e alterna entre duas saídas de execução. Na primeira vez que é chamado, a saída A é executada. Na segunda vez, B. Depois A, B e assim por diante. O nó também possui uma saída booleana que permite rastrear quando a Saída A foi chamada.

**Blueprint.**

![Figura: Bluprint Flip FLop.](imagens/estruturascontrole/blueprint_example_flip_flop.webp "Figura: Bluprint Flip FLop.")

> Figura: Bluprint Flip FLop.

**C++.**

```cpp
// Não tem similar em C++, deve ser implementado
```

### Gate e Multi Gate

O nó `MultiGate` recebe um único pulso de dados e o encaminha para qualquer número de saídas potenciais. Isso pode ocorrer sequencialmente, aleatoriamente e pode ou não ser executado em loop.

**Blueprint.**

![Figura: Blueprint MultiGate.](imagens/estruturascontrole/blueprint_example_multigate.webp "Figura: Blueprint MultiGate.")

> Figura: Blueprint MultiGate.

**C++.**

```cpp
// Não tem similar em C++, deve ser implementado
```

## Estruturas de repetição

Podemos utilizar estruturas de repetição para repetir instruções ou nós, a seguir vamos entender algumas dessas estruturas.

### For Loop

O nó `For Loop` funciona como um loop de código padrão, disparando um pulso de execução para cada índice entre o início e o fim.

**Blueprint.**

![Figura: Blueprint for loop.](imagens/estruturascontrole/blueprint_example_forloop.webp "Figura: Blueprint for loop.")

> Figura: Blueprint for loop.

**C++.**

```cpp
for (int i = 0; i < 4; i++ ){
      cout << "Contanto: ";
      cout << i;
    }

UE_LOG(LogTemp, Warning, TEXT("Terminei de contar"));

```

### While Loop

Uma condição de teste e um corpo são tudo o que constitui um *loop While*. Antes de executar a (s) instrução (ões) em seu corpo, o **Blueprint** avalia a condição de teste `While Loops` para determinar se ela é verdadeira.

**Blueprint.**

![Figura: Bluprint While loop.](imagens/estruturascontrole/blueprint_example_whileloop.webp "Figura: Bluprint While loop.")

> Figura: Bluprint While loop.

**C++.**

```cpp
int32 valor = 0;
while ( valor <= 4) {
    i++;
    cout << i;
    }
UE_LOG(LogTemp, Warning, TEXT("Terminei de contar"));
```

### Do N

O nó `Do N` disparará um pulso de execução N vezes. Depois que o limite for atingido, ele interromperá todas as execuções de saída até que um pulso seja enviado para sua entrada Reset.

**Blueprint.**

![Figura: Blueprint Do N.](imagens/estruturascontrole/blueprint_example_do_n.webp "Figura: Blueprint Do N.")

> Figura: Blueprint Do N.

No exemplo acima toda vez que a tecla H for pressionada um valor vai ser apresentado. Quanto o valor 10 for atingido a instrução `Print String` não será executada.

Pressionando a tecla J a contagem será reiniciada.

**C++.**

```cpp
// Não tem similar em C++, deve ser implementado
```

### Do once

O nó `Do Once` - como o nome sugere - disparará um pulso de execução apenas uma vez. Desse ponto em diante, ele interromperá toda a execução de saída até que um pulso seja enviado para sua entrada Reset. Este nó é equivalente a um nó `Do N` onde N = 1.

**Blueprint.**

![Figura: Blueprint Do Once.](imagens/estruturascontrole/blueprint_example_do_once.webp "Figura: Blueprint Do Once.")

> Figura: Blueprint Do Once.

**C++.**

```cpp
// Não tem similar em C++, deve ser implementado.
```

## O que são variáveis do tipo array?

É um conjunto de variáveis do mesmo tipo agrupadas dentro de uma estrutura e acessíveis por um índice. Podemos representar os *arrays* como uma tabela onde os dados são acessados por um índice que indica a posição do elemento, a seguir um exemplo.

| s         |s[0] |s[1] |s[2] | s[3]  |
|---        |---  |---  |---  |---    |
|**Valor**  |Ana  |José |Hugo |Hulda  |
|**Índice** |  0  | 1   | 2   | 3     |

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

Para declarar variáveis do tipo *array* devemos primeiro escolher um tipo de variável primitivo, como por exemplo um tipo `String`, e logo em seguida determinar que será um *array*, vamos aos exemplos.

**Blueprint.**

![Figura: Blueprint array details.](imagens/array/blueprint_array_declare.webp "Figura: Blueprint array details.")

> Figura: Blueprint array details.

- `Nomes` - É uma variável *array*, como o ícone de mini grid informa,do tipo `String`;

- `Default Value` - Contem a lista de valores contidos inicialmente no `array`.

Em **Blueprint** a variável é representada por um ícone 3x3.

![Figura: Blueprint Arrays.](https://docs.unrealengine.com/4.27/Images/ProgrammingAndScripting/Blueprints/UserGuide/Arrays/array_selected.webp "Figura: Blueprint Arrays.")

> Figura: Blueprint Arrays.

### Método Get para arrays

Para acessar qualquer elemento dentro *array* é necessários utilizar o índice, como no exemplo abaixo.  

**Blueprint.**  

![Figura: Blueprint Get para Array.](imagens/array/blueprint_array_get.webp "Figura: Blueprint Get para Array.")

> Figura: Blueprint Get para Array.

**C++.**  

```cpp
FString s = pessoa[0];
UE_LOG(LogTemp,Warning,TEXT("O nome é %s",*s));
```

### Get utilizando uma variável como índice

Podemos utilizar uma variável para substituir o índice e acessar elementos do *array*.

**Blueprint.**

![Figura: Blueprint Get utiliando uma variável como índice.](imagens/array/blueprint_array_get_string.webp "Figura: Blueprint Get utiliando uma variável como índice.")

> Figura: Blueprint Get utilizando uma variável como índice.

No exemplo acima definimos o valor de Índice igual a 1 para acessar o elemento de mesma posição.

**C++.**  

```cpp
int32 indice = 4;
FString s = pessoa[indice];
UE_LOG(LogTemp,Warning,TEXT("O nome é %s",*s));
```

### Último índice e a quantidade de elementos do array

Podemos determinar a quantidade de elementos ou valor do último índice do *array* utilizando os nós abaixo.

**Blueprint.**

![Figura: Blueprint Last Index.](imagens/array/blueprint_array_last_index.webp "Figura: Blueprint Last Index.")

> Figura: Blueprint Last Index.

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

Percorrer **array** implica em ler todos ou alguns elementos da estrutura, para tal usamos vários nós ou funções que permitem dependendo da necessidade facilitar a lógica.

### Listando todos os elementos utilizando For

Na lógica abaixo percorremos todo *array* e listamos cada elemento.

**Bluprint.**

![Figura: Blueprint  Array com loop.](imagens/array/blueprint_array_with_forloop.webp "Figura: Blueprint  Array com loop.")

> Figura: Blueprint  Array com loop.

**C++.**

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

### Usando o comando Find

`Find` procura um elemento dentro do *array* e se encontra retorna o valor do índice do elemento, caso não encontre retorna -1.

**Blueprint.**

![Figura: Blueprint Find e Array.](imagens/array/blueprint_array_search_string.webp "Figura: Blueprint Find e Array.")

> Figura: Blueprint Find e Array.

**C++.**

```cpp
int32 Index;
if (StrArr.Find(TEXT("Hello"), Index))
{
    // Index == 3
}
```

### Contando elementos dentro de um array

O exemplo abaixo conta todos os elementos do *array* `Nomes` que são iguais a variável `NomeBusca`.

**Bluprint.**

![Figura: Blueprint for para escrever o total de ocorrências.](imagens/array/blueprint_array_write_total_occurrence.webp "Figura: Blueprint for para escrever o total de ocorrências.")

> Figura: Blueprint for para escrever o total de ocorrências.

**C++.**

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

### Percorrendo e atualizando dados

O exemplo abaixo vamos percorrer o *array* utilizando uma instrução `for` e atualizar outro *array*.

**Blueprint.**

![Figura: Blueprint preenchendo o array com strings.](imagens/array/blueprint_array_fill_string.webp "Figura: Blueprint preenchendo o array com strings")

> Figura: Blueprint preenchendo o array com strings.

**C++.**

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

É possível remover elementos de dentro de um *array*, após a remoção a quantidade e índice final da estrutura vai ser atualizada, a seguir vamos apresentar algumas funções.

### Removendo utilizando Remove

A função `Remove` exclui um elemento do *array*, o valor a ser removido tem que ser informado como parâmetro.

**Blueprint.**

![Figura: Blueprint Remove Array.](imagens/array/blueprint_array_remove.webp "Figura: Blueprint Remove Array.")

> Figura: Blueprint Remove Array.

**C++.**

```cpp

TArray<FString> Nomes;
...
Nomes.Remove(TEXT("Ana"));
```

### Removendo passando uma variável como parâmetro

O comando `Remove`executa uma busca utilizando um parâmetro, **NomeBusca** no exemplo abaixo, e o remove do *array*.

**Bluprint.**

![Figura: Blueprint Remove array com index.](imagens/array/blueprint_array_remove_index.webp "Figura: Blueprint Remove array com index.")

> Figura: Blueprint Remove array com index.

**C++.**

```cpp
FString StrNomeBusca = TEXT("Ana");

TArray<FString> Nomes;
...
Nomes.Remove(StrNomeBusca);
```

### Removendo utilizando nó Remove Index

`Remove Index` exclui um elemento do *array* utilizando o índice do *array*.

**Blueprint.**

![Figura: Blueprint Find e remove.](imagens/array/blueprint_array_find.webp "Figura: Blueprint Find e remove.")

> Figura: Blueprint Find e remove.

**C++.**

```cpp
int32 Index;
if (Nomes.Find(TEXT("Hello"), Index))
{
    Nomes.RemoveAt(Index);
}

```

### Limpando o array com Clear

`Clear` remove todos os elementos do *array*.

**Blueprint.**

![Figura: Blueprint Clear Array.](imagens/array/blueprint_array_clear.webp "Figura: Blueprint Clear Array.")

> Figura: Blueprint Clear Array.

**C++.**

```cpp

Nomes.Empty();

```

## O que são Enums?

Uma enumeração é um tipo definido pelo usuário que consiste em um conjunto de constantes integrais nomeadas que são conhecidas como enumeradores.

Exemplo:

```cpp
enum cores = { vermelho,amarelo, azul, verde = 20, preto}
```

### Criando Enums no Unreal Engine

**Blueprint.**

Execute o comando no menu de contexto `Blueprints` > `Enumeration` e logo depois preencha os valores conforme a tela abaixo.  

![Figura: Blueprint e Enum.](imagens/enum/blueprint_enum_declare.webp "[Figura: Blueprint e Enum.")

> Figura: Blueprint e Enum.

Objeto criado `EN_Estado` e `EN_Pedra`.  

![Figura: Blueprint Enum no Context Browser.](imagens/enum/blueprint_enum.webp "Figura: Blueprint Enum no Context Browser.")

> Figura: Blueprint Enum no Context Browser.

**C++.**

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

**Blueprint.**

![Figura: Blueprint Verificando o estado de uma lâmpada.](imagens/enum/blueprint_enum_example_lamp_state.webp "Figura: Blueprint Verificando o estado de uma lâmpada.")

> Figura: Blueprint Verificando o estado de uma lâmpada.

**C++.**

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

**Blueprint.**

![Figura: Blueprint Ligando e desligando o PointLight.](imagens/enum/blueprint_enum_example_lamp_offon.webp "Figura: Blueprint Ligando e desligando o PointLight.")

> Figura: Blueprint Ligando e desligando o PointLight.

**C++.**

Arquivo Header.

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

Verificando o estado utilizando o `Enum`.

**Blueprint.**

![Figura: Blueprint Lendo Enum.](imagens/enum/blueprint_enum_example_lamp_read_state.webp "Figura: Blueprint Lendo Enum.")

> Figura: Blueprint Lendo Enum.  

**C++.**

```cpp
// Definindo um status no enum.
status = EStatusEnum::Ligada;

UE_LOG(LogTemp, Warning,TEXT("O enum é = %s"), *UEnum::GetValueAsString(status));
```

Ligando e desligando utilizando o `Enum`.

**Blueprint.**

![Figura: Blueprint Ligando e desligando usando Enum.](imagens/enum/blueprint_enum_example_lamp_off.webp "Figura: Blueprint Ligando e desligando usando Enum.")

> Figura: Blueprint Ligando e desligando usando Enum.

**C++.**

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
  ![Figura: Blueprint alterando Enum.](imagens/enum/blueprint_enum_example_rock.webp "Figura: Blueprint alterando Enum.")

  > Figura: Blueprint alterando Enum.

2. Apresentando o estado emocional da pedra.
  ![Figura: Blueprint escrevendo o conteúdo do Enum.](imagens/enum/blueprint_enum_example_rock_state.webp "Figura: Blueprint escrevendo o conteúdo do Enum.")

  >Figura: Blueprint escrevendo o conteúdo do Enum.

3. Alterando as cores da pedra conforme a emoção.  
  ![Figura: Blueprint alterando o material de uma malha utilizando um Enum como parâmetro.](imagens/enum/blueprint_enum_example_rock_set_material.webp "Figura: Blueprint alterando o material de uma malha utilizando um Enum como parâmetro.")

  > Figura: Blueprint alterando o material de uma malha utilizando um Enum como parâmetro.
