---
title: Actor, Pawn e Character
excerpt: Neste capítulo serão apresentados as classes Actor, Pawn e Character e seus componentes.
categories: 
  - "unreal-engine"
  - "capitulo-1"
date: 2024-03-08T08:48:05-04:00
order: 108
tags:
  - Character
  - Actors
sidebar:
  nav: unreal-engine  
---

## 1. Classe Actor

A classe **Actor** compreende objetos básicos que podem ser adicionados ao mundo. Atores podem conter coleções de componentes, os quais podem ser usados para controlar como o ator se move, como é renderizado, etc. Atores suportam transformações 3D tal como translação, rotação e escala.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-class-actor-details.webp"
    alt="Figura: Actor > Class Defaults."
    caption="Figura: Actor > Valores iniciais da classe."
%}

**`Parent Class`** : Classe pai de Actor (Classe **C++**).

## 2. Classe Pawn

A classe **Pawn** ou peão é a classe base de todos os atores que podem ser controlados por jogadores ou IA. Um peão é a representação física de um jogador ou entidade de IA dentro do mundo. Isso não significa apenas que o peão determina a aparência visual do jogador ou entidade de IA, mas também como ele interage com o mundo em termos de colisões e outros aspectos físicos

**Informação:** Isso pode ser confuso em certas circunstâncias, pois alguns tipos de jogos podem não ter uma malha de jogador ou avatar visível dentro do jogo. Independentemente disso, o peão, *pawn*, ainda representa a localização física, rotação, etc. de um jogador ou entidade dentro do jogo. Um personagem é um tipo especial de peão que tem a capacidade de andar.  
{: .notice--info}

### 2.1. Default Pawn

Enquanto a classe *Pawn* fornece apenas o essencial para a criação de uma representação física de um jogador ou entidade de IA no mundo, a subclasse `DefaultPawn` vem com alguns componentes e funcionalidades adicionais.

A classe `DefaultPawn` contém um componente `DefaultPawnMovementComponent` nativo, um `CollisionComponent` esférico e um `StaticMeshComponent`.

Para controlar o `DefaultPawnMovementComponent`, bem como a câmera, uma propriedade do tipo *Booleano* para adicionar ligações de movimento padrão também está presente na classe `DefaultPawn` e é definido como verdadeiro por padrão.

### 2.2. Spectator Pawn

A classe `SpectatorPawn` é uma subclasse de `DefaultPawn`. Por meio de um **GameMode**, diferentes classes podem ser especificadas como padrões para *Pawn* e `SpectatorPawn`, e esta classe fornece uma estrutura simples ideal para a funcionalidade de espectador.

As Classes tem propriedades que definem a estrutura do objeto.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-class-pawn-details.webp"
    alt="Figura: Pawn > Class Defaults."
    caption="Figura: Pawn > Valores iniciais da classe."
%}

- `Start with Tick Enabled` - Habilita o evento Tick na lógica. Pode ser desabilitado para ganhar performance;

- `Use Controller Rotation Pitch/Yaw` - Pode usar movimentação dos controladores;

- `Auto Possess Player/AI` - Faz com o **PlayerController** possua automaticamente o peão (*Pawn*);

- `Replication` : Opções para replicar o objeto pela rede.

- `Can be Damaged` : Habilita os eventos de dano do objeto.

## 3. Classe Character

Um personagem é um *Pawn* que tem algumas funcionalidades básicas de movimento bípede por padrão.  
Com a adição de um componente `CharacterMovementComponent`, um `CapsuleComponent` e um `SkeletalMeshComponent`, a classe *Pawn* é estendida para a classe *Character* com muitos recursos. Um personagem é projetado para uma representação do jogador orientada verticalmente que pode andar, correr, pular, voar e nadar pelo mundo. Esta classe também contém implementações de rede básica e modelos de entrada.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-class-character-details.webp"
    alt="Figura: Character > Class Defaults."
    caption="Figura: Character > Valores iniciais da classe."
%}

- `Animation Mode` - Habilita uma animação simples ou um **Blueprint** de animação ao objeto;

- `Anim Class` - Blueprint de animação associado.

- `Skeletal Mesh Asset` - Malha esquelética.

## 4. Componentes e Actors

Os componentes são um tipo especial de objeto que os atores podem anexar a si próprios como subobjetos. Os componentes são úteis para compartilhar comportamentos comuns, como a capacidade de exibir uma representação visual e reproduzir sons. Eles também podem representar conceitos específicos do projeto, como a maneira como um veículo interpreta a entrada e muda sua própria velocidade e orientação. Por exemplo, um projeto com carros, aeronaves e barcos controláveis pelo usuário pode implementar as diferenças no controle e movimento do veículo, alterando qual componente um ator do veículo usa.

### 4.1. Adicionando componentes

Na aba `Components`s podemos adicionar componentes para os objetos de forma hierarquia.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-add-component.webp"
    alt="Figura: Components > Add."
    caption="Figura: Adicionando componentes."
%}

{% include imagelocal.html
    src="unreal/actor/unreal-engine-add-component-hierarchy.webp"
    alt="Figura: Components."
    caption="Figura: Estrutura hierárquica dos componentes."
%}

