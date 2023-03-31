---
title: Lógica de animação
excerpt: Em este capítulo iremos implementar várias animações utilizando um eixo de movimentação utilizando o elemento e editor Blend space 1D e Blend space.
permalink: /pages/unreal_engine/animacao_logica
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true 
---

## 1. O que é Blend Space?

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_blend_space.webp"
    alt="Figura: Blend Space"
    caption="Editor de animações."
%}

O objetivo do `Blend Space` é reduzir a necessidade de criar nós individuais codificados para mesclar animações com um editor que realiza a mesclagem com base em propriedades ou condições específicas. Permitindo que o animador ou programador especifique as entradas, as animações e como as entradas são usadas para mesclar entre as animações, virtualmente qualquer tipo de mesclagem pode ser executado usando o Blend Space.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_blend_1d.webp"
    alt="Figura: Unreal Engine - Menu de contexto Animation > Blend Space 1D."
    caption="Para carregar o editor de animação na horizontal usamos o menu de contexto Animation > Blend Space 1D e em seguida selecionamos o esqueleto base das animações."
%}

**Informação:** Nos próximos passos vamos criar várias sequencias de animações para o personagem BP_Human.
{: .notice--info}

***

## 2. Blend Space 1D

Os Blend Spaces também podem ser criados em um formato unidimensional, conhecido como `Blend Space 1D`. Eles podem se misturar entre qualquer número de poses ou animações, mas o fazem com base em um único valor de entrada. Um exemplo de caso de uso para um`Blend Space 1D` seria quando você tem um personagem que se orienta automaticamente na direção em que está se movendo. Se o personagem não pode se desviar ou se mover em várias direções, um Blend Space 1D pode ser usado para se misturar de um Idle a um Walk e, finalmente, a Run com base em um único valor de Speed (como mostrado no exemplo abaixo).

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_Blend_Space_1D.webp"
    alt="Figura: Editor Blend Space 1D."
    caption="Utilizamos este elemento quando temos somente um parâmetro para controle da mudança de animações, neste caso o eixo horizontal com o parâmetro Speed."
%}

***

## 3. Implementando os personagens

A seguir os parâmetros para o personagem Human:

- Nome do arquivo: BS_Human1D;

- Sequencia de animação: Arraste as animações para o sequenciador conforme o parâmetro `Speed`;

- `Horizantal Axis`: Speed;

- `Maximum Axis Value`: 600;

  - (Velocidade máxima de corrida do personagem);

- `Interpolation Time`: 0.25.

  - Altere esse valor gradativamente para melhorar a mudança de estados.

Para acompanhar o movimentação pressione Shift + LMB e arrastre o mouse.

**Nota:** Alteramos o nome do parâmetro para Speed com a finalidade de facilitar a identificação dentro da lógica de programação Blueprint que usaremos posteriormente.
{: .notice--warning}

Parâmetros para o personagem Mutant.

- Nome do arquivo: BS_Mutant

- `Horizontal Axis`

  - `Name` : Speed

  - `Maximum axis value` : 220

  - `Interpolation time` : 0.5

Para criar a movimentação no eixo horizontal vamos arrastar os elementos apresentados em `Asset Browser` para a linha do tempo.

- Mutant_Idle em tempo 0;  

- Mutant_Walking em tempo 110;  

- Mutant_Run em tempo 220;  

### 3.1. Vídeo Animation Blend Space 1D

{% include video.html
    link="https://youtu.be/arRhm3KRUR0"
    src="https://img.youtube.com/vi/arRhm3KRUR0/0.jpg"
    alt="Vídeo: Unreal Engine - Animation Blend Space 1D."
    caption="Unreal Engine Animação - 04 Blend Space 1D."
%}

***

## 4. Blend Space

Este elemento é utilizado quanto existem dois parâmetros para controle das animações por exemplo: Direction/Direção e Speed/Velocidade.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_Blend_Space.webp"
    alt="Figura: Unreal Engine - Editor Blend Space."
    caption="Menu de contexto Animation > Blend Space."
%}

- Nome do arquivo: BS_Human;

- Sequencia de animação: Arraste as animações para o sequenciador conforme o parâmetro `Speed` e `Direction`;

- `Horizontal Axis`: Direction;

