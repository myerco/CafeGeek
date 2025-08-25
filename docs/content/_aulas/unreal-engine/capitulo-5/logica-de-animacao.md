---
title: Lógica de animação
excerpt: Em este capítulo iremos implementar várias animações utilizando um eixo de movimentação utilizando o elemento e editor Blend space 1D e Blend space.
categories: 
  - "unreal-engine"
  - "capitulo-5"
date: 2024-07-04T08:48:05-04:00
order: 504
tags:
  - Animação
  - Blend space
  - Amingraph
  - Aim offset
  - Layered Blend per bone
  - Layered Blend by bool
sidebar:
  nav: unreal-engine  
---

## 1. O que é Blend Space?

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-blend-space.webp"
    alt="Figura: Blend Space"
    caption="Figura: Editor de animações."
%}

O objetivo do `Blend Space` é reduzir a necessidade de criar nós individuais codificados para mesclar animações com um editor que realiza a mesclagem com base em propriedades ou condições específicas. Permitindo que o animador ou programador especifique as entradas, as animações e como as entradas são usadas para mesclar entre as animações, virtualmente qualquer tipo de mesclagem pode ser executado usando o Blend Space.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-blend-1d.webp"
    alt="Figura: Blend Space 1D."
    caption="Figura: Para carregar o editor de animação na horizontal usamos o menu de contexto Animation > Blend Space 1D e em seguida selecionamos o esqueleto base das animações."
%}

**Informação:** Nos próximos passos vamos criar várias sequencias de animações para o personagem BP_Human.
{: .notice--info}

## 2. Blend Space 1D

Os Blend Spaces também podem ser criados em um formato unidimensional, conhecido como `Blend Space 1D`. Eles podem se misturar entre qualquer número de poses ou animações, mas o fazem com base em um único valor de entrada. Um exemplo de caso de uso para um`Blend Space 1D` seria quando você tem um personagem que se orienta automaticamente na direção em que está se movendo. Se o personagem não pode se desviar ou se mover em várias direções, um Blend Space 1D pode ser usado para se misturar de um Idle a um Walk e, finalmente, a Run com base em um único valor de Speed (como mostrado no exemplo abaixo).

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-blend-space-1D.webp"
    alt="Figura: Editor Blend Space 1D."
    caption="Figura: Utilizamos este elemento quando temos somente um parâmetro para controle da mudança de animações, neste caso o eixo horizontal com o parâmetro Speed."
%}

## 3. Implementando os personagens

A seguir os parâmetros para o personagem Human:

Nome do arquivo: **BS_Human1D**;

Sequencia de animação: Arraste as animações para o sequenciador conforme o parâmetro `Speed`;

`Horizantal Axis`: Speed;

`Maximum Axis Value`: 600 (Velocidade máxima de corrida do personagem);

`Interpolation Time`: 0.25.

Altere esse valor gradativamente para melhorar a mudança de estados.

Para acompanhar o movimentação pressione Shift + LMB e arrastre o mouse.

**Nota:** Alteramos o nome do parâmetro para Speed com a finalidade de facilitar a identificação dentro da lógica de programação Blueprint que usaremos posteriormente.
{: .notice--warning}

Parâmetros para o personagem Mutant.

Nome do arquivo: **BS_Mutant**

`Horizontal Axis`

- `Name` : Speed

- `Maximum axis value` : 220

- `Interpolation time` : 0.5

Para criar a movimentação no eixo horizontal vamos arrastar os elementos apresentados em `Asset Browser` para a linha do tempo.

- Mutant_Idle em tempo 0;  

- Mutant_Walking em tempo 110;  

- Mutant_Run em tempo 220;  

### 3.1. Vídeo Animation Blend Space 1D

{% include video id="arRhm3KRUR0" provider="youtube" %}

## 4. Blend Space

Este elemento é utilizado quanto existem dois parâmetros para controle das animações por exemplo: Direction/Direção e Speed/Velocidade.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-blend-space.webp"
    alt="Figura: Editor Blend Space."
    caption="Figura: Menu de contexto Animation > Blend Space."
%}

Salve o objeto com o nome do arquivo `BS_Human` e em Sequencia de animação arraste as animações para o sequenciador conforme o parâmetro `Speed` e `Direction`;

`Horizontal Axis`: Direction

- `Minimum Axis Value`: -180;

