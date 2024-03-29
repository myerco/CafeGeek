---
title: Classes
excerpt: Classes de Objetos na linguagem C++
permalink: /unreal-engine-capitulo-8/classes
last_modified_at: 2023-03-27T08:48:05-04:00
order: 805
tags:
  - cpp
  - C++
  - Classes    
---

{% include figure image_path="/assets/images/cpp/uday-awal-UjJWhMerJx0-unsplash.webp" alt="Uday Awal" caption="" %}

## 1. Classes

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

## 2. O fluxo de desenvolvimento e Herança

Um modelo de desenvolvimento utilizando **C++** pode ser visto abaixo onde primeiro criamos a classe do objeto A em **C++** e depois uma classe **Blueprint** B filha da classe A. Fazendo isso pode-se aproveitar as características de ambas linguagens, como por exemplo: lógica em **C++** e parametrização de componentes visuais usando o Editor **Blueprint**.  

### 2.1. Exemplo Herança

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

### 2.2. Exemplo em C++

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

### 2.3. Exemplo em Blueprint

```cpp
class Hugo: Pessoa
      // iVida -- Herdada
      // movimentacao() - Herdada  

      AddActiveTrigger()  
      float SpeedPlataforma  
      int32 Vida #Error  
```

## 3. Polimorfismo em C++

Polimorfismo em linguagens orientadas a objeto, é a capacidade de objetos se comportarem de forma diferenciada em face de suas características ou do ambiente ao qual estejam submetidos, mesmo quando executando ação que detenha, semanticamente, a mesma designação.

O polimorfismo em C++ se apresenta sob diversas formas diferentes, desde as mais simples, como funções com mesmo nome e lista de parâmetros diferentes, até as mais complexas como funções virtuais, cujas formas de execução são dependentes da classe a qual o objeto pertence e são identificadas em tempo de execução.

## 4. Funções virtuais

"Uma função virtual é uma função de membro que é declarada dentro de uma classe base e é redefinida (Substituída) por uma classe derivada. Quando você se refere a um objeto de classe derivada usando um ponteiro ou uma referência à classe base, pode chamar uma função virtual para esse objeto e executar a versão da função da classe derivada."[Funções Virtuais](https://pt.wikipedia.org/wiki/Fun%C3%A7%C3%A3o_virtual "Funções Virtuais")

- As funções virtuais garantem que a função correta seja chamada para um objeto, independentemente do tipo de referência (ou ponteiro) usado para a chamada da função;

- Eles são usados principalmente para obter polimorfismo de tempo de execução;

- As funções são declaradas com uma palavra-chave virtual na classe base;

- A resolução da chamada de função é feita em tempo de execução.

### 4.1. Exemplo de função virtual em C++ com Unreal Engine

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

### 4.2. Exemplo de função virtual no C++

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
