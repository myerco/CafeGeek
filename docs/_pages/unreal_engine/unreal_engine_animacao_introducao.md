---
title: Animação de personagens
excerpt: Neste capitulo vamos apresentar o fluxo de trabalho e os elementos necessários para a animação de personagens.
permalink: /pages/unreal_engine/animacao_introducao
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true 
---

## 1. Fluxo de trabalho para animação utilizando Unreal Engine

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation.webp"
    alt="Figura: Unreal Engine e Animação de personagens."
    caption=""
%}

A animação de personagens consiste em associar um esqueleto com pontos de controle a uma malha 3D, o objeto então pode ser adicionado a uma sequencia de animações.

{% include imagelocal.html
    src="unreal/animacao/Skeleton-over-a-mesh.webp"
    alt="Figura: Skeleton over a Mesh."
    caption="A malha envolve a estrutura do esqueleto."
%}

{% include imagelocal.html
    src="unreal/animacao/Animation-pose-keyframes-and-timeline.webp"
    alt="Figura: Animation pose keyframes and timeline."
    caption="Adicionamos uma pose a uma linha de tempo para simular movimento."
%}

{% include image.html
    src="https://www.researchgate.net/profile/Santiago-Moreno-Diaz-2/publication/337228005/figure/fig1/AS:824881293836293@1573678434329/Walk-cycle-https-rustyanimatorcom-walk-cycle-animation.jpg"
    alt="Figura: Walk Cycle."
    caption="Motion Matching in Unreal Engine."
    ref="https://www.researchgate.net/publication/337228005_Motion_Matching_in_Unreal_Engine/"
%}

O **Unreal Engine** fornece um fluxo de trabalho simples para construção de animações utilizando Skeletal Mesh importadas de aplicativos 3D para uso em jogos. Atualmente, apenas uma única animação para cada `Skeletal Mesh` pode ser exportada / importada em um único arquivo.

Abaixo uma visão geral técnica do uso do processo de construção de animações.

| Importar       | Malha            | Animação      | Classe       |
| :------------- | :--------------- | :------------ | :----------- |
| 1. Arquivo FBX | 2. Skeletal Mesh | 4. Sequence   | 7. Character |
|                | 3. Skeletal      | 5. Anim Graph |              |

## 2. Arquivo FBX

Embora o formato FBX seja proprietário, muitos aplicativos de modelagem e animação que não são da Autodesk podem abrir arquivos FBX. Isso permite que os criadores compartilhem modelos 3D entre si usando o formato FBX, que é eficiente porque armazena modelos como dados binários. Os arquivos .OBJ, .DXF, .3DS e .DAE (COLLADA) podem ser convertidos em arquivos FBX, usando o Autodesk FBX Converter (disponível para Windows e Mac, mas sem suporte a partir de 2013) ou Autodesk Viewer (Web).[(fileinfo)](https://fileinfo.com/extension/fbx "Fileinfo")

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_fbx_export_unreal.webp"
    alt="Figura: Arquivo FBX."
    caption="Exportando um modelo 3D do Autodesk Maya para o Unreal."
%}

## 3. Skeleton

Skeleton ou Esqueleto da malha importada no arquivo FBX contendo controle de movimentação e `Sockets` para colar outros objetos e ossos virtuais.

`Sockets` - Ponto de controle do esqueleto, permitindo colar outros objetos no ponto;

`Virtual Bones` - Adiciona um osso que não está na malha original;

`Retargeting` - Permite que as animações sejam reutilizadas entre os personagens que usam o mesmo recurso `Skeleton`;

`Physics` - Controle de física e animação dos ossos.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_skeleton_mannequim.webp"
    alt="Figura: Editor de esqueleto ou Skeleton."
    caption="Ao abrir um objeto do tipo esqueleto é fornecido um editor específico para a manipulação esse tipo de objeto."
%}

### 3.1. Animation Editors

