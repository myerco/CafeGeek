---
title: Eventos, funções e macros
excerpt: Estrutura de programação utilizando métodos, funções e macros.
categories: 
  - "unreal-engine-com-c-e-blueprint"
  - "capitulo-1-introducao-aos-blueprints"
permalink: /:categories/:title
sidebar:
  nav: dev_unreal_1
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 113
tags:
  - blueprint
---

## 1. Entendo Métodos e funções em programação

Para entender melhor a estrutura de programação que representa a construção de eventos e funções vamos abordar alguns conceitos de programação orientada a objetos.

### 1.1. Programação Orientada a Objetos

{% include image.html
    src="https://4.bp.blogspot.com/-Bx-UYCheS3Y/UwSDeRIkSZI/AAAAAAAACgY/_-J6s4GzjEc/s1600/image.jpg"
    alt="Figura: Programação Orientada a Objetos: Uma introdução."
    caption="Figura: A Programação Orientada a Objetos (POO) surgiu com a finalidade de facilitar a vida daqueles que trabalham com desenvolvimento de software, pois na POO o difícil não é desenvolver bem um software, mas sim desenvolver um software que satisfaça o cliente, ou seja, garantir que o que será entregue será realmente o que foi pedido. Uma das características da POO é fazer com que o programador pense as coisas de forma distintas, transformando-as assim em objeto, aplicando propriedades e métodos, que comentaremos mais adiante, reduzindo assim a complexidade no desenvolvimento e manutenção de software, aumentando a produtividade."
%}

Um método é um procedimento ou função em Conceitos de **Programação Orientada a Objetos**. Considerando que uma função é um grupo de código reutilizável que pode ser usado em qualquer parte do programa. Isso ajuda na necessidade de escrever o mesmo código repetidamente. Também ajuda os programadores a escrever códigos modulares.

### 1.2. Métodos

