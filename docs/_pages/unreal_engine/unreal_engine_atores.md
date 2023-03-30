---
title: Atores
excerpt: Neste capitulo serão apresentados e implementados os atores Actors do seu projetos.
permalink: /pages/unreal_engine/atores
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true  
---

## 1. O que são Actors?

Um ator é qualquer objeto que pode ser colocado em um nível, é uma classe de básica de objetos do **Unreal Engine**, neste capitulo serão apresentados e implementados os atores *Actors* do seu projeto.

**Actors** ou Atores são uma classe genérica que oferece suporte a transformações 3D, como translação, rotação e escala. Atores podem ser criados (gerados) e destruídos por meio de código de jogo (**C++**  ou **Blueprints**). Em **C ++**, **AActor** é a classe base de todos os atores.

É composto por Atributos, componentes, eventos e permitem Herança.

Para entender melhor devemos conceituar e entender o que são classes.

***

## 2. O que são Classes?

Classes são estruturas de dados que constituem a programação orientada a objetos. Contém seus próprios membros de dados e funções e podem ser acessados e usados criando uma instância de classe.

Classes determinam como os objetos serão quando criados.

Um objeto é uma instância de uma classe. Quando uma classe é definida, nenhuma memória é alocada, mas quando ela é instanciada (ou seja, um objeto é criado), a memória é alocada.

Abaixo vamos apresentar a estrutura hierarquia de classes.

```bash
|-- UObject C++
    |-- Actor C++
    |   |-- Pawn
    |   |   |-- Character
    |   |-- GameMode
    |   |-- GameController
    |   |   |-- PlayerController
    |   |   |-- IAController
|-- UObject C++
    |-- Actor BP
    |   |-- Pawn BP
    |   |   |-- Character BP
    |-- GameController BP
```

### 2.1. Exemplo de implementação utilizando C++

```cpp
class Hero
{
    int iLife=100;

    void SendMessage()
    {
        std::cout << "Message in a Bottle";
    }
};
```

### 2.2. Exemplo de implementação em Blueprint

Em **Blueprint** podemos obter os seguintes grupos de classes de atores:

- Actor;

- Pawn ;

- Character;

### 2.3. Utilizando classes com Blueprint

Como citado anteriormente classes são estruturas de dados com eventos, variáveis e componentes.

Para criar uma classe utilizando **Blueprint** acesse o menu de contexto e selecione `Blueprint Class`.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_pick_class.webp"
    alt="Figura: Pick Parent Class."
    caption="Permite selecionar uma classe predefinida para implementação de um nova classe."
%}

***

## 3. Classe Actor

A classe **Actor** compreende objetos básicos que podem ser adicionados ao mundo. Atores podem conter coleções de componentes, os quais podem ser usados para controlar como o ator se move, como é renderizado, etc. Atores suportam transformações 3D tal como translação, rotação e escala.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_class_actor_details.webp"
    alt="Figura: Actor > Class Defaults."
    caption="Valores iniciais da classe."
%}

- `Parent Class` : Classe pai de Actor (Classe **C++**).

***

## 4. Classe Pawn

A classe **Pawn** ou peão é a classe base de todos os atores que podem ser controlados por jogadores ou IA. Um peão é a representação física de um jogador ou entidade de IA dentro do mundo. Isso não significa apenas que o peão determina a aparência visual do jogador ou entidade de IA, mas também como ele interage com o mundo em termos de colisões e outros aspectos físicos

>Isso pode ser confuso em certas circunstâncias, pois alguns tipos de jogos podem não ter uma malha de jogador ou avatar visível dentro do jogo. Independentemente disso, o peão, *pawn*, ainda representa a localização física, rotação, etc. de um jogador ou entidade dentro do jogo. Um personagem é um tipo especial de peão que tem a capacidade de andar.  

`Default Pawn`  

Enquanto a classe *Pawn* fornece apenas o essencial para a criação de uma representação física de um jogador ou entidade de IA no mundo, a subclasse `DefaultPawn` vem com alguns componentes e funcionalidades adicionais.

