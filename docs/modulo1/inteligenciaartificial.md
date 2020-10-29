# Inteligência artificial

Neste projeto serão apresentados os elementos necessários para a construção de
simulação de comportamentos, como por exemplo, busca e detecção de jogadores bem como configurar o personagem controlado pela IA em diferentes estados de comportamento.
Vamos utilizar os seguintes elementos :
1. Programação com Blueprints;
1. AI Controllers;
1. Blackboards;
1. Behavior Trees;
1. Behavior Tree Services;
1. Behavior Tree Decorators;
1. Behavior Tree Tasks;

## Índice
> 1. [Preparando o projeto](#1)
> 1. [NPC básico](#2)
> 1. [Árvore de comportamento](#3)
> 1. [Movimentação do NPC](#4)
> 1. [Andando aleatoriamente](#5)
> 1. [Adicionando percepção - Visão](#6)
> 1. [Adicionando as condições de percepção na árvore 1](#7)
> 1. [Adicionando as condições de percepção na árvore 2](#8)
> 1. [Organizando os nós](#9)
> 1. [Mudando velocidade do NPC](#10)
> 1. [Patrulhamento com ponto de controle 01](#11)
> 1. [Tarefa para pegar um ponto de patrulhamento](#12)
> 1. [Tarefa para pegar o próximo ponto de controle](#13)
> 1. [Adicionando Enum para armazenar os estados do NPC](#14)
> 1. [Implementando tarefa para mudança de estado](#15)
> 1. [Testando a árvore com pontos de controle e perseguição](#16)
> 1. [Alerta de distância do jogador](#17)
***


<a name="1"></a>
## 1 - Preparando o projeto

Em este passo iremos preparar as pastas, configuração inicial do projeto e *Character* do
jogador.

1. Criar o projeto AulaIA;
1. Criar as pastas para organização do projeto:
    ```c
      Maps  
      Blueprints  
        Characters
        GameControls
      AI  
    ```
1. Criar um novo *level* de nome **LevelTeste** e salvar na pasta **Maps**, logo em seguida configure o projeto para que o **levelTeste** seja inicializado ao abrir o projeto:  
  **Project Settings-> Maps & Mods**
1. Criar as classes Blueprints:  
   - **BP_PlayerController** do tipo *PlayerController* ;
   - **BP_GameMode** do tipo *GameMode*;
   - **BP_PlayerBase** do tipo *Character* (vamos duplicar e utilizar o já existente no projeto);  
1. Configurar *World Settings* adicionando as classes de controle de jogador **BP_PlayerController**, modo do jogo **BP_GameMode** e o personagem **BP_PlayerBase**;

#### Vídeo Aula 01
  [![Aula 01](http://img.youtube.com/vi/XNGknrCy4JM/0.jpg)](https://www.youtube.com/watch?v=XNGknrCy4JM "Aula 01")
***

<a name="2"></a>
## 2 - NPC básico.

Em este passo iremos implementar a classe *Character* para o NPC (Personagem não jogável que será controlado pelo *Engine*).  

1. Criar a classe Blueprint **BP_NPC** do tipo *Character* e logo em seguida adicionar a malha do esqueleto (*Skeletal mesh*) e as animações do manequim padrão do *Engine* ;

  [![Aula 02](http://img.youtube.com/vi/3i5omWI6r-U/0.jpg)](https://www.youtube.com/watch?v=3i5omWI6r-U "Aula 02")
***

<a name="3"></a>
## 3 - Árvore de comportamento (*Behaivor Tree*).

Em este passo iremos implementar os elementos necessários para controles de movimentação
do NPC.

1. Criando as classes Blueprints :   
  - **BP_NPC_Controller** do tipo *AIController*;
  - **BH_NPC** do tipo *Behaivor Tree*;
  - **BB_NPC** do tipo *Blackboard*;  
1. A estrutura de controle das classes é a seguinte:  
  O *Character* tem como controlador o *AIController* que executa a árvore *Behaivor Tree* a qual utiliza o *Blackboard* para a armazenamento de variáveis.  
  **BP_NPC** -> **BP_NPC_Controller** -> (**BH_NPC**  + **BB_NPC**)
1. Adicionar o componente **NavMeshBoundVolume** para definir fronteiras de movimentação do NPC;
1. Configurando a árvore de comportamento:
    - Adicionando o nó de controle *sequence*;
    - Adicionar variáveis no *Blackboard* para que possam ser compartilhadas pelas *task* e *services*;  
1. Implementando a *task* **LocalizaJogador**:    

   Tarefas (*tasks*) são similares a funções que iniciam e finalizam com comandos específicos;   
   Podem ser adicionados parâmetros do tipo *Blackboard value* para comunicação entre tarefas;
   Na lógica utilizamos *Get Player Pawn* para obter o objeto *Pawn* instanciado do jogador e logo em seguida o vetor de retorno da função *Get Actor Location* para que possamos atualizar a variável passada como parâmetro;  

  [![Aula 03](http://img.youtube.com/vi/hpkZEdqbD6o/0.jpg)](https://www.youtube.com/watch?v=hpkZEdqbD6o "Aula 03")
***
<a name="4"></a>
## 4 -  Movimentação do NPC.

Neste passo iremos suavizar a movimentação do NPC configurando os controles de rotação.  
Na classe principal de **BP_NPC**:
1. Na classe principal **BP_NPC** configure *Use Controller Rotation Yaw* = *False* para que o personagem não utilize o controlador na rotação ;
1. No Componente *CharacterMovement* configure *Rotation Rate* Z=540   
  Aumenta a taxa de rotação;
1. Em *Orient Rotation to Movement* = *true*  
  Seu personagem se volta para a direção da viagem. Não importa para que lado a câmera esteja,   

[![Aula 04](http://img.youtube.com/vi/Q5F0Vr4t0mg/0.jpg)](https://www.youtube.com/watch?v=Q5F0Vr4t0mg "Aula 04")
***
<a name="5"></a>
## 5 -  Andando aleatoriamente.

Neste passo iremos adicionar a lógica para que o NPC caminhe para pontos
aleatórios.
1. Antes de adicionar a lógica vamos desconectar o nó da árvore **LocalizaJogador**;
1. No *Blackboard* da árvore adicionamos a variável do tipo *vetor* **LocalizacaoPonto**, usaremos a variável para armazenar as coordenadas do novo ponto de destino;
1. Localizar um ponto qualquer (randômico) no mapa a partir da posição do jogador;  
  Utilizaremos a função **GetRandomPointInNavigableRadius** com o valor de *Radius* igual a 1500
1. Mover-se até o ponto;
1. Aguardar 2 segundos;

[![Aula 05](http://img.youtube.com/vi/HSle6iTEBQI/0.jpg)](https://www.youtube.com/watch?v=HSle6iTEBQI "Aula 05")
***

<a name="6"></a>
## 6 - Adicionando percepção - Visão

Para este passo devemos adicionar componentes no personagem **BB_NPC** e implementar
lógica de detecção do jogador.
1. No *Blackboard* da árvore adicionamos a variável do tipo *boolean* **VendoJogador**, usaremos a variável para "avisar" quando o jogador for percebido;
1. Configurando a classe **BP_NPC**
  1. No personagem **BP_NPC** adicionaremos o componente *AIPerception*;
  1. No componente *AIPerception*  será adicionado e configurado o elemento *AISight Config*;    
    Este elemento adiciona os parâmetros que definem os ângulos e distâncias dos "sentidos" do NPC, bem como os objetos detectáveis (Inimigos, Neutros e Amigos);
  1. Adicionamos a lógica para receber e apresentar na tela quando um estimulo é disparado *Sucessfully Sensed*.
  1. Atualizaremos a variável **VendoJogador** do *Blackboard*;
1. Configurando a classe **BP_NPC_Controller**, repita os passos anteriores.
  Adicionar a lógica nesta classe permite distribuir a lógica entre as classes associadas, por
  exemplo várias classes de personagens.  

  > Esta configuração vai ser utilizada no projeto atual.

  [![Aula 06](http://img.youtube.com/vi/m7DflYieVE0/0.jpg)](https://www.youtube.com/watch?v=m7DflYieVE0 "Aula 06")
***
<a name="7"></a>
## 7 - Adicionando as condições de percepção na árvore

Neste passo vamos adicionar obstáculos no ambiente e configurar a árvore combinando os
nós perseguindo jogador e andando aleatoriamente.
1. Adicionaremos obstáculos no ambiente para obstruir a visão
1. Iremos adicionar os *Decorators* :
  1. **Não Está vendo jogador** - controlando a subárvore com a seguinte configuração:
  - *Observer aborts* =  *Both* Para que todas os nõs subjacentes sejam interrompidos;
  - *Key Query* = *Is Not Set*  Para somente executar a subárvore quando a variável **VendoJogador** for verdadeira.
  1. **Está vendo jogador** - controlando a subárvore para perseguir o jogador
  - *Observer aborts* =  *None* - Sem parâmetro de controle de interrupção ;
  - *Key Query* = *Is Set*.
1. Será criada a *task* **PersegueJogador** para substituir **Move To**;

[![Aula 07](http://img.youtube.com/vi/Ge69lptbC2g/0.jpg)](https://www.youtube.com/watch?v=Ge69lptbC2g "Aula 07")
***

<a name="8"></a>
## 8 - Adicionando as condições de percepção na árvore

Neste passo vamos adicionar um decorator loop para implementar um laço de repetição
dos nós.
1. No nó com o *decorator* **Está vendo o jogador** adicionaremos o *decorator* *Loop*
para reexecutar os elementos.  

[![Aula 08](http://img.youtube.com/vi/U9oIU841U44/0.jpg)](https://www.youtube.com/watch?v=U9oIU841U44 "Aula 08")
***

<a name="9"></a>
## 9 - Organizando os nós

Neste passo vamos renomear os nós para algo que faça sentido.
1. Nó **Patrulhando**  
1. Nó **Persegue Jogador**
1. Adicionar o *Decorator* *Colldown* para que adicionar um tempo de espera quando uma.
tarefa retornar *false*. O decorator *loop* deve ser removido.
1. Adicionar a tarefa **Persegue Jogador** removendo **Move To**.

[![Aula 09](http://img.youtube.com/vi/zoZxqSm42EQ/0.jpg)](https://www.youtube.com/watch?v=zoZxqSm42EQ "Aula 09")
***

<a name="10"></a>
## 10 - Mudando velocidade do NPC

Neste passo iremos criar um serviço que altera a velocidade do NPC;
1. Criar um serviço **MudandoVelocidade**;
1. Na classe NPC criar a variável **Pawn_NPC** para que possamos ter acesso aos componentes
e variáveis do NPC;

[![Aula 10](http://img.youtube.com/vi/-pPuWw-CL9o/0.jpg)](https://www.youtube.com/watch?v=-pPuWw-CL9o "Aula 10")
***
<a name="11"></a>
## 11 - Patrulhamento com ponto de controle 01

Nos próximos passos devemos implementar o patrulhamento utilizando pontos de controle.   
1. Começaremos implementando a classe  **BP_Caminho** do tipo *Actor Blueprint*;
1. Adicionaremos a variável **PontoCaminho** do tipo *vector* e deverá ser um *array*
para servir de marcação dos pontos. A variável deve ter os atributos *Instance Editable* e *Show 3D Widget* igual a *true* ;
1. No classe **BB_NPC** adicionaremos uma variável **Caminho** do tipo **BP_Caminho**
assim possibilitamos acesso do NPC ao caminho.

[![Aula 11](http://img.youtube.com/vi/vKeJ7n9Yf30/0.jpg)](https://www.youtube.com/watch?v=vKeJ7n9Yf30 "Aula 11")
***

<a name="12"></a>
## 12 - Tarefa para pegar um ponto de patrulhamento
Neste passo vamos implementar uma tarefa para pegar o ponto de controle dentro
do objeto caminho associado ao NPC.
1. Obtém o ator associado ao NPC **Caminho** e logo em seguida um vetor de marcação  **PontoCaminho**.
1. Insere a nova tarefa em uma subárvore e em sequencia adicionamos a tarefa **MoveTo**
com o parâmetro **PontoDestino** atualizado.  
[![Aula 12](http://img.youtube.com/vi/tx1BoKuQLnw/0.jpg)](https://youtu.be/tx1BoKuQLnw "Aula 12")
***

<a name="13"></a>
## 13 - Tarefa para pegar o próximo ponto de controle
Neste passo vamos implementar a tarefa para pegar o próximo ponto de controle.
1. Calculo de ponto atual + 1
1. Caso o resultado anterior seja maior que o número de pontos associados ao caminho, verificamos se a variável **RepeteCaminho** (Variável *boolean* do NPC) é verdadeira
para atribuir o valor 0 marcando o início dos pontos ou finalizamos a tarefa.  
[![Aula 13](http://img.youtube.com/vi/_JYS5mGJnMA/0.jpg)](https://youtu.be/_JYS5mGJnMA "Aula 13")
***
<a name="14"></a>
## 14 - Adicionando Enum para armazenar os estados do NPC
Neste passo vamos adicionar a variável **EstadoNPC** do tipo *Enum* com a finalidade
de armazenar diversos estados do NPC, como por exemplo:   
 - Patrulhando
 - Procurando
 - Perseguindo
 Logo em seguida vamos fazer o seguinte:
 1. Adicionar uma variável **EstadoNPC** no *blackboard*
 1. Implementar uma tarefa **MudaEstadoNPC**  
[![Aula 14](http://img.youtube.com/vi/TSXPr_P2bfE/0.jpg)](https://youtu.be/TSXPr_P2bfE "Aula 14")
***
<a name="15"></a>
## 15 - Implementando tarefa para mudança de estado
Neste passo vamos implementar uma tarefa para alterar a variável **EstadoNPC**
modificando o estado do NPC.  
[![Aula 14](http://img.youtube.com/vi/aqrjHEzfGbw/0.jpg)](https://youtu.be/aqrjHEzfGbw "Aula 15")
***
<a name="16"></a>
## 16  - Testando a árvore com pontos de controle e perseguição
Neste passo iremos organizar a árvore e testar o projeto
1. **Blackboard Based Condition** selecione o valor *Both* em *Observers aborts*
2. **Cooldown** adicione o valor 0.2 em *Cool Down Time*  
[![Aula 16](http://img.youtube.com/vi/AiIUC0Itds4/0.jpg)](https://youtu.be/AiIUC0Itds4 "Aula 16")
***

<a name="17"></a>
## 17 - Alerta de distância do jogador
Neste passo iremos implementar um aviso de alerta de proximidade de jogador
1. Tarefa **DistanciaJogador** calcula a distancia do NPC e o jogador
1. Variável **DistanciaDeAtaque**;
1. Variável **Distancia** com o valor 500 para servir como parâmetro de distâncias    
[![Aula 17](http://img.youtube.com/vi/lDSNGngSvfg/0.jpg)](https://youtu.be/lDSNGngSvfg "Aula 17")
***

## Referências

- [Playlist IA](https://www.youtube.com/playlist?list=PLMRuH4-akjpSxkYxilTbg78pP-ybQwcy9)
- [Unreal IA documetação](https://docs.unrealengine.com/en-US/Gameplay/AI/index.html)
- [Unreal Start Guide](https://docs.unrealengine.com/en-US/Engine/ArtificialIntelligence/BehaviorTrees/BehaviorTreeQuickStart/index.html)
- [Raywenderlich Tutorial](https://www.raywenderlich.com/238-unreal-engine-4-tutorial-artificial-intelligence)
