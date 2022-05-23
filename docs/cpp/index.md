---
title: Programação em linguagem C++
description: Programação em linguagem C++
tags: [programação, cpp, c++, lógica]
layout: page
---

Aprenda a programar em linguagem C++.  

## Habilidades que serão aprendidas  
- Estrutura de arquivos;     
- Variáveis e ponteiros;
- Estruturas de controle de fluxo;
- Manipulando Arrays;

---

##  Índice


## Como o compilador C++ funciona?
Os arquivos C++ são divididos em dois tipos, um arquivo de código (.cpp) e um de cabeçalho (.h).

Os arquivos de código contem a lógica principal, estes arquivos podem incluir outros arquivos, utilizando a diretiva `#include`, são os arquivos de cabeçalho. A extensão não importa para o pré-processador C++ que substituirá literalmente a linha que contém a diretiva `#include`.

Cada arquivo de código deve se compilado dentro de um arquivo objeto (.obj), os arquivos objeto são juntados (linked) dentro de um executável (.exe)

```
Arquivo.cpp ->
Arquivo.obj + Arquivo2.obj ->
Arquivo.exe
```

A primeira etapa que o compilador fará em um arquivo de código é executar o pré-processador nele. Apenas os arquivos de código são passados ​​para o compilador (para pré-processar e compilar). Os arquivos de cabeçalho não são passados ​​para o compilador. Em vez disso, eles são incluídos nos arquivos de origem.

### Exemplo de arquivo sendo incluído em outro
**multiply.cpp**
```cpp
int multiply(int a, int b)
{
  return a * b;
#include "parte.h"
}
```

**parte.h**
```cpp
}
```

Cada arquivo de cabeçalho pode ser aberto várias vezes durante a fase de pré-processamento de todos os arquivos de lógica, dependendo de quantos arquivos de lógica os incluem ou de quantos outros arquivos de cabeçalho incluídos nos arquivos de lógica também os incluem (pode haver muitos níveis de apontamento) . Os arquivos de lógica, por outro lado, são abertos apenas uma vez pelo compilador (e pré-processador), quando são passados ​​para ele.

```
Arquivo.cpp + arquivo3.h ->
Arquivo.obj + Arquivo2.obj ->
Arquivo.exe
```

Para cada arquivo de lógica C++, o pré-processador construirá uma unidade de tradução inserindo conteúdo nela quando encontrar uma diretiva #include ao mesmo tempo em que removerá o código do arquivo de lógica e dos cabeçalhos quando encontrar a compilação condicional blocos cuja diretiva é avaliada como `false`. Ele também fará algumas outras tarefas, como substituições de macros.

### Exemplo de #IF
```cpp
#ifndef  FILE_H  
#include "file.h"
#endif
```


Arquivos de cabeçalho contem o nome de funções, Variáveis, classes e assim por diante, devem ser declarados antes que possam ser usados [1](https://docs.microsoft.com/pt-br/cpp/cpp/header-files-cpp?view=msvc-170), estes arquivos podem ser incluídos



Abaixo a sintaxe básica de um programa C++.
```cpp
#include <iostream>

int main()
{
    std::cout << "Meu primeiro programa." << std::endl;
}
```

- `std` - Namespace


**main.cpp**

```cpp

#include <iostream>
void Log(const char* message)
{
  std::cout << message std::endl;
}

int main() {
  Log("Hello World")
  std::cout << "Meu primeiro..." std::endl;
  std::cin.get();
}
```

## Passo 2
**main.cpp**

```cpp
void Log(const char* message);

int main() {
  Log("Hello World")
  std::cin.get();
}
```

**log.cpp**

```cpp
#include <iostream>
void Log(const char* message)
{
  std::cout << message std::endl;
}
```

## Passo 3
**Math.cpp**

```cpp
#include <iostream>

#define INTEGER int

int Multuply(int i, int j)
{
  INTEGER result = i * j;
  return result;
}
```

**Math.cpp**

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

## Passo 4
**Math.cpp**

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

## Passo 5

**log.cpp**

```cpp
#include <iostream>
int main()
{
  int variable = 8;
  char texto = 'T';  
  float valor = 3.4;
  float valor2 = 3f;

  bool teste = true;

  std::cout << variable std::endl;
  std::cout << sizeof(int) std::endl;
  std::cout << sizeof(variable) std::endl;
  std::cin.get();
}
```

## Passo 6

**log.h**

```cpp
#pragma once

#ifndef _LOG_H

void InitLog();

void Log(const char* message);

#endif

```

**log.cpp**

```cpp
#include "Log.h"
#include <iostream>

// "..log" caminho relativo
// <log.h> caminho do diretórios

void InitLog()
{
  Log("Inicializando log...");
}

void Log(const char* message)
{
    std::cout << message << std::endl;
};

```

**main.cpp**
```cpp
#include "Log.h"

void main();
{
  InitLog();
  Log("Teste...");
}

```


***
## Referências
