---
title: Funções e Macros
excerpt: Funções e Macros com C++
categories: 
  - "unreal-engine"
  - "capitulo-8"
date: 2024-09-01T10:48:05-04:00
order: 803
tags:
  - cpp
  - C++ 
sidebar:
  nav: unreal-engine  
---

{% include figure image_path="/assets/images/cpp/uday-awal-UjJWhMerJx0-unsplash.webp" alt="Uday Awal" caption="" %}

## 1. Funções

Funções são blocos de código que somente são executados quando são chamados. Funções podem ser reutilizadas em outros trechos de código, uma vez definidas podem ser usadas várias vezes [[C++ Functions](https://www.w3schools.com/cpp/cpp_functions.asp)].

É possível passar parâmetros para dentro da funções.

### 1.1. Exemplo da Função log

main.cpp

```cpp

#include <iostream>
void Log(const char* message)
{
  std::cout << message << std::endl;
}

int main() {
  Log("Hello World")
  std::cout << "Meu primeiro..." << std::endl;
  std::cin.get();
}
```

### 1.2. Exemplo da Função de multiplicação

main.cpp

```cpp
#include <iostream>
int Multiply(int a, int b)
{
  return a * b;
}

int main() {
  int resultado = Multiply(2,7);
  std::cout << "O resultado é : " << std::endl;
  std::cout << resultado << std::endl;
  std::cin.get();
}
```

### 1.3. Declarando funções em arquivos externos

main.cpp

```cpp
void Log(const char* message);

int main() {
  Log("Hello World")
  std::cin.get();
}
```

log.cpp

```cpp
#include <iostream>
void Log(const char* message)
{
  std::cout << message << std::endl;
}
```

## 2. Macros

Uma macro é um trecho de código em um programa que é substituído pelo valor da macro. A macro é definida pela diretiva #define . Sempre que um micronome é encontrado pelo compilador, ele substitui o nome pela definição da macro[[Macros e seus tipos em C / C++](https://acervolima.com/macros-e-seus-tipos-em-c-c/)].

Math.cpp

```cpp
#include <iostream>

#define INTEGER int

int Multuply(int i, int j)
{
  INTEGER result = i * j;
  return result;
}
```

Math.cpp

```cpp
#include <iostream>

#if 1
int Multuply(int i, int j)
{
  int result = i * j;
  return result;
}
#endif
```

### 2.1. Chamando uma função dentro de outra

Math.cpp

```cpp
#include <iostream>

const char* Log(const char* message)
{
    return message;
}

int Multuply(int i, int j)
{
  int result = i * j;
  Log("teste");
  return result;
}
```
