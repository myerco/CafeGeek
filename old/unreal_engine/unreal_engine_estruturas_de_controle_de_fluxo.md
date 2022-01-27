---
title: Estruturas de controle de fluxo
description: Neste capitulo serão apresentados as estruturas de controle de lógica de programação.
tags: [Unreal Engine,estruturas de controle de fluxo]
layout: page
---

Neste capitulo serão apresentados as estruturas de controle de lógica de programação.

## Índice
1. **[O que são estruturas de controle ou fluxo?](#1)**
1. **[Estruturas de fluxo condicional](#2)**
    1. [Controle de fluxo com Branch (if)](#2.1)
    1. [Sequenciamento de fluxo com Sequence](#2.2)
    1. [Flip Flop](#2.3)
    1. [Gate e Multi Gate](#2.4)
1. **[Estruturas de repetição](#3)**
    1. [For Loop](#3.1)
    1. [While Loop](#3.2)
    1. [Do N](#3.3)
    1. [Do once](#3.4)
1. [Atividades](#4)
    1. [Implemente um projeto que crie vários atores na cena e os posicione em áreas diferentes da cena](#4.1)

***

<a name="1"></a>
## 1. O que são estruturas de controle ou fluxo?
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

**[⬆ Volta para o início](#índice)**

<a name="2"></a>
## 2. Estruturas de fluxo condicional
A seguir vamos entender como é fluxo condicional é descrito com programação visual usando Blueprint.

<a name="2.1"></a>
### 2.1 Controle de fluxo com Branch (if)
`Branch` é uma estrutura condicional que testa uma variável utilizando uma expressão lógica e redireciona o fluxo da lógica.

**Blueprint.**

![Figura: Blueprint e branch ou if.](imagens/estruturascontrole/blueprint_example_if.jpg "Figura: Blueprint e branch ou if.")

*Figura: Blueprint e branch ou if.*

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

<a name="2.2"></a>
### 2.2 Sequenciamento de fluxo com Sequence
O nó `Sequence` permite que um único pulso de execução acione uma série de eventos em ordem. O nó pode ter qualquer número de saídas, todas chamadas assim que o nó Sequência receber uma entrada. Eles sempre serão chamados em ordem, mas sem qualquer demora. Para um usuário típico, as saídas provavelmente parecerão ter sido disparadas simultaneamente.

**Blueprint.**

![Figura: Blueptint Sequence.](imagens/estruturascontrole/blueprint_example_sequence.jpg "Figura: Blueptint Sequence.")

*Figura: Blueptint Sequence.*

**C++.**
```cpp
// Não tem similar em C++, deve ser implementado
```

<a name="2.3"></a>
### 2.3 Flip Flop
O nó `Flip Flop` obtém uma saída de execução e alterna entre duas saídas de execução. Na primeira vez que é chamado, a saída A é executada. Na segunda vez, B. Depois A, B e assim por diante. O nó também possui uma saída booleana que permite rastrear quando a Saída A foi chamada.

**Blueprint.**

![Figura: Bluprint Flip FLop.](imagens/estruturascontrole/blueprint_example_flip_flop.jpg "Figura: Bluprint Flip FLop.")

*Figura: Bluprint Flip FLop.*

**C++.**

```cpp
// Não tem similar em C++, deve ser implementado
```

<a name="2.4"></a>
### 2.4 Gate e Multi Gate
O nó `MultiGate` recebe um único pulso de dados e o encaminha para qualquer número de saídas potenciais. Isso pode ocorrer sequencialmente, aleatoriamente e pode ou não ser executado em loop.

**Blueprint.**

![Figura: Blueprint MultiGate.](imagens/estruturascontrole/blueprint_example_multigate.jpg "Figura: Blueprint MultiGate.")

*Figura: Blueprint MultiGate.*

**C++.**

```cpp
// Não tem similar em C++, deve ser implementado
```

**[⬆ Volta para o início](#índice)**

<a name="3"></a>
## 3. Estruturas de repetição
Podemos utilizar estruturas de repetição para repetir instruções ou nós, a seguir vamos entender algumas dessas estruturas.

<a name="3.1"></a>
### 3.1 For Loop
O nó `For Loop` funciona como um loop de código padrão, disparando um pulso de execução para cada índice entre o início e o fim.

**Blueprint.**

![Figura: Blueprint for loop.](imagens/estruturascontrole/blueprint_example_forloop.jpg "Figura: Blueprint for loop.")

*Figura: Blueprint for loop.*

**C++.**
```cpp
for (int i = 0; i < 4; i++ ){
      cout << "Contanto: ";
      cout << i;
    }

UE_LOG(LogTemp, Warning, TEXT("Terminei de contar"));

```

<a name="3.2"></a>
### 3.2 While Loop
Uma condição de teste e um corpo são tudo o que constitui um *loop While*. Antes de executar a (s) instrução (ões) em seu corpo, o Blueprint avalia a condição de teste `While Loops` para determinar se ela é verdadeira.

**Blueprint.**

![Figura: Bluprint While loop.](imagens/estruturascontrole/blueprint_example_whileloop.jpg "Figura: Bluprint While loop.")

*Figura: Bluprint While loop.*

**C++.**

```cpp
int32 valor = 0;
while ( valor <= 4) {
    i++;
    cout << i;
    }
UE_LOG(LogTemp, Warning, TEXT("Terminei de contar"));
```

<a name="3.3"></a>
### 3.3 Do N
O nó `Do N` disparará um pulso de execução N vezes. Depois que o limite for atingido, ele interromperá todas as execuções de saída até que um pulso seja enviado para sua entrada Reset.

**Blueprint.**

![Figura: Blueprint Do N.](imagens/estruturascontrole/blueprint_example_do_n.jpg "Figura: Blueprint Do N.")

*Figura: Blueprint Do N.*

No exemplo acima toda vez que a tecla H for pressionada um valor vai ser apresentado. Quanto o valor 10 for atingido a instrução `Print String` não será executada.

Pressionando a tecla J a contagem será reiniciada.

**C++.**
```cpp
// Não tem similar em C++, deve ser implementado
```

<a name="3.4"></a>
### 3.4 Do once
O nó `Do Once` - como o nome sugere - disparará um pulso de execução apenas uma vez. Desse ponto em diante, ele interromperá toda a execução de saída até que um pulso seja enviado para sua entrada Reset. Este nó é equivalente a um nó `Do N` onde N = 1.

**Blueprint.**

![Figura: Blueprint Do Once.](imagens/estruturascontrole/blueprint_example_do_once.jpg "Figura: Blueprint Do Once.")

*Figura: Blueprint Do Once.*

**C++.**
```cpp
// Não tem similar em C++, deve ser implementado.
```
**[⬆ Volta para o início](#índice)**

***

<a name="4"></a>
## 4. Atividades
<a name="4.1"></a>
### 4.1 - Implemente um projeto que crie vários atores na cena e os posicione em áreas diferentes da cena.

#### Regras
1. Adicione diferentes tipos de atores.

#### Desafio      
1. Adicione um *array* para controlar melhor os objetos.

**[⬆ Volta para o início](#índice)**


## Referências
- [Flow Control](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/FlowControl/index.html)
- [C++](https://docs.microsoft.com/pt-br/cpp/cpp/if-else-statement-cpp?view=msvc-160)
- [Programar em C++/Decisão e controle de fluxo](https://pt.wikibooks.org/wiki/Programar_em_C%2B%2B/Decis%C3%A3o_e_controle_de_fluxo)
