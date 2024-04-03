---
title: Interface e editores
excerpt: Neste capítulo vamos apresentar a interface do Unreal Engine e seus editores de trabalho.
permalink: /unreal-engine-capitulo-1/interface-e-editores
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 104
tags:
  - interface
  - editores
gallery:
  - url: /assets/images/unreal/interface-editores/07-le-trans-widget.webp
    image_path: /assets/images/unreal/interface-editores/07-le-trans-widget.webp
    alt: "Move Tool (W)"
    title: "Move Tool (W)"
  - url: /assets/images/unreal/interface-editores/08-transform-rotate.webp
    image_path: /assets/images/unreal/interface-editores/08-transform-rotate.webp
    alt: "Rotate Tool (E)"
    title: "Rotate Tool (E)"
  - url: /assets/images/unreal/interface-editores/09-le-trans-scalewidget.webp
    image_path: /assets/images/unreal/interface-editores/09-le-trans-scalewidget.webp
    alt: "Scale Tool (R)"
    title: "Scale Tool (R)"
---

Neste capítulo descreveremos os elementos mais comuns da interface Unreal Engine 5 e o que eles fazem.  Alguns dos elementos descritos nesta página, como painéis e barras de menu, são geralmente os mesmos em várias partes do motor. Você deve gastar algum tempo se familiarizando com seu propósito geral e funcionalidade, especialmente se você é novo no desenvolvimento de jogos e aplicativos com o Unreal Engine.[REF](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface)

Quando você abre o Unreal Engine 5 pela primeira vez, o **`Level Editor`** (Editor de Níveis) é aberto. Você verá a seguinte janela:

{% include figure image_path="/assets/images/unreal/interface-editores/ue5-default-interface.webp" alt="Default interface"  %}

1. **Menu Bar** - Use esses menus para acessar comandos e funcionalidades específicos do editor;

2. **Main Toolbar** - Contém atalhos para algumas das ferramentas e editores mais comuns do Unreal Engine, bem como atalhos para entrar no modo Play (executar seu jogo dentro do Unreal Editor) e para implantar seu projeto em outras plataformas;

3. **Level Viewport** - Exibe o conteúdo do seu Nível, como Câmeras, Atores, Malhas Estáticas e assim por diante;

4. **Content Drawer Button** - Abre a `Content Drawer`, a partir da qual você pode acessar todos os ativos do seu projeto;

5. **Bottom Toolbar** -	Contém atalhos para o Console de Comando, Log de Saída e funcionalidade de Dados Derivados. Também exibe o status do controle de código fonte;

6. **Outliner** - Exibe uma visão de árvore hierárquica de todo o conteúdo em seu Nível;

7. **Details panel** - Aparece quando você seleciona um ator. Exibe várias propriedades para esse Ator, como sua Transformação (posição no Nível), Malha Estática, Material e configurações físicas. Este painel exibe configurações 

8. diferentes dependendo do que você selecionar na `Viewport` de nível.

**Level** - Um nível é todo ou parte do "mundo" do seu jogo. Os níveis contêm tudo o que um jogador pode ver e interagir, como ambientes, objetos utilizáveis, outros personagens e assim por diante. Nos videogames, é comum ter vários níveis com transições claramente delineadas entre eles (por exemplo, depois de vencer o chefe final de um nível, você passa para o próximo). Para outros tipos de experiências interativas feitas com o Unreal Engine, você pode usar níveis diferentes para fazer a transição entre diferentes tipos de vitrines ou ambientes.
{: .notice}

## 1. Menu Bar

{% include figure image_path="/assets/images/unreal/interface-editores/menu-bar.webp" alt="Menu bar"  %}

Cada editor do Unreal Engine tem uma barra de menus localizada no canto superior direito da janela do editor (Windows) ou na parte superior da tela (macOS). Alguns dos menus, como File, Window e Help, estão presentes em todas as janelas do editor, não apenas no **Level Editor**. Outros são editores-específicos.

## 2. Main Toolbar

A barra de ferramentas principal contém atalhos para algumas das ferramentas e comandos mais usados no Unreal Editor. É dividido nas seguintes áreas:

{% include figure image_path="/assets/images/unreal/interface-editores/main-toolbar.webp" alt="Main Tollbar"  %}

### 2.1. Botão para salvar

Clique neste botão para salvar o nível que está aberto no momento.

### 2.2. Seleção de Modos

Contém atalhos para alternar rapidamente entre diferentes modos para editar conteúdo dentro do seu Nível:

- Select Editing;

- Landscape Editing;

- Foliage Editing;

- Mesh Painting;

- Fracture Editing;