A classe `DefaultPawn` contém um componente `DefaultPawnMovementComponent` nativo, um `CollisionComponent` esférico e um `StaticMeshComponent`.

Para controlar o `DefaultPawnMovementComponent`, bem como a câmera, uma propriedade do tipo *Booleano* para adicionar ligações de movimento padrão também está presente na classe `DefaultPawn` e é definido como verdadeiro por padrão.

`Spectator Pawn`  

A classe `SpectatorPawn` é uma subclasse de `DefaultPawn`. Por meio de um **GameMode**, diferentes classes podem ser especificadas como padrões para *Pawn* e `SpectatorPawn`, e esta classe fornece uma estrutura simples ideal para a funcionalidade de espectador.

As Classes tem propriedades que definem a estrutura do objeto.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_class_pawn_details.webp"
    alt="Figura: Pawm > Class Defaults."
    caption="Valores iniciais da classe."
%}

- `Start with Tick Enabled` - Habilita o evento Tick na lógica. Pode ser desabilitado para ganhar performance;

- `Use Controller Rotation Pitch/Yaw` - Pode usar movimentação dos controladores;

- `Auto Possess Player/AI` - Faz com o **PlayerController** possua automaticamente o peão (*Pawn*);

- `Replication` : Opções para replicar o objeto pela rede.

- `Can be Damaged` : Habilita os eventos de dano do objeto.

***

## 5. Classe Character

Um personagem é um *Pawn* que tem algumas funcionalidades básicas de movimento bípede por padrão.  
Com a adição de um componente `CharacterMovementComponent`, um `CapsuleComponent` e um `SkeletalMeshComponent`, a classe *Pawn* é estendida para a classe *Character* com muitos recursos. Um personagem é projetado para uma representação do jogador orientada verticalmente que pode andar, correr, pular, voar e nadar pelo mundo. Esta classe também contém implementações de rede básica e modelos de entrada.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_class_character_details.webp"
    alt="Figura: Character > Class Defaults."
    caption="Valores iniciais da classe."
%}

- `Animation Mode` - Habilita uma animação simples ou um **Blueprint** de animação ao objeto;

- `Anim Class` - Blueprint de animação associado.

- `Skeletal Mesh Asset` - Malha esquelética.

***

## 6. Componentes e Actors

Os componentes são um tipo especial de objeto que os atores podem anexar a si próprios como subobjetos. Os componentes são úteis para compartilhar comportamentos comuns, como a capacidade de exibir uma representação visual e reproduzir sons. Eles também podem representar conceitos específicos do projeto, como a maneira como um veículo interpreta a entrada e muda sua própria velocidade e orientação. Por exemplo, um projeto com carros, aeronaves e barcos controláveis pelo usuário pode implementar as diferenças no controle e movimento do veículo, alterando qual componente um ator do veículo usa.

### 6.1. Adicionando componentes

Na aba `Components`s podemos adicionar componentes para os objetos de forma hierarquia.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_add_component.webp"
    alt="Figura: Components > Add."
    caption="Adicionando componentes."
%}

{% include imagelocal.html
    src="unreal/actor/unreal_engine_add_component_hierarchy.webp"
    alt="Figura: Components."
    caption="Estrutura hierárquica dos componentes."
%}

Exemplo de Componentes que podemos adicionar a classe:  

- `Actor Child` - Componente associa outro ator a classe principal.

- `Static Mesh` - Adiciona um objeto de 3D;

- `Box Collsion` - Adiciona uma caixa de colisão;

Para editar os componentes utilizamos o Editor de objetos e componentes.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_component_details.webp"
    alt="Figura: Component > Details."
    caption="Podemos editar as propriedades dos componentes."
%}

### 6.2. Static Mesh - Malhas estáticas

**Static Mesh** são a unidade básica usada para criar a geometria do mundo para níveis (*level*) criados no **Unreal Engine**. A grande maioria de qualquer mapa em um jogo feito com **Unreal** consistirá em Malhas Estáticas, geralmente na forma de Atores de Malha Estática.