- `Maximum Axis Value`: 180 (A direção do personagem varia entre esses valores);

`Vertical Axis`: Speed

- `Minimum Axis Value`: 0;

- `Maximum Axis Value`: 600 (Velocidade do personagem);

**Informação:** Alteramos os nomes dos parâmetros para Speed e Direction com a finalidade de facilitar a identificação dentro da lógica de programação **Blueprint** que usaremos posteriormente.
{: .notice--info}

## 5. O que é Animation Blueprint?

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-animation-blueprint-main.webp"
    alt="Figura: Animation Blueprint Editor."
    caption="Figura: Animação e Blueprint."
%}

É um **Blueprint** especializado que controla a animação de uma malha esquelética. Os gráficos são editados dentro do `Animation Blueprint Editor`, onde você pode realizar a combinação da animação, controlar diretamente os ossos de um esqueleto ou configurar a lógica que definirá a pose final da animação para uma malha esquelética a ser usada por quadro.

**Informação:** Vamos implementar a lógica de movimentação utilizando o elemento `Animation Blueprint` para os personagens Human e Mutant.
{: .notice--info}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-animation-blueprint.webp"
    alt="Figura: Menu contexto Animation > Animation Blueprint."
    caption="Figura: Para criar o objeto ABP_Human utilizamos o menu de contexto."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-editor-graph.webp"
    alt="Figura: Editor Animmation Blueprint MyBlueprint."
    caption="Figura: A aba MyBlueprint apresenta a organização do editor."
%}

O Editor é separado em `AnimGraph` e `EventGraph`, onde o primeiro implementa a lógica de nós de sequencias de animação e o segundo a lógica de programação **Blueprint**.

## 6. Estados de maquina ou State Machine

Uma máquina de estados representa uma sequencie lógica de estados associados a uma animação.

O nó `Output Pose` é o estado ou pose final da animação. A seguir vamos criar vários nós e a sua lógica.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-human-state-base.webp"
    alt="Figura: Animation graphs Output Pose."
    caption="Figura: No editor Animation Graphs crie o estado Base com Add new state;"
%}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-human-blendspace-1d-state.webp"
    alt="Figura: Idle/Walk/Run."
    caption="Figura: Dentro do nó criado adicionaremos um novo estado com Add State com o nome Idle/Walk/Run."
%}

## 7. Blend Space e State Machine

Para exemplificar vamos apresentar os dois métodos de Blend Space com o personagem Humano mas antes vamos adicionar a lógica para implementar as variáveis `Speed` e `Direction` que servirão como parâmetros para as animações.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-blueprint-direction-speed.webp"
    alt="Figura: Animation Blueprint -Speeed e Direction."
    caption="Figura: No gráfico de eventos ou EventGraph vamos adicionar o seguinte código.."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-human-blendspace-1d-animation.webp"
    alt="Figura: Blend Space 1D dentro do State."
    caption="Figura: Criado anteriormente, BS_Human1D recebe como parâmetro Speed dentro do nó Idle/Walk/Run."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-human-blendspace-state.webp"
    alt="Figura: Blend Space."
    caption="Figura: Nó Idle/Walk/Run adicionamos BS_Human que recebe como parâmetro Speed e Direction pois trabalha com duas coordenadas."
%}

Para os passos posteriores vamos utilizar o BS_Human (Blend Space).

### 7.1. Exemplo de um personagem saltando

Para simular o salto do personagem vamos adicionar os seguintes estados e em seguida fazer as suas conexões.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-state-jump.webp"
    alt="Figura: Sequencia de estados do personagem."
    caption="Figura: Iniciando em Idle/Walk/Run e logo em seguida os estados para simulação do salto."
%}

**Nota:** A animação de salto pode ser dividida em Início de Salto (Jump_Start), Salto no Ar (Jump_Loop) e Finalização do Salto (Jump_End), pois o personagem pode se manter na aminação de Salto no Ar dependendo da altura.
{: .notice--warning}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-state-jump-start.webp"
    alt="Figura: State Jump Start"
    caption="Figura: Em Jump_Start adicionamos a animação S_Human_Jump_Start iniciando a animação de salto."
%}

Repetimos a operação para os outros estados adicionando as animações :

- S_Human_Jump_Loop;

- S_Human_Jump_End;