{% include image.html
    src="https://arquivo.devmedia.com.br/artigos/henrique_gasparotto/4_pilares_oo/image001.png"
    alt="Figura: Os 4 pilares da Programação Orientada a Objetos."
    caption="Figura: ...vemos uma comparação muito clara entre a programação estruturada e a programação orientada a objetos no que diz respeito aos dados. Repare que, no paradigma estruturado, temos procedimentos (ou funções) que são aplicados globalmente em nossa aplicação. No caso da orientação a objetos, temos métodos que são aplicados aos dados de cada objeto. Essencialmente, os procedimentos e métodos são iguais, sendo diferenciados apenas pelo seu escopo."
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

### 1.3. Funções

Uma função é um bloco de instruções que recebe uma entrada específica, faz alguns cálculos e, finalmente, produz a saída;  

Uma função é definida independentemente. Por exemplo: main () em **C++**;

Por padrão, uma função é pública;

Ele pode ser acessado em qualquer lugar em todo o programa;  

É chamado pelo próprio nome;  

Ele tem a capacidade de retornar valores, se necessário;

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

## 2. O que são Eventos em Blueprint

Os eventos são nós chamados a partir do código do jogo para iniciar a execução de uma rede individual dentro do `EventGraph`. Eles permitem que os **Blueprints** executem uma série de ações em resposta a certos eventos que ocorrem dentro do jogo, como quando o jogo começa, quando um nível é reiniciado ou quando um jogador sofre dano.

Os eventos podem ser acessados dentro do **Blueprints** para implementar novas funcionalidades ou para substituir ou aumentar a funcionalidade padrão. Qualquer número de eventos pode ser usado em um único `EventGraph`; embora apenas um de cada tipo possa ser usado.

### 2.1. Evento de dano  no personagem

{% include imagelocal.html
    src="unreal/modulos/unreal-engine-event-damaged.webp"
    alt="Figura: Blueprint - Evento de CausaDano."
    caption="Figura: Criando um método customizado CausaDano no BP_Hero podemos adicionar a lógica para o tratamento da variável Vida."
%}

- `CausaDano` é um evento customizado utilizando a opção `Add Custom Event` no menu de contexto dentro do `Event Graph`;

- Pertence a classe *BP_Hero* do tipo `Character`.

{% include imagelocal.html
    src="unreal/modulos/unreal-engine-event-damaged-overlap.webp"
    alt="Figura: Chamando o evento OnComponentBeginOverlap."
    caption="Figura: Utilizando o evento OnComponentBeginOverlap para acionar o evento CausaDano."
%}

### 2.2. Evento e Métodos

Os métodos são procedimentos ou funções que realizam as ações próprias do objeto. Assim, os métodos são as ações que o objeto pode realizar. Tudo o que o objeto faz é através de seus métodos, pois é através dos seus métodos que um objeto se manifesta, através deles que o objeto interage com os outros objetos.

### 2.3. Exemplo C++

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

## 3. Funções no Unreal Engine

São mini programas com as características de alocação de memória, estruturas internas de código e variáveis locais.

Podem receber parâmetros externos e retornam algum valor para o programa que executou a chamada.  

- Tem seu próprio `Event Graph`;

- Funções não suportam o nó `Delay` ou eventos de temporização;

- Funções podem ter ser replicadas em jogos multiplayer;

- Não aceitam eventos customizados.

### 3.1. Exemplo de uma função em C++

```cpp
// Função com parâmetros
void CalculoIMC(float pPeso, float pAltura) {
  // Variável local
  float resultado;
  resultado =  (pAltura * pAltura) / pPeso;
  return = resultado;
};
```

### 3.2. Exemplo de uma função Blueprint

{% include imagelocal.html
    src="unreal/modulos/unreal-engine-function-calc-imc.webp"
    alt="Figura: Blueprint - Exemplo de CalculoIMC."
    caption="Figura: A função recebe dois parâmetros e retorna um valor."
%}

### 3.3. Funções Puras

Na programação de computadores, uma função pura é uma função que possui as seguintes propriedades[[1](https://en.wikipedia.org/wiki/Pure_function)]:

- Os valores de retorno da função são idênticos para argumentos idênticos (sem variação com variáveis estáticas locais, variáveis não locais, argumentos de referência mutáveis ou fluxos de entrada) e

- O aplicativo de função não tem efeitos colaterais (nenhuma mutação de variáveis estáticas locais, variáveis não locais, argumentos de referência mutáveis ou fluxos de entrada/saída).

Abaixo alguns exemplos de funções puras em **C++**:

- `sin` - Retorna sempre o mesmo valor;

- `strlen` - Retorna o tamanho de uma área de memória;

- `max` - Retorna o maior de dois valores;

Exemplos de funções impuras usando variáveis `static`[[Classes de Armazenamento](https://docs.microsoft.com/pt-br/cpp/cpp/storage-classes-cpp?view=msvc-170)]:

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

## 4. Macros

Blueprint Macros, ou Macros, são essencialmente iguais a gráficos de nós recolhidos. Eles têm um ponto de entrada e um ponto de saída designado por nós de túnel. Cada túnel pode ter qualquer número de pinos de execução ou de dados que são visíveis no nó da macro quando usados em outros **Blueprints** e gráficos.

- São basicamente um modelo *Template* de código ou nós;

- Não aceitam eventos customizados;

- Não podem ser replicados em jogos multiplayer.

### 4.1. Exemplo de uma macro em C++

```cpp
#define MIN(a,b) (((a)<(b)) ? a : b)

std::cout << "The minimum is " << MIN(42, 8) << endl;
```

### 4.2. Exemplo de uma macro em Blueprint

{% include imagelocal.html
    src="unreal/modulos/unreal-engine-macro-example.webp"
    alt="Figura: Blueprint - Exemplo Macro."
    caption="Acima a lógica de uma macro."
%}

## 5. Collapse Nodes

Usado principalmente para organização de código, escondendo nós da estrutura principal.

{% include imagelocal.html
    src="unreal/modulos/unreal-engine-collapse-nodes-example.webp"
    alt="Figura: Blueprint - Exemplo Collapse nodes."
    caption="Figura: Selecionando os nós e acionando o menu de contexto (RMB) escolhemos Collapse Nodes."
%}

- Aceitam parâmetros de entrada e saída;

- No menu de contexto do `Event Graph`  acionamos a opção `Collapse Nodes`;

- Vai ser criado um gráfico de eventos próprio.

## 6. Executando a função e a macro

{% include imagelocal.html
    src="unreal/modulos/unreal-engine-call-function-macro.webp"
    alt="Figura: Blueprint - Exemplo de Call function marco."
    caption="Figura: No exemplo acima usamos a função e uma macro."
%}

## 7. Eventos predefinidos para causar e receber Dano

{% include imagelocal.html
    src="unreal/dano/unreal-engine-applydamage.webp"
    alt="Figura: Blueprint - Apply Damage."
    caption="Figura: Ao colidir no objeto de controle é acionado o evento Appy Damage para registrar que um dano foi efetuado. O valor do dano é informado como parâmetro."
%}

{% include imagelocal.html
    src="unreal/dano/unreal-engine-anydamage.webp"
    alt="Figura: Blueprint - Any Damage."
    caption="Figura: A variável vida foi definida no objeto que RECEBE o dano, ao ser acionada."
%}
