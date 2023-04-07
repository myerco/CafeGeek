---
title: Objetos Poligonais
excerpt: Modelando objetos poligonais
permalink: /pages/modelagem3d/objetos-poligonais
last_modified_at: 2023-03-27T08:48:05-04:00
toc: true
sidebar:
    nav: dev_modelagem3d  
---


## 1. Começando a trabalhar com Autodesk Maya

### 1.1. Interface

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

### 1.2. Configurando a Interface

`Windows` > `Settings/Preferences` > `Preferences` > `Show - What´s new`

Habilita ou desabilita a janela inicial de avisos de mudanças de versão.

`Window` > `Settings/Preferences` > `Preferences`

Configurar a interface

`Interface` > (Menu Set,Show...)  

### 1.3. Configurando projetos

`File` > `Project Window`

Para configurar as pastas do projeto utilize a opção acima. Configurar uma pasta de trabalho auxilia na organização dos arquivos que irão compor a cena.

`File` > `Set Project`

Quando importamos um novo projeto de outra máquina podemos configurar a pasta de trabalho ou pasta de projeto.

`File` > `New Scene`

Cria novas cenas, uma cena pode conter vários elementos e deverão estar separados e organizados.

### 1.4. Comandos de navegação

- Alt + RMB - Movimentação de câmera;

- Alt + LMB - Zoom;

- Alt + Scroll - Scroll da a câmera;

- Scroll - Zoom;

### 1.5. Configuração de ViewPort

#### 1.5.1. Mostrando a quantidade de polígonos e vértices

`Display` > `Heads Up Display` > `Poly Count`[ [Poly Count](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2019/ENU/Maya-Modeling/files/GUID-53E46D0C-4B7B-4404-AEB0-3BDD1FF8608A-htm.html) ]

#### 1.5.2. Visualização

Este menu Sombreamento é exibido acima da visualização da cena ou acima de cada painel de visualização em um layout com várias visualizações de cena (como o layout de quatro visualizações).

| Tecla |                                                  |
| :---: | :----------------------------------------------- |
|   0   | Configuração de exibição de qualidade padrão     |
|   1   | Configuração de exibição de qualidade aproximada |
|   2   | Configuração de exibição de qualidade média      |
|   3   | Configuração de exibição de qualidade suave      |
|   4   | Estrutura de arame                               |
|   5   | Exibição sombreada                               |
|   6   | Exibição sombreada e texturizada                 |
|   7   | Usar todas as luzes                              |

- [Shading](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-Basics/files/GUID-C6188583-EA9E-4880-AAE7-8D895FD94DD6-htm.html)

