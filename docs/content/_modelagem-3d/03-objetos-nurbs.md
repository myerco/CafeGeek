---
title: Objetos NURBS
excerpt: Apresentação de objetos NURBS
permalink: /modelagem-3d/objetos-nurbs
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 103
tags:
  - nurbs
  - curvas
---

## 1. Modelagem NURBS

NURBS (Non-Uniform Rational B-Splines) é um tipo de geometria que você pode usar para criar curvas e superfícies 3D no Maya. Os outros tipos de geometria fornecidos pelo Maya são superfícies de polígono e subdivisão.

- Não Uniforme refere-se à parametrização da curva. Curvas não uniformes permitem, entre outras coisas, a presença de multi-nós, que são necessários para representar curvas de Bezier.

- Racional refere-se à representação matemática subjacente. Essa propriedade permite que NURBS represente cônicas exatas (como curvas parabólicas, círculos e elipses) além de curvas de forma livre.

- B-splines são curvas polinomiais por partes (splines) que têm uma representação paramétrica.

NURBS são úteis para construir muitos tipos de formas 3D orgânicas devido à natureza suave e mínima das curvas que eles usam para construir superfícies. Os tipos de superfície NURBS são amplamente utilizados nas áreas de animação, jogos, visualização científica e design industrial.

O tipo de dados NURBS 3D pode ser facilmente exportado para aplicativos de software CAD exportando as superfícies usando o formato de arquivo IGES. Além disso, o Maya pode importar muitos tipos de dados bezier e NURBS de muitos aplicativos de software CAD.

Se seus requisitos são usar o tipo de superfície de polígono em suas cenas, você pode inicialmente construir suas superfícies usando NURBS e depois convertê-las em polígonos.

### 1.1. Objetos primitivos

#### 1.1.1. Esfera

São compostos por :

- Star Sweep - Valor de início da curva;

- End Sweep - Valor final da curva;

- Sections - Quantidade de seções da malha (Vertical);

- Spans - Quantidade de `spans` (Horizontal)

#### 1.1.2. Cubo

O objeto é uma composição de várias outros **agrupados**.

#### 1.1.3. Cilindro

Criando o objeto habilitando a opção `Interactive Creation` as partes superior e inferior do objeto são preenchidas, utilizando uma **hierarquia** de três objetos.

- NurbsCylinder1 > BottomCap1 > TopCap1.

#### 1.1.4. Plano

Para aumentar os vértices criados utilizamos : `Patches U` e `Patches V`.

### 1.2. Componentes de seleção

#### 1.2.1. CV

{% include image.html
    src="https://download.autodesk.com/us/maya/2011help/images/MED/Sherlock/NURBS/comp_N19b.png"
    alt="Figura: CVs."
    caption="Figura: CVs."
%}

Control Vertices, controlar como a curva é “puxada” de uma linha reta entre os pontos de edição. Eles são os meios mais básicos e importantes para controlar a forma de uma curva. Linhas entre CVs consecutivos formam o Hull de controle.

O número de CVs é igual ao grau da curva mais um. Assim, por exemplo, uma curva de grau 3 tem quatro CVs por vão. Para aumentar o número de CVs para obter mais controle sobre a forma da curva, você pode aumentar o número de extensões inserindo pontos de edição ou aumentar o grau da curva.

O Maya desenha CVs de forma diferente para permitir que você saiba a diferença entre o início e o fim de uma curva. O primeiro CV (no ponto inicial da curva) é desenhado como uma caixa. O segundo CV é desenhado como um pequeno “U”, para mostrar a dimensão U crescente a partir do ponto inicial. Todos os outros CVs são desenhados como pequenos pontos.

#### 1.2.2. Edit Points

{% include image.html
    src="https://download.autodesk.com/us/maya/2011help/images/MED/Sherlock/NURBS/comp_N20a.png"
    alt="Edit Points."
    caption="Figura: Edit Points."
%}

Você pode dizer quando uma curva é feita a partir de vários segmentos de várias maneiras. Uma é procurar pontos de edição na curva. Os pontos de edição marcam o ponto de conexão entre dois segmentos. O Maya desenha pontos de edição como pequenos Xs.

