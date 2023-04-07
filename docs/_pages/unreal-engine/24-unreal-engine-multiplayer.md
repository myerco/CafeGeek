---
title: Implementando o jogo Multiplayer.
excerpt: Implementando um jogo multiplayer com Unreal Engine
permalink: /pages/unreal-engine/multiplayer
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true 
---

Neste capítulo vamos implementar e organização elementos para conexão, replicação e inicialização de um jogo multiplayer.

## 1. Implementando um jogo multiplayer

### 1.1. Tipos de Conexão

- A conexão somente é possível com versões do mesmo programa.

#### 1.1.1. Cliente e Servidor

Programa cliente se conecta através de uma rede a um programa servidor.

Servidor pode ficar somente no atendimento ou pode realizar tarefas

{% include imagelocal.html
    src="unreal/multiplayer/diagrama1.webp"
    alt="Figura: Unreal Engine - Tipos de conexão - Cliente Servidor."
    caption="Figura: Unreal Engine - Tipos de conexão - Cliente Servidor."
%}

#### 1.1.2. Ponto a Ponto

Programa cliente se conecta com outro computador ouvindo a rede

Os computadores ficam operantes;

{% include imagelocal.html
    src="unreal/multiplayer/diagrama2.webp"
    alt="Figura: Unreal Engine - Tipos de conexão - Ponto a Ponto."
    caption="Figura: Unreal Engine - Tipos de conexão - Ponto a Ponto."
%}

### 1.2. Implementação no jogo

- Servidor (Host) - Jogo em modo escuta *listen*;

- Cliente - Jogo tem que conectar em um outro através de um endereço de rede;

- Busca servidores;

#### 1.2.1. Exemplo Servidor

```sh
  C:\Program Files\UE_4.17\Engine\Binaries\Win64\UE4Editor.exe
  C:\PATH_TO_MY_PROJECT.uproject /Game/ThirdPersonCPP/Maps/ThirdPersonExampleMap -server -log -port=8003
  ```

#### 1.2.2. Exemplo Cliente

```sh
C:\Program Files\UE_4.17\Engine\Binaries\Win64\UE4Editor.exe
C:\PATH_TO_MY_PROJECT.uproject 192.168.1.90:8003 -game -log
```

## 2. Executando e configurando o projeto

Para executar o jogo em modo multiplayer utilize o menu principal e acesse a opção `Play` escolhendo as seguintes opções:

- `Number of Players` : Escolha a quantidade de conexões que o projeto recebera.

- `Net Mode`.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer14.webp"
    alt="Figura: Unreal Engine - Multiplayer, Executando várias instâncias do jogo."
    caption="Figura: Unreal Engine - Multiplayer, Executando várias instâncias do jogo."
%}

A seguir vamos implementar as estruturas de controle do game `GameMode`, `GameInstance` e `PlayerController`.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer2.webp"
    alt="Figura: Unreal Engine - Multiplayer, Implementando estruturas de controle."
    caption="Figura: Unreal Engine - Multiplayer, Implementando estruturas de controle."
%}

Criando o `GameInstance`.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer3.webp"
    alt="Figura: Unreal Engine - Multiplayer, Implementando a GameInstance."
    caption="Figura: Unreal Engine - Multiplayer, Implementando a GameInstance."
%}

Implementando o evento *OpenMenu*.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer5.webp"
    alt="Figura: Unreal Engine - Multiplayer, Implementando a chamada do menu do jogo."
    caption="Figura: Unreal Engine - Multiplayer, Implementando a chamada do menu do jogo."
%}

Configurando o projeto com GameInstance.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer4.webp"
    alt="Figura: Unreal Engine - Multiplayer, Configurando a Gameinstance."
    caption="Figura: Unreal Engine - Multiplayer, Configurando a Gameinstance."
%}

## 3. Implementando o menu

Implementando os mapas.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer1.webp"
    alt="Figura: Unreal Engine - Multiplayer, Menu."
    caption="Figura: Unreal Engine - Multiplayer, Menu."
%}

Implementando a lógica de chamada do menu no level *Menu* utilizando o `Open Level Blueprints`.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer6.webp"
    alt="Figura: Unreal Engine - Multiplayer, Chamando o menu com BeginPlay."
    caption="Figura: Unreal Engine - Multiplayer, Chamando o menu com BeginPlay."
%}

Implementando o `Widget` WBP_Menu.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer8.webp"
    alt="Figura: Unreal Engine - Multiplayer, Implementando o Widget para o Menu."
    caption="Figura: Unreal Engine - Multiplayer, Implementando o Widget para o Menu."
%}

Implementando os seguintes elementos do menu.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer9.webp"
    alt="Figura: Unreal Engine - Multiplayer, Adicionando botões no menu."
    caption="Figura: Unreal Engine - Multiplayer, Adicionando botões no menu."