- [Atalhos de teclado do Autodesk Maya](https://www.autodesk.com.br/shortcuts/maya)

#### 1.5.3. Hotbox

Pressione a barra de espaço

{% include image.html
    src="https://forums.autodesk.com/autodesk/attachments/autodesk/area-b201/85095/1/likethis.PNG"
    alt="Figura: Space bar."
    caption="Figura: Space bar."
%}

## 2. Objetos Poligonais

***

{% include image.html
    src="https://i.ytimg.com/vi/7sR_Tux5u7M/maxresdefault.jpg"
    alt="Figura: Autodesk Maya objetos poligonais."
    caption="Figura: Autodesk Maya objetos poligonais."
%}

Uma malha poligonal é uma coleção de arestas, faces e pontos de conexão usados ​​para fornecer um modelo poligonal para modelagem 3D e animação por computador. Sua composição geométrica pode ser armazenada para facilitar vários tipos de simulação de renderizações tridimensionais [[DEFINERTEC](https://definirtec.com/malha-poligonal/)].

### 2.1. Menu de contexto para manipulação de malhas

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

### 2.2. Freeze e Reset parâmetros

Ao deformar ou movimentar um objeto as coordenadas X,Y Z serão alteradas conforme informado pelo usuário, é interessante ao exportar para outra ferramenta, como por exemplo o Unreal, zerar essas coordenadas para que representem o ponto central do objeto na cena, para isso usamos:

- `Modify` > `Freeze transformations` - Zera as coordenadas do objeto;

- `Modify` > `Reset Transformations` - Retorna o pivo ao centro da cena;

- `Modify` > `Center Pivo` - Posiciona o pivo ao centro do objeto;

### 2.3. Snap de objetos

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

### 2.4. Seleção de objetos e componentes

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

### 2.5. Utilizando Soft Selection

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

### 2.6. Simetria ou Symmetry

`Move Tool` > `Symmetry Settings`

Seleciona elementos simtricamente alinhados em um determinado eixo.

- `Symmetry` - Escolha o eixo;

### 2.7. Duplicando objetos

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

### 2.8. Pivot

`Modify` > `Center Pivot`

Centraliza o pivot do objeto.
  
Tecle D para mover o pivot.

`Snap to points`

Alinha o pivot nos elementos.

### 2.9. Deformando a malha poligonal

#### 2.9.1. Extrude

- shift + mouse - `Move tool Preferences` > `Smart Duplicate Settings` > Shift + drag to..)

- Ctrl + E

- `Menu` > `Edit Mesh` > `Extrude`

#### 2.9.2. Adicionando edges

- `Menu` > `Mesh Tools` > `Insert Edge loop`;

- `Mesh Tools` > `Insert Edge loop Settings` > `Number of edge loops`;

#### 2.9.3. Bevel

1. Ctrl + B ou `Edit Mesh` > `Bevel`

    - Fraction - espaço entre segmentos;

    - Segments - Número de segmentos;

#### 2.9.4. Removendo edges

Ctrl + Backspace - Remove edges e vértices.

#### 2.9.5. Multicut

Cuidado não podemos ter vértices sem conexão com outros.

Adicione edges.

#### 2.9.6. Merge de vértices

`Edit Mesh`  > `Merge`

Selecione dois vértices e aplique a ferramenta.

### 2.10. Suavizando objetos poligonais

#### 2.10.1. Smooth

`Mesh` > `Smooth`

Adiciona mais vertices no objeto, possibilitando esolher a quantidade de divisões.

`Mesh Display` > `Soften Edge`

Suaviza a malha sem adicionar novos vértices.

#### 2.10.2. Visualizando a suavização

{% include image.html
    src="imagens/autodesk_maya_smooth_view.webp"
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

#### 2.10.3. Extract

`Edit Mesh` > `Extract`

Extrai partes de um objeto. Selecione a área para extrair e aplique a ferramenta.

### 2.11. Append e Bridged Tool

`Edit Mesh` > `Bridge`

Adiciona faces nos objeto .

`Mesh Tool` > `Append to Polygon`

Duas soluções robustas para conectar componentes.

`Bridge tool`

Trabalha com faces poligonais, permitindo não apenas a criação de planos planos.

`Append to Polygon`

É ideal em situações em que você precisa conectar seletivamente partes da mesma malha [[3D Modeling Part 7: Tools and Techniques in Autodesk Maya](https://www.shutterstock.com/blog/3d-modeling-autodesk-maya)].

### 2.12. Fill Hole

Preenchendo um buraco no objeto.

Para exemplificar, selecione `Edge` e marque todas as arestas adjacentes ao espaço que queremos preencher.

`Mesh` > `Fill Hole`

### 2.13. Target Weld

Movimenta e solda vertices, selecione `Vertex` e logo em seguida `Mesh Tool` > `Target Weld`.

## 3. Combine e Separate

`Mesh` > `Combine`

Selecione os objetos para que eles fiquem juntos

`Mesh` > `Separate`

Separa os objetos e cria um novo grupo.

## 4. Booleans

Para projetar ou misturar objetos podemos usar [`Booleans`](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Maya/files/GUID-9467513F-47C3-4C73-8251-6FF8C0DE4982-htm.html).

`Mesh` > `Booleans`

- `Union`;
- `Diference`;
- `Intersection`;

## 5. Organizando em camadas

***

## 6. Layer
  
- V - Mostra ou oculta uma camada. Consulte Ocultar camadas de exibição para obter mais informações.
  
- P - Um "P" na caixa significa que a camada está visível durante a reprodução. Desligue o "P" para ocultar a camada durante a reprodução.
  
- T - Um “T” significa que os objetos na camada são modelados: eles são exibidos em estrutura de arame e não podem ser selecionados.

- R - Um “R” significa que os objetos aos quais a camada está referenciada: eles não podem ser selecionados, mas mantêm o modo de exibição atual. Uma caixa em branco significa que os objetos na camada são normais e podem ser selecionados.

Podemos adicionar uma cor na camada fazendo com que todos os objetos selecionados fiquem com a cor escolhida.

## 7. Hierarquia
  
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

## 8. Group

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