- Brush Editing.

### 2.3. Atalhos de conteúdo

Contém atalhos para adicionar e abrir tipos comuns de conteúdo dentro do `Level Editor`.

- **Create** - Escolha a partir de uma lista de Ativos/Tipos comuns para adicionar rapidamente ao seu Nível. Você também pode acessar os painéis Place Actors a partir deste menu;

- **Blueprints** -Criar e acessar Blueprints.

- **Cinematics** - Criar uma Sequência de Nível ou `Master sequence cinematic`.

### 2.4. Controles de execução do jogo

Contém botões de atalho (Play, Skip, Stop e Eject) para executar o seu jogo no Editor.

### 2.5. Menu para escolha de plataformas

Contém uma série de opções que você pode usar para configurar, preparar e implantar seu projeto em diferentes plataformas, como desktop, dispositivos móveis ou consoles.

### 2.6. Configurações

Contém várias configurações para o Unreal Editor, `Level Editor Viewport` e comportamento do jogo.

## 3. Level Viewport

O `Level Viewport` exibe o conteúdo do Nível que está aberto no momento. Quando você abre um projeto no Unreal Engine, o nível padrão do projeto é aberto no Viewport de nível por padrão. É aqui que você pode visualizar e editar o conteúdo do seu nível ativo, seja um ambiente de jogo, um aplicativo de visualização de produto ou outra coisa.

A Viewport de nível geralmente pode exibir o conteúdo do nível de duas maneiras diferentes:

- **Perspective** - que é uma visão 3D, você pode navegar para ver o conteúdo da viewport de diferentes ângulos.

- **Ortographic** - que é uma visão 2D que olha para baixo um dos eixos principais (X, Y ou Z).

{% include figure image_path="/assets/images/unreal/interface-editores/viewport-examples.webp" alt="View port"  caption="Vistas diferentes do Level Viewport no Unreal Engine 5. Top: Perspective View. Parte inferior: Ortographic view." %}

## 4. Content Drawer e Content Browser

O `Content Drawer` é uma janela do explorador de arquivos que exibe todos os ativos, blueprints e outros arquivos contidos em seu projeto. Você pode usá-lo para navegar pelo seu conteúdo, arrastar os ativos para o nível, migrar ativos entre projetos e muito mais.

{% include figure image_path="/assets/images/unreal/interface-editores/ue5_1-content-browser.webp" alt="Content Browser window in Unreal Engine 5"  caption="Content Browser window in Unreal Engine 5." %}

O botão`Content Drawer`, localizado no canto inferior esquerdo do Unreal Editor, abre uma instância especial do `Content Browse` que minimiza automaticamente quando ele perde o foco (ou seja, quando você clica para longe dele). Para mantê-lo aberto, clique no botão `Dock` no Layout no canto superior direito do `Content Drawser`. Isso cria uma nova instância do `Content Browse`, mas você ainda pode abrir um novo `Content Drawer`.

## 5. Bottom Toolbar

A barra de ferramentas de fundo contém atalhos para a funcionalidade `Command Console`, `Output Log` e `Derived Data`. Ele também exibe o status de controle de código fonte. É dividido nas seguintes áreas:

{% include figure image_path="/assets/images/unreal/interface-editores/bottom-toolbar.webp" alt="Bottom Toolbar"  %}

- **Output Log** - Ferramenta de depuração que imprime informações úteis enquanto seu aplicativo está em execução.

- **Command Console** - Comporta-se como qualquer outra interface de linha de comando: digite comandos do console para acionar comportamentos específicos do editor.

- **Derived Data** - Fornece funcionalidade Derived Data.

- **Source Control Status** - Exibe o status do controle de seu código fonte se o projeto estiver conectado ao controle de código (por exemplo, GitHub ou Perforce). Caso contrário, isso dirá o controle de origem desligado.

## 6. Outliner

O painel Outliner (anteriormente conhecido como `World Outliner`) exibe uma visão hierárquica de todo o conteúdo em seu Nível. Por padrão, ele está localizado no canto superior direito da janela do Editor Unreal. Você pode ter até quatro Outliners diferentes, cada um com seu próprio layout de coluna e configuração de filtro.

{% include figure image_path="/assets/images/unreal/interface-editores/ue5_1-outliner.webp" alt="Outliner"   %}

Você também pode usar o painel Outliner para:

- Oculta ou revele rapidamente os Atores clicando no botão Olho associado;

- Acesse o menu de contexto de um ator clicando com o botão direito do mouse sobre esse ator. Você pode executar operações adicionais específicas do Ator a partir desse menu;

- Crie, mova e exclua pastas de conteúdo.

