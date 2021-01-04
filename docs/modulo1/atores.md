[Home](https://myerco.github.io/unreal-engine) / [Unreal](https://myerco.github.io/unreal-engine/unreal.html)

# Atores
Neste capitulo serão apresentados e implementados os atores *Actors* do seu
projeto.

## Índice
>1. [Conceituando atores](#1)
>   1. [Classes](#11)
>   1. [Hierarquia](#12)
>   1. [Implementação](#13)
> 1. [Classes Bluprint](#2)
>   1. [Actor](#21)
>   1. [Pawn](#22)
>   1. [Character](#23)
> 1. [Componentes](#3)
>   1. [Adicionando componentes](#31)
>   1. [Editor de objetos e componentes](#32)
> 1. [Static Mesh - Malhas estáticas](#4)
>   1. [Componente StaticMesh](#41)
>   1. [Propriedades do componente](#42)
>   1. [Editor de StaticMesh](#43)
> 1. [Skeletal Mesh - Malha Esquelética](#5)
>   1. [Estrutura](#51)
>   1. [Componentes](#52)
>   1. [Detalhes](#53)
>   1. [Editor](#52)
> 1. [Posição e coordenadas](#6)
>   1. [Coordenadas no ViewPort](#61)
>   1. [Transform](#62)
>   1. [Escrevendo na tela o posicionamento do ator no mundo](#63)
>   1. [Posição relativa no mundo](#64)
>   1. [Escrevendo na tela o posição relativa do componente](#64)
> 1. [Herança](#7)
>   1. [Componente ChildActor implementa a ligação com outro ator](#71)
>   1. [Herança de propriedades e métodos](#72)
>   1. [Referências de atores e componentes](#73)
> 1. [Manipulando atores](#8)
>   1. [Listando atores por classe](#81)
>   1. [Listando atores utilizando tag (etiquetas)](#81)
> 1. [Colisões](#9)

<a name="1"></a>
## 1. Conceituando atores
Um ator é qualquer objeto que pode ser colocado em um nível. Atores são uma classe genérica que oferece suporte a transformações 3D, como translação, rotação e escala. Atores podem ser criados (gerados) e destruídos por meio de código de jogo (C ++ ou Blueprints). Em C ++, AActor é a classe base de todos os atores.  
É composto por Atributos, componentes  e eventos.   
Permitem Herança.

<a name="11"></a>
### 1.1 Classes
Classes são estruturas de dados que constituem a programação orientada a objetos. Contém seus próprios membros de dados e funções e podem ser acessados e usados criando uma instância de classe.   
Classes determinam como os objetos serão quando criados.   
Um objeto é uma instância de uma classe. Quando uma classe é definida, nenhuma memória é alocada, mas quando ela é instanciada (ou seja, um objeto é criado), a memória é alocada.   

<a name="12"></a>
### 1.2 Hierarquia
```
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

<a name="13"></a>
### 1.3 Implementação
**C++**  
```cpp
class MyClass
{
    int MyInt;

    void MyFunction()
    {
        // do stuff
    }
};
```

**Blueprint**   
Em Blueprint podem obter as seguintes grupo de classes de atores:
- Actor
- Pawn  
- Character

<a name="2"></a>
## 2. Blueprint Classes
Como citado anteriormente classes são estruturas de dados com eventos, variáveis e componentes.   
![Classes de atores](../imagens/actor/actor1.png)

<a name="21"></a>
### 2.1 Actor
Objeto básico que pode ser adicionado a o mundo.  
![Classe Actor](../imagens/actor/actor2.png)  
- Parent Class : Actor (Classe C++)

<a name="22"></a>
### 2.2 Pawn
A classe **Pawn** é a classe base de todos os atores que podem ser controlados por jogadores ou IA. Um peão é a representação física de um jogador ou entidade de IA dentro do mundo. Isso não significa apenas que o peão determina a aparência visual do jogador ou entidade de IA, mas também como ele interage com o mundo em termos de colisões e outros aspectos físicos

    Isso pode ser confuso em certas circunstâncias, pois alguns tipos de jogos podem não ter uma malha de jogador ou avatar visível dentro do jogo. Independentemente disso, o peão ainda representa a localização física, rotação, etc. de um jogador ou entidade dentro do jogo. Um personagem é um tipo especial de peão que tem a capacidade de andar.  
**Default Pawn**  
Enquanto a classe Pawn fornece apenas o essencial para a criação de uma representação física de um jogador ou entidade de IA no mundo, a subclasse DefaultPawn vem com alguns componentes e funcionalidades adicionais.

A classe DefaultPawn contém um DefaultPawnMovementComponent nativo, um CollisionComponent esférico e um StaticMeshComponent. Para controlar o DefaultPawnMovementComponent, bem como a câmera, um Booleano para adicionar ligações de movimento padrão também está presente na classe DefaultPawn e é definido como verdadeiro por padrão.

**Spectator Pawn**  
A classe SpectatorPawn é uma subclasse de DefaultPawn. Por meio de um GameMode, diferentes classes podem ser especificadas como padrões para Pawn e SpectatorPawn, e esta classe fornece uma estrutura simples ideal para a funcionalidade de espectador.

<a name="221"></a>
#### 2.2.1 Propriedades
![Classe Actor](../imagens/actor/actor51.png)
- Start with Tick Enabled: Habilita o evento Tick na lógica. Pode ser desabilitado para ganhar performance.
- Use Controller Rotation Pitch/Yaw : Pode usar movimentação dos controladores.
- Auto Possess Player/AI : Faz com o PlayerController possua automaticamente o peão (Pawn)
- Replication : Opções para replicar o objeto pela rede.  
![Classe Actor](../imagens/actor/actor52.png)  
- Can be Damaged : Habilita os eventos de dano do objeto.

<a name="23"></a>
### 2.3 Character
Um personagem é um peão que tem algumas funcionalidades básicas de movimento bípede por padrão.  
Com a adição de um CharacterMovementComponent, um CapsuleComponent e um SkeletalMeshComponent, a classe Pawn é estendida para a classe Character com muitos recursos. Um personagem é projetado para uma representação do jogador orientada verticalmente que pode andar, correr, pular, voar e nadar pelo mundo. Esta classe também contém implementações de rede básica e modelos de entrada.   
![Editor](../imagens/actor/actor53.png)
- **Animation Mode** - Habilita uma animação simples ou um Bluprint de animação ao objeto.
- **Anim Class** - Blueprint de animação associado.

<a name="3"></a>
### 3. Componentes
Os componentes são um tipo especial de objeto que os atores podem anexar a si próprios como subobjetos. Os componentes são úteis para compartilhar comportamentos comuns, como a capacidade de exibir uma representação visual e reproduzir sons. Eles também podem representar conceitos específicos do projeto, como a maneira como um veículo interpreta a entrada e muda sua própria velocidade e orientação. Por exemplo, um projeto com carros, aeronaves e barcos controláveis pelo usuário pode implementar as diferenças no controle e movimento do veículo, alterando qual componente um ator do veículo usa.    

<a name="31"></a>
### 3.1 Adicionando componentes
![Classes de atores](../imagens/movimentacao/movimentacao1.png)  
Exemplo de Componentes :  
- Actor Child: Componente associa outro ator a classe principal.
- Static Mesh : Adiciona um objeto de 3D
- Box Collsion: Adiciona uma caixa de colisão.

<a name="32"></a>
### 3.2 Editor de objetos e componentes.  
![Editor](../imagens/actor/actor3.png)  

<a name="4"></a>
## 4. Static Mesh - Malhas estáticas
**Static Mesh** são a unidade básica usada para criar a geometria do mundo para níveis (*level*) criados no Unreal Engine. A grande maioria de qualquer mapa em um jogo feito com Unreal consistirá em Malhas Estáticas, geralmente na forma de Atores de Malha Estática.

Consistem em um conjunto de polígonos que podem ser armazenados em cache na memória de vídeo e renderizados pela placa de vídeo. Isso permite que eles sejam renderizados com eficiência, o que significa que podem ser muito mais complexos do que outros tipos de geometria, como **Brushes**. Como são armazenados em cache na memória de vídeo, as malhas estáticas podem ser traduzidas, giradas e dimensionadas, mas não podem ter seus vértices animados de nenhuma forma.

![Classe Actor](../imagens/actor/actor54.png)  

<a name="41"></a>
### 4.1 Componente StaticMesh
![Classes de atores](../imagens/movimentacao/movimentacao2.png)  
- A aba **Components** apresenta uma lista hierarquia com os componentes associados ao objeto.

<a name="42"></a>
### 4.2 Propriedades do componente
![Classes de atores](../imagens/movimentacao/movimentacao3.png)  
- **Transform** - Propriedades de localização do componente.
- **Static Mesh** - Malha associada ao componente.
- **Material** - Material associado a malha.
- **Simulate Physcis** - Habilita a simulação de física do objeto.

<a name="43"></a>
### 4.3 Editor de StaticMesh
![Classes de atores](../imagens/movimentacao/movimentacao4.png)
- Visualização da malha e suas propriedades (vértices, UV e modelo de colisão).

<a name="5"></a>
## 5 Skeletal Mesh - Malha Esquelética
As **Skeletal mesh** são compostas por duas partes: Um conjunto de polígonos compostos para formar a superfície da Malha Esquelética e um conjunto hierárquico de ossos interconectados que podem ser usados para animar os vértices dos polígonos.   
**Skeletal mesh** são frequentemente usados no *Unreal Engine 4* para representar personagens ou outros objetos animados.

<a name="51"></a>
### 5.1 Estrutura
```
|-- Ator
    |-- Skeletal mesh
    |   |-- Mesh
    |   |-- Animation
    |   |-- Skeleton
    |   |-- Blueprint
    |   |-- Physics
    |-- Animation mode
    |   |-- Use Animation Bluprint
    |-- Anim Class
    |   |-- ThirdPerson_AnimBP_C
```
- **Mesh** - Malha do elemento
- **Animation** - Animações associadas ao esqueleto.
- **Skeleton** - Estrutura de coordenadas alinhadas para marcar os ossos dos elementos.
- **Bluprint** - Lógica para sequenciamento de animações.
- **Physics** - Estrutura para gerenciamento da física da estrutura.

<a name="52"></a>
### 5.2 Componentes
![Classes de atores](../imagens/movimentacao/movimentacao5.png)  
- **Mesh** - Malha Esquelética.
- **CameraBoom** - Objeto do tipo **SpringArm** (Braço) para controlar a câmera.
- **FollowCamera** - Objeto do tipo **Camera**.
- **CharacterMovement** - Componente responsável pela lógica de movimentos do objeto.

<a name="53"></a>
### 5.3 Detalhes do componente
![Classes de atores](../imagens/movimentacao/movimentacao6.png)  

<a name="54"></a>
### 5.4 Editor
![Classes de atores](../imagens/movimentacao/movimentacao7.png)
- **dadsa**

<a name="6"></a>
## 6. Posição e coordenadas
Os objetos adicionados em uma cena possuem coordenadas de localização dentro do 'mundo'.

<a name="61"></a>
### 6.1 Coordenadas no ViewPort
![Editor](../imagens/actor/actor48.png)  

<a name="62"></a>
### 6.2 Transform
A seção **Transform** do painel Detalhes permite que você visualize e edite as transformações - Localização, Rotação e Escala - do (s) ator (es) selecionado (s). Além disso, quando aplicável, também contém as configurações para Mobilidade do Ator.

![Editor](../imagens/actor/actor49.png)  

<a name="63"></a>
### 6.3 Escrevendo na tela o posicionamento do ator no mundo.  
![Posição](../imagens/actor/actor4.png)
- GetActorLocation - Retorna um vetor contendo as coordenadas X,Y e Z da posição do ator no mundo. Utiliza o componente **RootComponent** para determinar os valores.
- GetwordLocarion - Retorna um vetor de coordenadas da posição do componente no mundo.

<a name="64"></a>
### 6.4 Posição relativa no mundo  
Os elementos associados a um ator, como por exemplo **StaticMeshes** tem posições relativas ao objeto ao qual estão associados.  

Considere o exemplo abaixo
```
|-- BP_Ator
    |-- DefaultSceneRoot
    |   |-- StaticMesh
```
![Posição](../imagens/actor/actor50.png)

A posição do ator no mundo é calculada utilizando o componente **DefaultSceneRoot** do tipo **Scene**. O componente **StaticMesh** tem um vetor de coordenadas relativas ao objeto de hierarquia superior, sendo X=0,Y=0 e Z=0.

<a name="65"></a>
### 6.5 Escrevendo na tela o posição relativa do componente.
![Posição Relativa](../imagens/actor/actor5.png)

<a name="7"></a>
## 7. Herança
Herança permite usar classes já definidas para derivar novas classes.  
Exemplo:  
```
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
<a name="71"></a>
### 7.1 Componente *ChildActor* implementa a ligação com outro ator.  
![Componentes](../imagens/actor/actor6.png)

<a name="72"></a>
### 7.2 Herança de propriedades e métodos.  
![Herança](../imagens/actor/actor10.png)

<a name="73"></a>
### 7.3 Referências de atores e componentes.  
![Herança](../imagens/actor/actor11.png)

<a name="8"></a>
## 8. Manipulando atores

<a name="81"></a>
### 8.1 Criando e destruindo atores.  
O processo de criação de uma nova instância de um ator é conhecido como spawning. A geração de atores é realizada usando a função **SpawnActor**. Esta função cria uma nova instância de uma classe especificada e retorna um ponteiro para o Actor recém-criado.**SpawnActor** só pode ser usado para criar instâncias de classes que herdam da classe Actor em sua hierarquia.

![Herança](../imagens/actor/actor12.png)
- Utilizando o *Level Bluprint* podemos implementar o código acima.
- Ao pressionar a tecla **H** o ator e criado na cena utilizando as coordenadas de um componente **targetPoint** adicionando na cena.
- O comando **flip/flop** é utilizado para intercalar entre criar e destruir o ator, com os métodos **SpawnActor** e **DestroyActor** respectivamente.
- Usamos **IsValid** para verificar se o ator existe na cena.

<a name="82"></a>
### 8.2 Listando atores por classe
![Herança](../imagens/actor/actor13.png)

<a name="83"></a>
### 8.3 Listando atores utilizando *tag* (etiquetas)  
![Herança](../imagens/actor/actor14.png)

<a name="9"></a>
## 9. Colisões
- Simplex collision
- Complex collision  

***

## Referências
- [Game mode](https://docs.unrealengine.com/en-US/Gameplay/Framework/GameMode/index.html)  
- [Arms](https://docs.unrealengine.com/en-US/Gameplay/HowTo/UsingCameras/SpringArmComponents/index.html)  
- [Spawned no cliente](https://docs.unrealengine.com/en-US/Gameplay/HowTo/SpawnAndDestroyActors/Blueprints/index.html)  
- [Editor](https://docs.unrealengine.com/en-US/Engine/Content/Types/StaticMeshes/Editor/index.html)  
- [Static Mesh](https://www.youtube.com/watch?v=8WvwFPN1XNA)  
- [Static Mesh Actors](https://docs.unrealengine.com/en-US/Engine/Actors/StaticMeshActor/index.html)
- [Skeletal Mesh Actors](https://docs.unrealengine.com/en-US/Engine/Actors/SkeletalMeshActors/index.html)  
- [Componentes](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Actors/Components/index.html)
- [Brushes](https://docs.unrealengine.com/en-US/Basics/Actors/Brushes/index.html)
- [Actors](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/Actors/index.html)
- [Collsion Overview](https://docs.unrealengine.com/en-US/InteractiveExperiences/Physics/Collision/Overview/index.html)