Ao contrário dos pontos de controle na curva das curvas de Bezier (usados em muitos programas de ilustração 2D), os pontos de edição NURBS geralmente não são usados para editar curvas. Os CVs controlam a forma de uma curva NURBS e os pontos de edição são apenas indicadores de quantos spans uma curva possui.

#### 1.2.3. Hulls

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

#### 1.2.4. Isoparms

Silimiar aos Edges dos objetos poligonais.

### 1.3. Curve Tools

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

### 1.4. Revolve
  
Ordem de seleção do objeto altera a forma final;

Escolha o Eixo em `Resolve Options`.

A curva fica associada ao objeto criado até que o histórico seja removido;

### 1.5. Loft

Possibilita a criação de figuras utilizando várias curvas curva

- Crie uma curva do tipo circulo e depois a duplique;

- Selecione todas as curvas (A última selecionada fica com a cor verde);

- Utilize a ferramenta `Surfaces` > `Loft`

- Os parâmetros do objeto:
  - Degree: Cubic/Linear;

  - Uniform e Close;
  
  - Autreverse - reverte as faces do objeto

### 1.6. Extrude Nurbs

É possível criar um objeto poligonal na construção usando as configurações:

- Crie um objeto Nurbs qualquer;

- Crie um curva para servir como caminho;

- Selecione os objetos;

- Parametros:
  
  - No objeto podemos fixar o objeto para a curva: CTRL + A - Fixed Path;

  - Rotation e Scale;

### 1.7. Isoparm
  
#### 1.7.1. Separar objetos

É possível separar ou juntar usando `Surface` > `Detach` ou `Attach`

#### 1.7.2. Inserindo Isoparms

Selecione um isoparm e logo em seguida utilize `Surface` > `Insert Isoparms`.

### 1.8. Close e Open

Para curvas abertas utilize `Curve` > `Close` para fechar a curva.

Para objetos do tipo nurbs abertos utilize `Surfaces` > `Close` para fechar a curva.

#### 1.8.1. Preenchendo uma superfície de um objeto

`Surface` > `Planar`

Selecione uma curva fechada e aplique a opção `Planar` para preencher a curva.

#### 1.8.2. Preenchendo o espaço entre dois objetos

`Surface` > `Loft`

Duplique isoparms de objetos distintos e aplique `Loft` para preencher o espaço entre eles.

### 1.9. Project Curve on Surface

É possível projetar a imagem de uma curva em outro com :

`Surfaces` > `Project Curve on Surface`

Selecione primeiro o objeto que deve ter a sombra da curva;

A projeção da curva considera a posição da camera;

`Surfaces` > `Trim Tool`  

Corta a superfície desejeda, selecione o que vai ser mantido e pressione `ENTER`.

Todos os itens pontilhados vão ser removidos.

### 1.10. Convertendo NURBS para poligonais

Para exportar objetos para o Unreal Engine devemos transformar os objetos NURBS em objetos poligonais.

`Modify` > `Convert` > `NURBS to Poligons`

- `Standart fit` - O ajuste padrão é o método de mosaico padrão. É uma tesselação “adaptativa”, o que significa que as opções a seguir são usadas para determinar quando parar a tesselação.

Por exemplo, a tecelagem para no valor de tolerância fracionária que você definiu. Se houver uma aresta mais curta que o comprimento mínimo da aresta, a tesselação para nessa aresta. Se a superfície for plana o suficiente dentro da borda (a razão corda/altura especificada é pequena o suficiente), a tesselação para aí.

- `Type` - Selecione o tipo de polígonos a ser usado ao converter a geometria NURBS em dados poligonais. Se você selecionar Triângulo (o padrão), polígonos de 3 lados serão criados. Se você selecionar Quads, polígonos de 4 lados serão criados.

- `Tessellation` - Tessellation significa que você cria um conjunto de polígonos da geometria NURBS.

>Em [computação gráfica](https://en.wikipedia.org/wiki/Tessellation), tesselação refere-se à divisão de conjuntos de dados de polígonos (às vezes chamados de conjuntos de vértices) apresentando objetos em uma cena em estruturas adequadas para renderização.

## 2. Sculpting

`Sculpt Tool`

`Smooth Tool`