Na condição de controle de fluxo entre `Idle/Walk/Run` e `Jump_Start` vamos utilizar a variável `InAir` e testar se o valor é `True`.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-state-jump-start-inair.webp"
    alt="Figura: Animação de personagem permanecendo no ar."
    caption="Figura: State Jump Start InAir."
%}

Na condição de controle de fluxo entre `Jump_End` e `Idle/Walk/Run` vamos utilizar a variável `InAir` e testar se o valor não é `True`.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-state-jump-start-not-inair.webp"
    alt="Figura: Início da animação."
    caption="Figura: Figura: Início da animação."
%}

Na condição de controle de fluxo entre `Jump_Start` e `Jump_Loop` vamos utilizar a função `Current Time (Ratio) (S_Jump_Start)`. Esta função retorna a proporção de tempo atual da sequência e se o valor for menor 0.1 (10%) de tempo para acabar deve ser feito a transição para outro nó.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-state-jump-start-end-time.webp"
    alt="Figura: Animação e Current Time. "
    caption="Figura: State Condition Current Time (Ratio)."
%}

Na condição de controle de fluxo entre `Jump_End` e `Idle/Walk/Run` vamos utilizar a função `Current Time (Ratio) (S_Jump_End)` com a mesma lógica do nó descrito anteriormente.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-state-jump-end-time.webp"
    alt="Figura: Animação de final do salto."
    caption="Figura: State Condition Current Time (Ratio) Jump End."
%}

Devemos considerar que o salto depende se o personagem esta em queda e se a função `Jump` foi acionado na lógica da classe do personagem, neste casso `BP_Human`.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-blueprint-jump.webp"
    alt="Figura: Exemplo da Classe BP e a Função Jump."
    caption="Figura: InputAction Jump associado aos nós Jump e Stop Jumping."
%}

### 7.2. Implementado Animation Blueprint utilizando o Mutante

Usamos o menu de contexto `Animation > Animation Blueprint` para criar ABP_Mutant.

Agora vamos copiar todos os nos do `Event Graph` de `ThirdPerson_AnimBP` para o componente criado, logo em seguida arrastre o elemento BS_Mutant para `AnimGraph`.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animations-bs-mutant-graph.webp"
    alt="Figura: Animação do mutante."
    caption="Figura: AnimGraph BS_Mutant."
%}

### 7.3. Vídeo Animation Blueprint do Mutante

{% include video id="a2JULC4-P1o" provider="youtube" %}

## 8. Implementando a Corrida

Em este passo iremos implementar a corrida do personagem. Vamos configura o evento `Left Shift` para alterar a propriedade `Max Walk Speed` do componente `CharacterMomement` com os valores 220 para velocidade máxima e 110 para caminhada.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-blueprint-running.webp"
    alt="Figura: Implementando a corrida do mutante."
    caption="Figura: Blueprint running."
%}

### 8.1. Vídeo Implementando a corrida do mutante

{% include video id="k6tGHVm2BNQ" provider="youtube" %}

## 9. Animation Montage

Uma `Animation Montage` ou montagem de animação (ou montagem, para abreviar) fornece uma maneira de controlar um ativo de animação diretamente por meio do código Blueprint ou C ++. Com uma montagem de animação, você pode combinar várias sequências de animação diferentes em um único ativo que você pode dividir em seções para reprodução individualmente ou em combinação. Você também pode disparar eventos dentro de uma montagem que pode executar uma variedade de tarefas locais ou replicadas, como tocar sinais de som ou efeitos de partículas, alterar valores do jogador como contagem de munição ou até mesmo replicar o movimento raiz em jogos em rede (desde que o movimento raiz esteja ativado na animação).

Em este passo utilizaremos o `Animation Montage` para montar as animações de ataque esquerda e direita.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-montage.webp"
    alt="Figura: Animation Montage para o ataque."
    caption="Figura: Menu de contexto Animation > Animation Montage."
%}

