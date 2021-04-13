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


https://docs.unrealengine.com/en-US/Resources/ContentExamples/MaterialNodes/1_1/index.html
https://en.wikibooks.org/wiki/Concepts_of_Computer_Graphics/Output_Space/Colors

---
## Referências
1. [Interplay of Light](https://interplayoflight.wordpress.com/2017/10/25/how-unreal-renders-a-frame-part-2/)
1. [Iluminação](https://www.inf.pucrs.br/~pinho/CG/Aulas/Iluminacao/Ilumina.html)
1. [CG Aula 12 Iluminação](http://www.ic.uff.br/~anselmo/cursos/CGI/slidesGrad/CG_aula12(iluminacao).pdf)
