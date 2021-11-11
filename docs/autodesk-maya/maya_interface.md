---
title: Maya Interface e comandos básicos
description: Maya Interface e comandos básicos  
keywords: [Desonvolvimento com Unreal Engine, Maya]
tags: [Unreal Engine, jogos digitais, Maya]
layout: page
---

## Interface básico
1. [Menus](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-Basics/files/GUID-D90A2BDB-FD05-4528-8A95-C33A02D15129-htm.html)
   - Create - Cria objetos
   - Select - Seleciona objetos;
   - Modify - modifica objetos;
   - Display - apresenta objetos;
   - Windows - Apresenta e configura os Editores;
1. Barra de tarefas
   - Modeling toolKit.
1. Fluxos de trabalho
1. [Tools box](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2018/ENU/Maya-Basics/files/GUID-B345E162-0149-4E09-AC98-48DCFC227F33-htm.html)
1. Layout
1. [Outliner](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-Basics/files/GUID-4B9A9A3A-83C5-445A-95D5-64104BC47406-htm.html)
1. [Workspace](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2019/ENU/Maya-Basics/files/GUID-0384C282-3CA1-4587-9775-F7164D3F6980-htm.html)
   - Modeling - Standard

## Configurando a Interface   
1. Para habilitar ou desabilitar a janela inicial de avisos de mudanças de versão.
   - Windows > Settings / Preferences > Preferences > `Show - What´s new`
1. Window > Settings / Preferences > Preferences
   - Interface (Menu Set,Show...)  

## Configurando projetos
1. Configurando as pastas do projeto
  - File > Project Window
1. Criando novas cenas
  - File > New Scene
1. Configurando projeto novos importados
  - File > Set Project

## Comandos de navegação
1. Alt + RMB - Movimentação de câmera.
1. Alt + LMB - Zoom.
1. Alt + Scroll - Scroll da a câmera.
1. Scroll - Zoom

## Configuração de ViewPort
1. Mostrando a quantidade de polígonos e vértices.
   - [Display > Heads Up Display > Poly Count](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2019/ENU/Maya-Modeling/files/GUID-53E46D0C-4B7B-4404-AEB0-3BDD1FF8608A-htm.html).    
1. Visualização
    1. [Shading](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-Basics/files/GUID-C6188583-EA9E-4880-AAE7-8D895FD94DD6-htm.html)
1. Hotbox - pressione a barra de espaço
1. RMB - Menu de contexto


## Seleção de objetos
1. Seleciona um objetos.
1. Seleciona elementos do objeto.
1. CTRL + RMB - Adiciona um elemento na Seleção      
1. CTRL + LMB - Remove um elemento da Seleção      
1. CTRL no ícone para entrar nas configurações.
1. Shift + 2 click no elemento ao lado - Seleciona todos os elementos ao redor

## Pivot
1. Modify > Center Pivot
Centralizar pivot
1. Movendo Pivot
Tecla D
1. Snap to points para alinhar o pivot nos elementos.

## Extrude
1. Extrude
    - shift + mouse (Move tool Preferences > Smart Duplicate Settings > Shift + drag to..)
    - Ctrl + E
    - Menu > Edit Mesh > Extrude
1. Adicionando edges
    - Menu > Mesh Tools > Insert Edge loop
    - Mesh Tools > Insert Edge loop Settings > Number of edge loops

## Bevel
1. Ctrl + B
    - Fraction - espaço entre segmentos
    - Segments - Número de segmentos

## Removendo edges
1. Ctrl + Backspace - Remove edges e vértices.

## Multicut
Cuidado não podemos ter vértices sem conexão com outros
1. Adicione edges    

## Merge de vértices
1. Menu > Edit Mesh  > Merge (Antes Selecione dois vértices)

## Organizando
1.  Layer
- V - Mostra ou oculta uma camada. Consulte Ocultar camadas de exibição para obter mais informações.
- P - Um "P" na caixa significa que a camada está visível durante a reprodução. Desligue o "P" para ocultar a camada durante a reprodução.
- T - Um “T” significa que os objetos na camada são modelados: eles são exibidos em estrutura de arame e não podem ser selecionados. Um “R” significa que os objetos aos quais a camada está referenciada: eles não podem ser selecionados, mas mantêm o modo de exibição atual. Uma caixa em branco significa que os objetos na camada são normais e podem ser selecionados.


## Grupos

1. Hierarquia
  MMB (Botão do meio) arreste os elementos para dentro de outros.
  Selecionando o objeto principal todos os objetos são selecionados.
  As alterações do objeto principal refletem em todos os objetos.
1. Selecione os objetos (ctrl+G)  
  Diferente de Hierarquia é criado um objeto separado para controlar os demais.

## Combine e Separate
1. Combine - Selecione os objetos `Mesh` > `Combine`
1. Separate - Selecione o objeto `Mesh` > `Separate` vai ser criado um grupo.

## Duplicando
1. Duplicando - Ctrl + D
1. Duplicando aproveitando a transformação  -  shift + D

## Booleans

1. `Mesh` > `Booleans`

## Modelagem NURBS

1. Revolve
  1. Ordem de seleção do objeto altera a forma final;
  1. A curva fica associada ao objeto criado até que o histórico seja removido;
1. Loft
1. Extrude
  1. É possível criar um objeto poligonal na construção usando as configurações
1. Isoparm
  1. É possível separar ou juntar usando `Surface` > `Detach` ou `Attach`
1. Project Curve on Surface
  1. Trim Tool para cortar surface

## Texturas

## Desenho 3D Modeling

## Materiais
- Render
  - Menu: `Arnold` > `Arnold RenderView`
  - Cameras
  - Iluminação
## Tipos de Materiais (Maya)
- Lambert (simples sem reflexo, brilho e transparência)
  - Color: cor do material
  - transparência: Aumenta o alpha
  - Ambiente color: aumenta a tonalidade da cor
  - Incandescência: Adiciona uma luz ao material
  - Bump Mapping: adiciona textura para associar rugosidade ou padrões.
  - Diffuse: Torna mais claro ou escuro a cor
- Blind (Com brilho e reflexo)
  - Specular [Reflexão especular](https://pt.wikipedia.org/wiki/Reflex%C3%A3o_especular)
  - Eccentricty: Aumenta o brilho
  - Specular Roll off: Desfoque aplicado no brilho
  - Specular color : Cor do brilho   
  - Reflectivity: Aumenta a intensidade do reflexo
- [Phong](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Maya/files/GUID-3EDEB1B3-4E48-485A-9714-9998F6E4944D-htm.html) (Parecido com o Blind mas com mais parâmetros)  
  - Specular Shadding
  - Roughness: rugosidade
  - Highlight size: tamanho do desfoque
- Anisotropic
  - Specular Shader
  - Angle: ângulo da luz


## Mapeamento UV
- Menu `UV` > `UV Editor`;
- Painéis lado a lado
  - ViewPort `Panels` > `Saved Layouts` > `Persp/UV Editor`
- Menu UV toolKit
  - `Tools` > `Show UV toolKit`
- UV Shells : Context Menu > UV > select vertex > ctrl > context menu > To UV shells

## Preferências
- [maya](https://help.autodesk.com/view/MAYAUL/2020/ENU/)
- [Mapeamento UV](https://pt.wikipedia.org/wiki/Mapeamento_UV)
