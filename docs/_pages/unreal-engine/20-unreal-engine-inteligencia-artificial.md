---
title: Inteligência Artificial
excerpt: Trabalhando com Inteligência Artificial
permalink: /pages/unreal-engine/inteligencia-artificial
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true 
categories:
  - Unreal Engine
tags:
  - IA
  - behavior tree
  - inteligência articial
---

Neste projeto serão apresentados os elementos necessários para a construção de
simulação de comportamentos, como por exemplo, busca e detecção de jogadores bem como configurar o personagem controlado pela IA em diferentes estados de comportamento.

## 1. Preparando o projeto

Em este passo iremos preparar as pastas, configuração inicial do projeto e *Character* do
jogador.

**1.** Vamos criar o projeto AulaIA;

**2.** Criar as pastas para organização do projeto:

```cp
      Maps  
      Blueprints  
        Characters
        GameControls
      AI  
```

**3.** Criar um novo *level* de nome **LevelTeste** e salvar na pasta **Maps**, logo em seguida configure o projeto para que o **levelTeste** seja inicializado ao abrir o projeto:  
  `Project Settings` > `Maps & Mods`

**4.** Criar as classes Blueprints:  

- **BP_PlayerController** do tipo `PlayerController` ;

- **BP_GameMode** do tipo `GameMode`;

- **BP_PlayerBase** do tipo *Character* (vamos duplicar e utilizar o já existente no projeto);  

**5.** Configurar `World Settings` adicionando as classes de controle de jogador **BP_PlayerController**, modo do jogo **BP_GameMode** e o personagem **BP_PlayerBase**;

### 1.1. Vídeo preparando o projeto de IA

{% include video id="XNGknrCy4JM" provider="youtube" %}

### 1.2. NPC básico

Em este passo iremos implementar a classe *Character* para o NPC (Personagem não jogável que será controlado pelo *Engine*).  

A classe Blueprint **BP_NPC** do tipo *Character* e logo em seguida adicionar a malha do esqueleto (*Skeletal mesh*) e as animações do manequim padrão do *Engine*.

### 1.3. Inteligência Artificial, implementando o NPC

{% include video id="3i5omWI6r-U" provider="youtube" %}

## 2. Árvore de comportamento ou Behaivor Tree

Em este passo iremos implementar os elementos necessários para controles de movimentação
do NPC.

**1.** Devemos criar as classes Blueprints:

- BP_NPC_Controller do tipo `AIController`;

- BH_NPC do tipo `Behaivor Tree`;

- BB_NPC do tipo `Blackboard`;  

**2.** A estrutura de controle das classes é a seguinte: O *Character* tem como controlador o `AIController` que executa a árvore `Behaivor Tree` a qual utiliza o `Blackboard` para a armazenamento de variáveis.  

**BP_NPC** -> **BP_NPC_Controller** -> (**BH_NPC**  + **BB_NPC**)

**3.** Adicionar o componente **NavMeshBoundVolume** para definir fronteiras de movimentação do NPC;

**4.** Configurando a árvore de comportamento:

- Adicionando o nó de controle `sequence`;

- Adicionar variáveis no `Blackboard` para que possam ser compartilhadas pelas *task* e *services*;  

**5.** Implementando a *task* **LocalizaJogador**:

Tarefas (*tasks*) são similares a funções que iniciam e finalizam com comandos específicos;

Podem ser adicionados parâmetros do tipo *Blackboard value* para comunicação entre tarefas;

Na lógica utilizamos *Get Player Pawn* para obter o objeto *Pawn* instanciado do jogador e logo em seguida o vetor de retorno da função *Get Actor Location* para que possamos atualizar a variável passada como parâmetro;  

### 2.1. VídeoImplementando a árvore de comportamento

{% include video id="hpkZEdqbD6o" provider="youtube" %}

## 3. Movimentação do NPC

Neste passo iremos suavizar a movimentação do NPC configurando os controles de rotação.  
Na classe principal de **BP_NPC**:

**1.** Na classe principal **BP_NPC** configure `Use Controller Rotation Yaw` = *False* para que o personagem não utilize o controlador na rotação ;

**2.** No Componente `CharacterMovement` configure `Rotation Rate` Z=540

Aumenta a taxa de rotação;

**3.** Em `Orient Rotation to Movement` = *true*  

