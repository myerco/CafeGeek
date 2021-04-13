---
title: RenderDoc
description: **RenderDoc** é uma ferramenta de depuração de quadros de código aberto e gratuita que pode ser usada para analisar quadros únicos gerados por outros programas de software, como jogos.
tags: [Unreal Engine,RenderDoc]
---

# RenderDoc
Neste capitulo vamos apresentar o aplicativo RenderDoc.

## Índice
1. [O aplicativo e plugin Renderdoc](#1)
1. [Ativando o Plugin no Unreal Engine 4](#2)

<a name="1"></a>
## 1. O aplicativo e plugin Renderdoc
**RenderDoc** é uma ferramenta de depuração de quadros de código aberto e gratuita que pode ser usada para analisar quadros únicos gerados por outros programas de software, como jogos.

<a name="2"></a>
## 2 Ativando o Plugin no Unreal Engine 4
1. Plugin     
  ![ue4_renderdoc_plugin](imagens/ue4_renderdoc_plugin.jpg)  

    *Figura: Edit->Plugins*  
1. Instalação do aplicativo no Windows.       
  [Baixe aqui](https://renderdoc.org/)
1. Capturando o frame desejado.        
  ![ue4_renderdoc_plugin_view](imagens/ue4_renderdoc_plugin_view.jpg)      

    *Figura: Icon no Viewport*

1. Carregando o frame capturado.        
  ![ue4_renderdoc](imagens/ue4_renderdoc.jpg)

    *Figura: Aba Localhost - UEEditor*  

1. Apresentando a textura carregada e suas saídas por processamento.        
  ![ue4_renderdoc_texture_viewer](imagens/ue4_renderdoc_texture_viewer.jpg)

    *Figura: A aba Textures Viewer*  
1. Lista de elementos renderizados por ordem de execução.   
  ![ue4_renderdoc_event_browser](imagens/ue4_renderdoc_event_browser.jpg)

    *Figura: Event Browser*  
  - Para apresentar o tempo de duração de cada Drawcall clique em **Time Durations for the Drawcalls**.

---
## Referências
1. [RenderDoc](https://en.everybodywiki.com/RenderDoc)
1. [RenderDoc Documentação](https://renderdoc.org/docs/index.html)
