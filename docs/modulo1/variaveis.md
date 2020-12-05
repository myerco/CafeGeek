[Home](https://myerco.github.io/unreal-engine) / [Unreal](https://myerco.github.io/unreal-engine/unreal.html)

# Variáveis

> 1. [Variáveis básicas](#1)  
> 1. [Métodos GET e SET](#2)  
> 1. [String e Text](#3)  
> 1. [Integer e Float](#4)  
> 1. [Boolean](#5)  
> 1. [Variável Pública e Privada](#6)  
> 1. [Operadores (Subtração, soma e divisão)](#7)
> 1. [Manipulação de String](#8)
> 1. [Organização e convenção](#9)

<a name="1"></a>
## 1. Variáveis básicas
Variáveis são propriedades que contêm um valor ou fazem referência a um objeto ou ator no mundo. Essas propriedades podem ser acessíveis internamente ao Blueprint que as contém, ou podem ser tornadas acessíveis externamente para que seus valores possam ser modificados por designers que trabalham com instâncias do Blueprint colocadas em um nível.

- Declaração   
![](../imagens/variaveis/variaveis1.png)
- Propriedades   
![](../imagens/variaveis/variaveis2.png)
> Observe que a propriedade **Category** agrupa as variáveis por uma categoria.

<a name="2"></a>
## 2. Métodos GET e SET
- **Get**: Obtém o valor de uma variável.
- **Set**: Atualiza o valor da variável.

![](../imagens/variaveis/variaveis3.png)


<a name="2"></a>
## 3. String, Name e Text

| Variável |Tamanho  |  |
|:-:|-|-|
| **Text** | 40 Bytes | Podemos adicionar opções avançadas como exemplo: **String Table**  |
| **String** | 16 Bytes |  |
|  **Name**| 8 Bytes |  |

- Tramento  
![](../imagens/variaveis/variaveis4.png)

<a name="2"></a>
## 4. Integer e Float

- Integer : Armazena números inteiros.
- Floar : Armazena números com ponto flutuante (reais) com precição simples.

- Tratamento
![](../imagens/variaveis/variaveis5.png)

<a name="2"></a>
## 5. Boolean
Armazena dois valores : falso (*false*) ou verdadeiro (*true*).
- Tratamento  
![](../imagens/variaveis/variaveis6.png)

<a name="2"></a>
## 6. Variável Pública e Privada

<a name="2"></a>
## 7. Operadores (Subtração, soma e divisão)

<a name="2"></a>
## 8. Manipulação de String

***

## Referências
- [Blueprint Variables](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Variables/index.html)
- [Coding Standard](https://docs.unrealengine.com/en-US/Programming/Development/CodingStandard/index.html)
- [Properties](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Reference/Properties/index.html)
- [String](https://docs.unrealengine.com/en-US/BlueprintAPI/Utilities/String/index.html)
- [Srting Tables](https://docs.unrealengine.com/en-US/Gameplay/Localization/StringTables/index.html)
- [Integer](https://docs.unrealengine.com/en-US/BlueprintAPI/Math/Integer/index.html)
- [Float](https://docs.unrealengine.com/en-US/BlueprintAPI/Math/Float/index.html)
