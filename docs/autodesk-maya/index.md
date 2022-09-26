---
title: Modelagem usando Autodesk Maya
description: Modelagem com Autodesk Maya
keywords: [Autodesk Maya, modelagem 3d]
tags: [Autodesk Maya, modelagem 3d]
layout: page
---

O objetivo deste curso é apresentar e construir elementos na ferramenta de modelagem artística 3D Autodesk Maya. O curso está associado a construção **Estética** do jogo pois nele construímos elementos para representar a narrativa e a jogabilidade.

**Habilidades que serão aprendidas.**

- Interface e estrutura de menus;
- Configuração de ambiente de trabalho e projeto;
- Movimentação, dimensionamento e Rotacionamento de objetos;
- Extrudar, inserir e deformar elementos;
- Mapeamento UV;
- Iluminação de cenas;
- Animação de elementos;
- Construção de objetos com NURBS;

| M         |  D          | A         |
|:-         |:-           |:-         |
| Mecânicas | Dinâmicas   | **Estéticas** |

***

- [O que é Modelagem de objetos 3D?](modelagem_usando_autodesk_maya.html#modelagem_usando_autodesk_maya#o-que---modelagem-de-objetos-3d-)
  - [Tipos de modelagem 3D](modelagem_usando_autodesk_maya#tipos-de-modelagem-3d)
  - [Processo de construção de cenas 3D](modelagem_usando_autodesk_maya#processo-de-constru--o-de-cenas-3d)
  - [Softwares para modelagem tridimensional](modelagem_usando_autodesk_maya#softwares-para-modelagem-tridimensional)
- [Começando a trabalhar com Autodesk Maya](modelagem_usando_autodesk_maya#come-ando-a-trabalhar-com-autodesk-maya)
  - [Interface](modelagem_usando_autodesk_maya#interface)
  - [Configurando a Interface](modelagem_usando_autodesk_maya#configurando-a-interface)
  - [Configurando projetos](modelagem_usando_autodesk_maya#configurando-projetos)
  - [Comandos de navegação](modelagem_usando_autodesk_maya#comandos-de-navega--o)
  - [Configuração de ViewPort](modelagem_usando_autodesk_maya#configura--o-de-viewport)
    - [Mostrando a quantidade de polígonos e vértices](modelagem_usando_autodesk_maya#mostrando-a-quantidade-de-pol-gonos-e-v-rtices)
    - [Visualização](modelagem_usando_autodesk_maya#visualiza--o)
    - [Hotbox](modelagem_usando_autodesk_maya#hotbox)
- [Objetos Poligonais](modelagem_usando_autodesk_maya#objetos-poligonais)
  - [Menu de contexto para manipulação de malhas](modelagem_usando_autodesk_maya#menu-de-contexto-para-manipula--o-de-malhas)
  - [Freeze e Reset parâmetros](modelagem_usando_autodesk_maya#freeze-e-reset-par-metros)
  - [Snap de objetos](modelagem_usando_autodesk_maya#snap-de-objetos)
  - [Seleção de objetos e componentes](modelagem_usando_autodesk_maya#sele--o-de-objetos-e-componentes)
  - [Utilizando Soft Selection](modelagem_usando_autodesk_maya#utilizando-soft-selection)
  - [Simetria ou Symmetry](modelagem_usando_autodesk_maya#simetria-ou-symmetry)
  - [Duplicando objetos](modelagem_usando_autodesk_maya#duplicando-objetos)
  - [Pivot](modelagem_usando_autodesk_maya#pivot)
  - [Deformando a malha poligonal](modelagem_usando_autodesk_maya#deformando-a-malha-poligonal)
    - [Extrude](modelagem_usando_autodesk_maya#extrude)
    - [Adicionando edges](modelagem_usando_autodesk_maya#adicionando-edges)
    - [Bevel](modelagem_usando_autodesk_maya#bevel)
    - [Removendo edges](modelagem_usando_autodesk_maya#removendo-edges)
    - [Multicut](modelagem_usando_autodesk_maya#multicut)
    - [Merge de vértices](modelagem_usando_autodesk_maya#merge-de-v-rtices)
  - [Suavizando objetos poligonais](modelagem_usando_autodesk_maya#suavizando-objetos-poligonais)
    - [Smooth](modelagem_usando_autodesk_maya#smooth)
    - [Visualizando a suavização](modelagem_usando_autodesk_maya#visualizando-a-suaviza--o)
    - [Extract](modelagem_usando_autodesk_maya#extract)
  - [Append e Bridged Tool](modelagem_usando_autodesk_maya#append-e-bridged-tool)
  - [Fill Hole](modelagem_usando_autodesk_maya#fill-hole)
  - [Target Weld](modelagem_usando_autodesk_maya#target-weld)
  - [Combine e Separate](modelagem_usando_autodesk_maya#combine-e-separate)
  - [Booleans](modelagem_usando_autodesk_maya#booleans)
- [Organizando em camadas](modelagem_usando_autodesk_maya#organizando-em-camadas)
- [Layer](modelagem_usando_autodesk_maya#layer)
- [Hierarquia](modelagem_usando_autodesk_maya#hierarquia)
- [Group](modelagem_usando_autodesk_maya#group)
- [Modelagem NURBS](modelagem_usando_autodesk_maya#modelagem-nurbs)
  - [Objetos primitivos](modelagem_usando_autodesk_maya#objetos-primitivos)
    - [Esfera](modelagem_usando_autodesk_maya#esfera)
    - [Cubo](modelagem_usando_autodesk_maya#cubo)
    - [Cilindro](modelagem_usando_autodesk_maya#cilindro)
    - [Plano](modelagem_usando_autodesk_maya#plano)
  - [Componentes de seleção](modelagem_usando_autodesk_maya#componentes-de-sele--o)
    - [CV](modelagem_usando_autodesk_maya#cv)
    - [Edit Points](modelagem_usando_autodesk_maya#edit-points)
    - [Hulls](modelagem_usando_autodesk_maya#hulls)
    - [Isoparms](modelagem_usando_autodesk_maya#isoparms)
  - [Curve Tools](modelagem_usando_autodesk_maya#curve-tools)
  - [Revolve](modelagem_usando_autodesk_maya#revolve)
  - [Loft](modelagem_usando_autodesk_maya#loft)
  - [Extrude Nurbs](modelagem_usando_autodesk_maya#extrude-nurbs)
  - [Isoparm](modelagem_usando_autodesk_maya#isoparm)
    - [Separar objetos](modelagem_usando_autodesk_maya#separar-objetos)
    - [Inserindo Isoparms](modelagem_usando_autodesk_maya#inserindo-isoparms)
  - [Close e Open](modelagem_usando_autodesk_maya#close-e-open)
    - [Preenchendo uma superfície de um objeto](modelagem_usando_autodesk_maya#preenchendo-uma-superf-cie-de-um-objeto)
    - [Preenchendo o espaço entre dois objetos](modelagem_usando_autodesk_maya#preenchendo-o-espa-o-entre-dois-objetos)
  - [Project Curve on Surface](modelagem_usando_autodesk_maya#project-curve-on-surface)
  - [Convertendo NURBS para poligonais](modelagem_usando_autodesk_maya#convertendo-nurbs-para-poligonais)
- [Sculpting](modelagem_usando_autodesk_maya#sculpting)
- [Materiais](modelagem_usando_autodesk_maya#materiais)
  - [Criando materiais](modelagem_usando_autodesk_maya#criando-materiais)
  - [Tipos de Materiais (Maya)](modelagem_usando_autodesk_maya#tipos-de-materiais--maya-)
- [Mapeamento UV](modelagem_usando_autodesk_maya#mapeamento-uv)
- [Hide](modelagem_usando_autodesk_maya#hide)
- [Animando cenas no Autodesk Maya](modelagem_usando_autodesk_maya#animando-cenas-no-autodesk-maya)
