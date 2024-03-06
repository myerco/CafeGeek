---
title: Estruturas de controle
excerpt: Neste capítulo serão descritas as estruturas controle de fluxo, if, else, switch.
permalink: /pages/unreal-engine/estruturas-if-else-switch
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal_1
toc: true  
categories:
  - Unreal Engine
tags:
  - Blueprint
  - Controle de fluxo
  - if
  - else
  - switch
  - sequence
---

## 1. O que são estruturas de controle ou fluxo?

Em linguagens de programação existem métodos de tomada de decisão para tarefas corriqueiras que os programas podem executar, por exemplo a escolha de qual caminho ou instrução executar. Em **Blueprints** utilizamos nós específicos para controle de fluxo como por exemplo o `Branch`.

### 1.1. Exemplo de fluxo de execução em C++

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

### 1.2. Exemplo de fluxo condicional

|           | t1                                  | t2                                  | t3                                  | t4                                  | t5                                 | t6                                 | t7                                  | t8                                  | t9                                  |
| :-------- | :---------------------------------- | :---------------------------------- | :---------------------------------- | :---------------------------------- | :--------------------------------- | :--------------------------------- | :---------------------------------- | :---------------------------------- | :---------------------------------- |
| Principal | <span style="color:blue">--></span> | <span style="color:blue">--></span> | <span style="color:blue">--></span> | <span style="color:blue">-D-</span> |                                    |                                    | <span style="color:blue">-O-</span> | <span style="color:blue">--></span> | <span style="color:blue">--></span> |
| Desvio    |                                     |                                     |                                     | <span style="color:red">--></span>  | <span style="color:red">--></span> | <span style="color:red">--></span> | <span style="color:red">--></span>  |                                     |                                     |

### 1.3. Exemplo de fluxo de repetição

|           | t1                                  | t2                                  | t3                                  | t4                                  | t5                                 | t6                                 | t7                                  | t8                                  | t9                                  |
| :-------- | :---------------------------------- | :---------------------------------- | :---------------------------------- | :---------------------------------- | :--------------------------------- | :--------------------------------- | :---------------------------------- | :---------------------------------- | :---------------------------------- |
| Principal | <span style="color:blue">--></span> | <span style="color:blue">--></span> | <span style="color:blue">--></span> | <span style="color:blue">-D-</span> | <span style="color:red"><--</span> | <span style="color:red"><--</span> | <span style="color:blue">-O-</span> | <span style="color:blue">--></span> | <span style="color:blue">--></span> |
| Desvio    |                                     |                                     |                                     | <span style="color:blue">--></span> | <span style="color:red">--></span> | <span style="color:red">--></span> | <span style="color:red">--></span>  |                                     |                                     |

## 2. Estruturas de fluxo condicional

A seguir vamos entender como é fluxo condicional é descrito com programação visual usando **Blueprint**.

## 3. Controle de fluxo com Branch (if)

`Branch` é uma estrutura condicional que testa uma variável utilizando uma expressão lógica e redireciona o fluxo da lógica.

### 3.1. IF em Blueprint

{% include imagelocal.html
    src="unreal/estruturascontrole/unreal-engine-example-if.webp"
    alt="Figura: Blueprint e branch ou if."
    caption="O teste acima verifica se um valor é maior que o outro e redireciona o fluxo."
%}

### 3.2. IF em C++

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

## 4. Switch Nodes

O nó `Switch` lê uma entrada de dados e, com base no valor dessa entrada, envia o fluxo de execução para fora da saída de execução correspondente (ou padrão opcional). Existem vários tipos de opções disponíveis: `Int`, `String`, `Name` e `Enum`.

### 4.1. Switchs node em Blueprint

{% include imagelocal.html
    src="unreal/estruturascontrole/unreal-engine-exemple-switch.webp"
    alt="Figura: Blueprint e Switch ou Case."
    caption="Este comando verifica qual valor adente é igual ao parâmetro de entrada."
%}

### 4.2. Switchs node em C++

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

## 5. Sequenciamento de fluxo com Sequence

O nó `Sequence` permite que um único pulso de execução acione uma série de eventos em ordem. O nó pode ter qualquer número de saídas, todas chamadas assim que o nó Sequência receber uma entrada. Eles sempre serão chamados em ordem, mas sem qualquer demora. Para um usuário típico, as saídas provavelmente parecerão ter sido disparadas simultaneamente.

### 5.1. Sequence em Blueprint

{% include imagelocal.html
    src="unreal/estruturascontrole/unreal-engine-example-sequence.webp"
    alt="Figura: Blueprint Sequence."
    caption="A sequencia começa no 0 e podemos adicionar outros fluxos."
%}

### 5.2. Sequence em C++

```cpp
// Não tem similar em C++, deve ser implementado
```

### 5.3. Flip Flop em Blueprint

O nó `Flip Flop` obtém uma saída de execução e alterna entre duas saídas de execução. Na primeira vez que é chamado, a saída A é executada. Na segunda vez, B. Depois A, B e assim por diante. O nó também possui uma saída booleana que permite rastrear quando a Saída A foi chamada.

{% include imagelocal.html
    src="unreal/estruturascontrole/unreal-engine-example-flip-flop.webp"
    alt="Figura: Blueprint Flip FLop."
    caption="Alterna entre aberto e fechado a medida que se pressiona a tecla H."
%}

## 6. Flip Flop em C++

```cpp
// Não tem similar em C++, deve ser implementado
```

## 7. Gate e Multi Gate em Blueprint

O nó `MultiGate` recebe um único pulso de dados e o encaminha para qualquer número de saídas potenciais. Isso pode ocorrer sequencialmente, aleatoriamente e pode ou não ser executado em loop.

{% include imagelocal.html
    src="unreal/estruturascontrole/unreal-engine-example-multigate.webp"
    alt="Figura: Blueprint MultiGate."
    caption="Quando é pressionada tecla H pela primeira vez é apresentado o texto ZERO na tela, na próxima vez que pressionar o texto será UM e assim sucessivamente. Se pressionado J a sequencia é reiniciada. Caso a opção Is Ramdon esteja assinalada a sequencia será aleatória."
%}

## 8. Gate e Multi Gate em C++

```cpp
// Não tem similar em C++, deve ser implementado
```