Vamos baixar e instalar os arquivos Mutant_Punch.fbx e Mutant_Swipping do site [https://mixano.com](https://mixano.com) para animar ataque direita e ataque esquerda.

[![Mixano](/assets/images/unreal/animacao/mixamo-2-0-logo.webp)](https://www.mixamo.com/)
{: style="margin-top: 0.5em;"}

No editor de animação arrastre as animações para a linha de tempo. Observe que cada animação ocupa uma raia ou slot dentro de uma seção;

Adicione um novo slot de nome `Attack` e salve;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-montage-attack.webp"
    alt="Figura: Animation Montage para o ataque 2."
    caption="Figura: Selecione o novo slot em Montage > DefaultGroup.Attack e salve toda animação."
%}

### 9.1. Vídeo montando Animação de ataque

{% include video id="Kufu78tu9EE" provider="youtube" %}

## 10. AnimGraph

AnimGraph utiliza o conceito de máquinas de estado que fornecem uma maneira gráfica de quebrar a animação de uma malha esquelética em uma série de estados. Esses estados são então governados por Regras de transição que controlam como combinar de um estado para outro.

O processo de design para animação `Skeletal Mesh` se torna mais simples, pois você pode criar um gráfico que controla facilmente como seus personagens podem fluir entre os tipos de animação sem ter que criar uma rede **Blueprint** complexa.

**Informação:** Em este passo utilizaremos a lógica de programação com AnimGraph para combinar e programar a lógica de mudanças de estado ou poses.
{: .notice--info}

A seguir vamos criar os nós dentro do gráfico de estados para simular a animação básica.

Vamos adicionar um novo estado `Add New State Machine` com nome *BasicLocomotion*, este estado dever conter a animação criadas anteriormente com o Blend space 1D, BS_Mutant.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animgraph-basiclocomotion.webp"
    alt="Figura: AnimGraph BasicLocomotion."
    caption="Figura: Conectamos o nó em Output Pose substituindo os estados anteriores se existirem;."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animgraph-idle-walk-run.webp"
    alt="Figura: AnimGraph Idle/Walk/Run - Animação para andar, correr e parado."
    caption="Figura: Arrastamos e colamos BS_Mutant para a AnimGraph e renomeamos o nó para Idle/Walk/Run pois ele contem essas animações."
%}

Em este estado passamos como parâmetro a variável `Speed` para animação BS_Mutant;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animgraph-speed.webp"
    alt="Figura: Animação para corrida, AnimGraph Speed."
    caption="Figura: Conectando a variável Speed em BS_Mutant."
%}

## 11. Salvando estados e poses

Neste passo vamos implementar a animação de ataque com soco de direita e esquerda, salvando poses e passar de um estado para outro.

`New Save cached Pose...` - Salva o estado acionando o menu de contexto dentro do `AnimGraph`;

`Use cached pose BasicLocomotion` - Acessa um estado salvo anteriormente.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animgraph-attack.webp"
    alt="Figura: Animação de ataque com AnimaGraph Attack."
    caption="Figura: Podemos usar vários nós salvos de estados anteriores."
%}

`Slot DefaultGroup` - Associamos a montagem de animação `AM_Mutant_Attack` na qual definimos a sequencia de ataque usando o menu de context;

Selecionando o Slot criado atualizamos `Slot Name` para `DefaultGroup.Attack` para acessar a sequencia de animação.

Agora vamos implementar a lógica para chamar as animações quando forem pressionados os botões do mouse direito e esquerdo.

No objeto BP_Mutant adicione os eventos de chamada de função e associe a função `Play Anim Montage`.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animations-blueprint-attack.webp"
    alt="Figura: Blueprint para chamar a animação de ataque."
    caption="Figura: Ao acionar os botões do mouse é executada a animação."
%}

### 11.1. Vídeo montando o ataque

{% include video id="Ss22A7xrtCQ" provider="youtube" %}

## 12. Layered Blend per bone

Em este passo iremos continuar com a programação `AnimGraph` para fazer o personagem correr e atacar ao mesmo tempo, para isso vamos misturar os ossos das animações utilizando `Layered Blend per Bone`.

Podemos misturar várias animações no nó de estado e utilizar um osso (bone) como referência, no exemplo abaixo misturamos a animação básica `LocoCache`com `AttackingCache` adicionando o osso `Spine`.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animgraph-attack-simple.webp"
    alt="Figura: Unreal Engine - Animação - Layered Blend per bone."
    caption="Figura: Usando o nó para misturar duas poses."
%}

## 13. Layered Blend by bool

Neste passo vamos misturar as animações condicionando a uma variável para que possamos definir o estado do personagem, correndo ou parado.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animgraph-blend-by-bool.webp"
    alt="Figura: Unreal Engine - Animação - Layered Blend by bool."
    caption="Figura: Podemos condicionar a mistura de animações utilizando valores condicionais boolean."
%}

