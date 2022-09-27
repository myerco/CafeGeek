---
title: Autodesk Maya
description: Modelagem com Autodesk Maya
keywords: [Autodesk Maya, modelagem 3d]
tags: [Autodesk Maya, modelagem 3d]
categories: Autodesk Maya
author: 
- Cafegeek
layout: post
date: 2022-09-26 
---

## O que é Modelagem de objetos 3D?

Podemos entender a Modelagem 3D como a criação de objetos sólidos através da representação matemática de uma superfície ou de um objeto volumétrico, vivo ou inanimado. É a criação do modelo de um objeto tridimensional através de um software de processamento 3D.

{% include image.html
    src="https://ecdd.infnet.edu.br/wp-content/uploads/sites/7/2021/04/modelo-3d-lowpoly-1024x576.jpg"
    alt="Figura: Cabeça low poly de um modelo 3D (fonte: TurboSquid)"
    caption="Figura: Cabeça low poly de um modelo 3D (fonte: TurboSquid)"
%}

Podemos aplicar em várias áreas como por exemplo:

- Design, Engenharia e Produção de Produtos;

- Arquitetura e Engenharia Civil, Elétrica, Mecânica;

- Cinema e Jogos;

- Ilustrações.

### Tipos de modelagem 3D

- **Hard Surface** - (superfícies duras), são quaisquer objetos feitos ou construídos pelo homem. Exemplos de *hard surface* podem ser estruturas arquitetônicas, veículos, robôs, entre outros;

- **Organic** - (Orgânicos) são modelos, obviamente, orgânicos, ou seja, que existem na natureza. Isso inclui humanos, animais, árvores, pedras, terrenos, etc;

- **Render** - Fase para gerar a Iluminação e renderizar toda a cena.

### Processo de construção de cenas 3D

**Conceito** - *Concept art* ou arte conceitual;

{% include image.html
    src="https://cdnb.artstation.com/p/media_assets/images/images/000/649/263/large/sketch_viking_house.jpg?1600679970"
    alt="Figura: Arte conceitual (Artstation)"
    caption="Figura: Arte conceitual (Artstation)"
%}

**Modelagem** - Construção de modelos tridimensionais;

{% include image.html
    src="https://blenderartists.org/uploads/default/original/4X/f/d/0/fd0375c46a3df8b8fd489ab6a1d259b28ecb3ec4.jpeg"
    alt="Figura: Modelo tridimensional Blue Wooden house - <https://blenderartists>"
    caption="Figura: Modelo tridimensional Blue Wooden house - <https://blenderartists>"
%}

**Configuração de layout de cena** - Mapeamento, Iluminação e geração de câmeras;

{% include image.html
    src="https://blenderartists.org/uploads/default/original/4X/5/5/9/559c984fb29dadab1ae2cab740d99e94bd371779.jpeg"
    alt="Figura: Modelo tridimensional com Mapeamento e Iluminação Blue Wooden house - <https://blenderartists>"
    caption="Figura: Modelo tridimensional com Mapeamento e Iluminação Blue Wooden house - <https://blenderartists>"
%}

- **Geração de cenas** - Renderização e animação.

### Softwares para modelagem tridimensional

Segue abaixo quatro ferramentas para arte tridimensional e animação 3D. Todas elas tem versões educacionais gratuitas para praticar.

- Substance Painter;

- Autodesk Maya;

- Autodesk Mudbox

- Blender;

***

## Começando a trabalhar com Autodesk Maya

### Interface

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

    Apresenta todos os objetos da cena.

    Os objetos são representados por ícones;

    Facilita a seleção de objetos;

    Permite filtrar por tipo de objeto com a opção `Show`;

    - `Menu` > `Window` > `Outliner`;

1. [Workspace](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2019/ENU/Maya-Basics/files/GUID-0384C282-3CA1-4587-9775-F7164D3F6980-htm.html)

   - Modeling - Standard

1. `Channel Box`

    Ctrl + A para apresentar a ferramenta;

    Apresenta os parâmetros do objeto (`transalte`, `rotate` e `Scale`) de forma resumida;

    Permite alterar o nome do objeto;

1. `Atribute Editor`

    Parece com o `Channel Box` mas com mais opções.

    - Aba do nome do objeto - Parâmetros de transformação do objeto;

    - As outras abas tem todos as ferramentas aplicadas no objeto.

