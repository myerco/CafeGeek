---
title: Programação em linguagem C++
excerpt: Programação em linguagem C++
permalink: /pages/cpp/
last_modified_at: 2023-03-27T08:48:05-04:00
toc: true    
---

<!--

- [1. Habilidades que serão aprendidas](#1-habilidades-que-serão-aprendidas)
- [2. Como o compilador C++ funciona?](#2-como-o-compilador-c-funciona)
  - [2.1. Abaixo a sintaxe básica de um programa C++](#21-abaixo-a-sintaxe-básica-de-um-programa-c)
  - [2.2. Exemplo de arquivo sendo incluído em outro](#22-exemplo-de-arquivo-sendo-incluído-em-outro)
  - [2.3. Exemplo de #IF](#23-exemplo-de-if)
  - [2.4. Arquivo de cabeçalho](#24-arquivo-de-cabeçalho)
- [3. O Linker](#3-o-linker)
- [4. Funções](#4-funções)
  - [4.1. Exemplo da Função log](#41-exemplo-da-função-log)
  - [4.2. Exemplo da Função de multiplicação](#42-exemplo-da-função-de-multiplicação)
  - [4.3. Declarando funções em arquivos externos](#43-declarando-funções-em-arquivos-externos)
- [5. Macros](#5-macros)
  - [5.1. Chamando uma função dentro de outra](#51-chamando-uma-função-dentro-de-outra)
- [6. Variáveis](#6-variáveis)
  - [6.1. Declaração de variáveis](#61-declaração-de-variáveis)
- [7. Unsigned](#7-unsigned)
  - [7.1. Constantes](#71-constantes)
    - [7.1.1. Usando #define](#711-usando-define)
- [8. Usando const](#8-usando-const)
- [9. Pragma once](#9-pragma-once)
- [10. Ponteiros](#10-ponteiros)
  - [10.1. Impressão de Ponteiros](#101-impressão-de-ponteiros)
  - [10.2. Acessando conteúdo](#102-acessando-conteúdo)
- [11. Classes](#11-classes)

-->

***

## 1. Habilidades que serão aprendidas

- Estrutura de arquivos;
- Variáveis e ponteiros;
- Estruturas de controle de fluxo;
- Manipulando Arrays;

## 2. Como o compilador C++ funciona?

Os arquivos C++ são divididos em dois tipos, um arquivo de código (.cpp) e um de cabeçalho (.h).

Os arquivos de código contem a lógica principal, estes arquivos podem incluir outros arquivos, utilizando a diretiva `#include`, são os arquivos de cabeçalho. A extensão não importa para o pré-processador C++ que substituirá literalmente a linha que contém a diretiva `#include`.

Cada arquivo de código deve se compilado dentro de um arquivo objeto (.obj), os arquivos objeto são juntados (linked) dentro de um executável (.exe)

```bash
Arquivo.cpp ->
Arquivo.obj + Arquivo2.obj ->
Arquivo.exe
```

### 2.1. Abaixo a sintaxe básica de um programa C++

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

### 2.2. Exemplo de arquivo sendo incluído em outro 

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

### 2.3. Exemplo de #IF

```cpp
#ifndef  FILE_H  
#include "file.h"
#endif
```

Arquivos de cabeçalho contem o nome de funções, Variáveis, classes e assim por diante, devem ser declarados antes que possam ser usados, estes arquivos podem ser incluídos.[[Arquivos de cabeçalho (C++)](https://docs.microsoft.com/pt-br/cpp/cpp/header-files-cpp?view=msvc-170 "Arquivos de cabeçalho (C++)")]

### 2.4. Arquivo de cabeçalho

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

## 3. O Linker

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

## 4. Funções

Funções são blocos de código que somente são executados quando são chamados. Funções podem ser reutilizadas em outros trechos de código, uma vez definidas podem ser usadas várias vezes [[C++ Functions](https://www.w3schools.com/cpp/cpp_functions.asp)].

É possível passar parâmetros para dentro da funções.

### 4.1. Exemplo da Função log

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

### 4.2. Exemplo da Função de multiplicação

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

### 4.3. Declarando funções em arquivos externos

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

## 5. Macros

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

### 5.1. Chamando uma função dentro de outra

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

## 6. Variáveis

Variáveis são áreas de memória utilizadas para armazenar informação, essas áreas são nomeadas e devem possuir um tipo de dado, como por exemplo [As variáveis em C++](https://br.ccm.net/faq/10120-as-variaveis-em-c):

- `int` para armazenar números inteiros;
- `float` para armazenar números com casas decimais;
- `char` geralmente ocupa um byte na memória, permite armazenar um caractere ou cadeia de caracteres.

### 6.1. Declaração de variáveis

Para declarar uma variável, basta indicar o seu tipo seguido do seu nome. Existem várias convenções sobre o nome das variáveis. Alguns preferem separar as diferentes partes do nome com _ (traço baixo). Outros preferem escrever uma letra maiúscula para separá-los. Exemplo:

log.cpp

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
  // sifeof - Apresenta o tamanho em bytes na memória
  std::cout << sizeof(int) << std::endl;
  std::cout << sizeof(variable) << std::endl;
  std::cout << teste << std::endl;
  std::cin.get();
}
```

## 7. Unsigned

Assim como no C, o unsigned sozinho serve para nada (exceto o mostrado abaixo), ele é um modificador para determinar que um tipo numérico inteiro é sem sinal. Ou seja, você só terá valores positivos nele. Ele determina se o bit mais significativo será considerado o sinal de positivo ou negativo ou se este bit entrará no valor, por isso ele permite o dobro dos valores permitidos.

Um `int` vai de -2147483648 à 2147483647.

Um `unsigned` `int` vai de 0 à 4294967295.

### 7.1. Constantes

Assim como uma variável, uma constante também armazena um valor na memória do computador. Entretanto, esse valor não pode ser alterado: é constante. Para constantes é obrigatória a atribuição do valor[[Curso de C++/Variáveis e constantes](https://pt.wikiversity.org/wiki/Curso_de_C%2B%2B/Vari%C3%A1veis_e_constantes)].

Existem duas formas básicas para declarar uma constante em C++:

#### 7.1.1. Usando #define

Esta é uma maneira antiga de declarar constantes mas funciona normalmente;

Você deverá incluir a diretiva de pré-processador #define antes do início do código:

```cpp
#include <iostream>
using namespace std;
#define PI 3.1415
```

## 8. Usando const

Usando `const`, a declaração não precisa estar no início do código.

```cpp
const int i = 500; // uma constante inteira que armazena o número 500.
const double pi = 3.1415; // uma constante real que armazena o valor aproximado de pi.
```

## 9. Pragma once

Especifica que o compilador inclui o arquivo de header apenas uma vez, ao compilar um arquivo de código-fonte [[once pragma](https://docs.microsoft.com/pt-br/cpp/preprocessor/once?view=msvc-170)].

log.h

```cpp
#pragma once

#ifndef _LOG_H
#define _LOG_H

void InitLog();

void Log(const char* message);

#endif
```

log.cpp

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

main.cpp

```cpp
#include "Log.h"

void main();
{
  InitLog();
  Log("Teste...");
}
```

## 10. Ponteiros

Um ponteiro é uma variável capaz de armazenar um endereço de memória ou o endereço de outra variável[[Apontadores/ Ponteiros/ Pointers](https://www.inf.pucrs.br/~pinho/PRGSWB/Ponteiros/ponteiros.html)].

### 10.1. Impressão de Ponteiros

Podemos imprimir o endereço de memória dos ponteiros.

```cpp
#include <iostream>
using namespace std;
void main()
{
  int x;
  int *ptr;
  ptr = &x;
  cout << "O endereço de X é: " << ptr << endl;
  cout << "O valor de X é: " << x << endl;
}
```

### 10.2. Acessando conteúdo

Acessamos o conteúdo do valor contido no ponteiro, endereço de memória, utilizando o operador de referência (*) do lado esquerdo.

```cpp
#include <iostream>
using namespace std;
void main()
{
  int x;
  int *ptr;
  x = 5;
  ptr = &x;
  cout << "O valor da variável X é: " << *ptr << endl;
  *ptr = 10;
  cout << "Agora, X vale: " << *ptr << endl;
}
```

## 11. Classes

C++ é uma linguagem de programação orientada a objetos.

Tudo em C++ está associado a classes e objetos, juntamente com seus atributos e métodos. Por exemplo: na vida real, um carro é um objeto. O carro tem atributos, como peso e cor, e métodos, como direção e freio.

Atributos e métodos são basicamente variáveis e funções que pertencem à classe. Estes são muitas vezes referidos como "membros da classe".

Uma classe é um tipo de dados definido pelo usuário que podemos usar em nosso programa e funciona como um construtor de objetos ou um "projeto" para criar objetos[[C++ Classes and Objects](https://www.w3schools.com/cpp/cpp_classes.asp)].

conta.h

```cpp
#include <iostream>
using namespace std;

class Conta
{
  int numero;     // São atributos
  string nome;    // privados por
  float saldo;    // default
public:
  void inicializa(string n, float s);
  void deposita(float valor);
  void consulta();
  int saque(float valor);
};
```

conta.cpp

```cpp
#include "conta.h"

void Conta::inicializa(string n, float s)
{
  nome = n;
  saldo = s;
  if (saldo < 0)
    cout << "Erro na Criação da Conta!!!" << endl;
}

void Conta::deposita(float valor)
{
  saldo = saldo + valor;
}

void Conta::consulta()
{
  cout << "Cliente: " << nome << endl;
  cout << "Saldo Atual: " << saldo << endl;
  cout << "Numero da Conta: " << numero << endl;
}

int Conta::saque(float valor)
{
  if (saldo < valor)
    return 0;
  else
  {
    saldo = saldo - valor;
    return 1;
  }
}
```

arquivo.cpp

```cpp
#include "conta.h"

void main()
{
  Conta MinhaConta;
  Conta *OutraConta;

  MinhaConta.saldo = 10; // ERRO!!!

  MinhaConta.inicializa("Fulano", 10.25);
  OutraConta->inicializa("Beltrano", 220.00);

  MinhaConta.deposita(12.75);
  MinhaConta.consulta();
  MinhaConta.saque(15.00);
  MinhaConta.consulta();

  OutraConta->consulta();
}
```