Consistem em um conjunto de polígonos que podem ser armazenados em cache na memória de vídeo e renderizados pela placa de vídeo. Isso permite que eles sejam renderizados com eficiência, o que significa que podem ser muito mais complexos do que outros tipos de geometria, como **Brushes**. Como são armazenados em cache na memória de vídeo, as malhas estáticas podem ser traduzidas, giradas e dimensionadas, mas não podem ter seus vértices animados de nenhuma forma.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_static_mesh_viewport.webp"
    alt="Figura: Statis Mesh ViewPort."
    caption="Podemos manipular as transformações da Static Mesh."
%}

#### 6.2.1. Propriedades do componente Static Mesh

- `Transform` - Propriedades de localização do componente;

- `Static Mesh` - Malha associada ao componente;

- `Material` - Material associado a malha;

- `Simulate Physcis` - Habilita a simulação de física do objeto.

**Editor de StaticMesh.**

Visualização da malha e suas propriedades (vértices, UV e modelo de colisão).

{% include imagelocal.html
    src="unreal/actor/unreal_engine_static_mesh_editor.webp"
    alt="Figura: Editor de StaticMesh."
    caption="O editor permite adicionar uma caixa de colisão e visualizar o mapeamento UV."
%}

### 6.3. Skeletal Mesh - Malha Esquelética

As **Skeletal mesh** são compostas por duas partes: Um conjunto de polígonos compostos para formar a superfície da Malha Esquelética e um conjunto hierárquico de ossos interconectados que podem ser usados para animar os vértices dos polígonos. **Skeletal mesh** são frequentemente usados no **Unreal Engine 4** para representar personagens ou outros objetos animados.

#### 6.3.1. A Estrutura da malha esquelética

A baixo uma representação da hierarquia do Skeletal Mesh.

```bash
|-- Ator
    |-- Skeletal mesh
    |   |-- Mesh - (Malha do elemento)
    |   |-- Animation - (Animações associadas ao esqueleto)
    |   |-- Skeleton - (Estrutura de coordenadas alinhadas para marcar os ossos dos elementos)
    |   |-- Blueprint - (Lógica para sequenciamento de animações)
    |   |-- Physics - (Estrutura para gerenciamento da física da estruturas)
    |-- Animation mode
    |   |-- Use Animation Blueprint
    |-- Anim Class
    |   |-- ThirdPerson_AnimBP_C
```

#### 6.3.2. Propriedades do Skeletal Mesh

{% include imagelocal.html
    src="unreal/actor/unreal_engine_skeletal_mesh.webp"
    alt="Figura: Mesh (Character Mesh)."
    caption="Aba Componentes > Lista de componentes predefinidos da classe Character, Details >  Propriedades do componente."
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

#### 6.3.3. O Editor Skeletal Mesh

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_skeleton_mannequim.webp"
    alt="Figura: Editor Skeletal Mesh."
    caption="Permite a manipulação de cada osso do esqueleto e acesso aos objetos associados ao esqueleto."
%}

Observe que o editor é divido em :

- `Skeleton` - Estrutura de conexões representando os ossos;

- `Mesh` - Malha o objeto;

- `Animation` - Sequencia de animações que determina os movimentos do objeto;

- `Blueprint` - Lógica de programação para sequenciamento de animações;

- `Physcis` - Estruturas para representar a física do esqueleto.

***

## 7. Posição e coordenadas

Os objetos adicionados em uma cena possuem coordenadas de localização dentro do 'mundo', vamos apresentar como manipular coordenadas.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_viewport_coordinates.webp"
    alt="Figura: Coordenadas no ViewPort."
    caption="No campo inferior esquerdo são indicadas as posições x,y e z da cena. O objeto da cena apresenta o gizmo para indicar a sua posição na cena. No canto superior direito é possível alterar entre as coordenadas do mundo e do objeto."
%}

### 7.1. Transform