- `Minimum Axis Value`: -180;

- `Maximum Axis Value`: 180 (A direção do personagem varia entre esses valores);

- `Vertical Axis`: Speed

- `Minimum Axis Value`: 0;

- `Maximum Axis Value`: 600 (Velocidade do personagem);

**Informação:** Alteramos o nome do parâmetro para Speed com a finalidade de facilitar a identificação dentro da lógica de programação **Blueprint** que usaremos posteriormente.
{: .notice--info}

***

## 5. O que é Animation Blueprint?

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_animation_blueprint_main.webp"
    alt="Figura: Unreal Engine - Animação e Blueprint."
    caption="Figura: Unreal Engine - Animação e Blueprint."
%}

É um **Blueprint** especializado que controla a animação de uma malha esquelética. Os gráficos são editados dentro do `Animation Blueprint Editor`, onde você pode realizar a combinação da animação, controlar diretamente os ossos de um esqueleto ou configurar a lógica que definirá a pose final da animação para uma malha esquelética a ser usada por quadro.

Vamos implementar a lógica de movimentação utilizando o elemento Animation Blueprint para os personagens Human e Mutant.

### 5.1. Implementado Animation Blueprint utilizando o Humano

O Editor é separado em `AnimGraph` e `EventGraph`, onde o primeiro implementa a lógica de nós de sequencias de animação e o segundo a lógica de programação **Blueprint**.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_animation_blueprint.webp"
    alt="Figura: Menu contexto Animation > Animation Blueprint."
    caption="Para criar o objeto ABP_Human utilizamos o menu de contexto."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_editor_graph.webp"
    alt="Figura: Unreal Engine - Editor Animmation Blueprint MyBlueprint."
    caption="A aba MyBlueprint apresenta a organização do editor."
%}

***

## 6. Estados de maquina ou State Machine

Uma máquina de estados representa uma sequencie lógica de estados associados a uma animação.

O nó `Output Pose` é o estado ou pose final da animação. A seguir vamos criar vários nós e a sua lógica.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_human_state_base.webp"
    alt="Figura: Animation graphs Output Pose."
    caption="No editor Animation Graphs crie um State com Add new state;"
%}

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_human_blendspace_1d_state.webp"
    alt="Figura: Unreal Engine - Add State Idle/Walk/Run."
    caption="Dentro do nó criado adicionaremos um novo estado com Add State com o nome Idle/Walk/Run."
%}

***

## 7. Blend Space e State Machine

Para exemplificar vamos apresentar os dois métodos de Blend Space com o personagem Humano mas antes vamos adicionar a lógica para implementar as variáveis `Speed` e `Direction` que servirão como parâmetros para as animações.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_blueprint_direction_speed.webp"
    alt="Figura: Animation Blueprint -Speeed e Direction."
    caption="No gráfico de eventos ou EventGraph vamos adicionar o seguinte código.."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_human_blendspace_1d_animation.webp"
    alt="Figura: Blend Space 1D dentro do State."
    caption="Criado anteriormente, BS_Human1D recebe como parâmetro Speed dentro do nó Idle/Walk/Run."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_human_blendspace_state.webp"
    alt="Figura: Blend Space 1D dentro do State."
    caption="Nó Idle/Walk/Run adicionamos BS_Human que recebe como parâmetro Speed e Direction pois trabalha com duas coordenadas."
%}

Para os passos posteriores vamos utilizar o BS_Human (Blend Space).

### 7.1. Exemplo de um personagem saltando

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_state_jump.webp"
    alt="Figura: Animação de salto : State Jump."
    caption="Para simular o salto do personagem vamos adicionar os seguintes estados e em seguida fazer as suas conexões."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_state_jump_start.webp"
    alt="Figura: State Jump Start"
    caption="Em Jump_Start adicionamos a animação S_Human_Jump_Start iniciando a animação de salto."
%}

Repetimos a operação para os outros estados adicionando as animações :

- S_Human_Jump_Loop;

- S_Human_Jump_End;

N condição de controle de fluxo entre `Idle/Walk/Run` e `Jump_Start` vamos utilizar a variável `InAir` e testar se o valor é `True`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_state_jump_start_inair.webp"
    alt="Figura: Animação de personagem permanecendo no ar."
    caption="State Jump Start InAir."
