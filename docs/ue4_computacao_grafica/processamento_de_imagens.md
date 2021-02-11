---
title: Processamento de imagens
description: Neste capitulo vamos analisar como é realizado o processamento de imagens pela CPU e GPU.
tags: [processamento de imagens, gpu, cpu]
---

[CafeGeek](https://myerco.github.io/CafeGeek)  / [Computação Gráfica com Unreal Engine e Autodesk Maya](https://myerco.github.io/CafeGeek/ue4_computacao_grafica/index.html)

# Processamento de imagens
Neste capitulo vamos analisar como é realizado o processamento de imagens pela CPU e GPU.

## Índice

<a name="1"></a>
## 1. Processo de renderização

|  Threads|  | |  ||
|:-|-|-|-||
| **CPU** | Frame A | Frame B  | Frame C | Frame D|
| **DRAW CPU** |  | Frame A | Frame B  | Frame C|
| **GPU** |  |  | Frame A | Frame B|
| **Time** | **0** | **33** | **66** | |

**Time in miliseconds**
**(30 FPS)**

<a name="2"></a>
## 2. Processamento do Frame 0 - Time 0 - CPU
Calculo de toda a lógica e as transformações

1. Animações - Calcula quando as Animações iniciam e terminam.
1. Posição de modelos e objetos - Necessário para calcular a posição que influência .
1. Física - Calculo para determinar onde os objetos vão.
1. Inteligência Artificial
1. Cria e destrói, esconde e apresenta - Necessário para determinar onde os objetos aparecem no mundo.

> Qualquer coisa relativa a mudança e posição dos objetos.

**Resultado o UE4 conhece todas as transformações e todos os objetos**

<a name="3"></a>
## 3. Processamento do Frame 1 - Time 33ms - Preparar a Thread
Antes de podermos usar as transformações para renderizar a imagem, precisamos saber o que incluir na renderização.    
Isso é executado principalmente na CPU, mas algumas partes são manipuladas pela GPU.    
Processo de oclusão - Construção de lista de todos os objetos e modelos visíveis.
Processamento por objeto e não por polígono.

A seguir as 4 Etapas em ordem de execução

<a name="3.1"></a>
### 3.1 Distance Culling
Cull Distance Volumes usa uma matriz de distâncias e tamanhos para definir se um ator é renderizado ou não quando dentro do volume. Este método de seleção é ideal para grandes níveis externos, onde você teria edifícios ou estruturas de algum tipo com interiores detalhados, onde você gostaria de selecionar aqueles objetos que são pequenos demais para considerar importantes a distâncias distantes.

- A seleção de distância remove quaisquer objetos além de X da câmera
![](https://docs.unrealengine.com/Images/RenderingAndGraphics/VisibilityCulling/PerActorDistanceCullingSettings.webp)

  1. Configurar CulDistanceVolume
  1. Configurar o objeto

<a name="3.2"></a>  
### 3.2 Frustim Culling
A seleção de View Frustum usa a área visível da tela do campo de visão (FOV) da câmera para selecionar objetos fora deste espaço. O tronco da visão é uma forma piramidal que inclui um plano de recorte próximo e distante que define o mais próximo e o mais distante que qualquer objeto deve ser visível dentro deste espaço. Todos os outros objetos são removidos para economizar tempo de processamento.
![View Frustum](https://docs.unrealengine.com/Images/RenderingAndGraphics/VisibilityCulling/ViewFrustumDiagram.webp)
  1. O plano de recorte próximo é o ponto mais próximo da câmera em que os objetos ficarão visíveis.
  1. A Camera Frustum é a representação em formato piramidal da área de visualização visível entre os planos de clipe próximo e distante.
  1. O plano de recorte distante é o ponto mais distante da câmera em que os objetos serão visíveis.

<a name="3.3"></a>    
### 3.3 Precomputed Visibility
Volumes de visibilidade pré-computados armazenam o estado de visibilidade de atores não móveis em células colocadas acima de superfícies de projeção de sombras. Este método de seleção gera dados de visibilidade offline (durante uma construção de iluminação) e funciona melhor para níveis de tamanho pequeno a médio. A visibilidade pré-computada é ideal para hardware inferior e dispositivos móveis. Para tais hardwares e dispositivos, ao considerar os custos de desempenho, você obterá o máximo negociando custos de thread de renderização que são mais caros por aqueles com memória de tempo de execução, onde há mais flexibilidade em relação ao desempenho.

> Divide a cena em um grid, cada célula do grid registra o que é visível naquele local.

  1. Configurar PrecomputedVisibilityVolume.
  1. Show - Visualize -> Precomputed Visibility Cells
  1. A câmera ao entrar na célula pergunta    
    "o que pode ser ocluído?"   
    "O que pode ser renderizando e o que eu não devo renderizar?"     
    "neste local, lembramos que esses objetos eram visíveis e estes outros não eram"

<a name="3.4"></a>
### 3.4 Occlusion Culling
O sistema de oclusão dinâmica em UE4 vem com vários métodos de abate para escolher. Cada um desses métodos rastreia os estados de visibilidade dos Atores em um nível dentro do tronco de visão da câmera (ou campo de visão) que são obstruídos por outro Ator. As consultas são emitidas para a GPU ou CPU para verificar o estado de visibilidade de cada ator. Uma heurística é usada para reduzir o número de verificações de visibilidade necessárias, por sua vez, aumentando a eficácia geral de seleção e o desempenho.
  1. A seleção de oclusão verifica com precisão o estado de visibilidade em cada modelo, Isto é pesado.
  1. Use **freezerendering** para visualizar isto.
  1. **Stat initviews** mostra os custos.
  1. Verificar 10.000 objetos começa a ter um impacto.

**Performance**
- Configure distance Culling.
- Mais de 10-15k objetos pode ter impacto.
- Maior parte na CPU mas tem algum impacto na GPU.
- Grandes ambientes não ocluem bem,
- A mesma coisa para as partículas.
- Modelos grandes raramente irão ocluir e, assim, aumentar GPU.
- Mas combinar modelos com modelos grandes irá diminuir o custo da CPU.

**Resultado**
- Modelos A Visível.
- Modelos B Visível.
- Modelos C Não Visível.
- Modelos D Visível.
- Modelos E Não Visível.

A,B,D são processados na GPU.

***

## Referências

- [Visibility and Occlusion Culling](https://docs.unrealengine.com/en-US/RenderingAndGraphics/VisibilityCulling/index.html)
- [Cull Distance Volume](https://docs.unrealengine.com/en-US/RenderingAndGraphics/VisibilityCulling/CullDistanceVolume/index.html)
- [WTF Is? Volume - Cull Distance in Unreal Engine 4](https://www.youtube.com/watch?v=g0ML7oJll3w)
