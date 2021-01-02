[Home](https://myerco.github.io/unreal-engine) / [Unreal](https://myerco.github.io/unreal-engine/unreal.html)

# Blueprints

> 1. [Introdução ao *Blueprints Visual Scripting*](#1)  
> 1. [Level Blueprint](#2)  
> 1. [Blueprint de atores](#3)
> 1. [Utilizando o level Blueprint para escrever   mensagens na tela](#4)
> 1. [Comentários](#4)

<a name="1"></a>
## 1. Introdução ao *Blueprints Visual Scripting*
O sistema *Blueprints Visual Scripting* no *Unreal Engine* é um sistema completo de script de jogo baseado no conceito de usar uma interface baseada em nó para criar elementos de jogo a partir do *Unreal Editor*. Como acontece com muitas linguagens de script comuns, ele é usado para definir classes orientadas a objetos (OO) ou objetos no mecanismo. Ao usar o UE4, você frequentemente descobrirá que os objetos definidos usando o Blueprint são coloquialmente chamados apenas de "Blueprints".

### 1.1 Características
- Blueprints foca em ser acessível, versátil para qualquer membro do projeto.  
- Simplifica tarefas para programadores de engenheiros de projeto.
- Fácil de entender, interagir e construir.  

### 1.2 Construção
|**C++**  |**Blueprints**  | 7+ Ferramentas e editores  | Compilação e execução |
|:-:|-|-|-|
|  |Framework classes | Timeline|  |  Depuração e adicionais de performance|
|  | Replicação |Componentes| Comunicação entre BP |  |
|  |  |Editor de script|  |  |
|  |  |Características adicionais|  |  |

### 1.3 Esquema
[Arquivo](../files/Blueprint_poster_18x24.pdf)

<a name="2"></a>
## 2. Level Blueprint  
Um Level Blueprint é um tipo especializado de Blueprint que atua como um gráfico de evento global em todo o nível. Cada nível em seu projeto tem seu próprio Level Blueprint criado por padrão, que pode ser editado no *Unreal Editor*, no entanto, novos *Level Blueprints* não podem ser criados por meio da interface do editor.  

 ![Open Level Blueprint](https://docs.unrealengine.com/Images/Engine/Blueprints/UserGuide/Types/LevelBlueprint/toolbar_level_editor.webp)

<a name="3"></a>
## 3. Blueprint de atores
Atores são objetos que são adicionados na cena. São classes de objetos que suportam vários componentes, métodos e variáveis. A lógica de programação é expressada em Blueprint.  

### 3.1 Place Actors
No nível mais fundamental, um ator é qualquer objeto que você pode colocar em um nível e esta página irá mostrar os vários métodos em que você pode colocar esses atores dentro de seus níveis.  
![Atores](../imagens/actor/actor39.png)   

### 3.2 Blueprint Class
Uma classe Blueprint, muitas vezes abreviada como Blueprint, é um ativo que permite que os criadores de conteúdo adicionem funcionalidade facilmente às classes de jogo existentes. Os projetos são criados dentro do Unreal Editor visualmente, em vez de digitar o código, e salvos como ativos em um pacote de conteúdo. Essencialmente, eles definem uma nova classe ou tipo de ator que pode então ser colocado em mapas como instâncias que se comportam como qualquer outro tipo de ator.  
- Menu de acesso rápido  
![Atores](../imagens/actor/actor40.png)  
- Escolha de Classe de atores  
![Atores](../imagens/actor/actor41.png)


### 3.2 Components
Os *Components* ou componentes são um tipo especial de objeto que os atores podem anexar a si próprios como subobjetos. Os componentes são úteis para compartilhar comportamentos comuns, como a capacidade de exibir uma representação visual e reproduzir sons. Eles também podem representar conceitos específicos do projeto, como a maneira como um veículo interpreta a entrada e muda sua própria velocidade e orientação. Por exemplo, um projeto com carros, aeronaves e barcos controláveis pelo usuário pode implementar as diferenças no controle e movimento do veículo, alterando qual componente um ator do veículo usa.

![Atores](../imagens/actor/actor46.png)

### 3.3 Components e My Blueprint    
- Components - Apresenta todos os componentes anexados ao objeto principal.
- My Blueprint - Apresenta os eventos, funções, macros e variáveis presentes dentro do objeto.  

![Atores](../imagens/actor/actor42.png)

**Representação da organização do objeto**.

```
|-- Objeto
|   |-- Events
|   |   |-- BeginPlay
|   |   |-- ActorBeginOverlap
|   |   |-- Tick
|   |-- Functions
|   |   |-- ConstructionScript
|   |-- Variables      
|   |   |-- VariavelLocal
```
### 3.4 Construction Script

Lógica de que é executada na construção do objeto, similares ao eventos **Construtor** em C++.  
**Exemplo**

 ![Atores](../imagens/actor/actor43.png)

### 3.5 Event Graph
Contém um gráfico de nós e suas ligações representando a lógica de um Blueprint.     
![Atores](../imagens/actor/actor44.png)

**BeginPlay**

Este evento é acionado para todos os Atores quando o jogo é iniciado, quaisquer Atores gerados após o jogo ser iniciado terão isso chamado imediatamente.

**ActorBeginOverlap**

Este evento será executado quando uma série de condições forem atendidas ao mesmo tempo:
  - A resposta à colisão entre os atores deve permitir sobreposições.
  - Ambos os Atores que devem executar o evento têm Gerar Eventos de Sobreposição definido como verdadeiro.
  - E, finalmente, a colisão de ambos os Atores começa a se sobrepor; movendo-se juntos ou um é criado sobrepondo-se ao outro.

**Tick**

Este é um evento simples que é chamado em todos os quadros do jogo.

<a name="4"></a>
## 4. Utilizando o level Blueprint para escrever   mensagens na tela
 Utilizando o evento **BeginPlay** e conectando o nó **Print String** para escrever uma mensagem na tela.

![Atores](../imagens/actor/actor45.png)

<a name="5"></a>
## 5. Comentários   
Os comentários podem ser incluídos diretamente em nós **Blueprint** únicos ou podem ser incluídos como caixas de comentários para agrupar nós relacionados e fornecer descrições sobre sua funcionalidade. Eles podem ser usados apenas para fins organizacionais para tornar os gráficos mais legíveis, mas também podem ser usados para fins informativos, pois permitem que descrições textuais sejam adicionadas da mesma forma que adicionar comentários ao código.

- Selecione os nós e digite "C" no teclado para adicionar um comentário.

***

## Referências
- [Blueprint](https://docs.unrealengine.com/en-US/Engine/Blueprints/index.html)
- [Level Blurprint](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Types/LevelBlueprint/index.html)
- [Actors](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Actors/index.html)
- [Components](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Actors/Components/index.html)
- [Event Graph](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/EventGraph/index.html)
- [Placing Actors](https://docs.unrealengine.com/en-US/Engine/Actors/Placement/index.html)
- [Blueprint Class](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Types/ClassBlueprint/index.html)
- [Comments](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Comments/index.html)
-[Events](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/Events/index.html)