Seu personagem se volta para a direção da viagem. Não importa para que lado a câmera esteja,

### 3.1. Vídeo Implementando a movimentação do NPC

{% include video id="5F0Vr4t0mg" provider="youtube" %}

#### 3.1.1. Andando aleatoriamente

Neste passo iremos adicionar a lógica para que o NPC caminhe para pontos
aleatórios.

**1.** Antes de adicionar a lógica vamos desconectar o nó da árvore **LocalizaJogador**;

**2.** No `Blackboard` da árvore adicionamos a variável do tipo *vetor* **LocalizacaoPonto**, usaremos a variável para armazenar as coordenadas do novo ponto de destino;

**3.** Localizar um ponto qualquer (randômico) no mapa a partir da posição do jogador;  

Utilizaremos a função **GetRandomPointInNavigableRadius** com o valor de *Radius* igual a 1500

**4.** Mover-se até o ponto;

**5.** Aguardar 2 segundos;

### 3.2. Vídeo implementando o movimento aleatório

{% include video id="HSle6iTEBQI" provider="youtube" %}

## 4. Adicionando percepção de visão

Para este passo devemos adicionar componentes no personagem **BB_NPC** e implementar
lógica de detecção do jogador.

1. No `Blackboard` da árvore adicionamos a variável do tipo *boolean* **VendoJogador**, usaremos a variável para "avisar" quando o jogador for percebido;

1. Configurando a classe **BP_NPC**

    1. No personagem **BP_NPC** adicionaremos o componente `AIPerception`;

    2. No componente `AIPerception`  será adicionado e configurado o elemento `AISight Config`;
    Este elemento adiciona os parâmetros que definem os ângulos e distâncias dos "sentidos" do NPC, bem como os objetos detectáveis (Inimigos, Neutros e Amigos);

    3. Adicionamos a lógica para receber e apresentar na tela quando um estimulo é disparado `Sucessfully Sensed`.

    4. Atualizaremos a variável **VendoJogador** do `Blackboard`;

1. Configurando a classe **BP_NPC_Controller**, repita os passos anteriores.
  Adicionar a lógica nesta classe permite distribuir a lógica entre as classes associadas, por
  exemplo várias classes de personagens.  

  Esta configuração vai ser utilizada no projeto atual.

### 4.1. Vídeo implementando a percepção ou visão do NPC

{% include video id="m7DflYieVE0" provider="youtube" %}

#### 4.1.1. Adicionando as condições de percepção na árvore

Neste passo vamos adicionar obstáculos no ambiente e configurar a árvore combinando os
nós perseguindo jogador e andando aleatoriamente.

1. Adicionaremos obstáculos no ambiente para obstruir a visão

2. Iremos adicionar os *Decorators* :

   1. **Não Está vendo jogador** - controlando a subárvore com a seguinte configuração:

   - *Observer aborts* =  *Both* Para que todas os nõs subjacentes sejam interrompidos;

   - *Key Query* = *Is Not Set*  Para somente executar a subárvore quando a variável **VendoJogador** for verdadeira.

   1. **Está vendo jogador** - controlando a subárvore para perseguir o jogador

   - *Observer aborts* =  *None* - Sem parâmetro de controle de interrupção ;

   - *Key Query* = *Is Set*.

3. Será criada a *task* **PersegueJogador** para substituir **Move To**;

### 4.2. Vídeo implementando a percepção na árvore de comportamento

{% include video id="Ge69lptbC2g" provider="youtube" %}

#### 4.2.1. Adicionando o loop da percepção na árvore

Neste passo vamos adicionar um decorator loop para implementar um laço de repetição
dos nós.

1. No nó com o `decorator` **Está vendo o jogador** adicionaremos o `decorator` *Loop*
para reexecutar os elementos.

### 4.3. Vídeo implementando a percepção e o loop na árvore de comportamento

{% include video id="U9oIU841U44" provider="youtube" %}

## 5. Organizando os nós

Neste passo vamos renomear os nós para algo que faça sentido.

1. Nó **Patrulhando**  

2. Nó **Persegue Jogador**

3. Adicionar o `Decorator` `Colldown` para que adicionar um tempo de espera quando uma.
tarefa retornar *false*. O decorator *loop* deve ser removido.

4. Adicionar a tarefa **Persegue Jogador** removendo **Move To**.

