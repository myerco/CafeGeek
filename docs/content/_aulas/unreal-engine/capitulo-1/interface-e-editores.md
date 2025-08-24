---
title: Interface e Editores
excerpt: Descubra a interface do Unreal Engine 5 e conheça os principais editores de trabalho de forma simples e divertida!
categories: 
  - "unreal-engine"
  - "capitulo-1"
date: 2024-03-04T08:48:05-04:00
order: 3
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

Bem-vindo à interface do Unreal Engine 5!  
Aqui você vai conhecer os principais elementos da tela e aprender para que serve cada editor. Não se preocupe se parecer muita coisa: com o tempo, tudo vai ficar natural e divertido!

Quando você abre o Unreal Engine 5 pela primeira vez, o **Level Editor** (Editor de Níveis) é exibido. É nele que você vai passar boa parte do tempo criando mundos, personagens e aventuras!

{% include figure image_path="/assets/images/unreal/interface-editores/ue5-default-interface.webp" alt="Interface padrão do Unreal Engine 5" %}

---

## 1. Conhecendo a Interface

Vamos dar uma olhada nos principais elementos da tela:

1. **Menu Bar** – Onde ficam os menus principais, como Arquivo, Editar, Janela e Ajuda.
2. **Main Toolbar** – Atalhos para ferramentas importantes, como salvar, executar o jogo e acessar Blueprints.
3. **Level Viewport** – Aqui você vê e edita o seu mundo em 3D (ou 2D).
4. **Content Drawer Button** – Abre a “mochila” do seu projeto, onde ficam todos os arquivos e assets.
5. **Bottom Toolbar** – Atalhos para o console, log de saída e status do controle de versão.
6. **Outliner** – Mostra todos os objetos do seu nível em uma lista organizada.
7. **Details Panel** – Exibe as propriedades do objeto selecionado, como posição, cor, material e muito mais.

> **Dica:** Passeie com o mouse por cada painel e explore! Não tenha medo de clicar e descobrir o que cada botão faz.
{: .notice--info}

---

## 2. Menu Bar

{% include figure image_path="/assets/images/unreal/interface-editores/menu-bar.webp" alt="Menu bar" %}

A barra de menus fica no topo da janela. Aqui você encontra comandos para abrir, salvar, importar arquivos, acessar configurações e muito mais. Menus como **File**, **Window** e **Help** estão sempre presentes.

---

## 3. Main Toolbar

{% include figure image_path="/assets/images/unreal/interface-editores/main-toolbar.webp" alt="Main Toolbar" %}

A barra de ferramentas principal traz atalhos para:

- **Salvar** o nível atual
- Alternar entre modos de edição (Landscape, Foliage, Mesh Painting, etc.)
- Adicionar novos objetos e Blueprints
- Criar sequências cinematográficas
- Executar o jogo no editor (Play)
- Escolher a plataforma de destino (PC, mobile, console)
- Ajustar configurações do editor

---

## 4. Level Viewport

O **Level Viewport** é onde a mágica acontece!  
Aqui você visualiza e edita o seu mundo, seja em 3D (Perspective) ou em 2D (Orthographic).

{% include figure image_path="/assets/images/unreal/interface-editores/viewport-examples.webp" alt="Viewport" caption="Vistas diferentes do Level Viewport no Unreal Engine 5. Topo: Perspective View. Abaixo: Orthographic View." %}

- **Perspective:** Visualização 3D, perfeita para navegar pelo cenário.
- **Orthographic:** Visualização 2D, ótima para alinhar objetos com precisão.

---

## 5. Content Drawer e Content Browser

O **Content Drawer** é como um baú do tesouro: aqui ficam todos os assets do seu projeto!  
Imagens, sons, Blueprints, materiais, tudo organizado em pastas.

{% include figure image_path="/assets/images/unreal/interface-editores/ue5_1-content-browser.webp" alt="Content Browser window in Unreal Engine 5" %}

Clique no botão `Content Drawer` (canto inferior esquerdo) para abrir. Você pode arrastar assets direto para o seu nível!

> **Dica:** Para manter o Content Drawer sempre aberto, clique em “Dock” no canto superior direito dele.
{: .notice--info}

---

## 6. Bottom Toolbar

{% include figure image_path="/assets/images/unreal/interface-editores/bottom-toolbar.webp" alt="Bottom Toolbar" %}

Aqui você encontra:

- **Output Log:** Mostra mensagens e erros do seu projeto.
- **Command Console:** Digite comandos para testar e depurar.
- **Derived Data:** Gerencia dados derivados do projeto.
- **Source Control Status:** Mostra se o projeto está conectado ao controle de versão (como Git).

---

## 7. Outliner

O **Outliner** é uma lista de tudo que existe no seu nível, organizada em árvore.  
Você pode ocultar, renomear, mover e até criar pastas para organizar melhor seus objetos.

{% include figure image_path="/assets/images/unreal/interface-editores/ue5_1-outliner.webp" alt="Outliner" %}

---

## 8. Details Panel

Quando você seleciona um objeto no nível, o **Details Panel** mostra todas as propriedades dele: posição, rotação, escala, materiais, física e muito mais.

{% include figure image_path="/assets/images/unreal/interface-editores/details-panel.webp" alt="Details Panel" %}

---

## 9. Ferramentas de Transformação

Mover, girar e redimensionar objetos é fácil!  
Use as teclas **W** (Mover), **E** (Girar) e **R** (Escalar) para alternar entre as ferramentas.

{% include gallery caption="Esses controles estão relacionados a (W) - Movimento, (E) - Rotação e (R) - Dimensionamento de atores nas perspectivas de visualização usando as ferramentas de transformação" %}

{% include figure image_path="/assets/images/unreal/interface-editores/10-le-trans-widget-icons.webp" alt="Widget icons" %}

---

## 10. Referência Mundial e Local

![Viewport toolbar coordinates](/assets/images/unreal/interface-editores/viewport-toolbar-coordinates.webp){: .align-center}

Você pode escolher se quer mover o objeto em relação ao mundo ou ao próprio objeto. Isso ajuda muito na hora de alinhar e posicionar elementos!

---

## 11. Actor Snapping

{% include figure image_path="/assets/images/unreal/interface-editores/01-surface-snapping-option.webp" alt="Surface Snapping" %}

- **Surface Snapping:** Alinha objetos a superfícies.
- **Drag Grid:** Encaixa objetos em uma grade invisível.
- **Rotation Grid:** Faz rotações em passos definidos.
- **Scale Grid:** Escala objetos em incrementos fixos.

---

## 12. Velocidade da Câmera

{% include figure image_path="/assets/images/unreal/interface-editores/camera-speed.webp" alt="Camera Speed" %}

Você pode ajustar a velocidade da câmera para navegar mais rápido ou devagar pelo seu nível.

---

## 13. Modos de Visualização

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/BuildingWorlds/LevelEditor/Viewports/ViewModes/ViewMode_Header.webp"
    alt="Figura: View Modes"
    caption="Figura: View Modes."
    ref="https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LevelEditor/Viewports/ViewModes"
%}

Explore diferentes modos de visualização para ver seu nível de formas variadas: modo wireframe, iluminação, sombras, etc.

---

## 14. Customização do Layout

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/Basics/UI/InterfaceOverview/DockingEditorTabs2.webp"
    alt="Figura: Layout Customization"
    caption="Figura: Layout Customization."
    ref="https://docs.unrealengine.com/en-US/Engine/UI/InterfaceOverview/index.html"
%}

Você pode personalizar a disposição dos painéis, arrastando e encaixando onde preferir. Deixe o editor com a sua cara!

---

## 15. Play e Simulate

{% include figure image_path="/assets/images/unreal/interface-editores/01-play-in-editor.webp" alt="Play in Editor" %}

Clique em **Play** para testar seu jogo direto no editor!  
Você pode escolher entre diferentes modos:

- **Select ViewPort:** Joga na janela atual.
- **New Editor Window:** Abre uma nova janela para jogar.
- **Standalone Game:** Executa o jogo em um processo separado.
- **Simulate:** Simula o jogo sem controlar o personagem, ótimo para testar lógica e IA.

{% include figure image_path="/assets/images/unreal/interface-editores/02-button-play-menu.webp" alt="Buttom Play" %}

---

## Dicas Finais

- Explore cada painel e ferramenta sem medo!
- Use atalhos de teclado para agilizar seu trabalho ([Guia de atalhos do Unreal Engine](https://www.unrealengine.com/en-US/tech-blog/designer-s-guide-to-unreal-engine-keyboard-shortcuts)).
- Personalize o layout para se sentir em casa.
- Consulte a [documentação oficial](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface) sempre que tiver dúvidas.

---

**Agora que você já conhece a interface, está pronto para criar mundos incríveis! Continue explorando e divirta-se no Unreal Engine!
