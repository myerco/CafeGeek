---
title: Comunicação entre Blueprint
excerpt: Neste capítulo vamos organizar a comunicação entre objetos.
permalink: /pages/unreal-engine/comunicacao-blueprint
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true 
categories:
  - Unreal Engine
tags:
  - Blueprint
  - comunicação
  - dispatcher
---

[Avançado](/collection-archive/){: .btn .btn--danger}

## 1. Como facilitar a comunicação entre objetos Blueprint?

Construindo um meio para que objetos individuais separados interagirem uns com os outros.  

Útil para fazer coisas como:

- Transmitindo um evento para vários ouvintes;

- Dizendo a um objeto específico para fazer algo;

- Consultando outro objeto por:
  
  - Estado;

  - Valores de propriedade;

  - Valores variáveis;

  - Resultados.

### 1.1. Estrutura da comunicação entre Blueprints

A seguir apresentamos um diagrama de como os elementos podem se comunicar e trocar informações.

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-comunicacao-entre-atores.webp"
    alt="Figura: Estrutura de Comunicação entre Blueprints."
    caption="Figura: Estrutura de Comunicação entre Blueprints."
%}

A comunicação envolverá o seguinte:

- Um projeto de envio, um remetente de informações (Emissor);

- Pelo menos um `Receiving Blueprint` para receber as informações (Receptor);

- A comunicação exigirá uma referência em algum ponto.

  Em outras palavras, uma das partes, o remetente ou o receptor,  deve tomar conhecimento da outra, isso ocorre porque, como afirmado acima, não existe um sistema de comunicação de amplo espectro.

- Toda a comunicação do **Blueprint** é unilateral.

  - **Blueprints** podem enviar dados para frente e para trás, mas requer que ambos os **Blueprints** configurem seus próprios caminhos individuais de comunicação.
  - As consultas são possíveis, mas são iniciadas pelo remetente (ainda unidirecional).

### 1.2. Preparando o ambiente de testes

Vamos criar um ator com os seguintes parâmetros para que funcione como controlador de objetos;

1. Crie um `Blueprint Actor` com nome *ControleLuz*;

1. Adicione e configure um `Static Mesh`;

1. Adicione e configure um `Box Colision`;

1. Implemente a função *LampadaVisible* para desligar e ligar a iluminação os objetos `Light Point` passados como parâmetro;

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-light-off-on.webp"
    alt="Figura: Blueprint - Função para desligar e ligar uma point PointLight Component."
    caption="Figura: Blueprint - Função para desligar e ligar uma point PointLight Component."
%}

1. Adicione a variável *Lampada* do tipo `Point Light` e configure `Instance Editable` para `true`;

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-light-component.webp"
    alt="Figura: Blueprint - propriedades do elemento PointLightComponent."
    caption="Figura: Blueprint - propriedades do elemento PointLightComponent."
%}

1. Adicione dois objetos `Light Point` na cena;

1. Em um dos objetos de iluminação adicione a `tag` *lampada*;

1. Associe um objeto na cena com a propriedade *Lampada* do *ControleLuz*;

## 2. Comunicação utilizando Acesso direto

Nesta passo iremos acessar diretamente o objeto e suas propriedades, usando o evento `OnBeginOverLap` para alterar o estado da lâmpada de ligado para desligado pois o mesmo é passado como parâmetro.  

### 2.1. Chamando a função LampadaVisible

Criando um referência do objeto é possível acessar a função **LampadaVisible**.

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-light-overlap.webp"
    alt="Figura: Blueprint - Lógica da chamada da função usando OnBeginOverLap."
    caption="Figura: Blueprint - Lógica da chamada da função usando OnBeginOverLap."
%}

Quando qualquer objeto colidir com o *ControleLuz* a lâmpada ira desligar ou ligar.

### 2.2. Vídeo Comunicação entre Blueprints

{% include video id="td6_Nm2tYfc" provider="youtube" %}

## 3. Utilizando CAST

**CAST** ou conversão é um operador especial que força um tipo de dados a ser convertido em outro.

*C++.*

```cpp
AStaticMeshActor* StaticMesh = Cast<AStaticMeshActor>(SM);
```

O comando acima inicializa o objeto `StaticMesh` do tipo `AStaticMeshActor`.

Para este passo usaremos o evento `OnEndOverlap` para ler todos os objetos que tem a `tag` *lampada* da cena e carregar em um *array* de objetos. Para cada objeto será executado o comando `CAST` informando o `type` para ter acesso a todas a funcionalidades do objeto.

### 3.1. CAST do objeto PointLight

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-light-cast-tag.webp"
    alt="Figura:Blueprint - Lógica para pegar todos os objetos com uma determinada tag e chamar uma função usando GetAllActorWithTag e Cast to PointLight."
    caption="Figura:Blueprint - Lógica para pegar todos os objetos com uma determinada tag e chamar uma função usando GetAllActorWithTag e Cast to PointLight."
%}

- `GetAllActorWithTag` - Retorna um array com todos os objetos da cena com a **tag** passada como parâmetro, no caso *Lampada*.

### 3.2. Vídeo Comunicação entre Blueprints - Usando Cast 03 Unreal Engine

{% include video id="VT6uob6UiSQ" provider="youtube" %}

## 4. Utilizando o objeto Blueprint Interface

**Blueprint interface** permite que vários tipos diferentes de objetos compartilhem e sejam acessados através de uma interface comum. Simplificando, as **Blueprint interfaces** permitem que diferentes **Blueprints** compartilhem e enviem dados entre si.

### 4.1. Menu Blueprint/Blueprint Interface

