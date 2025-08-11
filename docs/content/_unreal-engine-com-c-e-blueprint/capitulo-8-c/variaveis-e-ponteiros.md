---
title: Variáveis e Ponteiros
excerpt: Armazenamento em memória usando variáveis e Ponteiros em linguagem C++
categories: 
  - "unreal-engine-com-c-e-blueprint"
  - "capitulo-8-c"
permalink: /:categories/:title
last_modified_at: 2023-03-27T08:48:05-04:00
order: 804
tags:
  - C++ 
  - Ponteiros
  - Variáveis   
---

{% include figure image_path="/assets/images/cpp/uday-awal-UjJWhMerJx0-unsplash.webp" alt="Uday Awal" caption="" %}

## 1. Variáveis

Variáveis são áreas de memória utilizadas para armazenar informação, essas áreas são nomeadas e devem possuir um tipo de dado, como por exemplo [As variáveis em C++](https://br.ccm.net/faq/10120-as-variaveis-em-c):

- `int` para armazenar números inteiros;
- `float` para armazenar números com casas decimais;
- `char` geralmente ocupa um byte na memória, permite armazenar um caractere ou cadeia de caracteres.

### 1.1. Declaração de variáveis

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

## 2. Unsigned

Assim como no C, o unsigned sozinho serve para nada (exceto o mostrado abaixo), ele é um modificador para determinar que um tipo numérico inteiro é sem sinal. Ou seja, você só terá valores positivos nele. Ele determina se o bit mais significativo será considerado o sinal de positivo ou negativo ou se este bit entrará no valor, por isso ele permite o dobro dos valores permitidos.

Um `int` vai de -2147483648 à 2147483647.

Um `unsigned` `int` vai de 0 à 4294967295.

### 2.1. Constantes

Assim como uma variável, uma constante também armazena um valor na memória do computador. Entretanto, esse valor não pode ser alterado: é constante. Para constantes é obrigatória a atribuição do valor[[Curso de C++/Variáveis e constantes](https://pt.wikiversity.org/wiki/Curso_de_C%2B%2B/Vari%C3%A1veis_e_constantes)].

Existem duas formas básicas para declarar uma constante em C++:

#### 2.1.1. Usando #define

Esta é uma maneira antiga de declarar constantes mas funciona normalmente;

Você deverá incluir a diretiva de pré-processador #define antes do início do código:

```cpp
#include <iostream>
using namespace std;
#define PI 3.1415
```

## 3. Usando const

Usando `const`, a declaração não precisa estar no início do código.

```cpp
const int i = 500; // uma constante inteira que armazena o número 500.
const double pi = 3.1415; // uma constante real que armazena o valor aproximado de pi.
```

## 4. Pragma once

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

## 5. Ponteiros

Um ponteiro é uma variável capaz de armazenar um endereço de memória ou o endereço de outra variável[[Apontadores/ Ponteiros/ Pointers](https://www.inf.pucrs.br/~pinho/PRGSWB/Ponteiros/ponteiros.html)].

### 5.1. Impressão de Ponteiros

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

### 5.2. Acessando conteúdo

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

Considerando a declaração anterior, podemos criar uma lista de elementos.

```cpp

class Human : public Character {
public:
    Human(const std::string& name, const std::string& sex, int health, int damage)
        : Character(name, sex, health, damage) {}
};


int main() {
    std::vector<Character*> characters;

    // Criação dos personagens
    Human human1("Gandalf", "Male", 100, 50);
    Human human2("Galadriel", "Female", 80, 40);
    
    characters.push_back(&human1);
    characters.push_back(&human2);
   
    // Listagem dos personagens e suas propriedades
    std::cout << "Personagens:" << std::endl;
    std::cout << "-------------" << std::endl;

    for (const auto& character : characters) {
        std::cout << "Name: " << character->getName() << std::endl;
        std::cout << "Sex: " << character->getSex() << std::endl;
        std::cout << "Health: " << character->getHealth() << std::endl;
        std::cout << "Damage: " << character->getDamage() << std::endl;
        std::cout << std::endl;
    }

    return 0;
}
```