### 5.1. Vídeo organizando os nós

{% include video id="zoZxqSm42EQ" provider="youtube" %}

## 6. Mudando velocidade do NPC

Neste passo iremos criar um serviço que altera a velocidade do NPC;

1. Criar um serviço **MudandoVelocidade**;

2. Na classe NPC criar a variável **Pawn_NPC** para que possamos ter acesso aos componentes
e variáveis do NPC;

### 6.1. Vídeo mudando a velocidade do NPC

{% include video id="-pPuWw-CL9o" provider="youtube" %}

## 7. Patrulhamento com ponto de controle 01

Nos próximos passos devemos implementar o patrulhamento utilizando pontos de controle.

1. Começaremos implementando a classe  **BP_Caminho** do tipo *Actor Blueprint*;

2. Adicionaremos a variável **PontoCaminho** do tipo *vector* e deverá ser um *array*
para servir de marcação dos pontos. A variável deve ter os atributos *Instance Editable* e *Show 3D Widget* igual a *true* ;

3. No classe **BB_NPC** adicionaremos uma variável **Caminho** do tipo **BP_Caminho**
assim possibilitamos acesso do NPC ao caminho.

### 7.1. Vídeo implementando patrulhamento e controle 1

{% include video id="vKeJ7n9Yf30" provider="youtube" %}

#### 7.1.1. Tarefa para pegar um ponto de patrulhamento

Neste passo vamos implementar uma tarefa para pegar o ponto de controle dentro
do objeto caminho associado ao NPC.

1. Obtém o ator associado ao NPC **Caminho** e logo em seguida um vetor de marcação  **PontoCaminho**.

1. Insere a nova tarefa em uma subárvore e em sequencia adicionamos a tarefa **MoveTo**
com o parâmetro **PontoDestino** atualizado.

### 7.2. Vídeo implementando a tarefa para pegar um ponto de patrulhamento

{% include video id="tx1BoKuQLnw" provider="youtube" %}

#### 7.2.1. Tarefa para pegar o próximo ponto de controle

Neste passo vamos implementar a tarefa para pegar o próximo ponto de controle.

1. Calculo de ponto atual + 1;

2. Caso o resultado anterior seja maior que o número de pontos associados ao caminho, verificamos se a variável **RepeteCaminho** (Variável *boolean* do NPC) é verdadeira
para atribuir o valor 0 marcando o início dos pontos ou finalizamos a tarefa.

### 7.3. Vídeo implementando a tarefa para pegar o próximo ponto de patrulhamento

{% include video id="_JYS5mGJnMA" provider="youtube" %}

## 8. Adicionando Enum para armazenar os estados do NPC

Neste passo vamos adicionar a variável **EstadoNPC** do tipo *Enum* com a finalidade
de armazenar diversos estados do NPC, como por exemplo:

- Patrulhando;

- Procurando;

- Perseguindo;

Logo em seguida vamos fazer o seguinte:

1. Adicionar uma variável **EstadoNPC** no `Blackboard`

2. Implementar uma tarefa **MudaEstadoNPC**  

{% include video id="TSXPr_P2bfE" provider="youtube" %}

### 8.1. Implementando tarefa para mudança de estado

Neste passo vamos implementar uma tarefa para alterar a variável **EstadoNPC** modificando o estado do NPC.  

### 8.2. Vídeo implementando tarefa para mudança de estado

{% include video id="aqrjHEzfGbw" provider="youtube" %}

## 9. Testando a árvore com pontos de controle e perseguição

Neste passo iremos organizar a árvore e testar o projeto.

1. `Blackboard Based Condition` selecione o valor `Both` em `Observers aborts`;

2. **Cooldown** adicione o valor 0.2 em *Cool Down Time*  

### 9.1. Vídeo testando a árvore com pontos de controle e perseguição

{% include video id="AiIUC0Itds4" provider="youtube" %}

## 10. Alerta de distância do jogador

Neste passo iremos implementar um aviso de alerta de proximidade de jogador.

1. Tarefa **DistanciaJogador** calcula a distancia do NPC e o jogador;

2. Variável **DistanciaDeAtaque**;

3. Variável **Distancia** com o valor 500 para servir como parâmetro de distâncias.

### 10.1. Vídeo alerta de distância do jogador

{% include video id="lDSNGngSvfg" provider="youtube" %}