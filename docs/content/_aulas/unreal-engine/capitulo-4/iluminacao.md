---
title: Iluminação
excerpt: Neste capítulo vamos implementar a Iluminação do jogo.
categories: 
  - "unreal-engine"
  - "capitulo-4"
date: 2024-06-03T08:48:05-04:00
order: 403
sidebar:
  nav: unreal-engine
---

## 1. Directional Light

**Directional Light** ou *luz direcional* simula a luz que está sendo emitida por uma fonte que está infinitamente distante. Isso significa que todas as sombras lançadas por essa luz serão paralelas, tornando-a a escolha ideal para simular a luz do sol. A luz direcional quando colocada pode ser definida para uma das três configurações de mobilidade:

### 1.1. Static

Significa que a luz não pode ser alterada no jogo. Este é o método mais rápido de renderização e permite iluminação *cozida*.

### 1.2. Stationary

Significa que a luz terá apenas seu sombreamento e iluminação rebatida da geometria estática preparada pelo **Lightmass**, todas as outras iluminações serão dinâmicas. Esta configuração também permite que a luz mude de cor e intensidade no jogo, mas não se move e permite iluminação parcial.

### 1.3. Moveable

Significa que a luz é totalmente dinâmica e permite sombreamento dinâmico. Este é o mais lento em termos de renderização, mas permite maior flexibilidade durante o jogo.

{% include image.html
    src="https://docs.unrealengine.com/4.26/Images/BuildingWorlds/LightingAndShadows/LightTypes/Directional/Directional_LightHeader.webp"
    alt="Figura: LightHeader."
    caption="Figura:Directional Light.."
%}

## 2. Sky Light

A **Sky Light** captura as partes distantes do seu nível e as aplica à cena como uma luz. Isso significa que a aparência do céu e sua iluminação / reflexos serão iguais, mesmo que o céu esteja vindo da atmosfera, ou nuvens em camadas no topo de um *skybox* ou montanhas distantes.
Você também pode especificar manualmente um mapa de cubo a ser usado.

### 2.1. Captura de cena

O **Sky Light** só irá capturar a cena em certas circunstâncias:

- Para **Static Sky Lights**, as atualizações acontecem automaticamente durante a construção da iluminação.
- Para **Sky Lights Stationary or Moveable**, as atualizações acontecem uma vez no carregamento e somente atualizações adicionais quando a **Recapture** é chamada, a menos que o recurso **Real Time Capture** esteja habilitado. Ambos podem ser acessados por meio do painel **Details** e a **Recapture** também pode ser chamada por meio do Blueprint no jogo.

> Um **Sky Light** deve ser usado em vez do **Ambient Cubemap** para representar a luz do céu, porque as **Sky Lights** suportam sombras locais, o que evita que áreas internas sejam iluminadas pelo céu.

## 3. Light Component

Um PointLightComponent funciona como uma lâmpada do mundo real, emitindo luz em todas as direções do filamento de tungstênio da lâmpada. No entanto, por uma questão de desempenho, PointLightComponents são simplificados emitindo luz igualmente em todas as direções de apenas um único ponto no espaço.

Propriedades básicas:

Intensity: Valor em candelas;

Intensity Units: Altera de Candelas para Lumens. É possível usar os valores de iluminação das luzes reais.

`Unitless` é um valor padrão.

Color: Cor da luz;

Temperature:

Attenation Radius : Raio de influência.

## 4. Spot Light

Um **Spot Light** emite luz de um único ponto em forma de cone. Os usuários recebem dois cones para moldar a luz, o Ângulo do Cone Interno e o Ângulo do Cone Externo.

Dentro do ângulo do cone interno, a luz atinge o brilho total. Conforme você vai da extensão do raio interno às extensões do Ângulo do Cone Externo, ocorre uma queda, criando uma penumbra ou suavizando em torno do disco de iluminação do **Spot Light**. O raio da luz define o comprimento dos cones. De forma mais simples, isso funcionará como uma luz de flash ou um palco pode acender.

## 5. Point Light

As **Point Lights** funcionam como uma lâmpada do mundo real, emitindo luz em todas as direções a partir do filamento de tungstênio da lâmpada. No entanto, por uma questão de desempenho, as **Point Lights** são simplificadas emitindo luz igualmente em todas as direções a partir de apenas um único ponto no espaço. O ponto de luz quando colocado pode ser definido para uma das três configurações de mobilidade:

- Stationarea: a área de influência não pode cruzar com outro point light