No `Event Graph` de `ABP_Mutant` adicionamos a lógica para verificar se o personagem esta me movimentando testando a variável `Speed`.

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-blueprint-animation-moving.webp"
    alt="Figura:Animação - Layered Blend by bool."
    caption="Figura: Definindo uma variável de controle Moving."
%}

### 13.1. Vídeo do personagem correndo e atacando

{% include video id="1gjkcrU7pmA" provider="youtube" %}

## 14. Aim Offset

Um Aim Offset é um recurso que armazena uma série de poses que podem ser combinadas para ajudar um personagem a apontar uma arma. Durante a animação, o resultado do Aim Offset é misturado com outros movimentos, como correr, caminhar, pular, etc. para fazer com que o personagem pareça olhar suavemente em todas as direções.

### 14.1. Animation Starter Pack

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-animation-starter-pack.webp"
    alt="Figura: Adicionando o pacote Animation Starter Pack."
    caption="Figura: A Epic Store oferece um pacote de animações para o Mannequin, facilitando a prototipação do personagem utilizando armas de tiro.."
%}

### 14.2. Preparando o projeto

Neste passo vamos criar várias animações com o personagem mirando utilizando a animação `Aim_Space_hip` como base. Estas animações servem de referência para realizar a interpolação.

**1.** Crie as pastas para organizar o projeto:

```bash
/Maps/Shooter
/Characters/Shooter
/Characters/Shooter/Animations
```

**2.** Mova o arquivo `/AnimStarterPack/Aim_Space_hip` para a pasta `/Characters/Shooter/Animations`

**3.** Duplique o arquivo várias vezes `Aim_Space_hip` e renomeio para os seguintes nomes:

- `Aim_Center`;

- `Aim_Center_Up`;

- `Aim_Center_Down`;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-aim-offset-editor.webp"
    alt="Figura: Editor Aim Offset."
    caption="Figura: Editando a animação para criar novas animações."
%}

### 14.3. Removendo frames

Vamos remover frames antes e depois da pose final que estamos querendo obter.

  1. Posicione no frame 0;

  2. Clicando com o botão direito do mouse na barra de tempo, escolha `Remove from frame N1 to frame N2`;

  3. Onde N1 é  o Início e N2 é o final.

| Arquivo         |Início | Antes     |Depois   |
|:-               |:-:    |:-:        |:-:      |  
|Aim_Center       | 0     |1-87       |         |
|Aim_Center_Up    | 0     |0-10       |1-78     |
|Aim_Center_Down  | 0     |0-20       |1-68     |
|Aim_Left_Center  |30     |0 - 30     |1 - 57   |
|Aim_Left_Up      |40     |0 - 40     |1 - 48   |
|Aim_Left_Down    |50     |0 - 50     |1 - 37   |
|Aim_Right_Center |60     |0 - 60     |1 - 27   |
|Aim_Right_Up     |70     |0 - 70     |1 - 17   |
|Aim_Right_Down   |80     |0 - 80     |1 - 8    |

Edite a propriedade de vária animações ao mesmo tempo

![Unreal Engine](https://docs.unrealengine.com/4.26/Images/AnimatingObjects/SkeletalMeshAnimation/AnimHowTo/AimOffset/AimOffset20.webp)

`AdditiveSettings`:

- Additive Anim Type : Mesh Space;

- Base Pose Type : Idle_Rifle_Hip.

Agora vamos criar `Aim Offset` Menu de contexto `Animation > Aim Offset` ou Escolha o esqueleto do Mannequin e utilizando BMP escolha `Create > Aim Offset`;

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-create-aim-offset.webp"
    alt="Figura: Editor Aim Offset."
    caption="Figura: Altere os parâmetros em Asset Details para os seguintes valores:"
%}

Coordenadas horizontais - Horizontal Axis:

- Name : Yaw

- Minimun Axis Value : -90

- Maximun Axis Value : 90

Coordenadas Verticais - Vertical Axis:

- Name : Pitch

- Minimun Axis Value : -90

- Maximun Axis Value : 90

Adicione as animações que foram preparadas anteriormente na janela Offset considerando a ordem dos eixos e movimentação.

|Animação         |Posição            |
|:-               |:-                 |
|Aim_Center       |Centro             |
|Aim_Left_Center  |Centro Esquerda    |

Continue adicionando as animações nas coordenadas.

