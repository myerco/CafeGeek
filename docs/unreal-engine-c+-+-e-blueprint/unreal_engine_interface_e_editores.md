---
title: Interface e Editores
description: Interface e Editores
tags: [Unreal Engine, interface, editor]
---

***

- [Editor de Level](#editor-de-level)
- [Editor de Viewports](#editor-de-viewports)
  - [Transformação de ciclo (espaço) e transformações (W/E/R)](#transformação-de-ciclo-espaço-e-transformações-wer)
  - [Transformação referência Mundial/Local](#transformação-referência-mundiallocal)
  - [Actor Snapping](#actor-snapping)
  - [Velocidade da Câmera](#velocidade-da-câmera)
  - [Customização do Layout](#customização-do-layout)
- [Play e Simulate](#play-e-simulate)

***

## Editor de Level

Uma visão geral da interface usada para o design e construção de níveis e ambientes de jogo.

![Figura: Level Editor - https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/](https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/DefaultInterface_Windows.webp "Figura: Level Editor - https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/")

> Figura: Level Editor - https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/ .

1. Tab Bar and Menu Bar

2. Toolbar

3. Place Actor / Modes

4. Viewports

5. Content Browser

6. World Outliner

7. Details

## Editor de Viewports

Conceitos e recursos básicos das Viewports no Unreal Editor.

![Figura: Viewport Basics - https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/Basics/](https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/Viewports_Topic.webp "Figura: Viewport Basics - https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/Basics/")

> Figura: Viewport Basics - https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/Basics/ .

### Transformação de ciclo (espaço) e transformações (W/E/R)

![Viewport Toolbar](https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/ViewportToolbar_TransformTools.webp "Viewport Toolbar")

> Figura: [Viewport Toolbar](https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/)

- R - A transição suave da escala ;

- W - Mover objeto;

- E - Girar objeto é essencial.

### Transformação referência Mundial/Local

![Coordinate System](https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/ViewportToolbar_Coordinate.webp "Coordinate System")

> Figura: [Coordinate System](https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/)

A referência de movimentação do objeto, por exemplo quando a referência é do objeto a movimentação é para a esquerda ou direita do objeto, quando a referência é o mundo o objeto é movimentado para a esquerda ou direita do mundo.

### Actor Snapping

![](https://docs.unrealengine.com/4.27/Images/Basics/Actors/ActorSnapping/LevelViewportToolbar-SurfaceSnapping.webp "S")

> Figura: [Actor Snapping](https://docs.unrealengine.com/4.27/en-US/Basics/Actors/ActorSnapping/)

- `Surface Snapping` - Faz com que os Atores se alinhem ao piso ou a outra superfície;

- `Drag Grid` - Permite o encaixe em uma grade implícita tridimensional dentro do Nível.

- `Rotation Grid` - Fornece snaps de rotação incremental.

- `Scale Grid` - A Grade de Escala força o gizmo de Escala a ajustar-se a incrementos aditivos;

### Velocidade da Câmera

![Camera Speed](https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/SettingCameraSpeed.webp "Camera Speed")

> Figura: [Camera Speed](https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewportToolbar/)

Outros controles.

- [Viewport Controls](https://docs.unrealengine.com/en-US/Engine/UI/LevelEditor/Viewports/ViewportControls/index.html)


Guia de designer para atalhos de teclado do **Unreal Engine**.

- [Designer's guide to Unreal Engine keyboard shortcuts](https://www.unrealengine.com/en-US/tech-blog/designer-s-guide-to-unreal-engine-keyboard-shortcuts "Designer's guide to Unreal Engine keyboard shortcuts")

Explicações para os modos de visualização disponíveis nas viewports.

![Figura: View Modes - https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewModes](https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/ViewModes/ViewMode_Header.webp "Figura: View Modes - https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewModes")

> Figura: View Modes - https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewModes .

### Customização do Layout

![Figura: Layout Customization - https://docs.unrealengine.com/en-US/Engine/UI/InterfaceOverview/index.html](https://docs.unrealengine.com/4.27/Images/Basics/UI/InterfaceOverview/DockingEditorTabs2.webp "Figura: Layout Customization - https://docs.unrealengine.com/en-US/Engine/UI/InterfaceOverview/index.html")

> Figura: Layout Customization - https://docs.unrealengine.com/en-US/Engine/UI/InterfaceOverview/index.html .

## Play e Simulate

![Figura: In-Editor Testing (Play & Simulate) - https://docs.unrealengine.com/en-US/Engine/UI/LevelEditor/InEditorTesting/index.html](https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/InEditorTesting/playInEditor.webp "Figura: In-Editor Testing (Play & Simulate) - https://docs.unrealengine.com/en-US/Engine/UI/LevelEditor/InEditorTesting/index.html")

> Figura: In-Editor Testing (Play & Simulate) - https://docs.unrealengine.com/en-US/Engine/UI/LevelEditor/InEditorTesting/index.html .

- `ViewPort` -  A jogabilidade será mostrada na janela de visualização ativa do Editor de níveis;

- `New Window` - A jogabilidade será mostrada em uma nova janela. Para alterar o tamanho padrão das novas janelas, use a janela de configurações do Play In Editor

- `Standalone Game` - A jogabilidade será mostrada em uma nova janela que é executada em seu próprio processo. Para alterar o tamanho da janela autônoma padrão, use a janela de configurações do Play In Editor.

- `Simulate` - O uso do botão Simular inicia uma sessão Simular no editor na viewport atualmente ativa. Durante a simulação, a jogabilidade começa, incluindo a execução de Blueprints e código C++ que não dependem da interação do jogador com o jogo. Ao simular, você tem acesso total às ferramentas do Editor, podendo modificar a cena e seu conteúdo, ou até mesmo colocar novos Atores. Você também pode selecionar e inspecionar os peões controlados pela IA enquanto executam ações e depurar e ajustar rapidamente os comportamentos de jogo. No entanto, como você não está usando um `PlayerController` durante a simulação, não é possível inserir controles do jogo. Você pode salvar algumas alterações feitas em uma sessão Simular no editor usando Manter alterações de simulação.