Exemplo de Componentes que podemos adicionar a classe:  

- `Actor Child` - Componente associa outro ator a classe principal.

- `Static Mesh` - Adiciona um objeto de 3D;

- `Box Collsion` - Adiciona uma caixa de colisão;

Para editar os componentes utilizamos o Editor de objetos e componentes.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-component-details.webp"
    alt="Figura: Component > Details."
    caption="Figura: Podemos editar as propriedades dos componentes."
%}

### 4.2. Static Mesh - Malhas estáticas

**Static Mesh** são a unidade básica usada para criar a geometria do mundo para níveis (*level*) criados no **Unreal Engine**. A grande maioria de qualquer mapa em um jogo feito com **Unreal** consistirá em Malhas Estáticas, geralmente na forma de Atores de Malha Estática.

Consistem em um conjunto de polígonos que podem ser armazenados em cache na memória de vídeo e renderizados pela placa de vídeo. Isso permite que eles sejam renderizados com eficiência, o que significa que podem ser muito mais complexos do que outros tipos de geometria, como **Brushes**. Como são armazenados em cache na memória de vídeo, as malhas estáticas podem ser traduzidas, giradas e dimensionadas, mas não podem ter seus vértices animados de nenhuma forma.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-static-mesh-viewport.webp"
    alt="Figura: Statis Mesh ViewPort."
    caption="Figura: Podemos manipular as transformações da Static Mesh."
%}

#### 4.2.1. Propriedades do componente Static Mesh

- `Transform` - Propriedades de localização do componente;

- `Static Mesh` - Malha associada ao componente;

- `Material` - Material associado a malha;

- `Simulate Physcis` - Habilita a simulação de física do objeto.

**Editor de StaticMesh.**

Visualização da malha e suas propriedades (vértices, UV e modelo de colisão).

{% include imagelocal.html
    src="unreal/actor/unreal-engine-static-mesh-editor.webp"
    alt="Figura: Editor de StaticMesh."
    caption="Figura: O editor permite adicionar uma caixa de colisão e visualizar o mapeamento UV."
%}

### 4.3. Skeletal Mesh - Malha Esquelética

As **Skeletal mesh** são compostas por duas partes: Um conjunto de polígonos compostos para formar a superfície da Malha Esquelética e um conjunto hierárquico de ossos interconectados que podem ser usados para animar os vértices dos polígonos. **Skeletal mesh** são frequentemente usados no **Unreal Engine 4** para representar personagens ou outros objetos animados.

#### 4.3.1. A Estrutura da malha esquelética

A baixo uma representação da hierarquia do Skeletal Mesh.

```bash
└── Ator
    ├── Skeletal mesh
    |   ├── Mesh - (Malha do elemento)
    |   ├── Animation - (Animações associadas ao esqueleto)
    |   ├── Skeleton - (Estrutura de coordenadas alinhadas para marcar os ossos dos elementos)
    |   ├── Blueprint - (Lógica para sequenciamento de animações)
    |   └── Physics - (Estrutura para gerenciamento da física da estruturas)
    ├── Animation mode
    |   └── Use Animation Blueprint
    └── Anim Class
        └── ThirdPerson_AnimBP_C
```

#### 4.3.2. Propriedades do Skeletal Mesh

{% include imagelocal.html
    src="unreal/actor/unreal-engine-skeletal-mesh.webp"
    alt="Figura: Mesh (Character Mesh)."
    caption="Figura: Aba Componentes > Lista de componentes predefinidos da classe Character, Details >  Propriedades do componente."
%}

Componentes da Classe Character:

- `Mesh` - Malha Esquelética;

- `CameraBoom` - Objeto do tipo `SpringArm` (Braço) para controlar a câmera;

- `FollowCamera` - Objeto do tipo `Camera`;

- `CharacterMovement` - Componente responsável pela lógica de movimentos do objeto.

Propriedades da Mesh (Skeletal):

- `Animation Mode` - Tipo de animação do componente;
  
- `Anim Class` - Lógica de animação, Animation Blueprint, associada ao componente;
  
- `Mesh` - Skeletal Mesh associada ao componente.

#### 4.3.3. O Editor Skeletal Mesh

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-skeleton-mannequim.webp"
    alt="Figura: Editor Skeletal Mesh."
    caption="Figura: Permite a manipulação de cada osso do esqueleto e acesso aos objetos associados ao esqueleto."
%}

Observe que o editor é divido em :

- `Skeleton` - Estrutura de conexões representando os ossos;

- `Mesh` - Malha o objeto;

- `Animation` - Sequencia de animações que determina os movimentos do objeto;

- `Blueprint` - Lógica de programação para sequenciamento de animações;

- `Physcis` - Estruturas para representar a física do esqueleto.

## 5. Posição e coordenadas

Os objetos adicionados em uma cena possuem coordenadas de localização dentro do 'mundo', vamos apresentar como manipular coordenadas.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-viewport-coordinates.webp"
    alt="Figura: Coordenadas no ViewPort."
    caption="Figura: No campo inferior esquerdo são indicadas as posições x,y e z da cena. O objeto da cena apresenta o gizmo para indicar a sua posição na cena. No canto superior direito é possível alterar entre as coordenadas do mundo e do objeto."