{% include image.html
    src="https://docs.unrealengine.com/4.26/Images/AnimatingObjects/SkeletalMeshAnimation/AnimHowTo/AimOffset/AimOffset29.webp"
    alt="Figura: Aim exemplo de coordenadas."
    caption="Figura: Coordenadas Yaw e Pitch."
    ref="https://docs.unrealengine.com/4.27/en-US/AnimatingObjects/SkeletalMeshAnimation/AnimHowTo/AimOffset/"
%}

## 15. Misturando animações

A seguir vamos apresentar o fluxo e a lógica do personagem Mannequim que utiliza dois tipos de estado, com arma e sem arma.

{% include iframe.html
    src="https://blueprintue.com/render/4qdfogtg/"
    title="Cafegeek - Animation BP State Base e Weapon"
    caption="Figura: Lógica do Animation Blueprint, carregando e atualizando variáveis."
    ref="https://blueprintue.com/render/4qdfogtg/"
%}

### 15.1. Variáveis do personagem

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-logic-variables-local.webp"
    alt="Figura: My Blueprint - Variáveis."
    caption="Figura: Valores para controle de velocidade e estados do personagem."
%}

### 15.2. Inicialização de variáveis

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-logic-initialize.webp"
    alt="Figura: Event Blueprint Initialize Animation."
    caption="Figura: Inicializa a variável Character Movement."
%}

### 15.3. Atualizando a animação

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-logic-update-animation.webp"
    alt="Figura: Event Blueprint Update Animation."
    caption="Figura: Se o objeto BP_Mannequin estiver instanciado determina o seu fluxo de eventos."
%}

#### 15.3.1. Calculando velocidade e direção

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-logic-velocity-direction.webp"
    alt="Figura: Velocity e Direction."
    caption="Figura: Defina Velocity e GroundSpeed a partir da velocidade dos componentes de movimento. A velocidade do solo é calculada apenas a partir dos eixos X e Y da velocidade, portanto, mover para cima ou para baixo não a afeta."
%}

#### 15.3.2. Limitando a velocidade e queda

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-logic-move-falling.webp"
    alt="Figura: GetCurrentAcceleration e IsFalling."
    caption="Figura: Define ShouldMove como verdadeiro somente se a velocidade do solo estiver acima de um pequeno limite (para evitar que velocidades incrivelmente pequenas acionem animações) e se houver aceleração (entrada) aplicada no momento. Define IsFalling como verdadeiro determinado pela função IsFalling."
%}

#### 15.3.3. Atualizando as variáveis de controle de estados

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-logic-update-action.webp"
    alt="Figura: Get BP_Mannequin."
    caption="Figura: Atualiza as variáveis que determinam os estados das animações."
%}

#### 15.3.4. Levantando a arma para mirar

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-logic-aim.webp"
    alt="Figura: AimPitch e AimYaw."
    caption="Figura: Atualiza as variáveis limitando o angulo de rotação em -90 e 90 graus."
%}

### 15.4. State Machines

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-state-base.webp"
    alt="Figura: Base Pose."
    caption="Figura: Animação base do personagem."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-state-base-2.webp"
    alt="Figura: Base - Event Graph."
    caption="Figura: Eventos da animação básica."
%}

#### 15.4.1. Weapon Base

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-state-2.webp"
    alt="Figura: Weapon Hip e Weapon Aim - Event Graph ."
    caption="Figura: Eventos com animações do personagem segurando uma arma e mirando."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-state-weapon-base.webp"
    alt="Figura: WeaponBase."
    caption="Figura: Evento AimOffset Player com seus parâmetros e Blend Poses by Bool para alternar entre uma pose ou outra."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-state-weapon-equip-reload.webp"
    alt="Figura: WeaponEquip."
    caption="Figura: Utilizamos Layered Blend per Bone para mesclar as animações a partir de um determinado osso."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-state-weapon-details-layered-per-bone.webp"
    alt="Figura: Details > Layered blend per bone."
    caption="Figura: Configuramos o objeto para utilizar o osso Spine_01 pois no caso do mannequim ele é o osso da cintura que queremos usar como referência para mistura de animações."
%}

### 15.5. Pose final

{% include imagelocal.html
    src="unreal/animacao/unreal-engine-abp-state-weapon-final.webp"
    alt="Figura: Output Pose."
    caption="Figura: Podemos usar várias opções em sequência para construir o estado final da animação."
%}
