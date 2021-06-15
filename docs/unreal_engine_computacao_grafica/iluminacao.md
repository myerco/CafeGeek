---
title: Iluminação
description: Iluminação e computação gráfica
tags: [Unreal Engine,Iluminação, Computação Gráfica]
---

# Iluminação
Neste capitulo serão apresentados como a iluminação funciona e suas propriedades.

## Índice
1. [Entendendo como os processos são executados pelo sistema operacional](#1)

<a name="1"></a>
## 1. Entendendo como os processos são executados pelo sistema operacional


## Cores
No mundo real, as cores podem assumir qualquer valor de cor conhecido, com cada objeto tendo sua (s) própria (s) cor (es). No mundo digital, precisamos mapear as (infinitas) cores reais para valores digitais (limitados) e, portanto, nem todas as cores do mundo real podem ser representadas digitalmente. As cores são representadas digitalmente usando um componente vermelho, verde e azul comumente abreviado como RGB. Usando diferentes combinações de apenas esses 3 valores, dentro de um intervalo de [0,1], podemos representar quase qualquer cor que existe.

A cor de um objeto que vemos na vida real não é a cor que ele realmente tem, mas é a cor refletida do objeto. As cores que não são absorvidas (rejeitadas) pelo objeto são as cores que percebemos dele. Como exemplo, a luz do sol é percebida como uma luz branca que é a soma combinada de muitas cores diferentes (como você pode ver na imagem). Se brilharmos essa luz branca em um brinquedo azul, ela absorverá todas as subcores da cor branca, exceto a cor azul. Como o brinquedo não absorve a parte de cor azul, ele é refletido. Essa luz refletida entra em nossos olhos, fazendo com que pareça que o brinquedo tem uma cor azul. A imagem a seguir mostra isso para um brinquedo de cor coral, onde ele reflete várias cores com intensidade variável:

![light_reflection](https://learnopengl.com/img/lighting/light_reflection.png)
*Figura: Reflexão - fonte https://learnopengl.com/*


A cor, um dos elementos mais naturais de nossa existência diária, pode ser difícil de descrever. Reconhecemos e nomeamos certas categorias amplas de cor, como "azul" e "amarelo", mas é muito difícil formalizar a noção de cor para que você possa observar, digamos, uma blusa de uma determinada cor e, em seguida, descrevê-la para um amigo para que eles tivessem exatamente a mesma imagem em mente.

No entanto, para que a computação gráfica funcione, devemos ser capazes de fazer exatamente essa descrição. Na verdade, devemos ir além disso e criar uma codificação para as cores para que possamos representá-las em formato digital como números. Felizmente, descobriu-se que a luz se presta a essa codificação. Um tratamento completo da cor, incluindo as propriedades da luz que ela representa, a maneira como o olho a percebe e a gama de diferentes representações dela não é importante no momento (consulte os links úteis abaixo para obter informações mais detalhadas).

Para nossos propósitos, será adequado observar que a maioria das cores com as quais precisamos lidar pode ser representada como uma combinação de intensidades de vermelho, verde e azul. Ou seja, vamos representar uma cor como três valores: a intensidade da luz vermelha em uma determinada cor, a intensidade da luz azul em uma determinada cor e a intensidade da luz verde em uma determinada cor. Chamamos cada um desses canais de cores componentes e chamamos esse sistema de representação de cores de espaço de cores RGB (ou apenas RGB).

## Cores no Unreal Engine
A Cor Base define a cor geral do Material, obtendo um valor Vector3 (RGB) onde cada canal é automaticamente fixado entre 0 e 1.

Se tirada do mundo real, esta é a cor quando fotografada usando um filtro polarizador (a polarização remove o especular dos não-metais quando alinhados).
![BaseColor_QS](https://docs.unrealengine.com/Images/RenderingAndGraphics/Materials/PhysicallyBased/BaseColor_QS.webp)

## reflections
- reflexões são muito difíceis de calcular em tempo real
- assim, usamos 3 técnicas diferentes, cada uma com prós / contras
- os 3 são renderizados e combinados em ordem
- uma vez prontos, eles são, por sua vez, mesclados com o resto da renderização

### Reflections Captures
Segue abaixo algumas características:
- Captura um mapa de cubo estático em um local específico
- Pré-calculado
- Muito rápido
- Impreciso
- Efeito local próximo ao local de captura
### Sphere Reflections
Atores de captura de reflexão são objetos estrategicamente colocados em todo o nível e alimentam dados de reflexão no ambiente de reflexão.

Existem atualmente duas formas de captura de reflexo: esfera e caixa. A forma é muito importante porque controla qual parte do nível é capturada no mapa do cubo, em que forma o nível é reprojetado em reflexos e em qual parte do nível pode receber reflexos desse mapa do cubo (área de influência).

Para obter mais informações sobre o ambiente de reflexão e as capturas de reflexão, consulte Ambiente de reflexão.

### Box Reflections

### Planar reflections
- não comum, captura de e para um plano, restrito a esse plano
- pode ser pesado
- ótimo para superfícies planas que precisam de reflexos precisos
- inadequado para todo o resto
- só funciona em uma área limitada
### PlanarReflextionVolume

### Screen space reflections (SSR)
Os reflexos do espaço da tela são um recurso do mecanismo que ajuda no aterramento de objetos em superfícies planas como o solo. Eles são ativados por padrão e se combinam com os resultados do Reflection Environment para fornecer uma sensação de reflexão mais completa.

- Sistema de reflexão padrão
- Afeta tudo e é tempo real
- Preciso
- Produz um resultado ruidoso e é meio pesado
- Só pode mostrar reflexos da geometria atualmente visíveis

### Considerações
A chave para obter os reflexos certos é colocar os Reflection Capture Actors em toda a sua cena. Seu primeiro impulso pode ser espalhar esses atores por toda a sua cena até ver um bom resultado. No entanto, existem algumas regras a serem observadas ao usar esses atores:

- **Screen Space** - Cada um dos atores de captura de reflexão incorre em um custo com base em quanto de sua tela é coberto por seu raio. Desta forma, eles são semelhantes a partículas ou luzes dinâmicas. Isso significa que você precisa ter cuidado para não ultrapassar os raios de seus Atores de captura.

- **Overlap** - Os raios do ator de captura de reflexão podem se sobrepor. Isso aumenta o custo por pixel de reflexos causados ​​por Atores sobrepostos. Quando combinado com o fato de que o custo aumenta com o espaço da tela, pode rapidamente se tornar proibitivo o desempenho simplesmente cobrir sua cena com Atores de captura de reflexão de alto raio.

- **Hierarchical Placement** - para economizar recursos e ainda ter um bom layout de Reflection Capture Actors, o uso de um layout hierárquico oferece uma configuração de reflexão sólida com o mínimo de sobreposição. Em tal sistema, uma captura de grande raio é colocada que captura os reflexos do fundo e, em seguida, uma série de Atores de captura menores capturam os reflexos em torno dos detalhes.

![Level Reflection](https://docs.unrealengine.com/4.26/Images/Resources/Showcases/Reflections/LevelReflection.webp)           
*Figura: Level Reflection*

### Performance
- **Reflection Captures** - São capturadas no carregamento do *Level* quando um projeto não é preparado para distribuição, portanto, ter muitos retardará o carregando de alguns e ter outros provavelmente não vai funcionar otimo ate o cozimento final
- Ficam mais pesadas quando muita operações de sombreamento se sobrepõem de pixel repetidas vezes.
- a nitidez da captura de reflexão pode ser definida por meio de sua resolução.


https://docs.unrealengine.com/en-US/Resources/ContentExamples/MaterialNodes/1_1/index.html
https://en.wikibooks.org/wiki/Concepts_of_Computer_Graphics/Output_Space/Colors

---
## Referências
1. [Interplay of Light](https://interplayoflight.wordpress.com/2017/10/25/how-unreal-renders-a-frame-part-2/)
1. [Iluminação](https://www.inf.pucrs.br/~pinho/CG/Aulas/Iluminacao/Ilumina.html)
1. [CG Aula 12 Iluminação](http://www.ic.uff.br/~anselmo/cursos/CGI/slidesGrad/CG_aula12(iluminacao).pdf)
