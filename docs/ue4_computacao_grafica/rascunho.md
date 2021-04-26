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

- [2](https://en.wikipedia.org/wiki/Deferred_shading)
- [3](https://gamedevelopment.tutsplus.com/articles/forward-rendering-vs-deferred-rendering--gamedev-12342)
- [4](https://pt.qaz.wiki/wiki/Gouraud_shading)
- [5](https://www.scratchapixel.com/lessons/3d-basic-rendering/introduction-to-shading/shading-normals)
- [6](https://en.wikipedia.org/wiki/Vertex_normal)

- [8](https://unrealartoptimization.github.io/book/profiling/passes/)

- [9](https://legalizeadulthood.wordpress.com/the-direct3d-graphics-pipeline/)
- [10](https://thebookofshaders.com/)
