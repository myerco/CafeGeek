---
title: Trabalhando com variáveis
description: Trabalhando com variáveis e seus métodos com Blueprint
tags: [Unreal Engine,Blueprint,variáveis, variable]
layout: page
---

Neste capítulo serão descritas as estruturas de armazenamento em memória e a sua manipulação.

## Índice
1. [O que são variáveis?](#1)  
1. [Tipos de variáveis](#2)  
1. [Declarando variáveis](#3)  
1. [Métodos Get e Set](#4)  
1. [String, Name e Text](#5)  
     1. [Tratamento de strings](#5.1)  
1. [Integer e Float](#6)  
1. [Boolean](#7)
1. [Variável Pública e Privada](#8)

***

<a name="1"></a>
## 1. O que são variáveis?
Variáveis são propriedades que contêm um valor ou fazem referência a um objeto ou ator no mundo. Essas propriedades podem ser acessíveis internamente ao **Blueprint** que as contém, ou podem ser tornadas acessíveis externamente para que seus valores possam ser modificados por designers que trabalham com instâncias do **Blueprint** colocadas em um nível.

<a name="2"></a>
## 2. Tipos de Variáveis
Para armazenar qualquer informação na memória devemos definir um tipo de dados primitivo ou mesmo uma estrutura de dados, a seguir alguns tipos de dados:

1.  `Boolean` - Armazena valores falso ou verdadeiro (true e false).

    ```cpp
  bool VariavelBoolean;
  VariavelBoolean = true;
  ```

1. `Integer` - Valores inteiros entre −2.147.483.648 e 2.147.483.647

    ```cpp
  int VariavelInt;
  VariavelInt = 1;
  ```
1. `Float` - Valores com casas decimais tal como 0,0553, 101,2887 e -78,322 .

    ```cpp
    float VariavelFloat;
    VariavelFloat = 2.4;
    ```

1. `String`- Grupo de caracteres alfanuméricos.

    ```cpp
  FString VariavelString ;
  VariavelString = "Alo mundo!!";
    ```

<a name="3"></a>
## 3. Declarando variáveis   
Declarando variáveis informamos ao computador que estamos reservando um espaço de memória temporário.  

1. Variáveis no Editor de Blueprint.

  ![Blueprint Variables](imagens/variaveis/unreal_engine_variable_details.jpg)

    *Figura: Blueprint Variables*

1. As variáveis tem tipos e propriedades que determinam o sua utilização.  

  ![Details ou properiedades das variáveis](imagens/variaveis/unreal_engine_variable_details.jpg)

    *Figura: Details ou properiedades das variáveis*

> Observe que a propriedade `Category` agrupa as variáveis por uma categoria.

<a name="4"></a>
## 4. Métodos Get e Set
Para acessar as variáveis utilizamos os métodos `Get` e `Set`.
- `Get`: Obtém o valor de uma variável.
- `Set`: Atualiza o valor da variável.

![unreal_engine_get_set](imagens/variaveis/unreal_engine_get_set.jpg)

*Figura: Métodos Get e Set*

- `BeginPlay` - Ao iniciar o jogo a lista de comandos deve ser acionado.
- `Print String` - Escreve um texto na cena do jogo.
- `Add +` - Variáveis numéricas podem ser manipuladas com operadores matemáticos.
- `Converts` - Converte tipos de variáveis, neste caso converte um valor do tipo `integer` em um do tipo `String`.

<a name="5"></a>
## 5. String, Name e Text
O armazenamento de caracteres alfanuméricos, `string`, apresetam diversas estruturas para melhor utilização e armazenamento.

| Variável          |Tamanho    | Considerações               |
|:-:                |-          |-                            |
| `Text`            | 40 Bytes  | Podemos adicionar opções avançadas como exemplo `String Table`, ideal para textos longos que podem variar conforme a lingua definida pelo jogador.  |
| `String`          | 16 Bytes  | Armazenamento e consumo de memória mediano |
| `Name`            | 8 Bytes   |  Cadeias de caracteres  curtas que ocupam pouca memória.|

<a name="5.1"></a>
### 5.1 Tratamento de strings

![unreal_engine_string_functions](imagens/variaveis/unreal_engine_string_functions.jpg)

*Figura: String functions*

- `Append` - Concatena duas ou mais strings.
- `Contains` - Procura uma sequencia de caracteres dentro de uma `string`.
  - `Search In` - Texto passado como parâmetro.
  - `Substring` - Texto que deve ser localizado.
  - `Use Case` - Diferencia maiúsculas e minúsculas.
  - `Search from end` - Inicia a busca pelo fim do texto.

<a name="6"></a>
## 6. Integer e Float
Valores numéricos utilizam operadores matemáticos para a sua manutenção.  

![unreal_engine_variable_division](imagens/variaveis/unreal_engine_variable_division.jpg)

*Figura: Divisão*

![unreal_engine_variable_multiplication](imagens/variaveis/unreal_engine_variable_multiplication.jpg)

*Figura: Multiplicação*

- (+) - soma.
- (*) - Multiplicação.
- (/) - Divisão.

<a name="7"></a>
## 7. Boolean
Armazena dois valores : falso `false` ou verdadeiro `true`.

![unreal_engine_variable_boolean](imagens/variaveis/unreal_engine_variable_boolean.jpg)

*Figura: Variável Boolean*

No exemplo acima se o valor de `life` for maior que 50 então o valor é atualizado para `true`.


<a name="8"></a>
## 8. Variável Pública e Privada
Como especificar quais variáveis de um objeto um usuário pode acessar e quais estão fora dos limites? - usando os especificadores de controle de acesso público e privado.

`Privada` - Com a opção Privada marcada em uma variável, isso evita que a variável seja modificada de **Blueprints** externos.  

![unreal_engine_variable_private_details](imagens/variaveis/unreal_engine_variable_private_details.jpg)

*Figura: Private details*

`Pública` - Para permitir que uma variável seja modificada de fora de seu  **Blueprint**, torne-a pública.  

![unreal_engine_variable_public](imagens/variaveis/unreal_engine_variable_public.jpg)

*Figura: Public*

![unreal_engine_variable_public_details](imagens/variaveis/unreal_engine_variable_public_details.jpg)

*Figura: Public details*


***

## Referências
- [Blueprint Variables](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Variables/index.html)
- [Coding Standard](https://docs.unrealengine.com/en-US/Programming/Development/CodingStandard/index.html)
- [Properties](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Reference/Properties/index.html)
- [String](https://docs.unrealengine.com/en-US/BlueprintAPI/Utilities/String/index.html)
- [Srting Tables](https://docs.unrealengine.com/en-US/Gameplay/Localization/StringTables/index.html)
- [Integer](https://docs.unrealengine.com/en-US/BlueprintAPI/Math/Integer/index.html)
- [Float](https://docs.unrealengine.com/en-US/BlueprintAPI/Math/Float/index.html)