{% include image.html
    src="https://docs.unrealengine.com/5.1/Images/animating-characters-and-objects/SkeletalMeshAnimation/Persona/AnimationEditorOverview.png"
    alt="Figura: Animation Editors."
    caption="O Skeletal Mesh Animation System no Unreal Engine é composto por editores de recursos de animação especializados que apresentam ferramentas de animação robustas que você pode usar ao trabalhar com Skeletal Meshes e outros recursos de animação. Com esses editores de animação, você pode criar animações de personagens, interações dentro dos níveis e outros comportamentos processuais."
    ref="https://docs.unrealengine.com/5.1/en-US/animation-editors-in-unreal-engine/"
%}

## 4. Skeletal Mesh

Skeletal Mesh ou Malha do esqueleto cobre os ossos para gerenciamento de `LOD` e `clothing` (roupas).

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_skeletal_mesh_editor.webp"
    alt="Figura: Skeletal Mesh."
    caption="Com este editor podemos manipular a malha do esqueleto."
%}

### 4.1. Skeletal Mesh Editor

{% include image.html
    src="https://docs.unrealengine.com/5.1/Images/animating-characters-and-objects/SkeletalMeshAnimation/Persona/MeshDetails/SkeletalMeshEditorOverview.png"
    alt="Figura: Skeletal Mesh Editor."
    caption="O modo Skeletal Mesh Editor é onde você pode encontrar as ferramentas para manipular e visualizar os ativos do Skeletal Mesh. É semelhante ao Static Mesh Editor. No Editor de malha esquelética, você pode fazer alterações na malha poligonal atribuindo materiais, adicionando elementos de vestuário, configurando LODs (nível de detalhe) e visualizando quaisquer Alvos Morph aplicados à malha."
    ref="https://docs.unrealengine.com/5.1/en-US/skeletal-mesh-editor-in-unreal-engine/"
%}

## 5. Anim Graph

Editor para implementação das animações utilizando codificação visual.

`Event Graph` - Código *Blueprint* onde deverão ser processadas todas as variáveis de inicialização para controle de fluxo das animações;  

`Anim Graph` - Nós de representação de máquinas de estado do personagem, `State Machine`;

- `Slots` - Permite adicionar uma camada de funcionalidade ao fluxo;

- `Layerd Blend` por bone - Permite diversas formas de mixar animações no fluxo;

- `Pose Caching` - Permite reutilizar a informação de um determinado "estado";

- `Final posse` - `Sequence recorder` e `Animation Sharing manager`.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animgraph.webp"
    alt="Figura: Editor Anim Graph."
    caption="Adicionamos toda a lógica de animação dos objetos utilizando um apresentação um fluxo de estados ou poses."
%}

### 5.1. Animation Blueprint Editor

{% include image.html
    src="https://docs.unrealengine.com/5.1/Images/animating-characters-and-objects/SkeletalMeshAnimation/AnimBlueprints/animation-blueprint-editor/EditorOverview.png"
    alt="Figura: Animation Blueprint Editor."
    caption="O Animation Blueprint Editor compartilha funcionalidade semelhante ao Blueprint Editor, mas contém recursos, ferramentas e janelas diferentes para auxiliar na criação de scripts de animação de personagens."
    ref="https://docs.unrealengine.com/5.1/en-US/skeletal-mesh-editor-in-unreal-engine/"
%}

## 6. Sequence

Editor que permite a edição e montage de animações.

`Blend Space` - Combina um grupo de animações com duas dimensões podendo usar variáveis;

`Blend Space 1D` - Combina grupo de animações com uma dimensão podendo usar variáveis;

`Montages` - Expõe a animação para o *Blueprint*;

`Pose Assets` - Permite gravar uma nova posse do *Character*;

`Notify Animations` - Adiciona uma etiqueta na `Timeline` da animação.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_Blend_Space_1D.webp"
    alt="Figura: Blueprint - Editor Blend Space 1D."
    caption="Podemos sequenciar animações associadas a variáveis possibilitando um fluxo de animações."
%}

### 6.1. Animation Sequence Editor

{% include image.html
    src="https://docs.unrealengine.com/5.1/Images/animating-characters-and-objects/SkeletalMeshAnimation/Persona/AssetEditor/AnimationSequenceEditorOverview.png"
    alt="Figura: Animation Sequence Editor."
    caption="O Animation Sequence Editor fornece acesso a vários recursos centrados em animação disponíveis para Skeletal Meshes no Unreal Engine. No Animation Sequence Editor, você pode editar e visualizar sequências de animação, montagens, curvas e muito mais."
    ref="https://docs.unrealengine.com/5.1/en-US/animation-sequence-editor-in-unreal-engine/"
%}

