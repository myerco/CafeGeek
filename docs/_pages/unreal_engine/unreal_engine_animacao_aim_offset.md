---
title: Animação de mira
excerpt: Neste capitulo vamos apresentar a animação Aim Offset.
permalink: /pages/unreal_engine/animacao_aim_offset
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true 
---

## 1. Aim Offset

***

Um Aim Offset é um recurso que armazena uma série de poses que podem ser combinadas para ajudar um personagem a apontar uma arma. Durante a animação, o resultado do Aim Offset é misturado com outros movimentos, como correr, caminhar, pular, etc. para fazer com que o personagem pareça olhar suavemente em todas as direções.

### 1.1. Animation Starter Pack

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_starter_pack.webp"
    alt="Figura: Adicionando o pacote Animation Starter Pack."
    caption="A Epic Store oferece um pacote de animações para o Mannequin, facilitando a prototipação do personagem utilizando armas de tiro.."
%}

### 1.2. Preparando o projeto

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

### 1.3. Removendo frames

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

- `AdditiveSettings`.

  - Additive Anim Type : Mesh Space;

  - Base Pose Type : Idle_Rifle_Hip.

Agora vamos criar `Aim Offset` Menu de contexto `Animation > Aim Offset` ou Escolha o esqueleto do Mannequin e utilizando BMP escolha `Create > Aim Offset`;

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_create_aim_offset.webp"
    alt="Figura: Editor Aim Offset."
    caption="Altere os parâmetros em Asset Details para os seguintes valores:"
%}

Coordenadas horizontais:

- Horizontal Axis

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
