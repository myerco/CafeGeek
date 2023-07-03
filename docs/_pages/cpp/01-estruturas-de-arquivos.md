---
title: Estruturas de arquivos
excerpt: Estruturas de arquivos
permalink: /pages/cpp/estruturas-de-arquivos
last_modified_at: 2023-03-27T08:48:05-04:00
toc: true  
sidebar:
    nav: dev_unreal_6  
categories:
  - Unreal Engine
  - cpp
tags:
  - cpp
  - C++ 
  - Estruturas de arquivos
---

[Avançado](/collection-archive/){: .btn .btn--danger}

{% include figure image_path="/assets/images/cpp/uday-awal-UjJWhMerJx0-unsplash.webp" alt="Uday Awal" caption="" %}

## 1. Como o compilador C++ funciona?

Os arquivos C++ são divididos em dois tipos, um arquivo de código (.cpp) e um de cabeçalho (.h).

Os arquivos de código contem a lógica principal, estes arquivos podem incluir outros arquivos, utilizando a diretiva `#include`, são os arquivos de cabeçalho. A extensão não importa para o pré-processador C++ que substituirá literalmente a linha que contém a diretiva `#include`.

Cada arquivo de código deve se compilado dentro de um arquivo objeto (.obj), os arquivos objeto são juntados (linked) dentro de um executável (.exe)

```bash
Arquivo.cpp ->
Arquivo.obj + Arquivo2.obj ->
Arquivo.exe
```

### 1.1. Abaixo a sintaxe básica de um programa C++

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

### 1.2. Exemplo de arquivo sendo incluído em outro

multiply.cpp

```cpp
int multiply(int a, int b)
{
  return a * b;
#include "parte.h"
}
```

parte.h

```cpp
}
```

Cada arquivo de cabeçalho pode ser aberto várias vezes durante a fase de pré-processamento de todos os arquivos de lógica, dependendo de quantos arquivos de lógica os incluem ou de quantos outros arquivos de cabeçalho incluídos nos arquivos de lógica também os incluem (pode haver muitos níveis de apontamento) . Os arquivos de lógica, por outro lado, são abertos apenas uma vez pelo compilador (e pré-processador), quando são passados ​​para ele.

```bash
Arquivo.cpp + arquivo3.h ->
Arquivo.obj + Arquivo2.obj ->
Arquivo.exe
```

Para cada arquivo de lógica C++, o pré-processador construirá uma unidade de tradução inserindo conteúdo nela quando encontrar uma diretiva #include ao mesmo tempo em que removerá o código do arquivo de lógica e dos cabeçalhos quando encontrar a compilação condicional blocos cuja diretiva é avaliada como `false`. Ele também fará algumas outras tarefas, como substituições de macros.

### 1.3. Exemplo de #IF

```cpp
#ifndef  FILE_H  
#include "file.h"
#endif
```

Arquivos de cabeçalho contem o nome de funções, Variáveis, classes e assim por diante, devem ser declarados antes que possam ser usados, estes arquivos podem ser incluídos.[[Arquivos de cabeçalho (C++)](https://docs.microsoft.com/pt-br/cpp/cpp/header-files-cpp?view=msvc-170 "Arquivos de cabeçalho (C++)")]

### 1.4. Arquivo de cabeçalho

my_class.h

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

my_class.cpp

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

## 2. O Linker

O `Linker` (vinculador) é um programa que cria arquivos executáveis. O linker resolve problemas de ligação, como o uso de símbolos ou identificadores que são definidos em uma unidade de tradução e são necessários de outras unidades de tradução. [[C++ Programming](https://en.wikibooks.org/wiki/C%2B%2B_Programming/Programming_Languages/C%2B%2B/Code/Compiler/Linker "C++ Programming")].

Resumindo, o trabalho do vinculador é resolver referências a símbolos indefinidos descobrindo qual outro objeto define um símbolo em questão e substituindo espaços reservados pelo endereço do símbolo.

Considere o arquivo sum.c que exporta duas funções, uma para adicionar dois inteiros ou `int` e outra para adicionar dois `float`:

sum.cpp

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

sum.h

```cpp
int sumI(int a, int b);
float sumF(float a, float b);
```

print.cpp

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