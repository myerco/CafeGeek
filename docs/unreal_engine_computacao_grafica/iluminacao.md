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


## Materiais

No mundo real, cada objeto tem uma reação diferente à luz. Objetos de aço costumam ser mais brilhantes do que um vaso de barro, por exemplo, e um recipiente de madeira não reage à luz da mesma forma que um recipiente de aço. Alguns objetos refletem a luz sem muita dispersão, resultando em pequenos realces especulares, e outros se espalham muito, dando ao realce um raio maior. Se quisermos simular vários tipos de objetos em OpenGL, temos que definir material propriedades específicas para cada superfície.

No capítulo anterior, definimos um objeto e uma cor de luz para definir a saída visual do objeto, combinada com um componente de intensidade ambiental e especular. Ao descrever uma superfície, podemos definir uma cor de material para cada um dos 3 componentes de iluminação: iluminação ambiente, difusa e especular. Ao especificar uma cor para cada um dos componentes, temos um controle refinado sobre a saída de cor da superfície. Agora adicione um componente de brilho a essas 3 cores e teremos todas as propriedades do material de que precisamos:

No shader de fragmento, criamos um structpara armazenar as propriedades materiais da superfície. Também podemos armazená-los como valores uniformes individuais, mas armazená-los como uma estrutura os mantém mais organizados. Primeiro definimos o layout da estrutura e, em seguida, simplesmente declaramos uma variável uniforme com a estrutura recém-criada como seu tipo.

Como você pode ver, definimos um vetor de cor para cada um dos componentes da iluminação Phong. O vetor de material ambiente define a cor que a superfície reflete sob a iluminação ambiente; geralmente é igual à cor da superfície. O vetor de material difuso define a cor da superfície sob iluminação difusa. A cor difusa é (assim como a iluminação ambiente) definida para a cor da superfície desejada. O vetor de material especular define a cor do realce especular na superfície (ou possivelmente reflete uma cor específica da superfície). Por último, o brilho impacta o espalhamento / raio do realce especular.

## Propriedades da luz

Com esses 4 componentes que definem o material de um objeto, podemos simular muitos materiais do mundo real. Uma tabela encontrada em devernay.free.fr mostra uma lista de propriedades de materiais que simulam materiais reais encontrados no mundo exterior. A imagem a seguir mostra o efeito que vários desses valores materiais do mundo real têm em nosso cubo:

O objeto é muito brilhante. A razão para o objeto ser muito brilhante é que as cores ambientais, difusas e especulares são refletidas com força total de qualquer fonte de luz. As fontes de luz também têm intensidades diferentes para seus componentes ambientais, difusos e especulares, respectivamente. No capítulo anterior, resolvemos isso variando as intensidades ambientais e especulares com um valor de força. Queremos fazer algo semelhante, mas desta vez especificando vetores de intensidade para cada um dos componentes de iluminação. Se visualizássemos lightColor como vec3(1.0)o código ficaria assim:

## Cores claras diferentes

Até agora usamos cores claras apenas para variar a intensidade de seus componentes individuais, escolhendo cores que vão do branco ao cinza ao preto, não afetando as cores reais do objeto (apenas sua intensidade). Como agora temos fácil acesso às propriedades da luz, podemos mudar suas cores com o tempo para obter alguns efeitos realmente interessantes. Uma vez que tudo já está configurado no sombreador de fragmento, alterar as cores da luz é fácil e cria imediatamente alguns efeitos funky:


## Mapas de iluminação

No capítulo anterior , discutimos a possibilidade de cada objeto ter um material único e próprio que reage de maneira diferente à luz. Isso é ótimo para dar a cada objeto uma aparência única em comparação com outros objetos, mas ainda não oferece muita flexibilidade na saída visual de um objeto.

No capítulo anterior, definimos um material para um objeto inteiro como um todo. Os objetos do mundo real, entretanto, geralmente não consistem em um único material, mas em vários materiais. Pense em um carro: seu exterior consiste em um tecido brilhante, tem janelas que refletem parcialmente o ambiente ao redor, seus pneus são quase brilhantes, então eles não têm reflexos especulares e tem aros que são super brilhantes (se você realmente lavou seu carro está certo). O carro também possui cores difusas e ambientes que não são iguais para todo o objeto; um carro exibe muitas cores ambientes / difusas diferentes. Em suma, tal objeto tem diferentes propriedades materiais para cada uma de suas diferentes partes.

Portanto, o sistema de materiais do capítulo anterior não é suficiente para todos, exceto para os modelos mais simples, portanto, precisamos estender o sistema introduzindo mapas difusos e especulares . Isso nos permite influenciar o difuso (e indiretamente o componente ambiente, já que devem ser os mesmos de qualquer maneira) e o componente especular de um objeto com muito mais precisão.

## Mapas difusos

O que queremos é alguma forma de definir as cores difusas de um objeto para cada fragmento individual. Algum tipo de sistema onde podemos recuperar um valor de cor com base na posição do fragmento no objeto?

Isso provavelmente deve soar familiar e já estamos usando esse sistema há algum tempo. Isso soa como texturas que discutimos extensivamente em um dos capítulos anteriores e é basicamente isso: uma textura. Estamos apenas usando um nome diferente para o mesmo princípio subjacente: usando uma imagem envolvida em um objeto que podemos indexar para valores de cor exclusivos por fragmento. Em cenas iluminadas, isso geralmente é chamado de mapa difuso (geralmente é assim que os artistas 3D os chamam antes do PBR), uma vez que uma imagem de textura representa todas as cores difusas do objeto.

Para demonstrar mapas difusos, vamos usar a seguinte imagem de um contêiner de madeira com uma borda de aço:

## Cubemaps
Já usamos texturas 2D há algum tempo, mas há mais tipos de textura que ainda não exploramos e, neste capítulo, discutiremos um tipo de textura que é uma combinação de várias texturas mapeadas em uma: um mapa de cubo.

Um mapa de cubo é uma textura que contém 6 texturas 2D individuais, cada uma formando um lado de um cubo: um cubo texturizado. Você pode estar se perguntando qual é o objetivo desse cubo? Por que se preocupar em combinar 6 texturas individuais em uma única entidade em vez de apenas usar 6 texturas individuais? Bem, os mapas de cubo têm a propriedade útil de poderem ser indexados / amostrados usando um vetor de direção. Imagine que temos um cubo unitário 1x1x1 com a origem de um vetor de direção residindo em seu centro. Amostrar um valor de textura do mapa do cubo com um vetor de direção laranja se parece um pouco com isto:

https://www.inf.pucrs.br/~pinho/CG/Aulas/Iluminacao/Ilumina.html
https://docs.unrealengine.com/en-US/WorkingWithContent/Types/StaticMeshes/HowTo/AutomaticLODGeneration/index.html



https://docs.unrealengine.com/en-US/Resources/ContentExamples/MaterialNodes/1_1/index.html
https://en.wikibooks.org/wiki/Concepts_of_Computer_Graphics/Output_Space/Colors

---
## Referências
1. [Interplay of Light](https://interplayoflight.wordpress.com/2017/10/25/how-unreal-renders-a-frame-part-2/)
1. [Iluminação](https://www.inf.pucrs.br/~pinho/CG/Aulas/Iluminacao/Ilumina.html)
1. [CG Aula 12 Iluminação](http://www.ic.uff.br/~anselmo/cursos/CGI/slidesGrad/CG_aula12(iluminacao).pdf)