## 7. Organizando pastas de bibliotecas

Neste capitulo vamos preparar e organizar os objetos e elementos necessários, como por exemplo, arquivos FBX, malhas e esqueletos e suas animações. Vamos também importar personagens do site Mixano.

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_animation_project.webp"
    alt="Figura: Modelos."
    caption="Podemos baixar vários modelos e importar para o nosso projeto."
%}

A seguir a configuração inicial do projeto e os pacotes com os necessários para as animações.

**1.** Criar o projeto AulaAnimação com `Blueprint ThirdPerson`;

**2.** Adicione ao projeto `Animation Starter Pack`;

**3.** Criar as pastas para organização do projeto:

**Nota:** Utilize a estrutura de pastas definidas em [Organizando as Pastas](https://cafegeek.eti.br/pages/unreal_engine/instalacao_configuracao#6-organizando-as-pastas).
{: .notice--warning}

Mova todas as pastas de bibliotecas externas para a pasta ExampleContent, como por exemplo ThirdPerson.

```bash
cp /Mannequim/Character/Mesh/Sk_Mannequim  /Characteres/Mannequim/Mesh
cp /Mannequim/Character/Mesh/SK_Mannequin_PhysicsAsset  /Characteres/Mannequim/Mesh
cp /Mannequim/Character/Mesh/UE4_Mannequin_Skeleton  /Characteres/Mannequim/Mesh
cp /Mannequim/Animations/  /Character/Mannequim/Animations
 ```

### 7.1. Classe do personagem Base

Podemos utilizar um personagem base para servir de Referência ou classe pai para outros personagens.

**1.** Criar a Classe `BP_PlayerBase` (Blueprint classe `Character`) em `/Core/Character`;

**2.** Copiar todos elementos do `Eventh Graph` de `ThirdPersonCharacter` para `BP_PlayerBase`;

**3.** Adicionar e alinhar os componentes em `BP_PlayerBase`:

- `Spring Arm` - (Location=0.0,0.0,8.4), habilite a opção `Use Pawn Control Rotation`;

- `Camera`. - Camera principal do personagem;

- `Mesh` - (Location=0.0,0.0,-89) (Rotation=-0,0,270).

**4.** Adicione as seguintes variáveis.

| Categoria          | Variável                     | Valor |
| :----------------- | :--------------------------- | :---: |
| Character          | fHealth (float)              |  100  |
|                    | sSound (Sound Cue)           |       |
|                    | tImage (Texture 2D)          |       |
|                    | cColor (Color)               |       |
| Character\Movement | fWalkSpeed (float)           |  300  |
|                    | fCrouchSpeed (float)         |  150  |
|                    | fRunSpeed(float)             |  600  |
|                    | bIsRunning (Boolean)         | false |
|                    | bIsCrouch (Boolean)          | false |
| Character\Action   | bActionLeftAttack (Boolean)  | false |
|                    | bActionRightAttack (Boolean) | false |
|                    | bIsShooting (Boolean)        | false |
|                    | bIsHoldingWeapon (Boolean)   | false |
|                    | bIsAim (Boolean)             | false |
|                    | bIsReloadWeapon (Boolean)    | false |

### 7.2. Classe do Humano

Esta classe irá utilizar o esqueleto e animações do Mannequim (Unreal Mannequim) para representar um humano.

Vamos criar a Classe `BP_Human` (Blueprint classe `BP_CharacterBase`) em `/Characters/Human`;
usando o Menu Context > `Blueprint` > `All Classes` > `BP_CharacterBase`, logo em seguida atualizamos a `Mesh` para `Sk_Mannequim`;

### 7.3. Classe Mutante ou  Mutant

Para esta classe vamos importar o esqueleto e animações.

Criemos o objeto BP_Mutant do tipo `BP_CharacterBase` e adicionamos o esqueleto e animação do personagem criados anteriormente, abaixo as propriedades que devem ser atualizadas.

`Skeletal Mesh`: Mutant;

`Animation Mode`: Use Animation Bluerint;

`Anim Class`: ABP_Mutant_C;

Em `CharacterMomement` atualize os valores para determinar a velocidade de movimentação do personagem, interessante notar que a velocidade de movimento do Mutante é diferente que a do Mannequim:

`Max Walk Speed`: 110;

`Max Walk Speed Crouched`: 110 ou

(Show InHerited Variables) > fWalkSpeed = 110;

(Show InHerited Variables) > fRunSpeed = 220;

**Informação:** Para testar a movimentação crie um level de teste e configure `World Settings` para  `Default Pawn` =  BP_Mutant.
{: .notice--info}

#### 7.3.1. Vídeo Classe do Mutant

{% include video.html
    link="https://youtu.be/obLJb4RBySA"
    src="https://img.youtube.com/vi/obLJb4RBySA/0.jpg"
    alt="Vídeo: Classe do personagem."
    caption="Unreal Engine Animação - 06 A classe do personagem."
%}

## 8. Ambiente e controle

Neste capítulo vamos implementar os controles do personagem e criar um level para testes, para tal vamos seguir os passos abaixo.

**1.** Crie os seguintes objetos *Blueprint*:

- BP_GameModeBase do tipo `Game Mode Base`;

- BP_PlayerController do tipo `Player Controller`.

**2.** Crie um `Level` do tipo `Default` de nome **LevelTest** e salve na pasta `Projeto/Maps`.

**3.** Em `World Settings` configure:

`GameMode Override` - BP_GameModeBase;

`Default Pawn Class` - BP_PlayerBase.

## 9. Animações e esqueleto do Mutant

A seguir vamos preparar o personagem Mutant, baixando e logo em seguida importando para dentro do Unreal Engine.

O personagem Mutant e suas animações estão disponíveis no o site [Mixano.com](https://www.mixamo.com/), então vamos baixar o personagem com os seguintes parâmetros.  

**1.** Character : Mutant

**2.** Animations:

- Mutant Walking (In place = true)

- Mutant Idle

- Mutant Run (In place = true)

- Mutant Jumping

**Observação:** Neste exemplo utilizaremos a opção `In Place = true` para exemplificar uma animação sem `root bone`.  
{: .notice--warning}

### 9.1. Vídeo Baixando personagem

{% include video.html
    link="https://youtu.be/G7c8DMdrsGY"
    src="https://img.youtube.com/vi/G7c8DMdrsGY/0.jpg"
    alt="Vídeo: Baixando personagem do Mixano."
    caption="Unreal Engine Animação - 02 Baixando o personagem."
%}

Para importar a Mesh e Skeletal baixada anteriormente para dentro do Unreal, na pasta configurada para o personagem, vamos seguir os passos abaixo:

**1.** Crie a pasta `/Projeto/Characteres/Mutant/Mesh`;

**2.** Copie o arquivo `mutant.fbx` para a pasta criada no passo anterior;

**3.** Importe o arquivo com a opção `Import All`:

{% include imagelocal.html
    src="unreal/animacao/unreal_engine_fbx_import_options.webp"
    alt="Figura: FBX import options."
    caption="Opções para importar o objeto do tipo FBX."
%}

Para importar as animações do personagem seguimos os passos abaixo:

**1.** Crie a pasta `/Projeto/Characteres/Mutant/animations`;

**2.** Copie os arquivos para pasta criada no passo anterior:

- Mutant_Run.fbx;

- Mutant_Idle.fbx;

- Mutant_Walking.fbx.

**3.** Desmarque a opção `Import Mesh` para que a malha não seja importada novamente;

**4.** Escolha o esqueleto do personagem com `SKeleton`.

### 9.2. Vídeo Importando personagem

{% include video.html
    link="https://youtu.be/6ZLatHfD7P8"
    src="https://img.youtube.com/vi/6ZLatHfD7P8/0.jpg"
    alt="Vídeo: Importando personagem FBX baixado do Mixano."
    caption="Unreal Engine Animação - 03 importando."
%}