%}

Na condição de controle de fluxo entre `Jump_End` e `Idle/Walk/Run` vamos utilizar a variável `InAir` e testar se o valor não é `True`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_state_jump_start_not_inair.webp"
    alt="Figura: Inicio da animação."
    caption="State Jump Start Not InAir."
%}

Na condição de controle de fluxo entre `Jump_Start` e `Jump_Loop` vamos utilizar a função `Current Time (Ratio) (S_Jump_Start)`. Esta função retorna a proporção de tempo atual da sequência e se o valor for menor 0.1 ou 10% de tempo para acabar deve ser feito a transição para outro nó.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_state_jump_start_end_time.webp"
    alt="Figura: Animação e Current Time. "
    caption="State Condition Current Time (Ratio)."
%}

Na condição de controle de fluxo entre `Jump_End` e `Idle/Walk/Run` vamos utilizar a função `Current Time (Ratio) (S_Jump_End)` com a mesma lógica do nó descrito anteriormente.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_state_jump_end_time.webp"
    alt="Figura: Animação de final do salto."
    caption="State Condition Current Time (Ratio) Jump End."
%}

Devemos considerar que o salto depende se o personagem esta em queda e se a função `Jump` foi acionado na lógica da classe do personagem, neste casso `BP_Human`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_blueprint_jump.webp"
    alt="Figura: Exemplo da Classe BP e a Função Jump."
    caption="InputAction Jump associado aos nós Jump e Stop Jumping."
%}

### 7.2. Implementado Animation Blueprint utilizando o Mutante

Usamos o menu de contexto `Animation > Animation Blueprint` para criar ABP_Mutant.

Agora vamos copiar todos os nos do `Event Graph` de `ThirdPerson_AnimBP` para o componente criado, logo em seguida arrastre o elemento BS_Mutant para `AnimGraph`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animations_bs_mutant_graph.webp"
    alt="Figura: Animação do mutante."
    caption="AnimGraph BS_Mutant."
%}

### 7.3. Vídeo Animation Blueprint do Mutante

{% include video.html
    link="https://youtu.be/a2JULC4-P1o"
    src="http://img.youtube.com/vi/a2JULC4-P1o/0.jpg"
    alt="Vídeo: Animação do mutante."
    caption="Unreal Engine Animação - 05 Animation Blueprints."
%}

***

## 8. Implementando a Corrida

Em este passo iremos implementar a corrida do personagem. Vamos configura o evento `Left Shift` para alterar a propriedade `Max Walk Speed` do componente `CharacterMomement` com os valores 220 para velocidade máxima e 110 para caminhada.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_blueprint_running.webp"
    alt="Figura: Implementando a corrida do mutante."
    caption="Blueprint running."
%}

### 8.1. Vídeo Implementando a corrida do mutante

{% include video.html
    link="https://youtu.be/k6tGHVm2BNQ"
    src="http://img.youtube.com/vi/k6tGHVm2BNQ/0.jpg"
    alt="Vídeo: Unreal Engine Animação."
    caption="Unreal Engine Animação - 07 Corrida."
%}

***

## 9. Montando a animação de ataque

Uma `Animation Montage` ou montagem de animação (ou montagem, para abreviar) fornece uma maneira de controlar um ativo de animação diretamente por meio do código Blueprint ou C ++. Com uma montagem de animação, você pode combinar várias sequências de animação diferentes em um único ativo que você pode dividir em seções para reprodução individualmente ou em combinação. Você também pode disparar eventos dentro de uma montagem que pode executar uma variedade de tarefas locais ou replicadas, como tocar sinais de som ou efeitos de partículas, alterar valores do jogador como contagem de munição ou até mesmo replicar o movimento raiz em jogos em rede (desde que o movimento raiz esteja ativado na animação).

Em este passo utilizaremos o `Animation Montage` para montar as animações de ataque esquerda e direita.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_montage.webp"
    alt="Figura: Animation Montage para o ataque."
    caption="Menu de contexto Animation > Animation Montage."
%}

