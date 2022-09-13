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

- [Modelagem 3D](modelagem_usando_autodesk_maya.html#modelagem-3d)

  - [O que é Modelagem de objetos 3D?](modelagem_usando_autodesk_maya.html#o-que-é-modelagem-de-objetos-3d)

  - [Tipos de modelagem 3D](modelagem_usando_autodesk_maya.html#tipos-de-modelagem-3d)

  - [Processo de construção de cenas 3D](modelagem_usando_autodesk_maya.html#processo-de-constru--o-de-cenas-3d)

  - [Softwares para modelagem tridimensional](modelagem_usando_autodesk_maya.html#softwares-para-modelagem-tridimensional)

- [Começando a trabalhar com Autodesk Maya](modelagem_usando_autodesk_maya.html#come-ando-a-trabalhar-com-autodesk-maya)

  - [Interface básico](modelagem_usando_autodesk_maya.html#interface-b-sico)

  - [Configurando a Interface](modelagem_usando_autodesk_maya.html#configurando-a-interface)

  - [Configurando projetos](modelagem_usando_autodesk_maya.html#configurando-projetos)
  
  - [Configuração de ViewPort](modelagem_usando_autodesk_maya.html#configura--o-de-viewport)  

- [Comandos de navegação](modelagem_usando_autodesk_maya.html#comandos-de-navegação)

  - [Snap de objetos](modelagem_usando_autodesk_maya.html#snap-de-objetos)

- [Seleção de objetos e componentes](modelagem_usando_autodesk_maya.html#seleção-de-objetos-e-componentes)

  - [Utilizando Soft Selection](modelagem_usando_autodesk_maya.html#utilizando-soft-selection)

  - [Simetria ou Symmetry](modelagem_usando_autodesk_maya.html#simetria-ou-symmetry)

- [Organização de objetos na cena](modelagem_usando_autodesk_maya.html#organizando-em-camadas)  

  - [Layer](modelagem_usando_autodesk_maya.html#layer)

  - [Hierarquia](modelagem_usando_autodesk_maya.html#hierarquia)  

  - [Grupos](modelagem_usando_autodesk_maya.html#group)

- [Edit](modelagem_usando_autodesk_maya.html#)

  - [Duplicando objetos](modelagem_usando_autodesk_maya.html#duplicando-objetos)

- [Modify](modelagem_usando_autodesk_maya.html#)

  - [Pivot](modelagem_usando_autodesk_maya.html#pivot)

  - [Freeze e Reset parâmetros](modelagem_usando_autodesk_maya.html#freeze-e-reset-parâmetros)

- [Display](modelagem_usando_autodesk_maya.html#)  

  - [Hide/Show](modelagem_usando_autodesk_maya.html#hide)

- [Mesh](modelagem_usando_autodesk_maya.html#)

  - [Fill Hole](modelagem_usando_autodesk_maya.html#fill-hole)

  - [Combine e Separate](modelagem_usando_autodesk_maya.html#combine-e-separate)

  - [Booleans](modelagem_usando_autodesk_maya.html#booleans)

- [Edit Mesh](modelagem_usando_autodesk_maya.html#)  

  - [Extrude](modelagem_usando_autodesk_maya.html#extrude)

  - [Merge de vértices](modelagem_usando_autodesk_maya.html#merge-de-v-rtices)  

  - [Append e Bridged Tool](modelagem_usando_autodesk_maya.html#append-e-bridged-tool)

  - [Bevel](modelagem_usando_autodesk_maya.html#bevel)

  - [Extract](modelagem_usando_autodesk_maya.html#extract)  

- [Mesh Tools](modelagem_usando_autodesk_maya.html#)  

  - [Adicionando edges](modelagem_usando_autodesk_maya.html#adicionando-edges)

  - [Removendo edges](modelagem_usando_autodesk_maya.html#removendo-edges)

  - [Multicut](modelagem_usando_autodesk_maya.html#multicut)

  - [Target Weld](modelagem_usando_autodesk_maya.html#target-weld)  

- [Modelagem NURBS](modelagem_usando_autodesk_maya.html#modelagem-nurbs)

- [Materiais](modelagem_usando_autodesk_maya.html#materiais)

  - [Tipos de Materiais (Maya)](modelagem_usando_autodesk_maya.html#tipos-de-materiais--maya-)

- [Mapeamento UV](modelagem_usando_autodesk_maya.html#mapeamento-uv)

- [Animando cenas no Autodesk Maya](modelagem_usando_autodesk_maya.html#animando-cenas-no-autodesk-maya)

- [Primeiros passos na modelagem 3D](modelagem_usando_autodesk_maya.html#primeiros-passos-na-modelagem-3d)

- [Modelagem 3D Luz, Câmera e Ação](modelagem_usando_autodesk_maya.html#modelagem-3d-luz--c-mera-e-a--o)

***

- [Modelagem 3D](#modelagem-3d)
- [O que é Modelagem de objetos 3D?](#o-que---modelagem-de-objetos-3d-)
- [Tipos de modelagem 3D](#tipos-de-modelagem-3d)
- [Processo de construção de cenas 3D](#processo-de-constru--o-de-cenas-3d)
- [Softwares para modelagem tridimensional](#softwares-para-modelagem-tridimensional)
- [Começando a trabalhar com Autodesk Maya](#come-ando-a-trabalhar-com-autodesk-maya)
- [Interface básico](#interface-b-sico)
- [Configurando a Interface](#configurando-a-interface)
- [Configurando projetos](#configurando-projetos)
- [Comandos de navegação](#comandos-de-navega--o)
- [Configuração de ViewPort](#configura--o-de-viewport)
- [Freeze e Reset parâmetros](#freeze-e-reset-par-metros)
- [Snap de objetos](#snap-de-objetos)
- [Seleção de objetos e componentes](#sele--o-de-objetos-e-componentes)
- [Utilizando Soft Selection](#utilizando-soft-selection)
- [Simetria ou Symmetry](#simetria-ou-symmetry)
- [Duplicando objetos](#duplicando-objetos)
- [Pivot](#pivot)
- [Extrude](#extrude)
- [Adicionando edges](#adicionando-edges)
- [Bevel](#bevel)
- [Removendo edges](#removendo-edges)
- [Multicut](#multicut)
- [Merge de vértices](#merge-de-v-rtices)
- [Extract](#extract)
- [Append e Bridged Tool](#append-e-bridged-tool)
- [Fill Hole](#fill-hole)
- [Target Weld](#target-weld)
- [Organizando em camadas](#organizando-em-camadas)
- [Layer](#layer)
- [Hierarquia](#hierarquia)
- [Group](#group)
- [Combine e Separate](#combine-e-separate)
- [Booleans](#booleans)
- [Modelagem NURBS](#modelagem-nurbs)
  * [Objetos primitivos](#objetos-primitivos)
    + [Esfera](#esfera)
    + [Cubo](#cubo)
    + [Cilindro](#cilindro)
    + [Plano](#plano)
  * [Componentes de seleção](#componentes-de-sele--o)
  * [Revolve](#revolve)
  * [Loft](#loft)
  * [Extrude Nurbs](#extrude-nurbs)
  * [Isoparm](#isoparm)
  * [Project Curve on Surface](#project-curve-on-surface)
  * [Convertendo NURBS para poligonais](#convertendo-nurbs-para-poligonais)
- [Materiais](#materiais)
  * [Criando materiais](#criando-materiais)
  * [Tipos de Materiais (Maya)](#tipos-de-materiais--maya-)
- [Mapeamento UV](#mapeamento-uv)
- [Hide](#hide)
- [Animando cenas no Autodesk Maya](#animando-cenas-no-autodesk-maya)
- [Primeiros passos na modelagem 3D](#primeiros-passos-na-modelagem-3d)
- [Modelagem 3D Luz, Câmera e Ação](#modelagem-3d-luz--c-mera-e-a--o)
