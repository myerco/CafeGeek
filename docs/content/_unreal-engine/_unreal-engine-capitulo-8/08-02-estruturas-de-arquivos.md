---
title: Estruturas de arquivos
excerpt: Como são as estruturas de arquivos na linguagem C++?
permalink: /unreal-engine-capitulo-8/estruturas-de-arquivos
last_modified_at: 2023-03-27T08:48:05-04:00
order: 802
tags:
  - Unreal Engine
  - C++ 
---

{% include figure image_path="/assets/images/cpp/uday-awal-UjJWhMerJx0-unsplash.webp" alt="Uday Awal" caption="" %}

## 1. Como o compilador C++ funciona?

Os arquivos C++ são divididos em dois tipos, um arquivo de código (.cpp) e um de cabeçalho (.h).

Os arquivos de código contem a lógica principal, estes arquivos podem incluir outros arquivos, utilizando a diretiva `#include`, são os arquivos de cabeçalho. A extensão não importa para o pré-processador C++ que substituirá literalmente a linha que contém a diretiva `#include`.

Cada arquivo de código deve se compilado dentro de um arquivo objeto (.obj), os arquivos objeto são juntados (linked) dentro de um executável (.exe)

```bash
## Arquivo código fonte
c:\arquivo.cpp

## Arquivo objeto
c:\arquivo.obj + Arquivo2.obj 

## Arquivo executável
c:\arquivo.exe
```

## 2. Usando o Microsoft Visual Studio com C++

Instale o Visual Studio e escolha os pacotes necessários para usar a linguagem C++. [Link](/unreal-engine-capitulo-1/instalacao-e-configuracao#3-instalando-o-visual-studio-para-programar-com-c)

Após a instalação vamos criar um projeto teste seguinte os passos:

1. Criar novo projeto;
2. Projeto vazio;
3. Usando o Gerenciador de Soluções adicione um arquivo main.cpp: Arquivos de Origem > Adicionar > Novo Item > Arquivo do C++ (.cpp)

## 3. Sintaxe básica de um programa C++

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

## 4. Estrutura de arquivos do Visual Studio

```bash
── Projeto  
    ├── Projeto.sln                         # Arquivo de configuração do projeto.
    └── Projeto
        ├── main.cpp
        └── teste.h
```

### 4.1. Exemplo de arquivo sendo incluído em outro

multiply.cpp

```cpp
int main()
{
    std::cout << "Meu primeiro programa." << std::endl;

#include "parte.h"
```

parte.h

```cpp
}
```

Cada arquivo de cabeçalho pode ser aberto várias vezes durante a fase de pré-processamento de todos os arquivos de lógica, dependendo de quantos arquivos de lógica os incluem ou de quantos outros arquivos de cabeçalho incluídos nos arquivos de lógica também os incluem (pode haver muitos níveis de apontamento) . Os arquivos de lógica, por outro lado, são abertos apenas uma vez pelo compilador (e pré-processador), quando são passados ​​para ele.

sum.cpp

```cpp
int sum(int a, int b)
{
  return a + b;
#include "parte.h"
}
```

Para cada arquivo de lógica C++, o pré-processador construirá uma unidade de tradução inserindo conteúdo nela quando encontrar uma diretiva `#include` ao mesmo tempo em que removerá o código do arquivo de lógica e dos cabeçalhos quando encontrar a compilação condicional blocos cuja diretiva é avaliada como `false`. Ele também fará algumas outras tarefas, como substituições de macros.

## 5. Diretiva de pré-processador

Definem como as operações de pré-processamento serão realizadas.

### 5.1. #DEFINE

Define constantes simbólicas.

```cpp
#define AREA_TRIAN(b, h) ((b * h)/2)

...

area = AREA_TRIAN(10,15)

```

### 5.2. #IF

Define se um bloco de será incluído caso a expressão seja `true`.

```cpp
#if defined(CREDIT)
    credit();
#elif defined(DEBIT)
    debit();
#else
    printerror();
#endif
```

### 5.3. #IFNDEF

Define um item se ele não tiver sido definido anteriormente.

```cpp
#ifndef  FILE_H  
#include "file.h"
#endif
```

Arquivos de cabeçalho contem o nome de funções, Variáveis, classes e assim por diante, devem ser declarados antes que possam ser usados, estes arquivos podem ser incluídos.[[Arquivos de cabeçalho (C++)](https://docs.microsoft.com/pt-br/cpp/cpp/header-files-cpp?view=msvc-170 "Arquivos de cabeçalho (C++)")]

### 5.4. Arquivo de cabeçalho

Character.h

```cpp
class Character
    {
    private:
        std::string name;
        std::string sex;
        int health;
        int damage;
    public:
    Character(const std::string& name, const std::string& sex, int health, int damage)
        : name(name), sex(sex), health(health), damage(damage) {}

    // Setters
    void setName(const std::string& name);

    void setSex(const std::string& sex);

    void setHealth(int health);

    void setDamage(int damage);

    // Getters
    std::string getName();

    std::string getSex();

    int getHealth();

    int getDamage();
};
```

Character.cpp

```cpp
#include "Character.h" // header in local directory
#include <iostream> // header in standard library

void Character::setName(const std::string& name) {
        this->name = name;
    }

    void Character::setSex(const std::string& sex) {
        this->sex = sex;
    }

    void Character::setHealth(int health) {
        if (health >= 0 && health <= 100) {
            this->health = health;
        }
        else {
            std::cout << "Health must be between 0 and 100." << std::endl;
        }
    }

    void Character::setDamage(int damage) {
        this->damage = damage;
    }

    std::string Character::getName()
    {
        return this->name;
    }

    std::string Character::getSex()
    {
        return this->sex;
    }

       int Character::getHealth() {
        return this->health;
    }

    int Character::getDamage() {
        return this->damage;
    }

```

## 6. O Linker

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