Vamos baixar e instalar os arquivos Mutant_Punch.fbx e Mutant_Swipping do site [https://mixano.com](https://mixano.com) para animar ataque direita e ataque esquerda.

No editor de animação arrastre as animações para a linha de tempo. Observe que cada animação ocupa uma raia ou slot dentro de uma seção;

Adicione um novo slot de nome `Attack` e salve;

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_montage_attack.webp"
    alt="Figura: Animation Montage para o ataque 2."
    caption="Selecione o novo slot em Montage > DefaultGroup.Attack e salve toda animação."
%}

### 9.1. Vídeo montando Animação de ataque

{% include video.html
    link="https://youtu.be/Kufu78tu9EE"
    src="http://img.youtube.com/vi/arRhm3KRUR0/0.jpg"
    alt="Vídeo: Unreal Engine - Animação de ataque.."
    caption="Vídeo: Unreal Engine - Animação de ataque."
%}

***

## 10. Animação básica com AnimGraph

AnimGraph utiliza o conceito de máquinas de estado que fornecem uma maneira gráfica de quebrar a animação de uma malha esquelética em uma série de estados. Esses estados são então governados por Regras de transição que controlam como combinar de um estado para outro.

O processo de design para animação `Skeletal Mesh` se torna mais simples, pois você pode criar um gráfico que controla facilmente como seus personagens podem fluir entre os tipos de animação sem ter que criar uma rede **Blueprint** complexa.

Em este passo utilizaremos a lógica de programação com AnimGraph para combinar e programar a lógica de mudanças de estado ou poses.

A seguir vamos criar um nós dentro do gráfico de estados para simular a animação básica.

### 10.1. BasicLocomotion

Este estado dever conter a animação criadas anteriormente com o Blend space 1D, BS_Mutant.

Vamos adicionar um novo estado `Add New State Machine` com nome *BasicLocomotion*;

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animgraph_basiclocomotion.webp"
    alt="Figura: AnimGraph BasicLocomotion."
    caption="Conectamos o nó em Output Pose substituindo os estados anteriores se existirem;."
%}

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animgraph_idle_walk_run.webp"
    alt="Figura: AnimGraph Idle/Walk/Run - Animação para andar, correr e parado."
    caption="Arrastamos e colamos BS_Mutant para a AnimGraph e renomeamos o nó para Idle/Walk/Run pois ele contem essas animações."
%}

### 10.2. Idle/Walk/Run

Em este estado passamos como parâmetro a variável `Speed` para animação BS_Mutant;

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animgraph_speed.webp"
    alt="Figura: Animação para corrida, AnimGraph Speed."
    caption="Conectando a variável Speed em BS_Mutant."
%}

***

## 11. Animação de ataque com AnimGraph

Neste passo vamos implementar a animação de ataque com soco de direita e esquerda.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animgraph_attack.webp"
    alt="Figura: Animação de ataque com AnimaGraph Attack."
    caption="Podemos usar vários nós salvos de estados anteriores."
%}

Para passar de um estado para outro devemos salvar o estado anterior acionando o menu de contexto `New Save cached Pose...` dentro do `AnimGraph`;

Um estado salvo pode ser acionado com  `Use cached pose BasicLocomotion`, perceba que usamos o nome do estado salvo anteriormente.

Associamos a montagem de animação `AM_Mutant_Attack` na qual definimos a sequencia de ataque usando o menu de context `Slot DefaultGroup`;

Selecionando o Slot criado atualizamos `Slot Name` para `DefaultGroup.Attack` para acessar a sequencia de animação.

Agora vamos implementar a lógica para chamar as animações quando forem pressionados os botões do mouse direito e esquerdo.

No objeto BP_Mutant adicione os eventos de chamada de função e associe a função `Play Anim Montage`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animations_blueprint_attack.webp"
    alt="Figura: Blueprint para chamar a animação de ataque."
    caption="Ao acionar os botões do mouse é executada a animação."
%}

### 11.1. Vídeo montando o ataque

{% include video.html
    link="https://youtu.be/Ss22A7xrtCQ"
    src="http://img.youtube.com/vi/Ss22A7xrtCQ/0.jpg"
    alt="Vídeo: Unreal Engine - Montando o ataque com Animação com AnimGraph."
    caption="Vídeo: Unreal Engine - Montando o ataque com Animação com AnimGraph."
%}

***

