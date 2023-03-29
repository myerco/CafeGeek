---
title: Controle de versão
excerpt: Neste capítulo vamos apresentar a interface do Unreal Engine e seus editores de trabalho.
permalink: /pages/unreal_engine/interface_editores
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true  
---

## 1. Editor de Level

Uma visão geral da interface usada para o design e construção de níveis e ambientes de jogo.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/DefaultInterface_Windows.webp"
    alt="Figura: Level Editor"
    caption="Figura: Level Editor."
    ref="https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/"
%}

1. Tab Bar and Menu Bar;

2. Toolbar;

3. Place Actor / Modes;

4. Viewports;

5. Content Browser;

6. World Outliner;

7. Details;

***

## 2. Editor de Viewports

Conceitos e recursos básicos das Viewports no Unreal Editor.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/Viewports_Topic.webp"
    alt="Figura: Viewport Basics"
    caption="Figura: Viewport Basics."
    ref="https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/Basics/"
%}

### 2.1. Transformação de ciclo (espaço) e transformações (W/E/R)

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/ViewportToolbar_TransformTools.webp"
    alt="Figura: Viewport Toolbar"
    caption="Figura: Viewport Toolbar."
    ref="https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/"
%}

- R - A transição suave da escala;

- W - Mover objeto;

- E - Girar objeto é essencial.

### 2.2. Transformação referência Mundial/Local

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/ViewportToolbar_Coordinate.webp"
    alt="Figura: Coordinate System"
    caption="Figura: Coordinate System."
    ref="https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/"
%}

A referência de movimentação do objeto, por exemplo quando a referência é do objeto a movimentação é para a esquerda ou direita do objeto, quando a referência é o mundo o objeto é movimentado para a esquerda ou direita do mundo.

### 2.3. Actor Snapping

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/Basics/Actors/ActorSnapping/LevelViewportToolbar-SurfaceSnapping.webp"
    alt="Figura: Actor Snapping"
    caption="Figura: Actor Snapping."
    ref="https://docs.unrealengine.com/4.27/en-US/Basics/Actors/ActorSnapping/"
%}

- `Surface Snapping` - Faz com que os Atores se alinhem ao piso ou a outra superfície;

- `Drag Grid` - Permite o encaixe em uma grade implícita tridimensional dentro do Nível.

- `Rotation Grid` - Fornece snaps de rotação incremental.

- `Scale Grid` - A Grade de Escala força o gizmo de Escala a ajustar-se a incrementos aditivos;

### 2.4. Velocidade da Câmera

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/SettingCameraSpeed.webp"
    alt="Figura: Camera Speed"
    caption="Figura: ACamera Speed."
    ref="https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/"
%}

Outros controles.

- [Viewport Controls](https://docs.unrealengine.com/en-US/Engine/UI/LevelEditor/Viewports/ViewportControls/index.html)

Guia de designer para atalhos de teclado do **Unreal Engine**.

- [Designer's guide to Unreal Engine keyboard shortcuts](https://www.unrealengine.com/en-US/tech-blog/designer-s-guide-to-unreal-engine-keyboard-shortcuts "Designer's guide to Unreal Engine keyboard shortcuts")

Explicações para os modos de visualização disponíveis nas viewports.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/ViewModes/ViewMode_Header.webp"
    alt="Figura: View Modes"
    caption="Figura: View Modes."
    ref="https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewModes"
%}

### 2.5. Customização do Layout

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/Basics/UI/InterfaceOverview/DockingEditorTabs2.webp"
    alt="Figura: Layout Customization"
    caption="Figura: Layout Customization."
    ref="https://docs.unrealengine.com/en-US/Engine/UI/InterfaceOverview/index.html"
%}

***

## 3. Play e Simulate

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/InEditorTesting/playInEditor.webp"
    alt="Figura: In-Editor Testing (Play & Simulate)"
    caption="Figura: In-Editor Testing (Play & Simulate)."
    ref="https://docs.unrealengine.com/en-US/Engine/UI/LevelEditor/InEditorTesting/index.html"
%}

- `ViewPort` -  A jogabilidade será mostrada na janela de visualização ativa do Editor de níveis;

- `New Window` - A jogabilidade será mostrada em uma nova janela. Para alterar o tamanho padrão das novas janelas, use a janela de configurações do Play In Editor

- `Standalone Game` - A jogabilidade será mostrada em uma nova janela que é executada em seu próprio processo. Para alterar o tamanho da janela autônoma padrão, use a janela de configurações do Play In Editor.

- `Simulate` - O uso do botão Simular inicia uma sessão Simular no editor na viewport atualmente ativa. Durante a simulação, a jogabilidade começa, incluindo a execução de Blueprints e código C++ que não dependem da interação do jogador com o jogo. Ao simular, você tem acesso total às ferramentas do Editor, podendo modificar a cena e seu conteúdo, ou até mesmo colocar novos Atores. Você também pode selecionar e inspecionar os peões controlados pela IA enquanto executam ações e depurar e ajustar rapidamente os comportamentos de jogo. No entanto, como você não está usando um `PlayerController` durante a simulação, não é possível inserir controles do jogo. Você pode salvar algumas alterações feitas em uma sessão Simular no editor usando Manter alterações de simulação.
