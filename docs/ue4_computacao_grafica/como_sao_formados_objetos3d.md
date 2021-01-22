---
title: Manipulando Arrays
description: Como manipular variáveis do tipo Array
tags: [Unreal Engine,blueprint,array,get,set]
---

# Como são formados os objetos em gráficos 3D?

## Índice
1. [Pontos](#1)
1. [Linhas, raios e segmentos](#1)
1. [Planos e Triângulos](#2)
1. [Polígonos](#3)
1. [Valores de ponto flutuante](#3)
1. [Cor](#5)  
1. [Transparência com Alpha](#6)
1. [Sistemas de coordenadas](#4)
    1. [À esquerda e à direita serão entregues de coordenadas](#41)


<a name="1"></a>
## Pontos
Na geometria, um ponto é representado por sua coordenada no espaço. Geometria usu-
ally usa um sistema de coordenadas cartesianas, onde as coordenadas de um ponto em
espaço são representados pela distância ao longo de cada um dos eixos principais para o
ponto. Enquanto outros sistemas de coordenadas são usados ​​em geometria (como spheri-
sistemas de coordenadas cal ou cilíndricas), os gráficos 3D usam uma coordenada cartesiana
sistema. A dimensionalidade de um ponto corresponde ao número de coordi-
nates necessários para representar o ponto. Assim, um ponto bidimensional requer dois
Coordenadas cartesianas e um ponto tridimensional requer três coordenadas.

## Linhas, raios e segmentos
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
## Planos e Triângulos
Um plano é uma folha orientada em 3 espaços sem espessura e com uma extensão infinita.
Um plano é definido por três pontos não colineares que cruzam o plano ou por
um ponto no plano e uma direção perpendicular ao plano. A direção
perpendicular a um plano é chamado de **normal** ao plano.
Um triângulo também é definido por três pontos no espaço 3 chamados vértices (singular
vértice). O triângulo está para o plano assim como o segmento de reta está para a reta. UMA
triângulo envolve uma área finita definida pela região interior delimitada pela linha
segmentos que unem seus vértices.

## Valores de ponto flutuante
Na matemática, todos os cálculos são exatos e realizam aritmética sobre os valores
não altera sua precisão. No entanto, os computadores armazenam aproximações para
números reais como valores de ponto flutuante e realizando operações aritméticas podem
fazer com que sua precisão mude. Nem todos os números reais podem ser representados exatamente
por uma representação de ponto flutuante. Números como π e outros transcendentais
os números têm uma expansão decimal infinita.
A natureza aproximada dos números de ponto flutuante geralmente levanta sua cabeça
ao comparar números de ponto flutuante e outras estruturas compostas de
números de pontos, como pontos, vetores, retas, planos, matrizes e assim por diante. o


## Sistemas de coordenadas
Objetos em Computação Gráfica possuem descrições numéricas (modelos) que caracterizam suas formas e dimensões.•   Esses números se referem a um sistema de coordenadas, normalmente o sistema Cartesiano de coordenadas: x, ye z.•   Em alguns casos, precisamos de mais de um sistema de coordenadas:–  Um sistema local para descrever partes individuais de uma máquina, por exemplo, que pode ser montada especificando-se a relação de cada sistema local das várias peças.
Normalmente, os apps de elementos gráficos 3D usam um dos dois tipos de sistemas de coordenadas cartesianas de esquerda e direita. Em ambos os sistemas de coordenadas, o eixo x positivo aponta para a direita e o eixo y positivo aponta para cima.

## À esquerda e à direita serão entregues de coordenadas
Você pode lembrar para qual direção o eixo z positivo aponta, apontando os dedos de sua mão direita ou esquerda na direção x positiva e curvando-os na direção y positiva. A direção do seu polegar aponta em sua direção ou para longe de você, é a direção em que o eixo z positivo aponta para esse sistema de coordenadas. A ilustração a seguir mostra esses dois sistemas de coordenadas.   
[leftrght](https://docs.microsoft.com/pt-br/windows/uwp/graphics-concepts/images/leftrght.png)

## Cor
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


## Transparência com Alpha
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

***

## Referências
- [Game Engine Overview](https://www.slideshare.net/sharadmitra/game-engine-overview)
- [Polygon Mesh](https://pt.qaz.wiki/wiki/Polygon_mesh)