A seção **Transform** do painel Detalhes permite que você visualize e edite as transformações - Localização, Rotação e Escala - do (s) ator (es) selecionado (s). Além disso, quando aplicável, também contém as configurações para Mobilidade do Ator.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_viewport_transform.webp"
    alt="Figura: Transform - Valores de transformação do objeto."
    caption="Valores relativos à Localização (Location), Rotação (Rotation) e Escala ou dimensionamento (Scale)."
%}

### 7.2. Escrevendo na tela o posicionamento do ator no mundo

{% include imagelocal.html
    src="unreal/actor/unreal_engine_print_location.webp"
    alt="Figura: Blueprint - Escreve na tela as coordenadas de localização do objeto."
    caption="Ao iniciar, BeginPlay, as funções GetActorLocation e GetWorldLocation são executadas."
%}

- `GetActorLocation` - Retorna um vetor contendo as coordenadas X,Y e Z da posição do ator no mundo. Utiliza o componente `RootComponent` para determinar os valores;

- `GetwordLocarion` - Retorna um vetor de coordenadas da posição do componente no mundo.

### 7.3. Posição relativa no mundo

Os elementos associados a um ator, como por exemplo `StaticMesh` tem posições relativas ao objeto ao qual estão associados.  

Considere o exemplo abaixo do objeto **BP_ActorBase**:

```bash
|-- BP_ActorBase
    |-- DefaultSceneRoot
    |   |-- StaticMesh
```

{% include imagelocal.html
    src="unreal/actor/unreal_engine_sceneroot.webp"
    alt="Figura: SceneRoot."
    caption="A malha (Mesh) está hierarquia abaixo do componente, então, as coordenadas são relativas, por exemplo: X=0,Y=0,Z=0."
%}

O objeto BP_ActorBase possui um componente `DefaultSceneRoot`.

A posição do ator no mundo é calculada utilizando o componente `DefaultSceneRoot` do tipo `Scene`. O componente `StaticMesh` tem um vetor de coordenadas relativas ao objeto de hierarquia superior, sendo X=0,Y=0 e Z=0.

A posição do ator no mundo é calculada utilizando o componente `DefaultSceneRoot` do tipo `Scene`. O componente `StaticMesh` tem um vetor de coordenadas relativas ao objeto de hierarquia superior, sendo X=0,Y=0 e Z=0.

### 7.4. Escrevendo na tela o posição relativa do componente

{% include imagelocal.html
    src="unreal/actor/unreal_engine_print_relative_location.webp"
    alt="Figura: Get Target Relative Location."
    caption="Retorna um vetor com as coordenadas da malha relativas ao sceneroot."
%}

{% include iframe.html
    src="https://blueprintue.com/render/xy8gbnli/"
    title="Cafegeek - Escreve na tela as coordenadas de localização do objeto"
    caption="Ao iniciar, BeginPlay, as funções GetActorLocation e GetWorldLocation são executadas."
    ref="https://blueprintue.com/render/xy8gbnli/"
%}

***

## 8. Trabalhando herança com Blueprint

Como apresentado no conceito de classes, a herança permite usar classes já definidas para derivar novas classes, a seguir vamos verificar como implementar utilizando **Blueprint**.  

Exemplo de classe Herói que derive de Humanos:  

```bash
|-- Character
    |-- BeginPlay()
    |-- Humanos
    |   |-- Vida (float) = 100    
    |   |-- Dano (float) = 100        
    |   |-- BeginPlay() (herdado)
    |   |-- Heroi
    |   |   |-- Vida = 100 (herdado)
    |   |   |-- Dano = 50 (herdado)
    |   |-- Vilao
    |   |   |-- Vida = 100 (herdado)
    |   |   |-- Dano = 80 (herdado)    
```

### 8.1. Criando uma classe filho

{% include imagelocal.html
    src="unreal/actor/unreal_engine_create_child_class.webp"
    alt="Figura: Create Child Blueprint Class."
    caption="Selecionando o objeto pai e acionamento o menu de contexto (RMB) acessamos a opção para criar a classe derivada."
%}

### 8.2. Variáveis da classe pai

