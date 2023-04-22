---
title: Estruturas de Repetição
excerpt: Neste capítulo serão descritas as estruturas de repetição.
permalink: /pages/unreal-engine/estruturas-loops
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true  
categories:
  - Unreal Engine
tags:
  - Blueprint
  - Repetição
  - Loop
---

## 1. Estruturas de repetição

Podemos utilizar estruturas de repetição para repetir instruções ou nós, a seguir vamos entender algumas dessas estruturas.

### 1.1. For Loop em Blueprint

O nó `For Loop` funciona como um loop de código padrão, disparando um pulso de execução para cada índice entre o início e o fim.

{% include imagelocal.html
    src="unreal/estruturascontrole/unreal-engine-example-forloop.webp"
    alt="Figura: Blueprint for loop."
    caption="Iniciando em zero e terminando em 4 será apresentado a cada passo o texto correspondente ao contador (índice)."
%}

### 1.2. For Loop em C++

```cpp
for (int i = 0; i < 4; i++ ){
      cout << "Contanto: ";
      cout << i;
    }

UE_LOG(LogTemp, Warning, TEXT("Terminei de contar"));

```

### 1.3. While Loop em Blueprint

Uma condição de teste e um corpo são tudo o que constitui um *loop While*. Antes de executar a (s) instrução (ões) em seu corpo, o **Blueprint** avalia a condição de teste `While Loops` para determinar se ela é verdadeira.

{% include imagelocal.html
    src="unreal/estruturascontrole/unreal-engine-example-whileloop.webp"
    alt="Figura: Blueprint While loop."
    caption="O loop será executado enquanto o valor for menor que 4."
%}

### 1.4. While Loop em C++

```cpp
int32 valor = 0;
while ( valor <= 4) {
    i++;
    cout << i;
    }
UE_LOG(LogTemp, Warning, TEXT("Terminei de contar"));
```

### 1.5. Do N em Blueprint

O nó `Do N` disparará um pulso de execução N vezes. Depois que o limite for atingido, ele interromperá todas as execuções de saída até que um pulso seja enviado para sua entrada Reset.

{% include imagelocal.html
    src="unreal/estruturascontrole/unreal-engine-example-do-n.webp"
    alt="Figura: Blueprint Do N."
    caption="No exemplo acima toda vez que a tecla H for pressionada um valor vai ser apresentado. Quanto o valor 10 for atingido a instrução Print String não será executada. Pressionando a tecla J a contagem será reiniciada."
%}

### 1.6. Do N em C++

```cpp
// Não tem similar em C++, deve ser implementado
```

### 1.7. Do once em Blueprint

O nó `Do Once` - como o nome sugere - disparará um pulso de execução apenas uma vez. Desse ponto em diante, ele interromperá toda a execução de saída até que um pulso seja enviado para sua entrada Reset. Este nó é equivalente a um nó `Do N` onde N = 1.

{% include imagelocal.html
    src="unreal/estruturascontrole/unreal-engine-example-do-once.webp"
    alt="Figura: Blueprint Do Once."
    caption="Se pressionada a tecla H é acionado evento Print String, caso for pressionada novamente nada acontece até que seja pressionada a tecla J para reiniciar o fluxo."
%}

### 1.8. Do once em C++

```cpp
// Não tem similar em C++, deve ser implementado.
```
