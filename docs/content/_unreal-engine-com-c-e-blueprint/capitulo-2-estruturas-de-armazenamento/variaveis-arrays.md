---
title: Variáveis Arrays
excerpt: Neste capítulo serão descritas as variáveis do tipo Array.
categories: 
  - "unreal-engine-com-c-e-blueprint"
  - "capitulo-2-estruturas-de-armazenamento"
permalink: /:categories/:title
sidebar:
  nav: dev_unreal_1
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 201
tags:
  - Blueprint
---

## 1. O que são variáveis do tipo array?

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
## 2. Declarando arrays e acessando os seus elementos

Para declarar variáveis do tipo *array* devemos primeiro escolher um tipo de variável primitivo, como por exemplo um tipo `String`, e logo em seguida determinar que será um *array*, vamos aos exemplos.

### 2.1. Array em Blueprint

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-declare.webp"
    alt="Figura: Blueprint array details."
    caption="Figura: Considere a variável Nomes que deve armazenar uma lista de nomes."
%}

- `Nomes` - É uma variável *array*, como o ícone de mini grid informa,do tipo `String`;

- `Default Value` - Contem a lista de valores contidos inicialmente no `array`.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/ProgrammingAndScripting/Blueprints/UserGuide/Arrays/array_selected.webp"
    alt="Figura: Blueprint Arrays."
    caption="Figura: Em Blueprint a variável é representada por um ícone 3x3."
%}

### 2.2. Método Get para arrays com Blueprint

Para acessar qualquer elemento dentro *array* é necessários utilizar o índice, como no exemplo abaixo.  

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-get.webp"
    alt="Figura: Blueprint Get para Array."
    caption="Figura: O método Get acessa a informação recebendo como parâmetro um valor de índice."
%}

### 2.3. Método Get para arrays com C++

```cpp
FString s = pessoa[0];
UE_LOG(LogTemp,Warning,TEXT("O nome é %s",*s));
```

### 2.4. Get utilizando uma variável como índice com Blueprint

Podemos utilizar uma variável para substituir o índice e acessar elementos do *array*.

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-get-string.webp"
    alt="Figura: Blueprint Get utilizando uma variável como índice."
    caption="Figura: No exemplo acima definimos o valor de Índice igual a 1 para acessar o elemento de mesma posição."
%}

### 2.5. Get utilizando uma variável como índice com C++

```cpp
int32 indice = 4;
FString s = pessoa[indice];
UE_LOG(LogTemp,Warning,TEXT("O nome é %s",*s));
```

### 2.6. Último índice e a quantidade de elementos do array em Blueprint

Podemos determinar a quantidade de elementos ou valor do último índice do *array* utilizando os nós abaixo.

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-last-index.webp"
    alt="Figura: Blueprint Last Index e Length."
    caption="Figura: Usando os nós predefinidos objetos o valor do índice."
%}

- `Last Index` - Retorna o valor do último índice e o comando;

- `Length` - Retorna a quantidade de elementos do *array*.

### 2.7. Último índice e a quantidade de elementos do array em C++

```cpp
FString Nome  = StrArr.Last();
UE_LOG(LogTemp,Warning,TEXT("O último nome é %s",nome));

int32 Tamanho = StrArr.Num();
UE_LOG(LogTemp,Warning,TEXT("O tamanho do array é %d",Tamanho));

```

## 3. Percorrendo arrays

Percorrer **array** implica em ler todos ou alguns elementos da estrutura, para tal usamos vários nós ou funções que permitem dependendo da necessidade facilitar a lógica.

### 3.1. Listando todos os elementos utilizando For usando Blueprint

Na lógica abaixo percorremos todo *array* e listamos cada elemento.

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-with-forloop.webp"
    alt="Figura: Blueprint  Array com loop."
    caption="Figura: Utilizando For Each Loop podemos percorrer todo array."
%}

### 3.2. Listando todos os elementos utilizando For usando C++

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

### 3.3. Usando o comando Find com Blueprint

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-search-string.webp"
    alt="Figura: Blueprint Find e Array."
    caption="Figura: Find procura um elemento dentro do *array* e se encontra retorna o valor do índice do elemento, caso não encontre retorna -1."
%}

### 3.4. Usando o comando Find com C++

```cpp
int32 Index;
if (StrArr.Find(TEXT("Hello"), Index))
{
    // Index == 3
}
```

### 3.5. Contando elementos dentro de um array com Blueprint

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-write-total-occurrence.webp"
    alt="Figura: Blueprint for para escrever o total de ocorrências."
    caption="Figura: O exemplo acima conta todos os elementos do array Nomes que são iguais a variável NomeBusca."
%}

### 3.6. Contando elementos dentro de um array com C++

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

### 3.7. Percorrendo e atualizando dados com Blueprint

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-fill-string.webp"
    alt="Figura: Blueprint preenchendo o array com strings."
    caption="Figura: O exemplo acima vamos percorrer o array utilizando uma instrução for e atualizar outro array."
%}

### 3.8. Percorrendo e atualizando dados com C++

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

## 4. Removendo elementos do array

É possível remover elementos de dentro de um *array*, após a remoção a quantidade e índice final da estrutura vai ser atualizada, a seguir vamos apresentar algumas funções.

### 4.1. Removendo utilizando Remove com Blueprint

A função `Remove` exclui um elemento do *array*, o valor a ser removido tem que ser informado como parâmetro.

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-remove.webp"
    alt="Figura: Blueprint Remove Array."
    caption="Figura: Exemplo do comando Remove."
%}

### 4.2. Removendo utilizando Remove com C++

```cpp

TArray<FString> Nomes;
...
Nomes.Remove(TEXT("Ana"));
```

### 4.3. Removendo passando uma variável como parâmetro com Blueprint

O comando `Remove`executa uma busca utilizando um parâmetro, **NomeBusca** no exemplo abaixo, e o remove do *array*.

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-remove-index.webp"
    alt="Figura: Blueprint Remove array com index."
    caption="Figura: Exemplo de Remove com um parâmetro."
%}

### 4.4. Removendo passando uma variável como parâmetro com C++

```cpp
FString StrNomeBusca = TEXT("Ana");

TArray<FString> Nomes;
...
Nomes.Remove(StrNomeBusca);
```

### 4.5. Removendo utilizando nó Remove Index com Blueprint

`Remove Index` exclui um elemento do *array* utilizando o índice do *array*.

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-find.webp"
    alt="Figura: Blueprint Find e remove."
    caption="Figura: Usando Find para obter o índice e passando o seu valor para Remove Index."
%}

### 4.6. Removendo utilizando nó Remove Index com C++

```cpp
int32 Index;
if (Nomes.Find(TEXT("Hello"), Index))
{
    Nomes.RemoveAt(Index);
}

```

### 4.7. Limpando o array com Clear com Blueprint

`Clear` remove todos os elementos do *array*.

{% include imagelocal.html
    src="unreal/array/unreal-engine-array-clear.webp"
    alt="Figura: Blueprint Clear Array."
    caption="Figura: Podemos otimizar o limpeza do array com Clear."
%}

### 4.8. Limpando o array com Clear com C++

```cpp

Nomes.Empty();

```
