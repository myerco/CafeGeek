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

- [Referências](#refer-ncias)

## Como o compilador C++ funciona?

Os arquivos C++ são divididos em dois tipos, um arquivo de código (.cpp) e um de cabeçalho (.h).

Os arquivos de código contem a lógica principal, estes arquivos podem incluir outros arquivos, utilizando a diretiva `#include`, são os arquivos de cabeçalho. A extensão não importa para o pré-processador C++ que substituirá literalmente a linha que contém a diretiva `#include`.

Cada arquivo de código deve se compilado dentro de um arquivo objeto (.obj), os arquivos objeto são juntados (linked) dentro de um executável (.exe)

```
Arquivo.cpp ->
Arquivo.obj + Arquivo2.obj ->
Arquivo.exe
```

### Abaixo a sintaxe básica de um programa C++.
```cpp
#include <iostream>

int main()
{
    std::cout << "Meu primeiro programa." << std::endl;
}
```

- `std` - Namespace, define um escopo para identificadores (funções,tipos e variáveis);
- `cout` - Função para escrever um texto no dispositivo de saída;


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


Arquivos de cabeçalho contem o nome de funções, Variáveis, classes e assim por diante, devem ser declarados antes que possam ser usados, estes arquivos podem ser incluídos.[[Arquivos de cabeçalho (C++)](https://docs.microsoft.com/pt-br/cpp/cpp/header-files-cpp?view=msvc-170 "Arquivos de cabeçalho (C++)")]

### Declarando variáveis no arquivo de cabeçalho

**my_class.h**

```cpp
// my_class.h
namespace N
{
    class my_class
    {
    public:
        void do_something();
    };
}
```

**my_class.cpp**
```cpp
// my_class.cpp
#include "my_class.h" // header in local directory
#include <iostream> // header in standard library

using namespace N;
using namespace std;

void my_class::do_something()
{
    cout << "Doing something!" << endl;
}
```


## O Linker

O `Linker` (vinculador) é um programa que cria arquivos executáveis. O linker resolve problemas de ligação, como o uso de símbolos ou identificadores que são definidos em uma unidade de tradução e são necessários de outras unidades de tradução. [[C++ Programming](https://en.wikibooks.org/wiki/C%2B%2B_Programming/Programming_Languages/C%2B%2B/Code/Compiler/Linker "C++ Programming")].

Resumindo, o trabalho do vinculador é resolver referências a símbolos indefinidos descobrindo qual outro objeto define um símbolo em questão e substituindo espaços reservados pelo endereço do símbolo.

Considere o arquivo sum.c que exporta duas funções, uma para adicionar dois inteiros ou `int` e outra para adicionar dois `float`:

**sum.cpp**
```cpp
int sumI(int a, int b) {
    return a + b;
}

float sumF(float a, float b) {
    return a + b;
}
```

Depois de compilar observe os símbolos exportados e importados por este objeto.

```bash
$nm sum.o
0000000000000014 T sumF
0000000000000000 T sumI
```
[nm Unix](https://en.wikipedia.org/wiki/Nm_(Unix))

> nm - list symbols from object files

Nenhum símbolo é importado e dois símbolos são exportados: sumF e sumI. Esses símbolos são exportados como parte do segmento .text (T), portanto são nomes de funções, código executável.

Se outros arquivos de origem (C ou C++) quiserem chamar essas funções, eles precisarão declará-las antes de chamar.

A maneira padrão de fazer isso é criar um arquivo de cabeçalho que os declare e os inclua em qualquer arquivo de origem que queiramos chamá-los. O cabeçalho pode ter qualquer nome e extensão.

**sum.h**

```cpp
int sumI(int a, int b);
float sumF(float a, float b);
```

**print.cpp**
```cpp
#include <iostream> // std::cout, std::endl
#include "sum.h" // sumI, sumF

void printSum(int a, int b) {
    std::cout << a << " + " << b << " = " << sumI(a, b) << std::endl;
}

void printSum(float a, float b) {
    std::cout << a << " + " << b << " = " << sumF(a, b) << std::endl;
}
```


## Funções
Funções são blocos de código que somente são executados quando são chamados. Funções podem ser reutilizadas em outros trechos de código, uma vez definidas podem ser usadas várias vezes [[C++ Functions](https://www.w3schools.com/cpp/cpp_functions.asp)].

É possível passar parâmetros para dentro da funções.

### Exemplo da Função log
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

### Declarando funções em arquivos externos

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

## Macros
Uma macro é um trecho de código em um programa que é substituído pelo valor da macro. A macro é definida pela diretiva #define . Sempre que um micronome é encontrado pelo compilador, ele substitui o nome pela definição da macro[[Macros e seus tipos em C / C++](https://acervolima.com/macros-e-seus-tipos-em-c-c/)].

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

## Resumo


***
## Referências
