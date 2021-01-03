[Home](https://myerco.github.io/unreal-engine) / [Unreal](https://myerco.github.io/unreal-engine/unreal.html)

# Manipulando Arrays
Neste capitulo serão apresentados os conceitos de estruturas de *arrays* ou vetores e suas funções para manipulação.

## Índice
> 1. [Conceito e implementação](#1)
> 1. [Declaração](#2)
> 1. [Método Get para arrays](#3)
> 1. [Get utilizando uma variável como índice](#4)
> 1. [Último índice e a quantidade de elementos do *array*](#5)
> 1. [Removendo elementos](#6)
> 1. [Listando todos os elementos utilizando **for**](#7)
> 1. [Usando o comando **find**](#8)
> 1. [Comando remove *index*](#9)
> 1. [Comando remove](#10)
> 1. [Limpando o *clear*](#11)
> 1. [Atualiza o *array* nome clássicos com dados do *array* de nome](#12)
> 1. [Contando elementos dentro de um *array*](#13)

<a name="1"></a>
## 1. Conceito e implementação
- É um conjunto de variáveis do mesmo tipo agrupadas  
Exemplo:  
Números inteiros  
a = ( 5,2,7,3,9)  
Números *float*  
a = ( 5.1,2.9,7.0,3.121,9.43)  
Números *String*  
s = ( "Ana","José","Hugo","Hulda")

- Podemos representar os arrays da seguinte forma:

| s |  s[0] |s[1]   |s[2]    | s[3]  |
|---|---|---|---|---|
|**Valor**|Ana|José|Hugo|Hulda|
|**Índice**|  0 | 1  | 2  | 3  |

<a name="2"></a>
## 2. Declaração
- Blueprints  
![Declarando array](../imagens/array/bp_array_1.png)
- Em C++  
```cpp
FString  pessoas[4] = { "Ana","José","Hugo","Hulda"};
int  pessoas[3] = { 4,3,7};
```

<a name="3"></a>
## 3. Método *Get* para *arrays*
Para acessar qualquer elemento dentro *array* é necessários utilizar o índice.  

- Blueprints  
![Declarando array](../imagens/array/bp_array_2.png)
- Em C++  
```
FString s = pessoa[0];
UE_LOG(LogTemp, Warning, TEXT("O nome é %s",*s);
```  

<a name="4"></a>
## 4. Get utilizando uma variável como índice
![Declarando array](../imagens/array/bp_array_3.png)

<a name="5"></a>
## 5. Último índice e a quantidade de elementos do *array*
![Declarando array](../imagens/array/bp_array_4.png)


<a name="6"></a>
## 6. Removendo elementos
![Declarando array](../imagens/array/bp_array_5.png)

<a name="7"></a>
## 7. Listando todos os elementos utilizando *for*
![Declarando array](../imagens/array/bp_array_6.png)


<a name="8"></a>
## 8. Usando o comando *find*
- Blueprint  
![Declarando array](../imagens/array/bp_array_7.png)
- c++
```
int32 Index;
if (StrArr.Find(TEXT("Hello"), Index))
{
    // Index == 3
}
```

<a name="9"></a>
## 9. Comando *remove index*
![Declarando array](../imagens/array/bp_array_8.png)

<a name="10"></a>
## 10. Comando *remove*
![Declarando array](../imagens/array/bp_array_9.png)

<a name="11"></a>
## 11. Limpando o *clear*
![Declarando array](../imagens/array/bp_array_10.png)

<a name="12"></a>
## 12. Atualiza o *array* **nome clássicos** com dados do *array* de **nome**

![Declarando array](../imagens/array/bp_array_11.png)

<a name="13"></a>
## 13. Contando elementos dentro de um *array*
![Declarando array](../imagens/array/bp_array_12.png)

***

### Referências
- [Unreal Engine Blueprints Array](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Arrays/index.html)   
- [Unreal Engine Array Nodes](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Arrays/ArrayNodes/index.html)    
- [C++](https://www.codegrepper.com/code-examples/cpp/ue4+c%2B%2B+array)
