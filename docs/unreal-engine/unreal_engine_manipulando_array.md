---
title: Manipulando Arrays
description: Neste capitulo serão apresentados os conceitos de estruturas de *arrays* ou vetores e suas funções para manipulação.
tags: [Unreal Engine,blueprint,array,get,set]
layout: page
---

Neste capitulo serão apresentados os conceitos de estruturas de *arrays* ou vetores e suas funções para manipulação.

## Índice
1. **[O que são variáveis do tipo array?](#1)**
     1. [Exemplo de números inteiros](#1.1)
     1. [Exemplo de números Números float](#1.2)
     1. [Exemplo com String](#1.3)
     1. [Representação](#1.4)
1. **[Declarando arrays e acessando os seus elementos](#2)**
     1. [Método Get para arrays](#2.1)
     1. [Get utilizando uma variável como índice](#2.2)
     1. [Último índice e a quantidade de elementos do array](#2.3)
1. **[Percorrendo arrays](#3)**
    1. [Listando todos os elementos utilizando For](#3.1)
    1. [Usando o comando Find](#3.2)
    1. [Contando elementos dentro de um array](#3.3)
    1. [Percorrendo e atualizando dados](#3.4)
1. **[Removendo elementos do array](#4)**    
    1. [Removendo elementos utilizando Remove](#4.1)
    1. [Removendo passando uma variável como parâmetro](#4.1)
    1. [Removendo utilizando nó Remove Index](#4.2)
    1. [Limpando o array com Clear](#4.3)


***

<a name="1"></a>
## 1. O que são variáveis do tipo *array*?
É um conjunto de variáveis do mesmo tipo agrupadas dentro de uma estrutura e acessíveis por um índice.  

Vamos aos exemplos.

<a name="1.1"></a>
### 1.1 Exemplo de números inteiros  

```cpp
a = ( 5,2,7,3,9)  
```

<a name="1.2"></a>
### 1.2 Exemplo de números float  

```cpp
a = ( 5.1,2.9,7.0,3.121,9.43)  
```

<a name="1.3"></a>
### 1.3 Exemplo com String  

```cpp
s = ( "Ana","José","Hugo","Hulda")
```

<a name="1.4"></a>
### 1.4 Representação
Podemos representar os *arrays* da seguinte forma:

| s         |s[0] |s[1] |s[2] | s[3]  |
|---        |---  |---  |---  |---    |
|**Valor**  |Ana  |José |Hugo |Hulda  |
|**Índice** |  0  | 1   | 2   | 3     |

- s[0] - O valor entre colchetes indica a posição (índice) do elemento no *array*;
- O índice em C++ inicia com o valor 0.

**[⬆ Volta para o início](#índice)**

<a name="2"></a>
## 2. Declarando arrays e acessando os seus elementos
Para declarar variáveis do tipo *array* devemos primeiro escolher um tipo de variável primitivo, como por exemplo um tipo `String`, e logo em seguida determinar que será um *array*, vamos aos exemplos.

**Blueprint.**    

![Figura: Blueprint array details.](imagens/array/blueprint_array_declare.jpg "Figura: Blueprint array details.")

*Figura: Blueprint array details.*

- `Nomes` - É uma variável array, como o ícone de mini grid informa,do tipo `String`.
- `Default Value` - Contem a lista de valores contidos inicialmente no `array`.

**C++.**  

```cpp
FString  pessoas[4] = { "Ana","José","Hugo","Hulda"};
int  pessoas[3] = { 4,3,7};
```

<a name="2.1"></a>
### 2.1 Método Get para arrays
Para acessar qualquer elemento dentro *array* é necessários utilizar o índice.  

**Blueprint.**  

![Figura: Blueprint Get para Array.](imagens/array/blueprint_array_get.jpg "Figura: Blueprint Get para Array.")

*Figura: Blueprint Get para Array.*

**C++.**  

```cpp
FString s = pessoa[0];
UE_LOG(LogTemp,Warning,TEXT("O nome é %s",*s));
```

<a name="2.2"></a>
### 2.2 Get utilizando uma variável como índice
Podemos utilizar uma variável para acessar elementos do *array*.

**Blueprint.**

![Figura: Blueprint Get utiliando uma variável como índice.](imagens/array/blueprint_array_get_string.jpg "Figura: Blueprint Get utiliando uma variável como índice.")

*Figura: Blueprint Get utilizando uma variável como índice.*

- **Indice** - Definimos o valor 1 para acessar o elemento da referida posição.

<a name="2.3"></a>
### 2.3 Último índice e a quantidade de elementos do array
Podemos determinar a quantidade de elementos ou valor do último índice do *array* utilizando as propriedades abaixo.    

![Figura: Blueprint Last Index.](imagens/array/blueprint_array_last_index.jpg "Figura: Blueprint Last Index.")

*Figura: Blueprint Last Index.*

- `Last Index` - Retorna o valor do último índice e o comando.
- `Length` - Retorna a quantidade de elementos do *array*.

**[⬆ Volta para o início](#índice)**

<a name="3"></a>
## 3. Percorrendo arrays

<a name="3.1"></a>
### 3.1 Listando todos os elementos utilizando For
Na lógica abaixo percorremos todo *array* e listamos cada elemento.   

![Figura: Blueprint  Array com loop.](imagens/array/blueprint_array_with_forloop.jpg "Figura: Blueprint  Array com loop.")

*Figura: Blueprint  Array com loop.*

- `For Each Loop` - Para cada elemento do *array* é processada uma interação.
- `For Loop` - Para cada elemento do *array*, dentro dos parâmetros `First Index` e `Last Index` é processada uma interação.

<a name="3.2"></a>
### 3.2 Usando o comando Find
`Find` procura um elemento dentro do *array* e se encontra retorna o valor do índice do elemento, caso não encontre retorna -1.   

**Blueprint.**      

![Figura: Blueprint Find e Array.](imagens/array/blueprint_array_search_string.jpg "Figura: Blueprint Find e Array.")

*Figura: Blueprint Find e Array.*    

**C++.**

```cpp
int32 Index;
if (StrArr.Find(TEXT("Hello"), Index))
{
    // Index == 3
}
```

<a name="3.3"></a>
### 3.3 Contando elementos dentro de um array

![Figura: Blueprint for para escrever o total de ocorrências.](imagens/array/blueprint_array_write_total_occurrence.jpg "Figura: Blueprint for para escrever o total de ocorrências.")

*Figura: Blueprint for para escrever o total de ocorrências.*

<a name="3.4"></a>
### 3.4 Percorrendo e atualizando dados

![Figura: Blueprint preenchendo o array com strings.](imagens/array/blueprint_array_fill_string.jpg)

*Figura: Blueprint preenchendo o array com strings.*

**[⬆ Volta para o início](#índice)**

<a name="4"></a>
## 4. Removendo elementos do array
É possível remover elementos de dentro de um *array*, a seguir vamos apresentar algumas funções.    

<a name="4.1"></a>
### 4.1 Removendo utilizando Remove
A função `Remove` exclui um elemento do *array*, o valor a ser removido tem que ser informado como parâmetro.    

![Figura: Blueprint Remove Array.](imagens/array/blueprint_array_remove.jpg "Figura: Blueprint Remove Array.")

*Figura: Blueprint Remove Array.*

<a name="4.2"></a>
### 4.2 Removendo passando uma variável como parâmetro
O comando `Remove`executa uma busca utilizando um parâmetro, **NomeBusca** no exemplo abaixo, e o remove do *array*.    

![Figura: Blueprint Remove array com index.](imagens/array/blueprint_array_remove_index.jpg "Figura: Blueprint Remove array com index.")

*Figura: Blueprint Remove array com index.*


<a name="4.3"></a>
### 4.2 Removendo utilizando nó Remove Index
`Remove Index` exclui um elemento do *array* utilizando o índice do *array*.      

![Figura: Blueprint Find e remove.](imagens/array/blueprint_array_find.jpg "Figura: Blueprint Find e remove.")

*Figura: Blueprint Find e remove.*


<a name="4.4"></a>
### 4.4 Limpando o array com Clear
`Clear` remove todos os elementos do *array*.

![Figura: Blueprint Clear Array.](imagens/array/blueprint_array_clear.jpg "Figura: Blueprint Clear Array.")

*Figura: Blueprint Clear Array.*

**[⬆ Volta para o início](#índice)**


***
### Referências
- [Unreal Engine Blueprints Array](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Arrays/index.html)   
- [Unreal Engine Array Nodes](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Arrays/ArrayNodes/index.html)    
- [C++](https://www.codegrepper.com/code-examples/cpp/ue4+c%2B%2B+array)

***