{% include imagelocal.html
    src="unreal/actor/unreal_engine_show_my_blueprints.webp"
    alt="Figura: MyBlueprint propriedades."
    caption="Podemos exibir as variáveis, componentes ou eventos da herdados da classe pai, no exemplo acima a variável NameBase pertence a classe pai."
%}

### 8.3. Herança de propriedades e métodos

É possível sobrescrever os métodos da classe pai para adicionar uma nova lógica, vamos aos passos.

Criando um evento para sobrescrever o evento `Begin Play`.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_functions_overrider.webp"
    alt="Figura: Functions Override."
    caption="Podemos sobrescrever os métodos da classe pai."
%}

### 8.4. Executando um evento da classe pai

{% include imagelocal.html
    src="unreal/actor/unreal_engine_beginplay_override.webp"
    alt="Figura: Parent: Begin Play."
    caption="Clicando com o botão direito (RMB) acessamos a opção Add Call to Parent Function que executa a classe pai antes de executar o próximo comando."
%}

### 8.5. Componente ChildActor

O componente `ChildActor` permite associar uma classe filha utilizando a lista de componentes.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_childActor.webp"
    alt="Figura: ChildActor."
    caption="O componente ChildActor associa uma outra classe ao objeto."
%}

- `ChildActor` - É necessário informar a classe filho neste componente.

### 8.6. Referências de atores e componentes

{% include imagelocal.html
    src="unreal/actor/unreal_engine_view_references.webp"
    alt="Figura: Reference Viewer."
    caption="Clicando com o botão direito (RMB) podemos acessar a opção para visualizar todas as referências do objeto. No exemplo acima BP_ActorChild2 é uma classe derivada do BP_ActorBase e BP_ActorChild está associada usando o componente ChildActor."
%}

***

## 9. Manipulando Actors

Podemos adicionar, remover ou selecionar os atores que estão na cena do jogo, a seguir vamos implementar e entender esses comandos.

### 9.1. Spawn e Destroy Actors - Criando e destruindo um Actor

O processo de criação de uma nova instância de um ator é conhecido como *spawning*. A geração de atores é realizada usando a função `SpawnActor`. Esta função cria uma nova instância de uma classe especificada e retorna um ponteiro para o Actor recém-criado. `SpawnActor` só pode ser usado para criar instâncias de classes que herdam da classe Actor em sua hierarquia.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_actor_spawn.webp"
    alt="Figura: Exemplo de SpawnActor e DestroyActor."
    caption="Cria o ator na posição do objeto TargetPoint e se ele já está na cena o destrói."
%}

Utilizando o `Level Bluprint` podemos implementar o código acima.

1. Ao pressionar a tecla **B** o ator e criado na cena utilizando as coordenadas de um componente `targetPoint` adicionando na cena;

1. O comando `flip/flop` é utilizado para intercalar entre criar e destruir o ator, com os métodos `SpawnActor` e `DestroyActor` respectivamente;

1. Usamos `IsValid` para verificar se o ator existe na cena.

### 9.2. Listando Actors por classe

Utilizando a função `GetAllActorOfClass` e o loop `For Each Loop` podemos listar todos os atores na cena.

{% include imagelocal.html
    src="unreal/actor/unreal_engine_get_all_ActorOfClass.webp"
    alt="Figura: GetAllActorOfClass."
    caption="Lista todos os objetos instanciados da classe BP_ActorBase e os destrói."
%}

{% include iframe.html
    src="https://blueprintue.com/render/xugypke9/"
    title="Cafegeek - Criando e destruindo objetos"
    caption="Criando, destruindo e listando objetos na cena."
    ref="https://blueprintue.com/render/xugypke9/"
%}

***

## 10. Colisões