%}

Implementar os eventos para instanciar uma conexão.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer11.webp"
    alt="Figura: Unreal Engine - Multiplayer, Lógica Blueprint para criar uma conexão no servidor remoto."
    caption="Figura: Unreal Engine - Multiplayer, Lógica Blueprint para criar uma conexão no servidor remoto."
%}

Conectar ao servidor utilizando IP.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer10.webp"
    alt="Figura: Unreal Engine - Multiplayer, Lógica Blueprint para criar uma conexão no servidor remoto por IP."
    caption="Figura: Unreal Engine - Multiplayer, Lógica Blueprint para criar uma conexão no servidor remoto por IP."
%}

### 3.1. Executando o jogo

- Number of Players: Quantidade de conexões

- Net Mode:
{% include imagelocal.html
    src="unreal/multiplayer/multiplayer14.webp"
    alt="Figura: Unreal Engine - Multiplayer, Play As Listen Server."
    caption="Figura: Unreal Engine - Multiplayer, Play As Listen Server."
%}

  - `Play Offline` - Executa o jogo em modo offline;  

  - `Play As Listen server` - Executa o jogo (tela principal) em modo servidor;  

  - `Play As Client` - Executa o jogo (tela principal) em modo Cliente, iniciando a servidor em outra janela.

- Adicionar dois `PlayerStart`.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer12.webp"
    alt="Figura: Unreal Engine - Multiplayer, Dois PlayerStart."
    caption="Figura: Unreal Engine - Multiplayer, Dois PlayerStart."
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

"Replicar Movimento" funciona apenas para um componente raiz. Para este recurso, `StaticMeshComponent` deve ser escolhido como "root".  

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
    alt="Figura: Unreal Engine - Multiplayer,Static Mesh para o jogo."
    caption="Figura: Unreal Engine - Multiplayer,Static Mesh para o jogo."
%}

O componente atachado também deverá ser replicado.  

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer24.webp"
    alt="Figura: Unreal Engine - Multiplayer, Component Replication."
    caption="Figura: Unreal Engine - Multiplayer, Component Replication."
%}

### 5.1. Implementando a manipulação do objeto pelo personagem

Eventos de entrada de dados (INPUT).

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer15.webp"
    alt="Figura: Unreal Engine - Multiplayer, Lógica Blueprint chamando a ação de segurar."
    caption="Figura: Unreal Engine - Multiplayer, Lógica Blueprint chamando a ação de segurar."
%}

Evento *AcaoDeSegurar*.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer16.webp"
    alt="Figura: Unreal Engine - Multiplayer, Lógica Blueprint do evento AcaoDeSegurar."
    caption="Figura: Unreal Engine - Multiplayer, Lógica Blueprint do evento AcaoDeSegurar."
%}

Evento *AcaoDeSegurar* continuação.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer17.webp"
    alt="Figura: Unreal Engine - Multiplayer, Lógica Blueprint do evento AcaoDeSegurar continuação."
    caption="Figura: Unreal Engine - Multiplayer, Lógica Blueprint do evento AcaoDeSegurar continuação."
%}

Agarrar objeto, este evento prende o objeto ao personagem.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer19.webp"
    alt="[Figura: Unreal Engine - Multiplayer, Lógica Blueprint do evento para prender o objeto."
    caption="[Figura: Unreal Engine - Multiplayer, Lógica Blueprint do evento para prender o objeto."
%}

Evento *Segurando*, este evento utiliza o event tick para alterar a posição do objeto preso ao personagem.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer18.webp"
    alt="Figura: Unreal Engine - Multiplayer, Lógica Blueprint do evento para alterar a posição do objeto preso ao personagem."
    caption="Figura: Unreal Engine - Multiplayer, Lógica Blueprint do evento para alterar a posição do objeto preso ao personagem."
%}

Soltando objeto.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer20.webp"
    alt="Figura: Unreal Engine - Multiplayer, Lógica Blueprint do evento para soltar o objeto."
    caption="Figura: Unreal Engine - Multiplayer, Lógica Blueprint do evento para soltar o objeto."
%}

Ação de arremessar o objeto.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer22.webp"
    alt="Figura: Unreal Engine - Multiplayer, Lógica Blueprint da ação que arremessa o objeto."
    caption="Figura: Unreal Engine - Multiplayer, Lógica Blueprint da ação que arremessa o objeto."
%}

Adicionando o objeto simulando um arremesso.

{% include imagelocal.html
    src="unreal/multiplayer/multiplayer21.webp"
    alt="Figura: Unreal Engine - Multiplayer, Lógica Blueprint simulando o arremesso."
    caption="Figura: Unreal Engine - Multiplayer, Lógica Blueprint simulando o arremesso."
%}
