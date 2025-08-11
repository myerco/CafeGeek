---
title: Herança de Objetos
excerpt: Neste capítulo será apresentado a estrutura de herança de objetos.
categories: 
  - "unreal-engine-com-c-e-blueprint"
  - "capitulo-1-introducao-aos-blueprints"
permalink: /:categories/:title
## sidebar:
##  nav: dev_unreal_1
last_modified_at: 2023-03-28T08:48:05-04:00
date: 2024-03-01T08:48:05-04:00
order: 109
tags:
  - Blueprint
  - Atores
  - Classes
---

## 1. Trabalhando herança com Blueprint

Como apresentado no conceito de classes, a herança permite usar classes já definidas para derivar novas classes, a seguir vamos verificar como implementar utilizando **Blueprint**.  

Exemplo de classe Herói que derive de Humanos:  

```bash
└── Character
    ├── BeginPlay()
    └── Humanos
        ├── Vida (float) = 100    
        ├── Dano (float) = 100        
        ├── BeginPlay() (herdado)
        ├── Heroi
        |   ├── Vida = 100 (herdado)
        |   └── Dano = 50 (herdado)
        └── Vilao
            ├── Vida = 100 (herdado)
            └── Dano = 80 (herdado)    
```

## 2. Criando uma classe filho

{% include imagelocal.html
    src="unreal/actor/unreal-engine-create-child-class.webp"
    alt="Figura: Create Child Blueprint Class."
    caption="Selecionando o objeto pai e acionamento o menu de contexto (RMB) acessamos a opção para criar a classe derivada."
%}

## 3. Variáveis da classe pai

{% include imagelocal.html
    src="unreal/actor/unreal-engine-show-my-blueprints.webp"
    alt="Figura: MyBlueprint propriedades."
    caption="Podemos exibir as variáveis, componentes ou eventos da herdados da classe pai, no exemplo acima a variável NameBase pertence a classe pai."
%}

## 4. Herança de propriedades e métodos

É possível sobrescrever os métodos da classe pai para adicionar uma nova lógica, vamos aos passos.

Criando um evento para sobrescrever o evento `Begin Play`.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-functions-overrider.webp"
    alt="Figura: Functions Override."
    caption="Podemos sobrescrever os métodos da classe pai."
%}

## 5. Executando um evento da classe pai

{% include imagelocal.html
    src="unreal/actor/unreal-engine-beginplay-override.webp"
    alt="Figura: Parent: Begin Play."
    caption="Clicando com o botão direito (RMB) acessamos a opção Add Call to Parent Function que executa a classe pai antes de executar o próximo comando."
%}

## 6. Componente ChildActor

O componente `ChildActor` permite associar uma classe filha utilizando a lista de componentes.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-childActor.webp"
    alt="Figura: ChildActor."
    caption="O componente ChildActor associa uma outra classe ao objeto."
%}

`ChildActor` - É necessário informar a classe filho neste componente.

## 7. Referências de atores e componentes

{% include imagelocal.html
    src="unreal/actor/unreal-engine-view-references.webp"
    alt="Figura: Reference Viewer."
    caption="Clicando com o botão direito (RMB) podemos acessar a opção para visualizar todas as referências do objeto. No exemplo acima BP_ActorChild2 é uma classe derivada do BP_ActorBase e BP_ActorChild está associada usando o componente ChildActor."
%}

## 8. Manipulando Actors

Podemos adicionar, remover ou selecionar os atores que estão na cena do jogo, a seguir vamos implementar e entender esses comandos.

### 8.1. Spawn e Destroy Actors - Criando e destruindo um Actor

O processo de criação de uma nova instância de um ator é conhecido como *spawning*. A geração de atores é realizada usando a função `SpawnActor`. Esta função cria uma nova instância de uma classe especificada e retorna um ponteiro para o Actor recém-criado. `SpawnActor` só pode ser usado para criar instâncias de classes que herdam da classe Actor em sua hierarquia.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-actor-spawn.webp"
    alt="Figura: Exemplo de SpawnActor e DestroyActor."
    caption="Cria o ator na posição do objeto TargetPoint e se ele já está na cena o destrói."
%}

Utilizando o `Level Bluprint` podemos implementar o código acima.

1. Ao pressionar a tecla **B** o ator e criado na cena utilizando as coordenadas de um componente `targetPoint` adicionando na cena;

1. O comando `flip/flop` é utilizado para intercalar entre criar e destruir o ator, com os métodos `SpawnActor` e `DestroyActor` respectivamente;

1. Usamos `IsValid` para verificar se o ator existe na cena.

### 8.2. Listando Actors por classe

Utilizando a função `GetAllActorOfClass` e o loop `For Each Loop` podemos listar todos os atores na cena.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-get-all-ActorOfClass.webp"
    alt="Figura: GetAllActorOfClass."
    caption="Lista todos os objetos instanciados da classe BP_ActorBase e os destrói."
%}

{% include iframe.html
    src="https://blueprintue.com/render/xugypke9/"
    title="Cafegeek - Criando e destruindo objetos"
    caption="Criando, destruindo e listando objetos na cena."
    ref="https://blueprintue.com/render/xugypke9/"
%}