**Collision Responses** e **Trace Responses** formam a base de como o Unreal Engine 4 lida com colisão e transmissão de raios durante o tempo de execução. Cada objeto que pode colidir recebe um tipo de objeto e uma série de respostas que definem como ele interage com todos os outros tipos de objeto. Quando ocorre um evento de colisão ou sobreposição, ambos (ou todos) os objetos envolvidos podem ser configurados para afetar ou serem afetados pelo bloqueio, sobreposição ou ignorando um ao outro. [Collision Overview](https://docs.unrealengine.com/4.27/en-US/InteractiveExperiences/Physics/Collision/Overview/)

**Trace Responses** funcionam basicamente da mesma maneira, exceto que o próprio rastreamento (*ray cast*) pode ser definido como um dos tipos de resposta de rastreamento, permitindo assim que os atores o bloqueiem ou ignorem com base em suas respostas de rastreamento.

### 10.1. Interações

Existem algumas regras a serem lembradas sobre como as colisões são tratadas:

- O bloqueio ocorrerá naturalmente entre dois (ou mais) Atores definidos como **Block** (Bloquear). No entanto, `Simulation Generates Hit Events` precisa ser habilitado para executar `Event Hit`, que é usado em Blueprints, `Destructible Actors`, `Triggers`, etc...

- Definir Atores para **Overlap** (Sobrepor) muitas vezes parecerá que eles ignoram uns aos outros e, sem Gerar Eventos de Sobreposição, eles são essencialmente os mesmos.

- Para que dois ou mais objetos de simulação bloqueiem um ao outro, ambos precisam ser configurados para bloquear seus respectivos tipos de objeto.

- Para dois ou mais objetos de simulação: se um for configurado para sobrepor um objeto e o segundo objeto for configurado para bloquear o outro, a sobreposição ocorrerá, mas não o bloqueio.

- Eventos de sobreposição, **Overlap**, podem ser gerados mesmo que um objeto Bloqueie outro, especialmente se estiver viajando em alta velocidade.

- Não é recomendado que um objeto tenha eventos de colisão e sobreposição. Embora seja possível, é necessário  manuseio manual.

- Se um objeto for configurado para ignorar e o outro for configurado para sobrepor, nenhum evento de sobreposição será disparado.

### 10.2. Exemplos comuns de interação de colisão

>As interações a seguir pressupõem que todos os objetos tenham `Collision Enabled` definido como `Collision Enabled`, de modo que estejam configurados para colidir totalmente com tudo. Se a colisão estiver desabilitada, é como se ignorar tivesse sido definido para todas as `Collision Responses` .

Para a seção a seguir, abaixo a configuração usada para explicar o que está acontecendo:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_setup.png"
    alt="Figura: Exemplo de colisão."
    caption="A esfera é um PhysicsBody e a caixa é WorldDynamic, e alterando suas configurações de colisão podemos obter uma série de comportamentos."
    ref="https://docs.unrealengine.com/4.27/en-US/InteractiveExperiences/Physics/Collision/Overview/"
%}

#### 10.2.1. Colisão

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent.png"
    alt="Figura: Collision Overview."
    caption="Ao definir ambas as configurações de colisão para bloquear uma à outra, você obtém uma colisão, ótima para que os objetos interajam entre si."
%}

Configuração de colisão de esfera.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Sphere.png"
    alt="Figura: Configuração de colisão de esfera."
    caption="Neste caso, a esfera é um PhysicsBody e está configurada para bloquear WorldDynamic (que é o que é a parede)."
%}

Configuração de colisão de parede.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Configuração de colisão de parede."
    caption="A parede é uma WorldDynamic e está configurada para bloquear os Atores PhysicsBody (que é o que a esfera é)."
%}

Nesse caso, a esfera e a parede simplesmente colidirão; nenhuma outra notificação da colisão ocorrerá.

#### 10.2.2. Colisão e Simulação Geram Eventos de acerto

Apenas a colisão é útil e, em geral, o mínimo para interações físicas, mas se você quiser que algo relate, ele colidiu para que um **Blueprint** ou seção de código possa ser acionado:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideEvent.png"
    alt="Figura: Colisão de eventos."
    caption="Eventos de colisão."
%}

Configuração de colisão de esfera:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideEvent_Sphere.png"
    alt="Figura: Configuração de Colisão de uma esfera."
    caption="Parâmetros da colisão."
%}

