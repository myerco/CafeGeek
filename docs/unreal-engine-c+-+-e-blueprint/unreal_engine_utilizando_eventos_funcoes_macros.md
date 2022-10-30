---
title: Utilizando Eventos, funções e macros no Unreal Engine
description: Neste capitulo serão apresentado como estruturar a lógica de programação utilizando métodos, funções e macros.
tags: [Unreal Engine, eventos, events, funções, functions, macro]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
date: 2022-09-21 
---

## Índice

***

- [Entendo Métodos e funções em programação](#entendo-métodos-e-funções-em-programação)

- [O que são Eventos em Blueprint](#o-que-são-eventos-em-blueprint)

- [Funções](#funções)

- [Funções Puras](#funções-puras)

- [Macros](#macros)

- [Collapse Nodes](#collapse-nodes)

- [Executando a função e a macro](#executando-a-função-e-a-macro)


*** 

## Entendo Métodos e funções em programação

***

Para entender melhor a estrutura de programação que representa a construção de eventos e funções vamos abordar alguns conceitos de programação.

### Programação Orientada a Objetos

{% include image.html
    src="https://4.bp.blogspot.com/-Bx-UYCheS3Y/UwSDeRIkSZI/AAAAAAAACgY/_-J6s4GzjEc/s1600/image.jpg"
    alt="Figura: Programação Orientada a Objetos: Uma introdução."
    caption="Figura: Programação Orientada a Objetos: Uma introdução."
%}

Um método é um procedimento ou função em Conceitos de **Programação Orientada a Objetos**. Considerando que uma função é um grupo de código reutilizável que pode ser usado em qualquer parte do programa. Isso ajuda na necessidade de escrever o mesmo código repetidamente. Também ajuda os programadores a escrever códigos modulares.

### Métodos

{% include image.html
    src="https://arquivo.devmedia.com.br/artigos/henrique_gasparotto/4_pilares_oo/image001.png"
    alt="Figura: Os 4 pilares da Programação Orientada a Objetos."
    caption="Figura: Os 4 pilares da Programação Orientada a Objetos."
%}

- Um método também funciona da mesma forma que o da função;

- Um método é definido dentro de uma classe. Por exemplo: main () em Java;  

- Um método pode ser privado, público ou protegido.

O método é invocado apenas por sua referência / objeto. Por exemplo: se a classe tem *obj* como um nome de objeto, o método é chamado por: obj.method ();  

Um método é capaz de operar em dados que estão contidos na classe.
Cada objeto tem seu próprio método que está presente na classe.

|Pessoa |                   |
|:-:    |:--                |
|+      |eyesColor:enum     |
|+      |hairColor:enum     |
|       |                   |
|+      |Walk()             |
|+      |Run()              |
|+      |Jump()             |
|+      |Crouch()           |

### Funções

Uma função é um bloco de instruções que recebe uma entrada específica, faz alguns cálculos e, finalmente, produz a saída.  

Uma função é definida independentemente. Por exemplo: main () em **C++**

Por padrão, uma função é pública.

Ele pode ser acessado em qualquer lugar em todo o programa.  

É chamado pelo próprio nome.  

Ele tem a capacidade de retornar valores, se necessário.

Se uma função for definida, ela será a mesma para todos os objetos criados.  

```cpp
#include <iostream>

static int multiply(int a, int b) {
  return a * b;
}

int main() {
  std::cout << multiply(2, 2) << std::endl;
  std::cin.get();
}
```

## O que são Eventos em Blueprint

***

Os eventos são nós chamados a partir do código do jogo para iniciar a execução de uma rede individual dentro do `EventGraph`. Eles permitem que os **Blueprints** executem uma série de ações em resposta a certos eventos que ocorrem dentro do jogo, como quando o jogo começa, quando um nível é reiniciado ou quando um jogador sofre dano.

Os eventos podem ser acessados dentro do **Blueprints** para implementar novas funcionalidades ou para substituir ou aumentar a funcionalidade padrão. Qualquer número de eventos pode ser usado em um único `EventGraph`; embora apenas um de cada tipo possa ser usado.

### Evento de dano  no personagem

{% include imagebase.html
    src="unreal/modulos/blueprint_event_damaged.webp"
    alt="Figura: Blueprint - Evento de CasoDano."
    caption="Figura: Blueprint - Evento de CasoDano."
%}

- `CausaDano` é um evento customizado utilizando a opção `Add Custom Event` no menu de contexto dentro do `Event Graph`;

- Pertence a classe *BP_Hero* do tipo **Character**.


{% include imagebase.html
    src="unreal/modulos/blueprint_event_damaged_overlap.webp"
    alt="Figura: Blueprint - Evento de chamado de evento."
    caption="Figura: Blueprint - Evento de chamado de evento."
%}

### Chamando o evento

- Utilizando o evento `OnComponentBeginOverlap` para acionar o evento **CausaDano**.

### Evento e Métodos

Os métodos são procedimentos ou funções que realizam as ações próprias do objeto. Assim, os métodos são as ações que o objeto pode realizar. Tudo o que o objeto faz é através de seus métodos, pois é através dos seus métodos que um objeto se manifesta, através deles que o objeto interage com os outros objetos.

### Exemplo C++

```cpp
class Actor {
  void BeginPlay();
  void Tick();
  void BeginOverlap();
  void Identificar() delegate;
};

class ExemploEventos : public Actor {

};
```

```cpp

void AProjeto::BeginPlay() {
  Super::BeginPlay();
};

void AProjeto::DestruaMundoNerd(World* mundo ) {
   destroy();
};

// Called every frame
void AProjeto::Tick(float DeltaTime)
{
  Super::Tick(DeltaTime);

};
```

## Funções

***

São mini programas com as características de alocação de memória, estruturas internas de código e variáveis locais.
Podem receber parâmetros externos e retornam algum valor para o programa que executou a chamada.  

- Tem seu próprio `Event Graph`;

- Funções não suportam o nó `Delay` ou eventos de temporização;

- Funções podem ter ser replicadas em jogos multiplayer;

- Não aceitam eventos customizados.

### Exemplo C++ de funções

```cpp
// Função com parâmetros
void CalculoIMC(float pPeso, float pAltura) {
  // Variável local
  float resultado;
  resultado =  (pAltura * pAltura) / pPeso;
  return = resultado;
};
```

### Exemplo Blueprint de funções

{% include imagebase.html
    src="unreal/modulos/blueprint_function_calc_imc.webp"
    alt="Figura: Blueprint - Exemplo de CalculoIMC."
    caption="Figura: Blueprint - Exemplo de CalculoIMC."
%}

## Funções Puras

Na programação de computadores, uma função pura é uma função que possui as seguintes propriedades[[1](https://en.wikipedia.org/wiki/Pure_function)]:

- Os valores de retorno da função são idênticos para argumentos idênticos (sem variação com variáveis estáticas locais, variáveis não locais, argumentos de referência mutáveis ou fluxos de entrada) e

- O aplicativo de função não tem efeitos colaterais (nenhuma mutação de variáveis estáticas locais, variáveis não locais, argumentos de referência mutáveis ou fluxos de entrada/saída).

Abaixo alguns exemplos de funções puras em **C++**:

- `sin` - Retorna sempre o mesmo valor;

- `strlen` - Retorna o tamanho de uma área de memória;

- `max` - Retorna o maior de dois valores;

Exemplos de funções impuras usando variáveis `static`[[2](https://docs.microsoft.com/pt-br/cpp/cpp/storage-classes-cpp?view=msvc-170)]:

```cpp
// static1.cpp
// compile with: /EHsc
#include <iostream>

using namespace std;
void showstat( int curr ) {
   static int nStatic;    // Value of nStatic is retained
                          // between each function call
   nStatic += curr;
   cout << "nStatic is " << nStatic << endl;
}

int main() {
   for ( int i = 0; i < 5; i++ )
      showstat( i );
}
```

No exemplo acima o valor de `nStatic` varia como uma variável não local.

```bash
nStatic is 0
nStatic is 1
nStatic is 3
nStatic is 6
```

"Funções puras têm uma desvantagem crucial. Eles não podem se comunicar com o mundo exterior. Porque funções para entrada e saída, funções para construir um estado ou funções para criar números aleatórios não podem ser puras..."

## Macros

***

Blueprint Macros, ou Macros, são essencialmente iguais a gráficos de nós recolhidos. Eles têm um ponto de entrada e um ponto de saída designado por nós de túnel. Cada túnel pode ter qualquer número de pinos de execução ou de dados que são visíveis no nó da macro quando usados em outros **Blueprints** e gráficos.

- São basicamente um modelo *Template* de código ou nós;

- Não aceitam eventos customizados;

- Não podem ser replicados em jogos multiplayer.

### Exemplo C++ de macros

```cpp
#define MIN(a,b) (((a)<(b)) ? a : b)

std::cout << "The minimum is " << MIN(42, 8) << endl;
```

### Exemplo Blueprint de macros

{% include imagebase.html
    src="unreal/modulos/blueprint_macro_example.webp"
    alt="Figura: Blueprint - Exemplo Macro."
    caption="Figura: Blueprint - Exemplo Macro."
%}

## Collapse Nodes

***

Usado principalmente para organização de código, escondendo nós da estrutura principal.

{% include imagebase.html
    src="unreal/modulos/blueprint_collapse_nodes_example.webp"
    alt="Figura: Blueprint - Exemplo Collapse nodes."
    caption="Figura: Blueprint - Exemplo Collapse nodes."
%}

- Aceitam parâmetros de entrada e saída;

- No menu de contexto do `Event Graph`  acionamos a opção `Collapse Nodes`;

- Vai ser criado um gráfico de eventos próprio.

## Executando a função e a macro 

{% include imagebase.html
    src="unreal/modulos/blueprint_call_function_macro.webp"
    alt="Figura: Blueprint - Exemplo de Call function marco."
    caption="Figura: Blueprint - Exemplo de Call function marco."
%}