### Configurando a Interface

`Windows` > `Settings/Preferences` > `Preferences` > `Show - What´s new`

Habilita ou desabilita a janela inicial de avisos de mudanças de versão.

`Window` > `Settings/Preferences` > `Preferences`

Configurar a interface

`Interface` > (Menu Set,Show...)  

### Configurando projetos

`File` > `Project Window`

Para configurar as pastas do projeto utilize a opção acima. Configurar uma pasta de trabalho auxilia na organização dos arquivos que irão compor a cena.

`File` > `Set Project`

Quando importamos um novo projeto de outra máquina podemos configurar a pasta de trabalho ou pasta de projeto.

`File` > `New Scene`

Cria novas cenas, uma cena pode conter vários elementos e deverão estar separados e organizados.

### Comandos de navegação

- Alt + RMB - Movimentação de câmera;

- Alt + LMB - Zoom;

- Alt + Scroll - Scroll da a câmera;

- Scroll - Zoom;

### Configuração de ViewPort

#### Mostrando a quantidade de polígonos e vértices

`Display` > `Heads Up Display` > `Poly Count`[ [Poly Count](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2019/ENU/Maya-Modeling/files/GUID-53E46D0C-4B7B-4404-AEB0-3BDD1FF8608A-htm.html) ]

#### Visualização

Este menu Sombreamento é exibido acima da visualização da cena ou acima de cada painel de visualização em um layout com várias visualizações de cena (como o layout de quatro visualizações).

|Tecla|                                                 |
|:-:  |:-                                               |
|0    |Configuração de exibição de qualidade padrão     |
|1    |Configuração de exibição de qualidade aproximada |
|2    |Configuração de exibição de qualidade média      |
|3    |Configuração de exibição de qualidade suave      |
|4    |Estrutura de arame                               |
|5    |Exibição sombreada                               |
|6    |Exibição sombreada e texturizada                 |
|7    |Usar todas as luzes                              |

- [Shading](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-Basics/files/GUID-C6188583-EA9E-4880-AAE7-8D895FD94DD6-htm.html)