[Por que isso?](https://michaeljcole.github.io/wiki.unrealengine.com/LightingTroubleshootingGuide/#Why_does_this_look_nothing_like_it_did_before.2C_or_Engine_Scalability_and_you)

As luzes estacionárias são limitadas a um máximo de 4 luzes de projeção de sombra sobrepostas. Quando o 5º for adicionado, haverá um 'X' vermelho indicando que a luz nesta área de sobreposição com o menor raio reverterá para uma luz dinâmica. Isso pode causar problemas de desempenho porque a iluminação dinâmica que projeta sombras é mais cara de usar do que a iluminação pré-definida.

Se a iluminação for construída com alguma luz estacionária que se sobreponha aos ofensores, haverá um aviso detalhando qual luz é o ofensor e as ramificações.

Para corrigir isso, certifique-se de que não haja mais de 4 sombras sobrepostas de luzes estacionárias em uma única área. Isso pode exigir a remoção de uma luz, desabilitar o sinalizador Cast Shadows ou ajustar o raio para que não fique mais sobreposto.

Se houver apenas três luzes estacionárias colocadas e houver um X vermelho sobre a 4ª luz, certifique-se de que não haja outras luzes estacionárias em seu nível que se sobreponham. Muitas vezes, essa seria a luz direcional definida como estacionária que está causando esse problema.

## 6. Rect Light

O **Rect Light** emite luz na cena a partir de um plano retangular com largura e altura definidas. Você pode usá-los para simular qualquer tipo de fonte de luz que tenha áreas retangulares, como televisores ou telas de monitor, luminárias suspensas ou arandelas de parede.

## 7. Propriedades da luz

As luzes no Unreal Engine são definidas usando unidades de iluminação baseadas fisicamente, tornando possível inserir valores conhecidos e mensuráveis para alcançar uma iluminação totalmente realista. Além dos tipos de luz que suportam diferentes unidades de iluminação, o **Post Process** para adaptação ocular (ou exposição automática) agora oferece suporte a uma ampla gama de valores e é expresso em EV100 (ISO 100).

> Entre as unidades baseadas fisicamente para iluminação e exposição automática, a criação de iluminação realista é muito mais alcançável sem números "mágicos" e os artistas tendo que "observar" valores diferentes.
Para esses tipos de luz, sua intensidade é exibida da seguinte forma:

- **Directional Light** usa **Direct Normal Illuminance** (iluminação normal direta), expressa como Lux, que é igual a um lúmen por metro quadrado.
- **Sky Light** e **Emissive Materials** como **Static Lights** usam a luminância expressa como Candela por metro quadrado (cd / m2).

- As **Point Light**, **Spot** e **Rect** podem selecionar entre as seguintes unidades de iluminação:
  - Candela (cd) é uma medida de intensidade luminosa emitida uniformemente em um ângulo sólido de um [esteradiano](https://pt.wikipedia.org/wiki/Esferorradiano). Por exemplo, uma luz definida para 1000 cd mede 1000 lux em um metro.
  - Lúmen (lm) é uma medida do fluxo luminoso emitido no ângulo de um esteradiano. Na fotometria, o fluxo luminoso (ou potência luminosa) é a medida da potência percebida da luz. Não importa sua distribuição (ponto largo ou estreito), a quantidade total de energia emitida será a mesma.
  - **Unitless** é um valor de intensidade de luz específico do mecanismo e mantém a compatibilidade com versões de mecanismo anteriores ao Unreal Engine 4.19.

## 8. Configuração no projeto

Para configurar utilize o menu:

`Project` > `Rendering` > `Light Unit`

## 9. Formas de captura de reflexão

O Reflection Environment funciona capturando o nível estático em muitos pontos e reprojetando-o em formas simples, como esferas em reflexos. Os artistas escolhem os pontos de captura colocando Atores ReflectionCapture. Os reflexos são atualizados em tempo real durante a edição para auxiliar no posicionamento, mas são estáticos no tempo de execução. Projetar o nível capturado em formas simples fornece paralaxe aproximada para a reflexão. Cada pixel se mistura entre vários mapas de cubo para obter o resultado final. Atores ReflectionCapture menores substituem os maiores, para que você possa refinar a precisão da paralaxe de reflexão em áreas conforme necessário. Por exemplo, você pode colocar uma captura no centro de uma sala e, em seguida, refinar o reflexo colocando capturas menores nos cantos da sala.

Atores de captura de reflexão são objetos estrategicamente colocados em todo o nível e alimentam dados de reflexão no ambiente de reflexão.

## 10. Sphere Reflection

Existem atualmente duas formas de captura de reflexo: esfera e caixa. A forma é muito importante porque controla qual parte do nível é capturada no mapa do cubo, em que forma o nível é reprojetado em reflexos e em qual parte do nível pode receber reflexos desse mapa do cubo (área de influência).

Para obter mais informações sobre o ambiente de reflexão e as capturas de reflexão, consulte Ambiente de reflexão.

## 11. Box Reflection Capture

## 12. Lightmass Importance Volume

**Lightmass** cria mapas de luz com interações de luz complexas, como sombreamento de área e inter-reflexão difusa. É usado para pré-calcular porções da contribuição de iluminação de luzes com mobilidade estacionária e estática.
Muitos mapas têm malhas até a borda da grade no editor, mas a área real de jogo que precisa de iluminação de alta qualidade é muito menor. A massa de luz emite fótons com base no tamanho do nível, portanto, essas malhas de fundo aumentarão muito o número de fótons que precisam ser emitidos e o tempo de construção de iluminação aumentará. O **Lightmass Importance Volume** controla a área em que a *Lightmass* emite fótons, permitindo concentrar apenas na área que precisa de iluminação indireta detalhada. As áreas fora do volume de importância recebem apenas um salto de iluminação indireta em uma qualidade inferior.

## 13. Auto exposure

Após desligar todas as luzes ainda ficam elementos visiveis, porque eles ainda tem marcas da iluminação, para desligar esses elementos utilize:

`Project Setting` > `Auto Exposure` > Off

O backlight ainda vai estar presente.

## 14. Build ligths

Para construir e calcular todas as sombras e reflexos da cena utilize :

`Build` > `Light`

## 15. Sombras

Construção de sombras usando back.

`View Mode` > `Optimization ViewModes` `LightMap Density`

Apresenta a o mapa de iluminação da malha.

As cores identificam a densidade da iluminação.

>O ideal é que o mapa sempre fique na cor verde.

Os objetos tem um mapa de luz para controlar a resolução de iluminação, para verificar utilize as propriedades do objeto:

``Ligthing` > `Overridden Light Map Res`

Alter os valores para a qualidade das sombras.

## 16. Unlit

Apresenta a cena sem iluminação.

## 17. Salvando a imagem da cena

Para salvar cena em um arquivo utilize:

`Viewports Options` > `High Resolution Sreenshot`

## 18. Reflexos

Material todo branco.
