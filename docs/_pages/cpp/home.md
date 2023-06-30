---
title: Programação em linguagem C++
excerpt: Programação em linguagem C++
permalink: /pages/cpp/
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

## 3. Funções

Funções são blocos de código que somente são executados quando são chamados. Funções podem ser reutilizadas em outros trechos de código, uma vez definidas podem ser usadas várias vezes [[C++ Functions](https://www.w3schools.com/cpp/cpp_functions.asp)].

É possível passar parâmetros para dentro da funções.

### 3.1. Exemplo da Função log

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

### 3.2. Exemplo da Função de multiplicação

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

### 3.3. Declarando funções em arquivos externos

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

## 4. Macros

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

### 4.1. Chamando uma função dentro de outra

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

## 5. Variáveis

Variáveis são áreas de memória utilizadas para armazenar informação, essas áreas são nomeadas e devem possuir um tipo de dado, como por exemplo [As variáveis em C++](https://br.ccm.net/faq/10120-as-variaveis-em-c):

- `int` para armazenar números inteiros;
- `float` para armazenar números com casas decimais;
- `char` geralmente ocupa um byte na memória, permite armazenar um caractere ou cadeia de caracteres.

### 5.1. Declaração de variáveis

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

## 6. Unsigned

Assim como no C, o unsigned sozinho serve para nada (exceto o mostrado abaixo), ele é um modificador para determinar que um tipo numérico inteiro é sem sinal. Ou seja, você só terá valores positivos nele. Ele determina se o bit mais significativo será considerado o sinal de positivo ou negativo ou se este bit entrará no valor, por isso ele permite o dobro dos valores permitidos.

Um `int` vai de -2147483648 à 2147483647.

Um `unsigned` `int` vai de 0 à 4294967295.

### 6.1. Constantes

Assim como uma variável, uma constante também armazena um valor na memória do computador. Entretanto, esse valor não pode ser alterado: é constante. Para constantes é obrigatória a atribuição do valor[[Curso de C++/Variáveis e constantes](https://pt.wikiversity.org/wiki/Curso_de_C%2B%2B/Vari%C3%A1veis_e_constantes)].

Existem duas formas básicas para declarar uma constante em C++:

#### 6.1.1. Usando #define

Esta é uma maneira antiga de declarar constantes mas funciona normalmente;

Você deverá incluir a diretiva de pré-processador #define antes do início do código:

```cpp
#include <iostream>
using namespace std;
#define PI 3.1415
```

## 7. Usando const

Usando `const`, a declaração não precisa estar no início do código.

```cpp
const int i = 500; // uma constante inteira que armazena o número 500.
const double pi = 3.1415; // uma constante real que armazena o valor aproximado de pi.
```

## 8. Pragma once

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

## 9. Ponteiros

Um ponteiro é uma variável capaz de armazenar um endereço de memória ou o endereço de outra variável[[Apontadores/ Ponteiros/ Pointers](https://www.inf.pucrs.br/~pinho/PRGSWB/Ponteiros/ponteiros.html)].

### 9.1. Impressão de Ponteiros

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

### 9.2. Acessando conteúdo

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

## 10. Classes

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

## 11. O fluxo de desenvolvimento e Herança

Um modelo de desenvolvimento utilizando **C++** pode ser visto abaixo onde primeiro criamos a classe do objeto A em **C++** e depois uma classe **Blueprint** B filha da classe A. Fazendo isso pode-se aproveitar as características de ambas linguagens, como por exemplo: lógica em **C++** e parametrização de componentes visuais usando o Editor **Blueprint**.  

### 11.1. Exemplo Herança

1. Vamos Criar uma **Blueprint** *BP_Plataforma* do tipo `static_mesh_actor`;

1. Depois Criar a classe **C++** `Plataforma` do tipo `AStaticMeshActor`;

1. Alterar classe pai do *BP_Plataforma* para *Plataforma*.

Onde :

| Origem      | Destino       |       |
|:-           |:-             |:-     |
|Classe C++   |Blueprints     |Certo  |
|Blueprints   |Classe C++     | Errado|

*Tabela: Representação do desenvolvimento descrito anteriormente.*

Sobre a herança de classes permitem usar classes já definidas para derivar classes novas onde a nova classe herda as propriedades da classe base.

### 11.2. Exemplo em C++

```cpp
// Classe Pessoa
class Pessoa {
  int32 iVida;
  FString sNome;
}

class Heroi: public Pessoa {
  float fForca = 100;
}

void main() {
   // instânciando o objeto Nostromo do tipo Heroi
    Heroi nostromo;
}
```

### 11.3. Exemplo em Blueprint

```cpp
class Hugo: Pessoa
      // iVida -- Herdada
      // movimentacao() - Herdada  

      AddActiveTrigger()  
      float SpeedPlataforma  
      int32 Vida #Error  
```

## 12. Polimorfismo em C++

Polimorfismo em linguagens orientadas a objeto, é a capacidade de objetos se comportarem de forma diferenciada em face de suas características ou do ambiente ao qual estejam submetidos, mesmo quando executando ação que detenha, semanticamente, a mesma designação.

O polimorfismo em C++ se apresenta sob diversas formas diferentes, desde as mais simples, como funções com mesmo nome e lista de parâmetros diferentes, até as mais complexas como funções virtuais, cujas formas de execução são dependentes da classe a qual o objeto pertence e são identificadas em tempo de execução.

## 13. Funções virtuais

"Uma função virtual é uma função de membro que é declarada dentro de uma classe base e é redefinida (Substituída) por uma classe derivada. Quando você se refere a um objeto de classe derivada usando um ponteiro ou uma referência à classe base, pode chamar uma função virtual para esse objeto e executar a versão da função da classe derivada."[Funções Virtuais](https://pt.wikipedia.org/wiki/Fun%C3%A7%C3%A3o_virtual "Funções Virtuais")

- As funções virtuais garantem que a função correta seja chamada para um objeto, independentemente do tipo de referência (ou ponteiro) usado para a chamada da função;

- Eles são usados principalmente para obter polimorfismo de tempo de execução;

- As funções são declaradas com uma palavra-chave virtual na classe base;

- A resolução da chamada de função é feita em tempo de execução.

### 13.1. Exemplo de função virtual em C++ com Unreal Engine

```cpp
class WeaponBase {
  public: virtual void OnFire() {}
};
class WeaponRifle : public WeaponBase {
  public: void OnFire() override {}
};

...
WeaponRifle
void anotherFunction(WeaponBase *someWeapon) {
  someWeapon->OnFire();
}
```

- Na função anotherFunction o método chamado em OnFire é WeaponRifle::OnFire().

- O método WeaponBase::OnFire não é chamado pois foi sobreposto.

### 13.2. Exemplo de função virtual no C++

```cpp
#include <iostream>

using std::cout;
using std::endl;

class Base {
public:
    // declaração da função virtual
    virtual void Quem_VIRTUAL()
    {
        cout << "Base\n";
    }
    // função comum
    void Quem_NAO_VIRTUAL()
    {
        cout << "Base\n";
    }
};

class Derivada : public Base {
public:
    // função virtual sobrescrita
    virtual void Quem_VIRTUAL()
    {
        cout << "Derivada\n";
    }
    // função comum sobrescrita
    void Quem_NAO_VIRTUAL()
    {
        cout << "Derivada\n";
    }
};

int main ()
{
    Base *ptr_base;
    Derivada derivada;

    ptr_base = &derivada;           // conversão implícita permissível
    ptr_base->Quem_VIRTUAL();       // chamada polimórfica (mostra: "Derivada")
    ptr_base->Quem_NAO_VIRTUAL();   // chamada comum, não-polimórfica (mostra: "Base")

    cout << endl;

    return 0;
}
```