## 7. Details Panel

Quando você seleciona um Ator na Viewport de Nível, o painel Detalhes mostrará as configurações e propriedades que afetam o Ator selecionado. Por padrão, ele está localizado no lado direito da janela do Unreal Editor, sob o painel Esboço Mundial.

{% include figure image_path="/assets/images/unreal/interface-editores/details-panel.webp" alt="Details Panel" caption="
Este exemplo mostra um painel de detalhes do Ator de malha estática do cubo. Com o cubo Static Mesh selecionado, o Painel de detalhes aparece atracado no lado direito do Unreal Editor"  %}

## 8. Controle de transformação

{% include gallery caption="Esses controles estão relacionados a (W) - Movimento, (E) - Rotação e (R) - Dimensionamento de atores nas perspectivas de visualização usando as ferramentas de transformação" %}

{% include figure image_path="/assets/images/unreal/interface-editores/10-le-trans-widget-icons.webp" alt="Widget icons" %}

## 9. Transformação referência Mundial e Local

![Viwport toolar coordinates](/assets/images/unreal/interface-editores/viewport-toolbar-coordinates.webp){: .align-center}

A referência de movimentação do objeto, por exemplo quando a referência é do objeto a movimentação é para a esquerda ou direita do objeto, quando a referência é o mundo o objeto é movimentado para a esquerda ou direita do mundo.

## 10. Actor Snapping

{% include figure image_path="/assets/images/unreal/interface-editores/01-surface-snapping-option.webp" alt="Bottom Toolbar"  %}

- **Surface Snapping** - Faz com que os Atores se alinhem ao piso ou a outra superfície;

- **Drag Grid** - Permite o encaixe em uma grade implícita tridimensional dentro do Nível.

- **Rotation Grid** - Fornece snaps de rotação incremental.

- **Scale Grid** - A Grade de Escala força o gizmo de Escala a ajustar-se a incrementos aditivos;

## 11. Velocidade da Câmera

{% include figure image_path="/assets/images/unreal/interface-editores/camera-speed.webp" alt="Bottom Toolbar"  %}

Outros controles.

- [Viewport Controls](https://docs.unrealengine.com/en-US/Engine/UI/LevelEditor/Viewports/ViewportControls/index.html)

Guia de designer para atalhos de teclado do Unreal Engine*.

- [Designer's guide to Unreal Engine keyboard shortcuts](https://www.unrealengine.com/en-US/tech-blog/designer-s-guide-to-unreal-engine-keyboard-shortcuts "Designer's guide to Unreal Engine keyboard shortcuts")

Explicações para os modos de visualização disponíveis nas viewports.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/ViewModes/ViewMode_Header.webp"
    alt="Figura: View Modes"
    caption="Figura: View Modes."
    ref="https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewModes"
%}

## 12. Customização do Layout

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/Basics/UI/InterfaceOverview/DockingEditorTabs2.webp"
    alt="Figura: Layout Customization"
    caption="Figura: Layout Customization."
    ref="https://docs.unrealengine.com/en-US/Engine/UI/InterfaceOverview/index.html"
%}

## 13. Play e Simulate

{% include figure image_path="/assets/images/unreal/interface-editores/01-play-in-editor.webp" alt="Play in Editor"  %}

{% include figure image_path="/assets/images/unreal/interface-editores/02-button-play-menu.webp" alt="Buttom Play"  %}

- **Select ViewPort** -  A jogabilidade será mostrada na janela de visualização ativa do Editor de níveis;

- **New Editor Window** - A jogabilidade será mostrada em uma nova janela. Para alterar o tamanho padrão das novas janelas, use a janela de configurações do Play In Editor

- **Standalone Game** - A jogabilidade será mostrada em uma nova janela que é executada em seu próprio processo. Para alterar o tamanho da janela autônoma padrão, use a janela de configurações do Play In Editor.

- **Simulate** - O uso do botão Simular inicia uma sessão Simular no editor na viewport atualmente ativa. Durante a simulação, a jogabilidade começa, incluindo a execução de Blueprints e código C++ que não dependem da interação do jogador com o jogo. Ao simular, você tem acesso total às ferramentas do Editor, podendo modificar a cena e seu conteúdo, ou até mesmo colocar novos Atores. Você também pode selecionar e inspecionar os peões controlados pela IA enquanto executam ações e depurar e ajustar rapidamente os comportamentos de jogo. No entanto, como você não está usando um `PlayerController` durante a simulação, não é possível inserir controles do jogo. Você pode salvar algumas alterações feitas em uma sessão Simular no editor usando Manter alterações de simulação.