%}

### 5.1. Transform

A seção **Transform** do painel Detalhes permite que você visualize e edite as transformações - Localização, Rotação e Escala - do (s) ator (es) selecionado (s). Além disso, quando aplicável, também contém as configurações para Mobilidade do Ator.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-viewport-transform.webp"
    alt="Figura: Transform - Valores de transformação do objeto."
    caption="Figura: Valores relativos à Localização (Location), Rotação (Rotation) e Escala ou dimensionamento (Scale)."
%}

### 5.2. Escrevendo na tela o posicionamento do ator no mundo

{% include imagelocal.html
    src="unreal/actor/unreal-engine-print-location.webp"
    alt="Figura: Blueprint - Escreve na tela as coordenadas de localização do objeto."
    caption="Figura: Ao iniciar, BeginPlay, as funções GetActorLocation e GetWorldLocation são executadas."
%}

- `GetActorLocation` - Retorna um vetor contendo as coordenadas X,Y e Z da posição do ator no mundo. Utiliza o componente `RootComponent` para determinar os valores;

- `GetwordLocarion` - Retorna um vetor de coordenadas da posição do componente no mundo.

### 5.3. Posição relativa no mundo

Os elementos associados a um ator, como por exemplo `StaticMesh` tem posições relativas ao objeto ao qual estão associados.  

Considere o exemplo abaixo do objeto **BP_ActorBase**:

```bash
└── BP_ActorBase
    └── DefaultSceneRoot
        └── StaticMesh
```

{% include imagelocal.html
    src="unreal/actor/unreal-engine-sceneroot.webp"
    alt="Figura: SceneRoot."
    caption="Figura: A malha (Mesh) está hierarquia abaixo do componente, então, as coordenadas são relativas, por exemplo: X=0,Y=0,Z=0."
%}

O objeto BP_ActorBase possui um componente `DefaultSceneRoot`.

A posição do ator no mundo é calculada utilizando o componente `DefaultSceneRoot` do tipo `Scene`. O componente `StaticMesh` tem um vetor de coordenadas relativas ao objeto de hierarquia superior, sendo X=0,Y=0 e Z=0.

A posição do ator no mundo é calculada utilizando o componente `DefaultSceneRoot` do tipo `Scene`. O componente `StaticMesh` tem um vetor de coordenadas relativas ao objeto de hierarquia superior, sendo X=0,Y=0 e Z=0.

### 5.4. Escrevendo na tela o posição relativa do componente

{% include imagelocal.html
    src="unreal/actor/unreal-engine-print-relative-location.webp"
    alt="Figura: Get Target Relative Location."
    caption="Figura: Retorna um vetor com as coordenadas da malha relativas ao sceneroot."
%}

{% include iframe.html
    src="https://blueprintue.com/render/xy8gbnli/"
    title="Cafegeek - Escreve na tela as coordenadas de localização do objeto"
    caption="Figura: Ao iniciar, BeginPlay, as funções GetActorLocation e GetWorldLocation são executadas."
    ref="https://blueprintue.com/render/xy8gbnli/"
%}

## 6. Manipulando Actors

Podemos adicionar, remover ou selecionar os atores que estão na cena do jogo, a seguir vamos implementar e entender esses comandos.

### 6.1. Spawn e Destroy Actors - Criando e destruindo um Actor

O processo de criação de uma nova instância de um ator é conhecido como *spawning*. A geração de atores é realizada usando a função `SpawnActor`. Esta função cria uma nova instância de uma classe especificada e retorna um ponteiro para o Actor recém-criado. `SpawnActor` só pode ser usado para criar instâncias de classes que herdam da classe Actor em sua hierarquia.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-actor-spawn.webp"
    alt="Figura: Exemplo de SpawnActor e DestroyActor."
    caption="Figura: Cria o ator na posição do objeto TargetPoint e se ele já está na cena o destrói."
%}

Utilizando o `Level Bluprint` podemos implementar o código acima.

1. Ao pressionar a tecla **B** o ator e criado na cena utilizando as coordenadas de um componente `targetPoint` adicionando na cena;

1. O comando `flip/flop` é utilizado para intercalar entre criar e destruir o ator, com os métodos `SpawnActor` e `DestroyActor` respectivamente;

1. Usamos `IsValid` para verificar se o ator existe na cena.

### 6.2. Listando Actors por classe

Utilizando a função `GetAllActorOfClass` e o loop `For Each Loop` podemos listar todos os atores na cena.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-get-all-ActorOfClass.webp"
    alt="Figura: GetAllActorOfClass."
    caption="Figura: Lista todos os objetos instanciados da classe BP_ActorBase e os destrói."
%}

{% include iframe.html
    src="https://blueprintue.com/render/xugypke9/"
    title="Cafegeek - Criando e destruindo objetos"
    caption="Blueprintue: Criando, destruindo e listando objetos na cena."
    ref="https://blueprintue.com/render/xugypke9/"
%}