Como no exemplo acima, a esfera é um `PhysicsBody` e está configurada para bloquear `WorldDynamic` (que é o que é a parede). No entanto, a esfera também habilitou `Simulation Generates Hit Event` para que acione um evento para si mesma sempre que colidir com algo.

Configuração de colisão de parede:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Configuração de Colisão da Parede."
    caption="Parâmetros da colisão."
%}

A parede é uma `WorldDynamic` e está configurada para bloquear os Atores `PhysicsBody` (que é o que a esfera é). Como a parede não está configurada para `Simulation Generates Hit Event` , ela não gerará um evento para si mesma.

Com a esfera definida como Simulação gera eventos de acerto, a esfera informará a si mesma que sofreu uma colisão. Ele irá disparar eventos como `ReceiveHit` ou `OnComponentHit` no **Blueprint** da esfera. Agora, se a caixa tivesse um evento de colisão, ela não dispararia porque nunca notificará a si mesma que aconteceu.

Além disso, um objeto que está relatando colisões rígidas relatará todas elas e relatórios de spam quando estiver apenas parado em algo, portanto, é melhor ter cuidado ao filtrar o que está colidindo em seu **Blueprint** ou no código.

### 10.3. Sobrepor e ignorar

Para todos os efeitos, *Overlap* (Sobrepor) e *Ignore* (Ignorar) funcionam exatamente da mesma forma, supondo que Gerar eventos de sobreposição esteja desativado. Nesse caso, a esfera está configurada para sobrepor ou ignorar a caixa:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_ignore.png"
    alt="Figura: Overlap and Ignore."
    caption="Sobrepor ou ignorar."
%}

Configuração das propriedades de colisão de esfera:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_OverlapNoEvent_Sphere.png"
    alt="Figura: Configuração de Colisão da  esfera."
    caption="Parâmetros da colisão."
%}

Aqui a esfera está configurada para se sobrepor,`Overlap`, aos `WorldDynamic Actors` (como nossa parede), mas não tem a opção Gerar Eventos de Sobreposição habilitado. No que diz respeito à esfera, ela não colidiu ou se sobrepôs a nada, efetivamente ignorou a parede.

Configuração das propriedades colisão de parede:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Configuração de colisão de parede."
    caption="Parâmetros da colisão."
%}

A parede é uma `WorldDynamic` e está configurada para bloquear,`Block`, os Atores `PhysicsBody` (que é o que a esfera é). Como dito acima, ambos os Atores precisam ser configurados para bloquear os respectivos tipos de objetos um do outro. Se não o fizerem, não colidirão.

Ou:

### 10.4. Configuração das propriedades da colisão de esfera

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_ignore_sphere.png"
    alt="Figura: Collide ignore Sphere."
    caption="Figura: Collide ignore Sphere."
%}

Aqui a esfera está configurada para ignorar, `Ignore`, os Atores `WorldDynamic` (como nossa parede), e ela passará pela parede.

Configuração das propriedades de colisão de parede:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Collide No Event."
    caption="Parâmetros da colisão."
%}

A parede é uma `WorldDynamic` e está configurada para bloquear os Atores `PhysicsBody` (que é o que a esfera é). Como dito acima, ambos os Atores precisam ser configurados para bloquear, `Block`, os respectivos tipos de objetos um do outro. Se não o fizerem, não colidirão.

### 10.5. Sobrepor e gerar eventos de sobreposição

Ao contrário das colisões que podem disparar todos os quadros, os eventos de sobreposição são `ReceiveBeginOverlap` e `ReceiveEndOverlap`, que são disparados apenas nesses casos específicos.

> Para que uma sobreposição ocorra, ambos os Atores precisam habilitar Gerar Eventos de Sobreposição. Isso é para desempenho. No caso em que tanto a Esfera quanto a Caixa desejam sobreposições quando movemos a Esfera ou a Caixa, fazemos uma consulta de sobreposição para ver se precisamos disparar algum evento.
>
>Se a caixa não quiser sobreposições, quando ela se mover, não faremos uma consulta de sobreposição. Mas agora poderíamos estar sobrepondo com a Esfera, e assim a Esfera precisaria marcar e verificar se há sobreposições em cada quadro caso alguém se movesse para eles.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_overlapEvent.png"
    alt="Figura: Evento overlap."
    caption="Evento de sobreposição."