- [Atalhos de teclado do Autodesk Maya](https://www.autodesk.com.br/shortcuts/maya)

#### Hotbox

Pressione a barra de espaço

{% include image.html
    src="https://forums.autodesk.com/autodesk/attachments/autodesk/area-b201/85095/1/likethis.PNG"
    alt="Figura: Space bar."
    caption="Figura: Space bar."
%}

## Objetos Poligonais

{% include image.html
    src="https://i.ytimg.com/vi/7sR_Tux5u7M/maxresdefault.jpg"
    alt="Figura: Autodesk Maya objetos poligonais."
    caption="Figura: Autodesk Maya objetos poligonais."
%}

Uma malha poligonal é uma coleção de arestas, faces e pontos de conexão usados ​​para fornecer um modelo poligonal para modelagem 3D e animação por computador. Sua composição geométrica pode ser armazenada para facilitar vários tipos de simulação de renderizações tridimensionais [[DEFINERTEC](https://definirtec.com/malha-poligonal/)].

### Menu de contexto para manipulação de malhas

Selecione uma objeto e presssione LMB para acessar o menu de contexto.

{% include image.html
    src="https://simplymaya.com/forum/attachment.php?attachmentid=56228&stc=1&thumb=1&d=1540913195"
    alt="Figura: Context Menu."
    caption="Figura: Context Menu."
%}

Os componentes dos objetos poligonais são:

- `Vertex` - Vértices;

- `Edge` - Arestas;

- `Face` - Faces.

### Freeze e Reset parâmetros

Ao deformar ou movimentar um objeto as coordenadas X,Y Z serão alteradas conforme informado pelo usuário, é interessante ao exportar para outra ferramenta, como por exemplo o Unreal, zerar essas coordenadas para que representem o ponto central do objeto na cena, para isso usamos:

- `Modify` > `Freeze transformations` - Zera as coordenadas do objeto;

- `Modify` > `Reset Transformations` - Retorna o pivo ao centro da cena;

- `Modify` > `Center Pivo` - Posiciona o pivo ao centro do objeto;

### Snap de objetos

Esta ferramenta é para alinhar o objeto a uma determinada coordenada ou objeto.

O pivo do objeto é a referência de alinhamento.

`Snap to grid`

Ou tecla X - Alinha o pivo no grid da cena. Para movimentar rapidamente para qualquer parte da cena ou parte de outro elemento/objeto:

- selecione o objeto com `Move Tool`;

- Posicione o mouse onde você gostaria que objeto se deslocasse;

- Mantendo a tecla X pressionada aperte o botão de rolagem do mouse (Sroll) e movimente *levemente*.

`Snap to points`

Ou tecla V - Alinha o pivo em um componente na cena;

- Mantendo a tecla V pressionada aperte o botão de rolagem do mouse (Sroll) e movimente *levemente* o objeto será alinhado ao ponto selecionado.

### Seleção de objetos e componentes

`Select Tool`

Seleciona objetos.

- Tecla Shitf + LMB para selecionar remover ou vários objetos;

- Ao adicionar novos objetos na seleção o ícone (+) é apresentado e ao remover objetos o ícone (-) é apresentado;

- É possível selecionar usando a aba `Outliner` ou segurando e arrastando o mouse;

- Tecla CTRL no ícone para entrar nas configurações;

- Shift + 2 click no elemento ao lado seleciona todos os elementos ao redor;

`Laso Tool`

Seleciona objetos usando a movimentação livre do mouse

- Ideal para componentes, como por exemplo: Vértices, Arestas e faces;
  
`Menu` > `Select`

Podemos variar as formas de seleção de objetos e elementos, como por exemplo:

- `All` e `Deselect All`- Seleciona e remove a seleção de todos os objetos da cena;

- `All by Type` - Seleciona por tipo de objeto;

- `Inverte` - Inverte a seleção;

### Utilizando Soft Selection

Para realizar uma seleção mais *Suave* podemos utilizar a ferramenta `Soft Selection`, a seguir um exemplo usando um objeto `Polygon Plane` com 50x50 divisões e aumentar a escala [[Soft Selection](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2022/ENU/Maya-Basics/files/GUID-FF7C8670-97C7-4C13-9A6F-3B0A8F881EC9-htm.html)].

`Move Tool` > `Soft Selection`

Configura a ferramenta ou e ative `Soft Selection` na ferramenta de seleção;

Apertando a tecla B é possível atividar e desativar a ferrmenta;

 Após configurar a ferramenta podemos selecionar novamente os vértices `Vertex` e perceba que a seleção e movimentação dos componentes estão mais arredondados;

`Falloff Radius`

Determina o raio da seleção.

Tecla B + LMB aumenta o raio da seleção;

`Falloff color`

As cores mais escuras determinan a suaviação dos elementos envolvidos na seleção;

`Curve presets`

 Determina o tipo de curvatura;

### Simetria ou Symmetry

`Move Tool` > `Symmetry Settings`

Seleciona elementos simtricamente alinhados em um determinado eixo.

- `Symmetry` - Escolha o eixo;

### Duplicando objetos

`Edit` > `Duplicate`

Ctrl + D - Duplica;

Shift + D - Aproveitando a transformação;

`Duplicate with Transform`

 Duplica objetos e adiciona uma transformação, exemplo, duplique o primeiro objeto e depois pressine a tecla Shift + D;

`Duplicate Special`

Configura a opções de cópia:
  
- `Copy` - É criada uma copia do objeto sem nenhuma ligação ao objeto original;

- `Instance` - Os comandos aplicados no novo objeto refletem na origem;

Podemos criar várias copias e alterar as configurações dos parâmetros de cada uma delas, por exemplo:

- `Translate` - eixo Z = 10;

- `Rotate` - exito Z = 20;

- `Number od copies` = 20;

Logo em seguida clique em `Apply`.

### Pivot

`Modify` > `Center Pivot`

Centraliza o pivot do objeto.
  
Tecle D para mover o pivot.

`Snap to points`

Alinha o pivot nos elementos.

### Deformando a malha poligonal

#### Extrude

- shift + mouse - `Move tool Preferences` > `Smart Duplicate Settings` > Shift + drag to..)

- Ctrl + E

- `Menu` > `Edit Mesh` > `Extrude`

#### Adicionando edges

- `Menu` > `Mesh Tools` > `Insert Edge loop`;

- `Mesh Tools` > `Insert Edge loop Settings` > `Number of edge loops`;

#### Bevel

1. Ctrl + B ou `Edit Mesh` > `Bevel`

    - Fraction - espaço entre segmentos;

    - Segments - Número de segmentos;

#### Removendo edges

Ctrl + Backspace - Remove edges e vértices.

#### Multicut

Cuidado não podemos ter vértices sem conexão com outros.

Adicione edges.

#### Merge de vértices

`Edit Mesh`  > `Merge`

Selecione dois vértices e aplique a ferramenta.

### Suavizando objetos poligonais

#### Smooth

`Mesh` > `Smooth`

Adiciona mais vertices no objeto, possibilitando esolher a quantidade de divisões.

`Mesh Display` > `Soften Edge`

Suaviza a malha sem adicionar novos vértices.

#### Visualizando a suavização

{% include image.html
    src="imagens/autodesk_maya/autodesk_maya_smooth_view.webp"
    alt="Figura: Visualizando a suavização"
    caption="Figura: Utilizando as teclas 1,2 e 3 podemos visualizar como o objeto deve ficar depois de usar Smooth."
%}

Tecla 1 para visualizar o objeto sem nenhuma divisão;

Tecla 2 para visualizar o objeto suavizado e objeto origem;

Tecla 3 para visualizar somente o objeto suavizado.

`Mesh Tool` > `Offset Edge Loop`

Adiciona dois novos segmentos (arestas) sincronizados na aresta selecionada.

`Mesh Tool` > `Crease`

Selecionando as arestas com LMB e arrastando com o botão do meio podemos puxar as arestas.

`Edit Mesh` >  `Edit Edge Flow`

Ao selecionar uma aresta e escolher a opção acima a aresta acompanha o arrendodamento do objeto.

#### Extract

`Edit Mesh` > `Extract`

Extrai partes de um objeto. Selecione a área para extrair e aplique a ferramenta.

### Append e Bridged Tool

`Edit Mesh` > `Bridge`

Adiciona faces nos objeto .

`Mesh Tool` > `Append to Polygon`

Duas soluções robustas para conectar componentes.

`Bridge tool`

Trabalha com faces poligonais, permitindo não apenas a criação de planos planos.

`Append to Polygon`

É ideal em situações em que você precisa conectar seletivamente partes da mesma malha [[3D Modeling Part 7: Tools and Techniques in Autodesk Maya](https://www.shutterstock.com/blog/3d-modeling-autodesk-maya)].

### Fill Hole

Preenchendo um buraco no objeto.

Para exemplificar, selecione `Edge` e marque todas as arestas adjacentes ao espaço que queremos preencher.

`Mesh` > `Fill Hole`

### Target Weld

Movimenta e solda vertices, selecione `Vertex` e logo em seguida `Mesh Tool` > `Target Weld`.

## Combine e Separate

`Mesh` > `Combine`

Selecione os objetos para que eles fiquem juntos

`Mesh` > `Separate`

Separa os objetos e cria um novo grupo.

## Booleans

Para projetar ou misturar objetos podemos usar [`Booleans`](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Maya/files/GUID-9467513F-47C3-4C73-8251-6FF8C0DE4982-htm.html).

`Mesh` > `Booleans`

- `Union`;
- `Diference`;
- `Intersection`;

## Organizando em camadas

## Layer
  
- V - Mostra ou oculta uma camada. Consulte Ocultar camadas de exibição para obter mais informações.
  
- P - Um "P" na caixa significa que a camada está visível durante a reprodução. Desligue o "P" para ocultar a camada durante a reprodução.
  
- T - Um “T” significa que os objetos na camada são modelados: eles são exibidos em estrutura de arame e não podem ser selecionados.

- R - Um “R” significa que os objetos aos quais a camada está referenciada: eles não podem ser selecionados, mas mantêm o modo de exibição atual. Uma caixa em branco significa que os objetos na camada são normais e podem ser selecionados.

Podemos adicionar uma cor na camada fazendo com que todos os objetos selecionados fiquem com a cor escolhida.

## Hierarquia
  
- MMB (Botão do meio) arreste os elementos em qualquer ordem de apresentação no `Outliner`;

- MMB (Botão do meio) arreste os elementos para dentro de outro para criar uma hierarquia;
  
- Selecionando o objeto principal todos os objetos abaixo dele são selecionados;

- As alterações do objeto principal refletem em todos os objetos.

- Exemplo:

```bash
[+] ObjetoPai
  ->ObjetoFilho1
    ->ObjetoFilho2
  ->ObjetoFilho3 
```

## Group

- Selecione os objetos e pressione Ctrl + G  ou `Edit` > `Group`
  
- Diferente de Hierarquia agora é criado um objeto separado para controlar os demais;

- O objeto Group criado não está na cena, somente no `Outliner`.

- O pivot do objeto é construído no centro da cena;

```bash
[+] Group1
  ->Objeto1
    ->Objeto2
  ->Objeto3 
```

## Modelagem NURBS

NURBS (Non-Uniform Rational B-Splines) é um tipo de geometria que você pode usar para criar curvas e superfícies 3D no Maya. Os outros tipos de geometria fornecidos pelo Maya são superfícies de polígono e subdivisão.

- Não Uniforme refere-se à parametrização da curva. Curvas não uniformes permitem, entre outras coisas, a presença de multi-nós, que são necessários para representar curvas de Bezier.

- Racional refere-se à representação matemática subjacente. Essa propriedade permite que NURBS represente cônicas exatas (como curvas parabólicas, círculos e elipses) além de curvas de forma livre.

- B-splines são curvas polinomiais por partes (splines) que têm uma representação paramétrica.

NURBS são úteis para construir muitos tipos de formas 3D orgânicas devido à natureza suave e mínima das curvas que eles usam para construir superfícies. Os tipos de superfície NURBS são amplamente utilizados nas áreas de animação, jogos, visualização científica e design industrial.

O tipo de dados NURBS 3D pode ser facilmente exportado para aplicativos de software CAD exportando as superfícies usando o formato de arquivo IGES. Além disso, o Maya pode importar muitos tipos de dados bezier e NURBS de muitos aplicativos de software CAD.

Se seus requisitos são usar o tipo de superfície de polígono em suas cenas, você pode inicialmente construir suas superfícies usando NURBS e depois convertê-las em polígonos.

### Objetos primitivos

#### Esfera

São compostos por :

- Star Sweep - Valor de início da curva;

- End Sweep - Valor final da curva;

- Sections - Quantidade de seções da malha (Vertical);

- Spans - Quantidade de `spans` (Horizontal)

#### Cubo

O objeto é uma composição de várias outros **agrupados**.

#### Cilindro

Criando o objeto habilitando a opção `Interactive Creation` as partes superior e inferior do objeto são preenchidas, utilizando uma **hierarquia** de três objetos.

- NurbsCylinder1 > BottomCap1 > TopCap1.

#### Plano

Para aumentar os vértices criados utilizamos : `Patches U` e `Patches V`.

### Componentes de seleção

#### CV

{% include image.html
    src="https://download.autodesk.com/us/maya/2011help/images/MED/Sherlock/NURBS/comp_N19b.png"
    alt="Figura: CVs."
    caption="Figura: CVs."
%}

Control Vertices, controlar como a curva é “puxada” de uma linha reta entre os pontos de edição. Eles são os meios mais básicos e importantes para controlar a forma de uma curva. Linhas entre CVs consecutivos formam o Hull de controle.

O número de CVs é igual ao grau da curva mais um. Assim, por exemplo, uma curva de grau 3 tem quatro CVs por vão. Para aumentar o número de CVs para obter mais controle sobre a forma da curva, você pode aumentar o número de extensões inserindo pontos de edição ou aumentar o grau da curva.

O Maya desenha CVs de forma diferente para permitir que você saiba a diferença entre o início e o fim de uma curva. O primeiro CV (no ponto inicial da curva) é desenhado como uma caixa. O segundo CV é desenhado como um pequeno “U”, para mostrar a dimensão U crescente a partir do ponto inicial. Todos os outros CVs são desenhados como pequenos pontos.

#### Edit Points

{% include image.html
    src="https://download.autodesk.com/us/maya/2011help/images/MED/Sherlock/NURBS/comp_N20a.png"
    alt="Edit Points."
    caption="Figura: Edit Points."
%}

Você pode dizer quando uma curva é feita a partir de vários segmentos de várias maneiras. Uma é procurar pontos de edição na curva. Os pontos de edição marcam o ponto de conexão entre dois segmentos. O Maya desenha pontos de edição como pequenos Xs.

Ao contrário dos pontos de controle na curva das curvas de Bezier (usados em muitos programas de ilustração 2D), os pontos de edição NURBS geralmente não são usados para editar curvas. Os CVs controlam a forma de uma curva NURBS e os pontos de edição são apenas indicadores de quantos spans uma curva possui.

#### Hulls

{% include image.html
    src="https://download.autodesk.com/us/maya/2011help/images/MED/Sherlock/NURBS/comp_N20b.png"
    alt="Figura: Hulls."
    caption="Figura: Hulls."
%}

 À medida que uma curva obtém mais spans e pontos de edição, você pode perder o controle da ordem dos CVs. Para mostrar a relação entre os CVs, o Maya pode traçar linhas entre eles. Essas linhas são chamadas de Hulls.

Os Hull são úteis para vários propósitos:

- Para mostrar a ordem dos CVs em uma cena lotada.

- Para mostrar a forma dos CVs quando seu objeto está tão cheio de CVs que você não pode determinar exatamente quais CVs adjacentes serão afetados quando você ajustar parte de um modelo.

- Para selecionar uma linha inteira de CVs de uma só vez.

#### Isoparms

Silimiar aos Edges dos objetos poligonais.

### Curve Tools

`CV Curve Tool`

Cria Control Vertex e a ligação entre eles, a letra `U` marca a diração da curva. A curva é criada usando a referência dos CVs

`EP Curve Tool`

A curva esta alinhada aos CVs.

`Bezier Curve Tool`

Cria uma curva com CVs usando o controle de angulo Bezier (Segure e arraste).

`Pencil Curve Tool`

Curva de mão livre.

`Three Point Circular Arc`

Curva formada calculando três pontos no espaço.

`Two Point Circular Arc`

Curva formada calculando dois pontos no espaço.

### Revolve
  
Ordem de seleção do objeto altera a forma final;

Escolha o Eixo em `Resolve Options`.

A curva fica associada ao objeto criado até que o histórico seja removido;

### Loft

Possibilita a criação de figuras utilizando várias curvas curva

- Crie uma curva do tipo circulo e depois a duplique;

- Selecione todas as curvas (A última selecionada fica com a cor verde);

- Utilize a ferramenta `Surfaces` > `Loft`

- Os parâmetros do objeto:
  - Degree: Cubic/Linear;

  - Uniform e Close;
  
  - Autreverse - reverte as faces do objeto

### Extrude Nurbs

É possível criar um objeto poligonal na construção usando as configurações:

- Crie um objeto Nurbs qualquer;

- Crie um curva para servir como caminho;

- Selecione os objetos;

- Parametros:
  
  - No objeto podemos fixar o objeto para a curva: CTRL + A - Fixed Path;

  - Rotation e Scale;

### Isoparm
  
#### Separar objetos

É possível separar ou juntar usando `Surface` > `Detach` ou `Attach`

#### Inserindo Isoparms

Selecione um isoparm e logo em seguida utilize `Surface` > `Insert Isoparms`.

### Close e Open

Para curvas abertas utilize `Curve` > `Close` para fechar a curva.

Para objetos do tipo nurbs abertos utilize `Surfaces` > `Close` para fechar a curva.

#### Preenchendo uma superfície de um objeto

`Surface` > `Planar`

Selecione uma curva fechada e aplique a opção `Planar` para preencher a curva.

#### Preenchendo o espaço entre dois objetos

`Surface` > `Loft`

Duplique isoparms de objetos distintos e aplique `Loft` para preencher o espaço entre eles.

### Project Curve on Surface

É possível projetar a imagem de uma curva em outro com :

`Surfaces` > `Project Curve on Surface`

Selecione primeiro o objeto que deve ter a sombra da curva;

A projeção da curva considera a posição da camera;

`Surfaces` > `Trim Tool`  

Corta a superfície desejeda, selecione o que vai ser mantido e pressione `ENTER`.

Todos os itens pontilhados vão ser removidos.

### Convertendo NURBS para poligonais

Para exportar objetos para o Unreal Engine devemos transformar os objetos NURBS em objetos poligonais.

`Modify` > `Convert` > `NURBS to Poligons`

- `Standart fit` - O ajuste padrão é o método de mosaico padrão. É uma tesselação “adaptativa”, o que significa que as opções a seguir são usadas para determinar quando parar a tesselação.

Por exemplo, a tecelagem para no valor de tolerância fracionária que você definiu. Se houver uma aresta mais curta que o comprimento mínimo da aresta, a tesselação para nessa aresta. Se a superfície for plana o suficiente dentro da borda (a razão corda/altura especificada é pequena o suficiente), a tesselação para aí.

- `Type` - Selecione o tipo de polígonos a ser usado ao converter a geometria NURBS em dados poligonais. Se você selecionar Triângulo (o padrão), polígonos de 3 lados serão criados. Se você selecionar Quads, polígonos de 4 lados serão criados.

- `Tessellation` - Tessellation significa que você cria um conjunto de polígonos da geometria NURBS.

>Em [computação gráfica](https://en.wikipedia.org/wiki/Tessellation), tesselação refere-se à divisão de conjuntos de dados de polígonos (às vezes chamados de conjuntos de vértices) apresentando objetos em uma cena em estruturas adequadas para renderização.

## Sculpting

`Sculpt Tool`

`Smooth Tool`

## Materiais

- Render

  - Menu: `Arnold` > `Arnold Render View`

  - Cameras

  - Iluminação

### Criando materiais

Menu/Opção `Rendering` > ``Light/Shading` > `New Material`

Logo em seguida é apresentado a lista de materiais existentes no Maya.

Atributos do material:

1. Color;

1. Transparency;

1. Incandescence;

1. Bump Mapping - Adiciona uma imagem para [Bump Mapping](https://pt.wikipedia.org/wiki/Bump_mapping)

### Tipos de Materiais (Maya)

- Lambert (simples sem reflexo, brilho e transparência)

  - Color: cor do material;

  - transparência: Aumenta o alpha;

  - Ambiente color: aumenta a tonalidade da cor;

  - Incandescência: Adiciona uma luz ao material;

  - Bump Mapping: adiciona textura para associar rugosidade ou padrões;

  - Diffuse: Torna mais claro ou escuro a cor.

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

  - `Tools` > `Show UV toolKit`;

- UV Shells : Context Menu > UV > select vertex > ctrl > context menu > To UV shells

- Cortando `3D Cut and Sew UV`

  - O corte é realizado por material utilizado;

  - Clicando e arrastrando;

  - Desmarcando CTRL+2x na vértice selecionado;

  - Quando uma área é fechada é criada "UV Shells";

  - Podemos selecionar as UV Shells;

- Costurando  `Cut and Sew`
  - Selecione dois vértices e depois clique em `Sew`;
  
  - `Sew Tool` - Costura interativa, selecione e arrastre;

- Expandindo/desdobra o Elemento  
  
  - `UV Toolkit` > `Unfold`;

- Movimentando ou aumentando

  - `Transform` > `Move`

- Copiando dados de um Shells para outra  

  - `Transform` > `Texel Density` > `Get` - copia os valores de um elemento selecionado;

  - `Transform` > `Texel Density` > `Set` - cola os valores para um elemento selecionado;

- Invertendo Shells `Tools`

  - `Flip` > `U` ou `V` - Horizontal ou vertical;

- `Arrange and Layout`

  - `Stack Shells` - Quando a textura aparece em duas faces é recomendado utilizar o recurso para empilhar uma sobre a outra;

  - `Orient Shells` - Separa e orienta as shells;

  - `Layout` - Organiza as Shells lado a lado;  

- `Align and Snap`  Alinhando

  - `Align` - Alinhando UV;

  - `Match UVs` - Alinha duas Shells empilhadas;

- `Pin`   Bloqueando

  - `Pin Tool` - Selecionando usando tecla `B` ou `P` para bloquear áreas;

## Hide  

Selecione um objeto e pressione Ctrl + H ou `Display` > `Hide` > `Hide Selection`

No `Outliner` os objetos ocultos ficam com a cor mais escura;

No `Channel Box` é possível alterar a visibilidade colocando o valor 1 (on) na propriedade `Visibilty`.

Para mostrar o último objeto escondido podemos usar `Display` > `Show` > `Show Last Hidden`.

Para apresentar um objeto escondido usando o `Outliner` usamos `Display` > `Show` > `Show Selection`.

## Animando cenas no Autodesk Maya

- S - Marcar frame

- Shift + LMB = Seleciona

- Preferences = timecode

- Adicionar uma curva no objeto = p

- Travar camera = lock

- key select em atributos

- Arnold - SkyDomeLight

- Playback

- Visualize > Ghost Selectd/Unselect

- Visualize > Create Editable Montion trail

- Visualize > Create Animation Snapshot
