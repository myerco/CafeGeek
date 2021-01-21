---
title: Unreal Engine 4 Rendering
description: Unreal Engine 4 Rendering
tags: [Unreal Engine,Rendering]
---

[CafeGeek](https://myerco.github.io/unreal-engine)

![MDA](https://myerco.github.io/unreal-engine/imagens/cafegeek_small.png)
# Unreal Engine 4 Rendering

## Conteúdo do curso
<a name="1"></a>
1. Antes de renderizar
1. Geometria renderizada
1. Rasterizing and GBUFFEr
1. Textures
1. Pixel Shaders and Materials
1. Reflections
1. Static Lightinh/Shadows
1. Dynamic Lighting/Shadows
1. Fog/Transparency
1. Post Processing

1. RTR
Real Time Rendering (RTR)
Custo de renderização

 - Identificar o target framerate

 O que pode ser feito, Qualidade, performance e características.

## Como são formados os objetos em gráficos 3D?
### Tecnologia de Display

### Correção de gama
A correção gama compensa as diferenças da exibição de cor em diferentes dispositivos de saída, de modo a que as imagens tenham a mesma aparência quando visualizadas em diferentes monitores.
Um valor gama de 1 corresponde a um monitor "ideal"; isto é, tem uma progressão perfeitamente linear de branco até cinza e preto.
Os monitores de vídeo e computador não exibem cores de forma linear (como na primeira ilustração). Além disso, o brilho de um monitor tende a fazer com que uma imagem pareça mais clara que aquilo que seus valores de intensidade realmente especificam. A correção gama resolve este problema e pode garantir a consistência entre diferentes aplicativos ou diferentes monitores. Quando você define gama, encontre um valor que faça com que um tom cinza médio em seu próprio monitor coincida com um tom cinza médio (50%) verdadeiro.
### Cor
Uma cor é descrita para o computador como uma tupla ordenada de valores de um
**cor space** (espaço de cor). Os próprios valores são chamados de **components**(componentes) e são coordenados
nates no espaço de cores. O GDI do Windows representa as cores como uma tupla ordenada
de componentes vermelhos, verdes e azuis com cada componente no intervalo [0 . 0 , 1 . 0]
representado como uma quantidade de bytes sem sinal no intervalo [0 , 255].
Por padrão, o Windows GDI usa o espaço de cores 2 sRGB . Este é um adotado
espaço de cores de padrão internacional que foi proposto pela Hewlett-Packard
e a Microsoft. No entanto, o espaço sRGB é dependente do dispositivo devido ao
não linearidades de sistemas de exibição.

Em computação gráfica, muitas vezes é conveniente usar as cores HLS e HSV

HLS: matiz, leveza, saturação
HSV: matiz,saturação,valor

espaços para a criação de rampas de cores. Se a intenção de seu aplicativo é mapear dados
a uma gama de cores perceptivelmente iguais, você vai querer usar um espaço de cor outro
do que sRGB. Incrementos iguais nos componentes de uma cor sRGB não dão
aumentar para incrementos iguais na mudança de cor percebida no monitor.
Um tratamento completo da cor e su


### Transparência com Alpha
Muitas vezes, em computação gráfica, desejamos combinar pixels como se eles
foram pintados em folhas transparentes empilhadas umas sobre as outras, como no tradicional
animação cel. No Direct3D, a transparência é representada como um canal adicional
de informações que representam a quantidade de transparência do pixel.
Quando um pixel é totalmente opaco, seu valor alfa é 1 . 0 e este pixel completamente
obscurece qualquer coisa por trás dele. Quando um pixel é totalmente transparente, seu valor alfa
é 0 . 0 e tudo por trás do pixel aparece. Quando o valor alfa é
entre 0 e 1, o pixel é parcialmente transparente. O valor alfa de um pixel
pode ser usado para combinar o primeiro plano do pixel com algum plano de fundo baseado
na seguinte fórmula:
C = αC f + (1 - α ) C b
Quando α = 0, a cor resultante C não contém nenhuma quantidade de primeiro plano
cor C f e toda a cor de fundo C b . Quando α = 0 . 5, a cor resultante
contém uma mistura igual de C f e C b . Quando α = 1 . 0, a cor resultante contém
apenas a cor de primeiro plano C f e nenhuma quantidade da cor de fundo C b .
O canal alfa de um pixel também pode ser usado para mascaramento generalizado e fosco
efeitos, além de simples transparência. Nestes casos, uma fórmula diferente
é usado para combinar pixels de primeiro e segundo plano. O alfa de um pixel é
independente do espaço de cor do qual o pixel é desenhado


### Pontos
Na geometria, um ponto é representado por sua coordenada no espaço. Geometria usu-
ally usa um sistema de coordenadas cartesianas, onde as coordenadas de um ponto em
espaço são representados pela distância ao longo de cada um dos eixos principais para o
ponto. Enquanto outros sistemas de coordenadas são usados ​​em geometria (como spheri-
sistemas de coordenadas cal ou cilíndricas), os gráficos 3D usam uma coordenada cartesiana
sistema. A dimensionalidade de um ponto corresponde ao número de coordi-
nates necessários para representar o ponto. Assim, um ponto bidimensional requer dois
Coordenadas cartesianas e um ponto tridimensional requer três coordenadas.
### Linhas, raios e segmentos
Uma linha tem direção e comprimento infinito. A direção de uma linha pode ser
definido por dois pontos distintos pelos quais a linha passa. Dois ou mais
pontos distintos, todos em uma linha, são considerados colineares. Porque uma linha é definida por
quaisquer dois pontos distintos, tais pontos são sempre colineares.
Um raio começa em um ponto e se estende infinitamente em uma direção distante do
ponto. Um raio é definido por um ponto e uma direção.
Um segmento de linha é uma linha de comprimento finito definida por seus dois pontos finais.
Em computadores, devemos lidar com quantidades finitas, então não podemos tirar o total
extensão de uma linha ou raio de acordo com sua definição matemática. No computador
gráficos quando nos referimos a “linhas”, geralmente nos referimos a segmentos de linha.
### Planos e Triângulos
Um plano é uma folha orientada em 3 espaços sem espessura e com uma extensão infinita.
Um plano é definido por três pontos não colineares que cruzam o plano ou por
um ponto no plano e uma direção perpendicular ao plano. A direção
perpendicular a um plano é chamado de **normal** ao plano.
Um triângulo também é definido por três pontos no espaço 3 chamados vértices (singular
vértice). O triângulo está para o plano assim como o segmento de reta está para a reta. UMA
triângulo envolve uma área finita definida pela região interior delimitada pela linha
segmentos que unem seus vértices.
### Valores de ponto flutuante
Na matemática, todos os cálculos são exatos e realizam aritmética sobre os valores
não altera sua precisão. No entanto, os computadores armazenam aproximações para
números reais como valores de ponto flutuante e realizando operações aritméticas podem
fazer com que sua precisão mude. Nem todos os números reais podem ser representados exatamente
por uma representação de ponto flutuante. Números como π e outros transcendentais
os números têm uma expansão decimal infinita.
A natureza aproximada dos números de ponto flutuante geralmente levanta sua cabeça
ao comparar números de ponto flutuante e outras estruturas compostas de
números de pontos, como pontos, vetores, retas, planos, matrizes e assim por diante. o

### Sistemas de coordenadas
Objetos em Computação Gráfica possuem descrições numéricas (modelos) que caracterizam suas formas e dimensões.•   Esses números se referem a um sistema de coordenadas, normalmente o sistema Cartesiano de coordenadas: x, ye z.•   Em alguns casos, precisamos de mais de um sistema de coordenadas:–  Um sistema local para descrever partes individuais de uma máquina, por exemplo, que pode ser montada especificando-se a relação de cada sistema local das várias peças.
Normalmente, os apps de elementos gráficos 3D usam um dos dois tipos de sistemas de coordenadas cartesianas de esquerda e direita. Em ambos os sistemas de coordenadas, o eixo x positivo aponta para a direita e o eixo y positivo aponta para cima.

### À esquerda e à direita serão entregues de coordenadas
Você pode lembrar para qual direção o eixo z positivo aponta, apontando os dedos de sua mão direita ou esquerda na direção x positiva e curvando-os na direção y positiva. A direção do seu polegar aponta em sua direção ou para longe de você, é a direção em que o eixo z positivo aponta para esse sistema de coordenadas. A ilustração a seguir mostra esses dois sistemas de coordenadas.   
[leftrght](https://docs.microsoft.com/pt-br/windows/uwp/graphics-concepts/images/leftrght.png)

### polígonos
### triângulos
### malhas

## Como são iluminados?
### normals
### Normals face
### normals Vertex
### Albedo
### Ambiente oclusion

## Como são sombreados?

## Como são renderizados?
### Processamento da CPU e GPU
### Quais passos são executados e onde são?
- Cull distance
- CullDistanceVolume
- Frustum culling



## Pipelines gráficos modernos
Para começar, precisamos entender um pouco sobre pipelines gráficos modernos ou programáveis.   
No passado, éramos limitados no que o pipeline de gráficos da placa de vídeo tinha. Não podíamos mudar como ele desenhava cada pixel, além de enviar uma textura diferente, e não podíamos deformar vértices uma vez que estavam no cartão. Mas os tempos mudaram e agora temos pipelines gráficos programáveis . Agora podemos enviar código para a placa de vídeo para alterar a aparência dos pixels, dando a eles uma aparência irregular com mapas normais e adicionando reflexão (e muito realismo).    
Este código está na forma de geometria , vértice e sombreadores de fragmento , e eles mudam essencialmente como a placa de vídeo renderiza seus objetos.

## Renderização para frente
A renderização direta é a técnica de renderização out-of-the-box padrão que a maioria dos motores usa. Você fornece a geometria da placa de vídeo, ela a projeta e a divide em vértices, e então estes são transformados e divididos em fragmentos, ou pixels, que recebem o tratamento de renderização final antes de serem passados ​​para a tela.
É bastante linear e cada geometria é passada pelo tubo, uma de cada vez, para produzir a imagem final.    

## Renderização Adiada
Na renderização adiada, como o nome indica, a renderização é adiada um pouco até que todas as geometrias tenham passado pelo tubo; a imagem final é então produzida aplicando sombreamento no final.    
A iluminação adiada é uma modificação da renderização adiada que reduz o tamanho do G-buffer usando mais passagens na cena.

## Desempenho de Iluminação
A iluminação é o principal motivo para seguir um caminho em relação ao outro. Em um pipeline de renderização direta padrão, os cálculos de iluminação devem ser executados em cada vértice e em cada fragmento na cena visível, para cada luz na cena.    
Se você tem uma cena com 100 geometrias e cada geometria tem 1.000 vértices, então você pode ter cerca de 100.000 polígonos (uma estimativa muito grosseira). Placas de vídeo podem lidar com isso facilmente. Mas quando esses polígonos são enviados para o sombreador de fragmento, é aí que acontecem os caros cálculos de iluminação e a verdadeira desaceleração pode ocorrer.

## Qual escolher?

A resposta curta é: se você estiver usando muitas luzes dinâmicas, deve usar a renderização adiada. No entanto, existem algumas desvantagens significativas:

- Este processo requer uma placa de vídeo com vários destinos de renderização. Placas de vídeo antigas não têm isso, então não funcionará nelas. Não há solução alternativa para isso.
- Requer alta largura de banda. Você está enviando grandes buffers e placas de vídeo antigas, novamente, podem não ser capazes de lidar com isso. Não há solução alternativa para isso também.
- Você não pode usar objetos transparentes. (A menos que você combine a renderização adiada com a renderização direta apenas para esses objetos transparentes; então, você pode contornar esse problema.)
- Não há anti-aliasing. Bem, alguns motores fariam você acreditar nisso, mas existem soluções para esse problema: detecção de borda , FXAA .
- Apenas um tipo de material é permitido, a menos que você use uma modificação de renderização adiada chamada Iluminação adiada .
- As sombras ainda dependem do número de luzes e a renderização adiada não resolve nada aqui.

## Normal
### Normal face
Cada face em uma malha possui um vetor normal perpendicular. A direção do vetor é determinada pela ordem em que os vértices são definidos e pelo fato de o sistema de coordenadas ser destro ou canhoto. A face normal aponta para longe da parte frontal da face. No Microsoft Direct3D, apenas a frente de um rosto é visível. Uma face frontal é aquela em que os vértices são definidos no sentido horário.   
Qualquer rosto que não seja frontal é posterior. O Direct3D nem sempre renderiza faces posteriores; portanto, as faces posteriores são consideradas eliminadas. Você pode alterar o modo de seleção para renderizar as faces posteriores, se desejar.
### Normal Vertex
O Direct3D usa os normais de vértice para efeitos de sombreamento, iluminação e texturização de Gouraud.

### Maya
- Menu Display->Polygons->Face Normals
- Menu Display->Polygons->Vertex Normals

## Sombreamento  Gouraud
O sombreamento de Gouraud , em homenagem a Henri Gouraud , é um método de interpolação usado em computação gráfica para produzir sombreamento contínuo de superfícies representadas por malhas poligonais . Na prática, o sombreamento Gouraud é mais frequentemente usado para obter iluminação contínua nas malhas do triângulo , computando a iluminação nos cantos de cada triângulo e interpolando linearmente as cores resultantes para cada pixel coberto pelo triângulo. Gouraud publicou a técnica pela primeira vez em 1971.

## O que é Albedo?

Simplificando, albedo é o brilho geral de um objeto.    
Albedo é o poder de reflexão de um material. Em Corona, é a soma dos componentes difusos, reflexivos, refrativos e translúcidos do material. A emissão não conta para isso.   
Na realidade, quase nenhum material tem albedo quase branco. Em Corona, o uso de albedo branco puro (por exemplo, cor difusa de branco 255 e nível 1 difuso) resulta em uma renderização lenta e muito pouco realista. Você geralmente deve manter o albedo de seus materiais sob RGB180. Se isso deixar sua cena muito escura, você pode aumentar o brilho alterando os controles de exposição ou aumentando a intensidade das luzes.

***
## Referências
- [1](https://www.slideshare.net/sharadmitra/game-engine-overview)
- [2](https://en.wikipedia.org/wiki/Deferred_shading)
- [3](https://gamedevelopment.tutsplus.com/articles/forward-rendering-vs-deferred-rendering--gamedev-12342)
- [4](https://pt.qaz.wiki/wiki/Gouraud_shading)
- [5](https://www.scratchapixel.com/lessons/3d-basic-rendering/introduction-to-shading/shading-normals)
- [6](https://en.wikipedia.org/wiki/Vertex_normal)
- [7](https://pt.qaz.wiki/wiki/Polygon_mesh)
- [8](https://unrealartoptimization.github.io/book/profiling/passes/)
