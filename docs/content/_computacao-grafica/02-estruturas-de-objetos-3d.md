---
title: Estrutura de objetos 3D
permalink: /computacao-grafica/estruturas-de-objetos-3d
excerpt: Neste curso apresentaremos conceitos de computação gráfica aplicados na prática usando o Unreal Engine e o Autodesk Maya.
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-27T08:48:05-04:00
order: 102
tags:
  - objetos 3D
  - arquivos de imagens
  - polígonos
  - ponto flutuante
  - sistema de coordenadas
---

## 1. Como são formados os objetos 3D?

Os objetos 3D são formados no computador através de processos de modelagem 3D, que podem ser realizados por meio de diferentes softwares, como o Blender, Maya, 3D Studio Max, entre outros.

Na modelagem 3D, o artista ou designer cria um modelo tridimensional digital do objeto, utilizando ferramentas como polígonos, curvas, superfícies e texturas. Esses modelos são criados a partir de uma variedade de técnicas, como modelagem por subdivisão, escultura digital e modelagem por NURBS.

Uma vez que o modelo 3D é criado, ele pode ser texturizado, iluminado e renderizado, permitindo a criação de imagens realistas do objeto em diferentes ambientes e condições de iluminação.

**Nota:** As telas dos computadores são essencialmente bidimensionais, são gráficos 3D são apenas ilusões de óptica 2D que fazem o seu cérebro achar que está olhando para um objeto 3D. [Fomas 3D](https://pt.khanacademy.org/computing/computer-programming/programming-games-visualizations/programming-3d-shapes/a/what-are-3d-shapes)
{: .notice--info}

### 1.1. Quais são os elementos que compõem imagens?

Imagens apresentadas nos dispositivos de saída são formadas por pontos  construídos e organizados pelas seguintes estruturas:

### 1.2. Arquivo Bitmap

Um bitmap é um tipo de imagem que é usado para armazenamento de imagens e pode ser definindo como um mapa de bits.

Cada pedaço da imagem é composto por um ponto chamado de pixel.

{% include image.html
    src="https://www.marceloaventura.art.br/blog/wp-content/uploads/2012/10/resolucao00.png"
    alt="Figura: Imagem bitmap."
    caption="Resolução de imagens (bitmap)"
    ref="https://www.marceloaventura.art.br/blog/resolucao-de-imagens-bitmap/"
%}

### 1.3. Vector Graphics ou imagem vetorizada

"É uma forma de computação gráfica em que as imagens visuais são criadas diretamente a partir de formas geométricas definidas em um plano cartesiano, como pontos, linhas, curvas e polígonos."

Em um programa de gráficos vetoriais, fornecemos o ponto inicial e o ponto final e o programa faz o resto.

{% include image.html
    src="https://etc.usf.edu/techease/wp-content/uploads/2017/12/Vector.jpg"
    alt="Figura: Vector Graphics."
    caption="What is the difference between bitmap and vector images?"
    ref="https://etc.usf.edu/techease/win/images/what-is-the-difference-between-bitmap-and-vector-images/"
%}

Mas tem outra vantagem. Se aplicarmos zoom a uma imagem bitmap, podemos ver os pixels e teremos uma imagem ruim. Em gráficos vetoriais, ampliar uma imagem não envolve uma imagem ruim porque a imagem é criada por uma fórmula matemática.

## 2. Lista de formatos e texturas que o Unreal Engine suporta

Para Materiais, as texturas são mapeadas para as superfícies às quais o Material é aplicado. As texturas podem ser usadas para uma variedade de cálculos dentro de um Material, sendo aplicadas diretamente a uma entrada (como Cor Base), usadas como uma máscara ou usando os valores RGBA para outros cálculos.

Os materiais podem fazer uso de várias texturas que são todas amostradas e aplicadas para diferentes propósitos. Por exemplo, um material simples pode ter uma textura Base Color, uma textura Specular e uma textura Normal Map. Além disso, pode haver um mapa para Emissivo e Rugosidade armazenado nos canais alfa de uma ou mais dessas mesmas texturas. O empacotamento de vários valores em uma única textura permite que eles sejam usados mais prontamente, economizando chamadas de desenho para desempenho e reduzindo o espaço em disco [[Textures](https://docs.unrealengine.com/5.0/en-US/textures-in-unreal-engine/)].
{: .text-justify}

Uma variedade de formatos de imagem e tipos de arquivo são suportados:

- .bmp - Bitmap;
- .float;
- .pcx;
- .png;
- .psd - Vector Graphics;
- .tga;
- .jpg - Bitmap com metadados e compressão;
- .exr.

## 3. O que são Pontos?

Na geometria, um ponto é representado por sua coordenada no espaço. Geometria usa um sistema de coordenadas cartesianas, onde as coordenadas de um ponto em espaço são representados pela distância ao longo de cada um dos eixos principais para o ponto.

{% include image.html
    src="https://conhecimentocientifico.r7.com/wp-content/uploads/2020/01/plano-cartesiano-o-que-e-como-fazer-caracteristicas-e-coordenadas.png"
    alt="Figura: Plano cartesiano."
    caption="Plano Cartesiano – O que é, como fazer, características e coordenadas."
    ref="https://conhecimentocientifico.com/plano-cartesiano/"
%}

Pontos são representados por pixels em monitores.

### 3.1. Pixel

"A palavra pixel é uma combinação dos termos “picture” e “element”. Ou seja, “elemento de imagem”. É a menor unidade de uma imagem digital, independente de sua fonte. Se você pegar uma foto e fizer uma aproximação (zoom), verá uma série de quadradinhos que a compõem. Cada um desses quadros é um pixel. São milhões ou milhares deles."[[O que é um pixel?](https://tecnoblog.net/responde/o-que-e-um-pixel/)]
{: .text-justify}

Pixel é o menor elemento em um dispositivo de exibição, sendo que cada pixel é composto por um conjunto de 3 pontos: verde, vermelho e azul.

{% include image.html
    src="https://i.pinimg.com/564x/6a/07/72/6a0772d93d74327025597ff3951996ff.jpg"
    alt="Figura: Pixel."
    caption="Um exemplo de formação de imagens."
%}

### 3.2. Bits por pixel

{% include image.html
    src="https://www.researchgate.net/publication/366169511/figure/fig2/AS:11431281106419063@1670675652164/Pixel-size-of-different-color-The-size-of-an-image-file-then-is-directly-related-to.png"
    alt="Figura: Pixel Color"
    caption="Tamanho do pixel de cor é diferente. O tamanho de um arquivo de imagem, portanto, está diretamente relacionado ao número de pixels e à granularidade da definição da cor. Uma imagem típica de 640x480 pixels usando uma paleta de 256 cores exigiria um arquivo de cerca de 307 KB de tamanho (640x480 bytes), enquanto uma imagem colorida de 24 bits de alta resolução de 1024x768 pixels resultaria em um arquivo de 2,36 MB (1024x768x3 bytes).."
%}

As cores do pixel dependem da quantidade de bits por pixel (bpp).

- 1 bpp, 2(1) = 2 colors (monochrome);
- 2 bpp, 2(2) = 4 colors;
- 3 bpp, 2(3) = 8 colors;
- 4 bpp, 2(4) = 16 colors;
- 8 bpp, 2(8) = 256 colors;
- 16 bpp, 2(16) = 65,536 colors ("Highcolor" );
- 24 bpp, 2(24) = 16,777,216 colors ("Truecolor").

Aumentando a qualidade de cores a imagem terá uma aparência mais realista mas consumira mais memória e processamento.

### 3.3. Uma dica para utilizar texturas no Unreal Engine

Formatos de textura menores resultam em materiais mais rápidos (por exemplo, [DXT1](https://www.khronos.org/opengl/wiki/S3_Texture_Compression) é de 4 bits por pixel, DXT5 é de 8 bpp, ARGB descompactado é de 32 bpp).

**Nota:** Compressão de imagens que usam blocos de bits.
{: .notice--info}

**GIMP:** [Exportando imagens do **Gimp** com compressão DXT1](https://wiki.thedarkmod.com/index.php?title=DDS_Creation_with_GIMP)

## 4. Linhas, raios e segmentos

Uma linha tem direção e comprimento infinito. A direção de uma linha pode ser definido por dois pontos distintos pelos quais a linha passa.

Um raio começa em um ponto e se estende infinitamente em uma direção distante do ponto. Um raio é definido por um ponto e uma direção.

Um segmento de linha é uma linha de comprimento finito definida por seus dois pontos finais.

{% include image.html

    src="https://cdn1.byjus.com/wp-content/uploads/2020/01/Line-segment.png"
    alt="Figura: Segmento de linha."
    caption="Em computadores, devemos lidar com quantidades finitas, então não podemos tirar o total extensão de uma linha ou raio de acordo com sua definição matemática. No computador gráficos quando nos referimos a “linhas”, geralmente nos referimos a segmentos de linha."
    ref="https://cdn1.byjus.com"
%}

### 4.1. Planos e Triângulos

Um plano é uma folha orientada em 3 espaços sem espessura e com uma extensão infinita.

Um plano é definido por três pontos não colineares que cruzam o plano ou por um ponto no plano e uma direção perpendicular ao plano.

A direção perpendicular a um plano é chamado de **Normal** ao plano.

Um triângulo também é definido por três pontos no espaço 3 chamados **Vértices** (singular vértice).

{% include imagelocal.html
    src="computacao-grafica/shad-tri-normal.webp"
    alt="Figura: Triangle Vertex Normal."
    caption="A face normal de um triângulo pode ser calculada a partir do produto vetorial de duas arestas desse triângulo."
    ref="https://www.scratchapixel.com/lessons/3d-basic-rendering/introduction-to-shading/shading-normals"
%}

## 5. Polígonos (Polygon)

As imagens tridimensionais formadas no computador são compostas por polígonos.

Polígonos são uma coleção de vértices, arestas e faces que definem a forma do objeto poliédrico.

### 5.1. Polígonos no Maya

Utilizando as opções em **Poly Modeling** podemos definir uma séria de elementos poligonais.

{% include imagelocal.html
    src="computacao-grafica/ue4_maya_wireframe.jpg"
    alt="Figura: Wireframe."
    caption="Polígonos no Maya utilizando a visualização Wireframe."
%}

`Channel Box/Layer Editor` - Propriedades do objeto com a sua quantidade de subdivisões, estes valores podem ser manipulados aumentando ou diminuindo a quantidade de arestas.
  
{% include imagelocal.html
    src="computacao-grafica/ue4_maya_show_vertex.jpg"
    alt="Figura: Poly Count."
    caption="Verts, Edges, Faces, Tris, UVs no Maya"
%}

Apresentado a quantidade de vértices e arestas.
  
`Display` > `Heads up display` > `Poly Count`.

### 5.2. Polígonos no Unreal Engine

Selecionando `Brush Wireframe` no `View Port` ou pressionando *Alt+2* a estrutura de malha de vértices dos polígonos na cena.

{% include imagelocal.html
    src="computacao-grafica/ue4_view_port_wireframe.jpg"
    alt="Figura: Unreal Wireframe"
    caption="Visualização a malha dos objetos, Unreal Engine 4 >  Brush Wireframes."
%}

{% include imagelocal.html
    src="computacao-grafica/ue4_view_statistics.jpg"
    alt="Figura: Apresentado a quantidade de vértices e arestas."
    caption="Visualizando estatísticas - Window > Statistics."
%}

## 6. Face

São as superfícies planas que constituem um sólido. Consistem em triângulos (malha de triângulo), quadriláteros ou outros polígonos convexos simples, uma vez que isso simplifica a renderização.

{% include image.html
    src="https://www.alura.com.br/artigos/assets/topologia-3d-por-que-e-importante/imagem3.jpg"
    alt="Figura: Face topologia."
    caption="O que é topologia no 3D?"
    ref="https://www.alura.com.br/artigos/topologia-3d-por-que-e-importante"
%}

### 6.1. Faces no Maya

Com botão direito pressionado (RMB) escolha **Face** para selecionar  a face.

{% include imagelocal.html
    src="computacao-grafica/ue4_maya_select_face.jpg"
    alt="Figura: Maya RMB."
    caption="Face."
%}

{% include imagelocal.html
    src="computacao-grafica/ue4_maya_face.jpg"
    alt="Figura: Maya e seleção de Face."
    caption="A face selecionada fica em outra cor."
%}

### 6.2. Faces no Unreal Engine

Somente é possível selecionar faces e vértices de objetos do tipo `Geometry` em `Place Actors`.

É necessário habilitar as opções de edição em `Modes` >  `Brush Editing`.

{% include imagelocal.html
    src="computacao-grafica/ue4_select_face_geometry.jpg"
    alt="Figura: Unreal Engine Faces de objetos."
    caption="Para editar a face no Unreal Engine utilize Modes > Brush Editing"
%}

## 7. Aresta

São segmentos de reta que são as intersecções de duas faces contíguas.

### 7.1. Arestas no Maya

{% include imagelocal.html
    src="computacao-grafica/ue4_maya_select_edge.jpg"
    alt="Figura: Maya e arestas."
    caption="Para selecionar utilize RMB a opção Edge."
%}

{% include imagelocal.html
    src="computacao-grafica/ue4_maya_edge.jpg"
    alt="Figura: Maya select Edge."
    caption="Selecionando a aresta é possível e manipular-la."
%}

### 7.2. Arestas no Unreal Engine

{% include imagelocal.html
    src="computacao-grafica/ue4_select_edge.jpg"
    alt="Figura: Unreal Engine Aresta."
    caption="Utilizamos - Modes > Brush Editing > Select Edge."
%}

## 8. Vértices

São os pontos de encontro das arestas.

### 8.1. Vértices no Maya

{% include imagelocal.html
    src="computacao-grafica/ue4_maya_select_vertex.jpg"
    alt="Figura: Maya RMB Vertex."
    caption="Selecionamos com RMB a opção Vertex."
%}

{% include imagelocal.html
    src="computacao-grafica/ue4_maya_vertex.jpg"
    alt="Figura: Maya select vertex."
    caption="Selecionando um vértice."
%}

### 8.2. Vértices no Unreal Engine

{% include imagelocal.html
    src="computacao-grafica/ue4_select_vertex.jpg"
    alt="Figura: Unreal Engine select Vertex."
    caption="Brush Editing."
%}

## 9. Valores de ponto flutuante

Na matemática, todos os cálculos são exatos e realizam aritmética sobre os valores e não alteram sua precisão. No entanto, os computadores armazenam aproximações para números reais como valores de ponto flutuante e realizando operações aritméticas podem fazer com que sua precisão mude. Nem todos os números reais podem ser representados exatamente por uma representação de ponto flutuante. Números como π e outros transcendentais os números têm uma expansão decimal infinita.
A natureza aproximada dos números de ponto flutuante geralmente levanta sua cabeça ao comparar números de ponto flutuante e outras estruturas compostas de números de pontos, como pontos, vetores, retas, planos, matrizes e assim por diante.
{: .text-justify}

{% include image.html
    src="https://media.geeksforgeeks.org/wp-content/uploads/Single-Precision-IEEE-754-Floating-Point-Standard.jpg"
    alt="Figura: Média."
    caption="Precisão de valores ponto flutuante."
    ref="https://media.geeksforgeeks.org"
%}

## 10. Sistemas de coordenadas

Objetos em Computação Gráfica possuem descrições numéricas (modelos) que caracterizam suas formas e dimensões. Esses números se referem a um sistema de coordenadas, normalmente o sistema Cartesiano de coordenadas: x, y e z.  Em alguns casos, precisamos de mais de um sistema de coordenadas.

{% include image.html
    src="https://www.tutorialspoint.com/computer_graphics/images/3d_coordinates.jpg"
    alt="Figura: Coordenadas."
    caption="Sistema X,Y e Z."
    ref="https://www.tutorialspoint.com"
%}

Normalmente, os softwares de elementos gráficos 3D, como por exemplo Maya ou Blender,  usam um dos dois tipos de sistemas de coordenadas cartesianas de esquerda e direita. Em ambos os sistemas de coordenadas, o eixo x positivo aponta para a direita e o eixo y positivo aponta para cima.
{: .text-justify}

### 10.1. À esquerda e à direita serão entregues de coordenadas

Você pode lembrar para qual direção o eixo z positivo aponta, apontando os dedos de sua mão direita ou esquerda na direção x positiva e curvando-os na direção y positiva. A direção do seu polegar aponta em sua direção ou para longe de você, é a direção em que o eixo z positivo aponta para esse sistema de coordenadas. A ilustração a seguir mostra esses dois sistemas de coordenadas.
{: .text-justify}

{% include image.html
    src="https://docs.microsoft.com/pt-br/windows/uwp/graphics-concepts/images/leftrght.png"
    alt="Figura: Left-handed e Right-handed."
    caption="Determinado a organização de coordenadas utilizando a mão"
    ref="https://docs.microsoft.com"
%}

**Unreal Engine** - Utiliza o sistema de coordenadas *Left-Handed*;
  
**Maya** - Utiliza o sistema de coordenadas *Right-Handed*.

### 10.2. Pivot - O centro do objeto 3D no Maya

Pivot é um ponto que marca o centro de objetos tridimensionais no Maya, onde :

- Todas as transformações de um objeto são relativas ao ponto de pivô do objeto;
- Os manipuladores 3D também contam com o ponto de pivô do objeto.

{% include imagelocal.html
    src="computacao-grafica/ue4_maya_pivot.jpg"
    alt="Figura: Maya select pivot."
    caption="Selecione o pivot usando a tecla W e depois Tecla Insert ou D."
%}

### 10.3. Pivot - O centro do objeto 3D no Unreal Engine

Comando : Alt + Scroll mouse.

## 11. Cor

Uma cor é descrita para o computador como uma tupla ordenada de valores de um **cor space** (espaço de cor). Os próprios valores são chamados de **components**(componentes) e são coordenados no espaço de cores. O GDI do Windows representa as cores como uma tupla ordenada de componentes vermelhos, verdes e azuis com cada componente no intervalo [0 . 0 , 1 . 0] representado como uma quantidade de bytes sem sinal no intervalo [0 , 255].
{: .text-justify}

Por padrão, o [Windows GDI](https://pt.wikipedia.org/wiki/GDI) usa o espaço de cores RGB.

Em computação gráfica, muitas vezes é conveniente usar as cores HLS e HSV.

- HLS: matiz, leveza, saturação;
  
- HSV: matiz,saturação,valor.

## 12. Transparência com Alpha

Muitas vezes, em computação gráfica, desejamos combinar pixels como se eles fossem pintados em folhas transparentes empilhadas umas sobre as outras. No Direct3D, a transparência é representada como um canal adicional de informações que representam a quantidade de transparência do pixel.
{: .text-justify}

Quando um pixel é totalmente opaco, seu valor alfa é 1 . 0 e este pixel completamente obscurece qualquer coisa por trás dele. Quando um pixel é totalmente transparente, seu valor alfa é 0. 0 e tudo por trás do pixel aparece. Quando o valor alfa é entre 0 e 1, o pixel é parcialmente transparente.
{: .text-justify}

{% include image.html
    src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2a/Alpha_compositing.svg/963px-Alpha_compositing.svg.png"
    alt="Figura: Alpha compositing."
    caption="Sobreposição de elementos."
    ref="https://en.wikipedia.org/wiki/Alpha_compositing"
%}
