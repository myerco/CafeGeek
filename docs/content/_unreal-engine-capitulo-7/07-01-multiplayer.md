---
title: Multiplayer.
excerpt: Implementando um jogo multiplayer com Unreal Engine
permalink: /unreal-engine-capitulo-7/multiplayer
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 701
tags:
  - multiplayer
---

Neste capítulo vamos implementar e organização elementos para conexão, replicação e inicialização de um jogo multiplayer.

## 1. Implementando um jogo multiplayer

### 1.1. Tipos de Conexão

A conexão somente é possível com versões do mesmo programa, isso significa que o cliente e o servidor devem estar sendo usados na mesma versão.

#### 1.1.1. Cliente e Servidor

Considerando a topologia de redes, Cliente/Servidor, onde o programa cliente se conecta através de uma rede a um programa servidor, sendo que o programa servidor pode ficar somente no atendimento ou pode realizar tarefas.

{% include imagelocal.html
    src="unreal/multiplayer/diagrama1.webp"
    alt="Figura: Tipos de conexão - Cliente Servidor."
    caption=""
%}

#### 1.1.2. Ponto a Ponto

Neste caso, o programa cliente se conecta com outro computador, não existe o papel de servidor e os computadores ficam operantes trocando informação.

{% include imagelocal.html
    src="unreal/multiplayer/diagrama2.webp"
    alt="Figura: Tipos de conexão - Ponto a Ponto."
    caption=""
%}

## 1.2. Implementação no jogo

No Unreal Engine consideramos a estrutura de Cliente/Servidor e configurando os elementos:

**Servidor (Host)** - Jogo em modo escuta *listen*.

```sh
  C:\Program Files\UE_4.17\Engine\Binaries\Win64\UE4Editor.exe
  C:\PATH_TO_MY_PROJECT.uproject /Game/ThirdPersonCPP/Maps/ThirdPersonExampleMap -server -log -port=8003
```

**Cliente** - Jogo tem que conectar em um outro através de um endereço de rede.

```sh
C:\Program Files\UE_4.17\Engine\Binaries\Win64\UE4Editor.exe
C:\PATH_TO_MY_PROJECT.uproject 192.168.1.90:8003 -game -log
```

Por último é necessário configurar dentro do projeto a busca de servidores na rede local ou remota;

## 2. Executando e configurando o projeto

Para executar o jogo em modo multiplayer utilize o menu principal e acesse a opção `Play` escolhendo as seguintes opções:

- `Number of Players` : Escolha a quantidade de conexões que o projeto recebera.

- `Net Mode` : *Play As Listem Server*, O jogo está sendo executado como um servidor que hospeda uma sessão multijogador em rede. Aceita conexões de clientes remotos e possui players locais diretamente no servidor. Este modo é frequentemente usado para multiplayer competitivo e cooperativo casual.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer14.webp"
    alt="Figura:Multiplayer, Executando várias instâncias do jogo."
    caption=""
%}

A seguir vamos implementar as estruturas de controle do game `GameMode`, `GameInstance` e `PlayerController`.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer2.webp"
    alt="Figura:Multiplayer, Implementando estruturas de controle."
    caption=""
%}

Criando o `GameInstance`.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer3.webp"
    alt="Figura: Multiplayer, Implementando a GameInstance."
    caption=""
%}

Implementando o evento *OpenMenu*.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer5.webp"
    alt="Figura: Multiplayer, Implementando a chamada do menu do jogo."
    caption=""
%}

Configurando o projeto com GameInstance.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer4.webp"
    alt="Figura: Multiplayer, Configurando a Gameinstance."
    caption=""
%}

## 3. Implementando o menu

Para exemplificar a conexão de rede do projeto, vamos implementar menus para possibilitar a inserção do endereço de rede do servidor, modo do jogo (Cliente ou Servidor) e localizar o jogo na rede.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer1.webp"
    alt="Figura: Criando level Menu"
    caption=""
%}

Implementando a lógica de chamada do menu no level *Menu* utilizando o `Open Level Blueprints`.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer6.webp"
    alt="Figura: Multiplayer, Chamando o menu com BeginPlay."
    caption=""
%}

Implementando o `Widget` WBP_Menu.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer8.webp"
    alt="Figura: Multiplayer, Implementando o Widget para o Menu."
    caption=""
