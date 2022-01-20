---
title: Trabalhando com iluminação
description: Iluminação.
tags: [Unreal Engine, HUD, user interface,UI]
layout: page
---

## Em construção

## Iluminação
1. Tipos de iluminação;
1. Propriedades de luz;
1. Lightmass Importance Volume;
1. Atmospheric Fog;
1. Post Process Volume;


## 1. Directional Light
[](https://docs.unrealengine.com/4.26/Images/BuildingWorlds/LightingAndShadows/LightTypes/Directional/Directional_LightHeader.webp)
*Figura: Directional Light*

**Directional Light** ou *luz direcional* simula a luz que está sendo emitida por uma fonte que está infinitamente distante. Isso significa que todas as sombras lançadas por essa luz serão paralelas, tornando-a a escolha ideal para simular a luz do sol. A luz direcional quando colocada pode ser definida para uma das três configurações de mobilidade:
- **Static** - Significa que a luz não pode ser alterada no jogo. Este é o método mais rápido de renderização e permite iluminação *cozida*.
- **Stationary** - Significa que a luz terá apenas seu sombreamento e iluminação rebatida da geometria estática preparada pelo **Lightmass**, todas as outras iluminações serão dinâmicas. Esta configuração também permite que a luz mude de cor e intensidade no jogo, mas não se move e permite iluminação parcial.
- **Moveable** - Significa que a luz é totalmente dinâmica e permite sombreamento dinâmico. Este é o mais lento em termos de renderização, mas permite maior flexibilidade durante o jogo.

## 2 Sky Light
A **Sky Light** captura as partes distantes do seu nível e as aplica à cena como uma luz. Isso significa que a aparência do céu e sua iluminação / reflexos serão iguais, mesmo que o céu esteja vindo da atmosfera, ou nuvens em camadas no topo de um *skybox* ou montanhas distantes.
Você também pode especificar manualmente um mapa de cubo a ser usado.

### Captura de cena
O **Sky Light** só irá capturar a cena em certas circunstâncias:

- Para **Static Sky Lights**, as atualizações acontecem automaticamente durante a construção da iluminação.
- Para **Sky Lights Stationary or Moveable**, as atualizações acontecem uma vez no carregamento e somente atualizações adicionais quando a **Recapture** é chamada, a menos que o recurso **Real Time Capture** esteja habilitado. Ambos podem ser acessados por meio do painel **Details** e a **Recapture** também pode ser chamada por meio do Blueprint no jogo.

> Um **Sky Light** deve ser usado em vez do **Ambient Cubemap** para representar a luz do céu, porque as **Sky Lights** suportam sombras locais, o que evita que áreas internas sejam iluminadas pelo céu.

## 2 Light Component

Um PointLightComponent funciona como uma lâmpada do mundo real, emitindo luz em todas as direções do filamento de tungstênio da lâmpada. No entanto, por uma questão de desempenho, PointLightComponents são simplificados emitindo luz igualmente em todas as direções de apenas um único ponto no espaço.


## 4 Spot Light
Um **Spot Light** emite luz de um único ponto em forma de cone. Os usuários recebem dois cones para moldar a luz, o Ângulo do Cone Interno e o Ângulo do Cone Externo.

Dentro do ângulo do cone interno, a luz atinge o brilho total. Conforme você vai da extensão do raio interno às extensões do Ângulo do Cone Externo, ocorre uma queda, criando uma penumbra ou suavizando em torno do disco de iluminação do **Spot Light**. O raio da luz define o comprimento dos cones. De forma mais simples, isso funcionará como uma luz de flash ou um palco pode acender.

## 5 Point Light
As **Point Lights** funcionam como uma lâmpada do mundo real, emitindo luz em todas as direções a partir do filamento de tungstênio da lâmpada. No entanto, por uma questão de desempenho, as **Point Lights** são simplificadas emitindo luz igualmente em todas as direções a partir de apenas um único ponto no espaço. O ponto de luz quando colocado pode ser definido para uma das três configurações de mobilidade:

## Rect Light

O **Rect Light** emite luz na cena a partir de um plano retangular com largura e altura definidas. Você pode usá-los para simular qualquer tipo de fonte de luz que tenha áreas retangulares, como televisores ou telas de monitor, luminárias suspensas ou arandelas de parede.

## Propriedades da luz
As luzes no Unreal Engine são definidas usando unidades de iluminação baseadas fisicamente, tornando possível inserir valores conhecidos e mensuráveis para alcançar uma iluminação totalmente realista. Além dos tipos de luz que suportam diferentes unidades de iluminação, o **Post Process** para adaptação ocular (ou exposição automática) agora oferece suporte a uma ampla gama de valores e é expresso em EV100 (ISO 100).

> Entre as unidades baseadas fisicamente para iluminação e exposição automática, a criação de iluminação realista é muito mais alcançável sem números "mágicos" e os artistas tendo que "observar" valores diferentes.
Para esses tipos de luz, sua intensidade é exibida da seguinte forma:

- **Directional Light** usa **Direct Normal Illuminance** (iluminação normal direta), expressa como Lux, que é igual a um lúmen por metro quadrado.
- **Sky Light** e **Emissive Materials** como **Static Lights** usam a luminância expressa como Candela por metro quadrado (cd / m2).

- As **Point Light**, **Spot** e **Rect** podem selecionar entre as seguintes unidades de iluminação:
  - Candela (cd) é uma medida de intensidade luminosa emitida uniformemente em um ângulo sólido de um [esteradiano](https://pt.wikipedia.org/wiki/Esferorradiano). Por exemplo, uma luz definida para 1000 cd mede 1000 lux em um metro.
  - Lúmen (lm) é uma medida do fluxo luminoso emitido no ângulo de um esteradiano. Na fotometria, o fluxo luminoso (ou potência luminosa) é a medida da potência percebida da luz. Não importa sua distribuição (ponto largo ou estreito), a quantidade total de energia emitida será a mesma.
  - **Unitless** é um valor de intensidade de luz específico do mecanismo e mantém a compatibilidade com versões de mecanismo anteriores ao Unreal Engine 4.19.
## Configuração no projeto
->Project->Rendering->Light Unit

## Formas de captura de reflexão
O Reflection Environment funciona capturando o nível estático em muitos pontos e reprojetando-o em formas simples, como esferas em reflexos. Os artistas escolhem os pontos de captura colocando Atores ReflectionCapture. Os reflexos são atualizados em tempo real durante a edição para auxiliar no posicionamento, mas são estáticos no tempo de execução. Projetar o nível capturado em formas simples fornece paralaxe aproximada para a reflexão. Cada pixel se mistura entre vários mapas de cubo para obter o resultado final. Atores ReflectionCapture menores substituem os maiores, para que você possa refinar a precisão da paralaxe de reflexão em áreas conforme necessário. Por exemplo, você pode colocar uma captura no centro de uma sala e, em seguida, refinar o reflexo colocando capturas menores nos cantos da sala.

Atores de captura de reflexão são objetos estrategicamente colocados em todo o nível e alimentam dados de reflexão no ambiente de reflexão.

## Sphere Reflection

Existem atualmente duas formas de captura de reflexo: esfera e caixa. A forma é muito importante porque controla qual parte do nível é capturada no mapa do cubo, em que forma o nível é reprojetado em reflexos e em qual parte do nível pode receber reflexos desse mapa do cubo (área de influência).

Para obter mais informações sobre o ambiente de reflexão e as capturas de reflexão, consulte Ambiente de reflexão.

## Box Reflection Capture


## Lightmass Importance Volume
**Lightmass** cria mapas de luz com interações de luz complexas, como sombreamento de área e inter-reflexão difusa. É usado para pré-calcular porções da contribuição de iluminação de luzes com mobilidade estacionária e estática.        
Muitos mapas têm malhas até a borda da grade no editor, mas a área real de jogo que precisa de iluminação de alta qualidade é muito menor. A massa de luz emite fótons com base no tamanho do nível, portanto, essas malhas de fundo aumentarão muito o número de fótons que precisam ser emitidos e o tempo de construção de iluminação aumentará. O **Lightmass Importance Volume** controla a área em que a *Lightmass* emite fótons, permitindo concentrar apenas na área que precisa de iluminação indireta detalhada. As áreas fora do volume de importância recebem apenas um salto de iluminação indireta em uma qualidade inferior.

## Referências

- [Components Lights](https://docs.unrealengine.com/4.26/en-US/Basics/Components/Lights/)
- [Lightmass](https://docs.unrealengine.com/4.26/en-US/RenderingAndGraphics/Lightmass/)
- [LightTypes](https://docs.unrealengine.com/4.26/en-US/BuildingWorlds/LightingAndShadows/LightTypes/)
- [candelas ou lumens qual é o correto](https://blogdaliga.com.br/candelas-ou-lumens-qual-e-correto/)
- [Reflections](https://docs.unrealengine.com/4.26/en-US/Resources/Showcases/Reflections/)