## 12. Atacando somente com os braços

Em este passo iremos continuar com a programação `AnimGraph` para fazer o personagem correr e atacar ao mesmo tempo, para isso vamos misturar os ossos das animações utilizando `Layered Blend per Bone`.

`Layered Blend per bone`.

Podemos misturar várias animações no nó de estado e utilizar um osso (bone) como referência, no exemplo abaixo misturamos a animação básica `LocoCache`com `AttackingCache` adicionando o osso `Spine`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animgraph_attack_simple.webp"
    alt="Figura: Unreal Engine - Animação - Layered Blend per bone."
    caption="Usando o nó para misturar duas poses."
%}

***

## 13. Animação de ataque completa e correndo somente os braços

Neste passo vamos misturar as animações condicionando a uma variável para que possamos definir o estado do personagem, correndo ou parado.

`Layered Blend by bool`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animgraph_blend_by_bool.webp"
    alt="Figura: Unreal Engine - Animação - Layered Blend by bool."
    caption="Podemos condicionar a mistura de animações utilizando valores condicionais boolean."
%}

No `Event Graph` de `ABP_Mutant` adicionamos a lógica para verificar se o personagem esta me movimentando testando a variável `Speed`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_blueprint_animation_moving.webp"
    alt="Figura:Animação - Layered Blend by bool."
    caption="Definindo uma variável de controle Moving."
%}

### 13.1. Vídeo do personagem correndo e atacando

{% include video.html
    link="https://youtu.be/1gjkcrU7pmA"
    src="http://img.youtube.com/vi/1gjkcrU7pmA/0.jpg"
    alt="Vídeo: Unreal Engine - Animação do personagem correndo e atacando ao mesmo tempo."
    caption="Vídeo: Unreal Engine - Animação do personagem correndo e atacando ao mesmo tempo."
%}

***

## 14. Aim Offset

Um Aim Offset é um recurso que armazena uma série de poses que podem ser combinadas para ajudar um personagem a apontar uma arma. Durante a animação, o resultado do Aim Offset é misturado com outros movimentos, como correr, caminhar, pular, etc. para fazer com que o personagem pareça olhar suavemente em todas as direções.

### 14.1. Animation Starter Pack

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_starter_pack.webp"
    alt="Figura: Adicionando o pacote Animation Starter Pack."
    caption="A Epic Store oferece um pacote de animações para o Mannequin, facilitando a prototipação do personagem utilizando armas de tiro.."
%}

### 14.2. Preparando o projeto

Neste passo vamos criar várias animações com o personagem mirando utilizando a animação `Aim_Space_hip` como base. Estas animações servem de referência para realizar a interpolação.

1. Crie as pastas para organizar o projeto:

```bash
/Maps/Shooter
/Characters/Shooter
/Characters/Shooter/Animations
```

1. Mova o arquivo `/AnimStarterPack/Aim_Space_hip` para a pasta `/Characters/Shooter/Animations`

1. Duplique o arquivo várias vezes `Aim_Space_hip` e renomeio para os seguintes nomes:

- `Aim_Center`;

- `Aim_Center_Up`;

- `Aim_Center_Down`;

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_aim_offset_editor.webp"
    alt="Figura: Editor Aim Offset."
    caption="Editando a animação para criar novas animações."
%}

### 14.3. Removendo frames

Vamos remover frames antes e depois da pose final que estamos querendo obter.

  1. Posicione no frame 0;

  2. Clicando com o botão direito do mouse na barra de tempo, escolha `Remove from frame N1 to frame N2`;

  3. Onde N1 é  o Inicio e N2 é o final.

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
    src="unreal/animacao/unreal_engine_create_aim_offset.webp"
    alt="Figura: Editor Aim Offset."
    caption="Altere os parâmetros em Asset Details para os seguintes valores:"
%}

Coordenadas horizontais:

Horizontal Axis:

- Name : Yaw

- Minimun Axis Value : -90

- Maximun Axis Value : 90

Coordenadas Verticais:

- Vertical Axis

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
    caption="Coordenadas Yaw e Pitch."
    ref="https://docs.unrealengine.com/4.27/en-US/AnimatingObjects/SkeletalMeshAnimation/AnimHowTo/AimOffset/"
%}