%}

### 10.6. Colisão de esfera

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_OverlapEvent_Sphere.png"
    alt="Figura: Colisão da esfera."
    caption="Parâmetros da colisão."
%}

Aqui, a esfera está configurada para sobrepor, `Overlap`, os Atores `WorldDynamic` (como nossa parede), e ela gerará um evento para si mesma quando se sobrepuser a algo.

### 10.7. Colisão de parede

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideOverLapEvent_Box.png"
    alt="Figura: Evento overlap no box."
    caption="Parâmetros da colisão."
%}

A parede é uma WorldDynamic e está configurada para bloquear, `Block`, os Atores `PhysicsBody` (que é o que a esfera é). Como dito acima, ambos os Atores precisam ser configurados para bloquear os respectivos tipos de objetos um do outro. Se não o fizerem, não colidirão. Mas, uma sobreposição ocorre aqui, e os eventos para a esfera e a caixa são disparados.

### 10.8. Colisão Simples versus Complexa

No **Unreal Engine**, você tem acesso a formas de colisão simples e complexas. Colisão Simples, `Simplex Collision`, são primitivos como cubos, esferas, cápsulas e cascos convexos. Colisão Complexa, `Complex Collsion`, é o `trimesh` de um determinado objeto. Por padrão, o **Unreal Engine** cria formas simples e complexas, então, com base no que o usuário deseja (consulta complexa versus consulta simples), o solucionador de física usará a forma correspondente para consultas de cena e testes de colisão. [Simple versus Complex Collision](https://docs.unrealengine.com/5.1/en-US/simple-versus-complex-collision-in-unreal-engine/)

### 10.9. Static Mesh e colisões

No painel `Static Mesh Editor > Details`, você pode encontrar as configurações de `Complex Collision` na categoria `Collision`.

{% include image.html
    src="https://docs.unrealengine.com/5.0/Images/making-interactive-experiences/Physics/collision/simple-vs-complex/StaticMeshSettingsCollisionComplexity.webp"
    alt="Figura: Staticmesh Settings Collision Complexity."
    caption="Configurando a colisão da Static Mesh."
%}

- `Project Default` :  Usa as configurações físicas do projeto, isso fará com que solicitações de colisão simples usem colisão simples e solicitações complexas usem colisão complexa; o comportamento "padrão".

- `Simple and Complex`:  Esse sinalizador permite a criação de formas simples e complexas, usando formas simples para consultas de cena regulares e testes de colisão e usando formas complexas (por poli) para consultas de cena complexas.

- `Use Simple Collision As Complex`:  Isso significa que, se uma consulta complexa for solicitada, o mecanismo ainda consultará formas simples; basicamente ignorando o trimesh. Isso ajuda a economizar memória, pois não precisamos preparar o trimesh e pode melhorar o desempenho se a geometria de colisão for mais simples.

- `Use Complex Collision As Simple`:  Isso significa que, se uma consulta simples for solicitada, o mecanismo consultará formas complexas; basicamente ignorando a simples colisão. Isso nos permite usar o trimesh para a colisão de simulação de física. Observe que, se você estiver usando `UseComplexAsSimple`, não poderá simular o objeto, mas poderá usá-lo para colidir com outros objetos simulados (simples).

Por exemplo, na imagem abaixo a cadeira à esquerda tem colisão simples, e quando o peão acima dela cai sobre ela, ele desliza para fora da grande superfície angulada que cobre o assento. No entanto; a cadeira à direita está usando `Use Complex Collision As Simple`, e quando o peão acima dele cair, ele pousará no assento da cadeira e permanecerá lá.

{% include image.html
    src="https://docs.unrealengine.com/5.0/Images/making-interactive-experiences/Physics/collision/simple-vs-complex/exImage.webp"
    alt="Figura: Simple vs Complex."
    caption="Comparando os tipos de colisão."
%}