Podemos implementar um `Blueprint interface` Utilizando o menu de contexto.

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-context-menu-interface.webp"
    alt="Figura: Blueprint - Menu > Blueprint Interface."
    caption="Figura: Blueprint - Menu > Blueprint Interface."
%}

Crie o objeto com o nome *BPI_Colecionaveis* para que possamos continuar o exemplo.

### 4.2. Editor de Blueprint Interface

Clicando e abrindo o objeto criado anteriormente perceba que o objeto não tem lógica pois neste caso o objeto funciona como uma ponte para eventos em outros objetos que deverão ter sua própria lógica.

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-editor-interface.webp"
    alt="Figura: Blueprint - Editor da function interface."
    caption="Figura: Blueprint - Editor da function interface."
%}

Em seguida adicione uma função chamada *Nome* para que possa servir como função ponte.

### 4.3. Implementando um objeto para utilizar a interface

1. Crie o ator *BP_Cadeira* do tipo `Blueprint Actor`;

1. Adicione e configure um `Static Mesh` com um malha de uma cadeira ou mesa;

1. Utilizando a opção `Class Settings` adicione a interface *BPI_Colecionaveis*.

1. Uma vez a interface configurada as funções de  *BPI_Colecionaveis* ficarão disponíveis através de eventos.

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-inteface-function.webp"
    alt="Figura: Blueprint - Lógica da função Nome com GetObjectName."
    caption="Figura: Blueprint - Lógica da função Nome com GetObjectName."
%}

1. Adicione no `Character` jogável *BP_Hero* e implemente a lógica abaixo.

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-inteface-tracebychannel.webp"
    alt="Figura: Blueprint - Utilizando a função SphereTraceByChannel para capturar objetos e chamar a função nome."
    caption="Figura: Blueprint - Utilizando a função SphereTraceByChannel para capturar objetos e chamar a função nome."
%}

- **RaioSegurar** - Raio da esfera que é disparada;

- **DistanciaSegurar** - Distância do raio disparado;

- **Nome** - A função *Nome* da interface ficará disponível para ser chamada.

### 4.4. Utilizando parâmetros na Interface

1. Implemente a função *ExecutaAcao* com parâmetro *Acao* do tipo `string`, usaremos esse parâmetro para determinar ações que o objeto pode executar;

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-interface-with-parameter.webp"
    alt="Figura: Blueprint - Declaração da função com parâmetros."
    caption="Figura: Blueprint - Declaração da função com parâmetros."
%}

1. Ao chamar a função é fornecido um valor.

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-interface-example-call.webp"
    alt="Figura: Blueprint - Exemplo da chamada da função com parâmetros."
    caption="Figura: Blueprint - Exemplo da chamada da função com parâmetros."
%}

1. Implemente a lógica de tratamento do parâmetro dentro do objeto cadeira ou mesa.

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-interface-example-event.webp"
    alt="Figura: Blueprint - Dentro do objeto podemos chamar o evento para chamar a Interface."
    caption="Figura: Blueprint - Dentro do objeto podemos chamar o evento para chamar a Interface."
%}

Podemos melhorar o controle utilizando uma variável `enumeration` para parametrizar as ações.  

### 4.5. Vídeo Comunicação entre Blueprints - Utilizando o objeto Blueprint Interface - 04 - Unreal Engine

{% include video id="ugqPc5-YQV4" provider="youtube" %}

### 4.6. Event Dispatcher

São eventos que transmitem mensagens para outros **Blueprints**, os receptores "ouvem" as mensagens e podem implementar a sua própria lógica de tratamento.

Vinculando um ou mais eventos a um `Event Dispatcher` , você pode fazer com que todos esses eventos sejam disparados assim que o `Event Dispatcher` for chamado.

Esses eventos podem ser vinculados a uma classe **Blueprint**, mas os `Event Dispatchers` também permitem que eventos sejam disparados dentro do `Level Blueprint`.

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-event-dispatcher.webp"
    alt="Figura: Estrutura do EventDispatcher."
    caption="Figura: Estrutura do EventDispatcher."
%}

### 4.7. Exemplo utilizando o Character BP_Hero que será o emissor dos eventos

1. Adicionamos `EventDispatcher`;

1. No `Event Graph` implementados a chamada do evento utilizando **Call** (Call nome do evento).

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-call-dispatchers.webp"
    alt="Figura: Blueprint - Exemplo de chamada do evento Bind Event com a função Arremessa Objetos."
    caption="Figura: Blueprint - Exemplo de chamada do evento Bind Event com a função Arremessa Objetos."
%}

### 4.8. Lógica dos objetos que vão interagir com o personagem

1. No objeto **BP-Cubo** por exemplo adicionamos referência ao personagem **BP_Hero** usando `cast` para ter acesso ao evento registrado no `dispatcher`;

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-dispatchers-bind.webp"
    alt="Figura: Blueprint - Cast de outro objeto para acessar o Dispatcher registrado dentro desse objeto."
    caption="Figura: Blueprint - Cast de outro objeto para acessar o Dispatcher registrado dentro desse objeto."
%}

1. Implementamos `Bind Event` do disptacher para  associar um evento a chamada.

{% include imagelocal.html
    src="unreal/comunicacao/unreal-engine-add-impulse-example.webp"
    alt="Figura: Blueprint - Adicionando impulso, arremessando os objetos."
    caption="Figura: Blueprint - Adicionando impulso, arremessando os objetos."
%}

### 4.9. Vídeo Comunicação entre Blueprints - Event Dispatcher - 05 -  Unreal Engine

{% include video id="bmxFZH3hFxc" provider="youtube" %}