%}

Implementando os seguintes elementos do menu.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer9.webp"
    alt="Figura: Multiplayer, Adicionando botões no menu."
    caption="Figura: Multiplayer, Adicionando botões no menu."
%}

Implementar os eventos para instanciar uma conexão.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer11.webp"
    alt="Figura: Multiplayer, Lógica Blueprint para criar uma conexão no servidor remoto."
    caption="Figura: Multiplayer, Lógica Blueprint para criar uma conexão no servidor remoto."
%}

Conectar ao servidor utilizando IP.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer10.webp"
    alt="Figura: Multiplayer, Lógica Blueprint para criar uma conexão no servidor remoto por IP."
    caption="Figura: Multiplayer, Lógica Blueprint para criar uma conexão no servidor remoto por IP."
%}

### 3.1. Executando o jogo

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer14.webp"
    alt="Figura: Multiplayer, Play As Listen Server."
    caption="Configurando o jogo para aceitar duas conexões e executar em modo Servidor."
%}

`Play Offline` - Executa o jogo em modo offline;  

`Play As Listen server` - Executa o jogo (tela principal) em modo servidor;  

`Play As Client` - Executa o jogo (tela principal) em modo Cliente, iniciando a servidor em outra janela.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer12.webp"
    alt="Figura: Multiplayer, Dois PlayerStart."
    caption="Adicionando dois PlayerStart."
%}

## 4. Replicação

### 4.1. Replicação de eventos

Para utilizar a replicação de eventos é necessário criar eventos customizados `Add custom event`.

*Servidor* - Executado apenas no servidor que hospeda o jogo;  

*Cliente* - Executado apenas no cliente que possui o ator ao qual a função pertence. Caso o Ator não possua conexão própria, esta lógica não será executada;

*NetMulticast* - Executado em todos os clientes que estão conectados ao servidor, bem como no próprio servidor.

### 4.2. Objetos não Replicados

- HUD

- UMG Widgets

Replicar Movimento" funciona apenas para um componente raiz. Para este recurso, `StaticMeshComponent` deve ser escolhido como "root".
{: .notice--info}  

[replication for moving actor](https://answers.unrealengine.com/questions/836572/replication-for-moving-actor.html?sort=oldest
)

### 4.3. Replicação de variáveis

Usaremos as variáveis *Vida*, *Nome* e *VidaMax* para exemplificar.

- Vida

- Nome

- VidaMax

## 5. Implementando o objeto de para ser arremessado

Implementando um Blueprints Static Mesh Actor e configurando a replicação do objeto.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer23.webp"
    alt="Figura: Multiplayer,Static Mesh para o jogo."
    caption=""
%}

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer24.webp"
    alt="Figura: Multiplayer, Component Replication."
    caption=" O componente que associado também deverá ser replicado.  "
%}

### 5.1. Implementando a manipulação do objeto pelo personagem

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer15.webp"
    alt="Figura: Multiplayer, Lógica Blueprint chamando a ação de segurar."
    caption="Eventos de entrada de dados (INPUT)."
%}

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer16.webp"
    alt="Figura: Multiplayer, Lógica Blueprint do evento AcaoDeSegurar."
    caption="Lógica para detectar o objeto na frente do jogador."
%}

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer17.webp"
    alt="Figura: Multiplayer, Lógica Blueprint do evento AcaoDeSegurar continuação."
    caption=""
%}

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer19.webp"
    alt="Figura: Multiplayer, Lógica Blueprint do evento para prender o objeto."
    caption="Agarrar objeto, este evento prende o objeto ao personagem."
%}

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer18.webp"
    alt="Figura: Multiplayer, Lógica Blueprint do evento para alterar a posição do objeto preso ao personagem."
    caption="Evento *Segurando*, este evento utiliza o event tick para alterar a posição do objeto preso ao personagem."
%}

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer20.webp"
    alt="Figura: Multiplayer, Lógica Blueprint do evento para soltar o objeto."
    caption=""
%}

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer22.webp"
    alt="Figura: Multiplayer, Lógica Blueprint da ação que arremessa o objeto."
    caption=""
%}

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer21.webp"
    alt="Figura: Multiplayer, Lógica Blueprint simulando o arremesso."
    caption=""
%}
