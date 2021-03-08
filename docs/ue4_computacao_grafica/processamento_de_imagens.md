---
title: Processamento de imagens
description: Neste capitulo vamos analisar como é realizado o processamento de imagens pela CPU e GPU.
tags: [processamento de imagens, gpu, cpu]
---

[CafeGeek](https://myerco.github.io/CafeGeek)  / [Computação Gráfica com Unreal Engine e Autodesk Maya](https://myerco.github.io/CafeGeek/ue4_computacao_grafica/index.html)

# Processamento de imagens
Neste capitulo vamos analisar como é realizado o processamento de imagens pela CPU e GPU.

## Índice
1. [O processo de renderização no Unreal Engine](#1)
1. [Processamento do Frame 0 - Time 0 - CPU](#2)
1. [Processamento do Frame 1 - Time 33ms - Preparar a Thread](#3)
    1. [Distance Culling](#3.1)
    1. [Frustim Culling](#3.2)
    1. [Precomputed Visibility](#3.3)
    1. [Occlusion Culling](#3.4)            
1. [ Processamento do Frame 2 - Time 66ms - GPU](#4)  
    1. [Drawcalls](#4.1)
    1. [O comando Stat RHI](#4.2)
    1. [O comando Stat unit e Stat FPS](#4.3)
    1. [Considerações](#4.4)

<a name="1"></a>
## 1. O processo de renderização no Unreal Engine

|  Threads| 1 | 2| 3 |4|
|:-|-|-|-||
| **CPU** | <span style="color:blue">Frame A</span> |  <span style="color:red">Frame B</span>  | Frame C | Frame D|
| **DRAW CPU** |  | <span style="color:blue">Frame A</span> |  <span style="color:red">Frame B</span>  | Frame C|
| **GPU** |  |  | <span style="color:blue">Frame A</span> | <span style="color:red"> Frame B</span>|
| **Time** | **0** | **33** | **66** | |

**Time in miliseconds**
**(30 FPS)**

<a name="2"></a>
## 2. Processamento do Frame 0 - Time 0 - CPU
Calculo de toda a lógica e as transformações:
> Qualquer coisa relativa a mudança e posição dos objetos.

1. **Animações** - Calcula quando as Animações iniciam e terminam.
1. **Posição de modelos e objetos** - Necessário para calcular a posição e sua influência.
1. **Física** - Calculo para determinar onde os objetos vão.
1. **Inteligência Artificial** - Por exemplo, em um veículo controlado por IA é necessário determinar, como ele se movimenta,  como o estado e onde o carro estará realmente.
1. **Cria e destrói, esconde e apresenta** - Necessário para determinar onde os objetos aparecem no mundo.

**Resultado:** o UE4 conhece todas as transformações e todos os objetos.

<a name="3"></a>
## 3. Processamento do Frame 1 - Time 33ms - Preparar a Thread
Antes de podermos usar as transformações para renderizar a imagem, precisamos saber o que incluir na renderização, isso é executado principalmente na CPU, mas algumas partes são manipuladas pela GPU, para tal finalidade é realizada a tarefa :        
- Processo de oclusão - Construção de lista de todos os objetos e modelos visíveis.
> O Processamento é realizado por objeto e não por polígono.

A seguir as 4 Etapas em ordem de execução desse processo.

1. **Distance Culling** - Remove quaisquer objetos além de X da câmera.
1. **Frustim Culling** - Verifica o que está na frente da câmera.
1. **Precomputed Visibility** - (Visibilidade pré-computada) Divide a cena em uma grade, cada célula da grade lembra o que está visível naquele local
1. **Occlusion Culling** - Verifica com precisão o estado de visibilidade em cada modelo.   

<a name="3.1"></a>
### 3.1 Distance Culling
**Cull Distance Volumes** usa uma matriz de distâncias e tamanhos para definir se um ator é renderizado ou não quando dentro do volume. Este método de seleção é ideal para grandes níveis externos, onde você teria edifícios ou estruturas de algum tipo com interiores detalhados, onde você gostaria de selecionar aqueles objetos que são pequenos demais para considerar importantes a distâncias distantes.

- A seleção de distância remove quaisquer objetos além de X da câmera
![PerActorDistanceCullingSettings](https://docs.unrealengine.com/Images/RenderingAndGraphics/VisibilityCulling/PerActorDistanceCullingSettings.webp)

  1. Configurar **Cull Distance Volume**.     

    Place Actors->Volumes.
  1. Configurar o objeto.     

    Alterar as dimensões do objeto para definir a área de corte.

<a name="3.2"></a>  
### 3.2 Frustim Culling
A seleção de **View Frustum** usa a área visível da tela do campo de visão (FOV) da câmera para selecionar objetos fora deste espaço. O tronco da visão é uma forma piramidal que inclui um plano de recorte próximo e distante que define o mais próximo e o mais distante que qualquer objeto deve ser visível dentro deste espaço. Todos os outros objetos são removidos para economizar tempo de processamento.
![View Frustum](https://docs.unrealengine.com/Images/RenderingAndGraphics/VisibilityCulling/ViewFrustumDiagram.webp)
  1. O plano de recorte próximo é o ponto mais próximo da câmera em que os objetos ficarão visíveis.
  1. A Camera Frustum é a representação em formato piramidal da área de visualização visível entre os planos de clipe próximo e distante.
  1. O plano de recorte distante é o ponto mais distante da câmera em que os objetos serão visíveis.

- Os objetos fora do campo de visão da câmera (o tronco de visão) não são visíveis e podem ser selecionados (objetos delineados em vermelho).
![TopdownSceneView](https://docs.unrealengine.com/Images/RenderingAndGraphics/VisibilityCulling/SceneView_ViewFrustumCulled.webp)

- Objetos selecionados fora do tronco de visão da câmera não são mais renderizados, deixando apenas um punhado de objetos dentro desta visão que são obstruídos por outro objeto que precisa ser verificado para visibilidade. Portanto, durante essa passagem, uma consulta será enviada à GPU para testar o estado de visibilidade de cada um desses objetos. Aqueles que são ocluídos por outro são retirados da vista (objetos delineados em azul).   
![SceneView_OccludedObjectsRemoved](https://docs.unrealengine.com/Images/RenderingAndGraphics/VisibilityCulling/SceneView_OccludedObjectsRemoved.webp)

- Todos os objetos que estão fora do tronco da vista ou que estão ocluídos são agora eliminados da vista. A vista final da cena agora corresponde aos objetos que sabemos serem visíveis na cena a partir da posição da câmera.
![Vis_FinalSceneView](https://docs.unrealengine.com/Images/RenderingAndGraphics/VisibilityCulling/Vis_FinalSceneView.webp)

<a name="3.3"></a>    
### 3.3 Precomputed Visibility
Volumes de visibilidade pré-computados armazenam o estado de visibilidade de atores não móveis em células colocadas acima de superfícies de projeção de sombras. Este método de seleção gera dados de visibilidade offline (durante uma construção de iluminação) e funciona melhor para níveis de tamanho pequeno a médio.
A visibilidade pré-computada é ideal para hardware inferior e dispositivos móveis. Para tais hardwares e dispositivos, ao considerar os custos de desempenho, você obterá o máximo negociando custos de thread de renderização que são mais caros por aqueles com memória de tempo de execução, onde há mais flexibilidade em relação ao desempenho.

> Divide a cena em um grid, cada célula do grid registra o que é visível naquele local.

1. Configurar **Precomputed Visibility Volume**.

  Place Actors->Volumes.
1. Marque a opção **Precompute Visibility** no objeto adicionado na cena.
1. Visualizando o Grid de células na cena.    

  Show - Visualize -> Precomputed Visibility Cells.
  > Se você já construiu a iluminação (**Bluid->Lighting**), pode usar o menu suspenso Construir na barra de ferramentas principal(**Show**) e selecionar **Precompute Static Visibility** para gerar células de visibilidade sem reconstruir a iluminação todas as vezes.

1. A câmera ao entrar na célula pergunta:    
  "o que pode ser ocluído?"   
  "O que pode ser renderizando e o que eu não devo renderizar?"     
  "Neste local, lembramos que esses objetos eram visíveis e estes outros não eram"

<a name="3.4"></a>
### 3.4 Occlusion Culling
O sistema de oclusão dinâmica em UE4 vem com vários métodos de abate para escolher. Cada um desses métodos rastreia os estados de visibilidade dos Atores em um nível dentro do tronco de visão da câmera (ou campo de visão) que são obstruídos por outro Ator. As consultas são emitidas para a GPU ou CPU para verificar o estado de visibilidade de cada ator. Uma heurística é usada para reduzir o número de verificações de visibilidade necessárias, por sua vez, aumentando a eficácia geral de seleção e o desempenho.
1. A seleção de oclusão verifica com precisão o estado de visibilidade em cada modelo.

1. Use o comando do console **freezerendering** que força a renderização para congelar ou retomar. Permite a visualização da cena conforme foi renderizada a partir do ponto em que o comando foi inserido.
```bash
    freezerendering
```
1. Comando do console **Stat initviews** exibe informações sobre quanto tempo levou a seleção de visibilidade e quão eficaz foi. A contagem de seções visíveis é a estatística mais importante com relação ao desempenho do thread de renderização e é dominada por Visible Static Mesh Elements em STAT INITVIEWS.
```bash
    Stat initviews
```

### Occlusion Culling é um processo pesado a partir de 10.000 objetos na cena.
Abaixo um exemplo em uma cena com 10.000 objetos
1. Distance Culling remove 3.000 restando 7.000.
1. Frustum Culling remove e renderiza 4.000.
1. Precomputed Visibility remove 1.000.
1. Occlusion Culling remove 1.000.  

A necessidade do sistema executar os passos acima e efetuar vários cálculos para cada um pode tornar o processo pesado.

**Performance**
- Configure distance Culling.
- Mais de 10-15k objetos pode ter impacto.
- Maior parte na CPU mas tem algum impacto na GPU.
- Grandes ambientes não ocluem bem,
- A mesma coisa para as partículas.
- Modelos grandes raramente irão ocluir e, assim, aumentar GPU.
- Mas combinar modelos com modelos grandes irá diminuir o custo da CPU.

**Resultado**
- (Cubo) Modelos A  Visível.
- (Cubo) Modelos B Visível.
- (Esfera) Modelos C Não Visível.
- (Cilindro) Modelos D Visível.
- (Cubo) Modelos E Não Visível.

A,B,D são processados na GPU.

<a name="4"></a>
## 4. Processamento do Frame 2 - Time 66ms - GPU
A GPU agora tem uma lista de modelos e transformações, mas se apenas renderizássemos esta informação iria causar uma grande quantidade de renderização de pixels redundantes, portanto, precisamos descobrir quais modelos serão exibidos com antecedência.

![Ray tracing skylight](imagens/ue4_gemeotry_hendering.jpg)
*Figura. 3 Objetos na cena.*

- Considerando a renderização de cada pixel na cena na imagem acima não poderia renderizar os pixels que estão detrás dos cilindros e os que estão ocultos por outros objetos.

- Menu Project Settings->Rendering->Early Z-Pass

<a name="4.1"></a>
### 4.1 Drawcalls
A GPU agora começa a renderizar, sendo feito objeto por objeto (DrawCall).      
Um grupo de poligonos compartilha a mesmas propriedades em um Drawcall, abaixo um exemplo de como é feita a renderização.

![ue4_gemeotry_hendering_drawcall_2](imagens/ue4_gemeotry_hendering_drawcall_2.jpg)
A imagem acima renderiza 5 vezes.
1. Chão.
1. Objetos 1, 2 e 3.
1. Céu.

![ue4_gemeotry_hendering_drawcall](imagens/ue4_gemeotry_hendering_drawcall.jpg)
A imagem acima renderiza 6 vezes.
1. Chão.
1. Objetos 1, 2 e parte do objeto 3.
1. Parte do Objeto 3.
1. Céu.

![ue4_gemeotry_hendering_drawcall_3](imagens/ue4_gemeotry_hendering_drawcall_3.jpg)
Acima o passo a passo.
A ordem de renderização depende da importância dos objetos na cena.
O chão é renderizado primeiro e depois os cilindos é porque classifica a cena por tipo de material, isso é mais rápido do contrário, tem que fazer uma mudança de estado de renderização no hardware.
A ordem de renderização não tem impacto no processamento.


<a name="4.2"></a>
### 4.2 O comando Stat RHI
RHI significa Rendering Hardware Interface. Este comando exibe várias estatísticas exclusivas:

![ue4_gemeotry_hendering_drawcall_3](imagens/ue4_stat_rhi.jpg)

- **Renderiza a memória de destino** -  Mostra o peso total de alvos de renderização como o GBuffer (que armazena as informações finais sobre iluminação e materiais) ou mapas de sombras. O tamanho dos buffers depende da resolução de renderização do jogo, enquanto as sombras são controladas pelas configurações de qualidade das sombras. É útil verificar esse valor periodicamente em sistemas com várias quantidades de RAM de vídeo e, em seguida, ajustar as predefinições de qualidade do seu projeto de acordo.
- **Triângulos desenhados** - Este é o número final de triângulos. É após o abate de frustum e oclusão. Pode parecer muito grande em comparação com o polycount de suas malhas. É porque o número real inclui sombras (que "copiam" malhas para desenhar mapas de sombras) e mosaico. No editor, também é afetado pela seleção.
- **Chamadas DrawPrimitive** -  As chamadas *Draw* podem ser um sério gargalo nos programas DirectX 11 e OpenGL4. São os comandos emitidos pela CPU para a GPU e, infelizmente, devem ser traduzidos pelo driver. Esta linha em **stat RHI** mostra a quantidade de chamadas de *draw* emitidas no quadro atual (excluindo apenas a IU do Slate). Este é o valor total, portanto, além da geometria (normalmente o maior número), também inclui decalques, sombras, volumes de iluminação translúcida, pós-processamento e muito mais.

#### Comando do console
```bash
stat RHI
```

<a name="4.3"></a>
### 4.3 O comando Stat unit e Stat FPS
**Stat fps** nos mostra o número final de *fps* e o tempo que levou para renderizar o último quadro. É o tempo total. Mas ainda não sabemos se o custo foi causado pela CPU ou pela GPU. Como explicado antes, um tem que esperar o outro. A renderização rápida na placa de vídeo não ajudará, se a CPU precisar de mais tempo para terminar o trabalho de jogabilidade, desenho (gerenciando a GPU) ou física.

![ue4_gemeotry_hendering_drawcall_3](imagens/ue4_stat_unit.jpg)

Podemos obter informações mais específicas usando o comando stat unit. A hora do último quadro é mostrada como 4 números.
- **Frame** - é igual ao FPS, o custo final.
- **Game** - é o trabalho da CPU no código do jogo.
- **Draw** -  é o trabalho da CPU na preparação de dados para a placa gráfica.
- **GPU** - é o tempo bruto necessário para renderizar um quadro na placa de vídeo.

#### Comandos do console
```bash
stat fps
stat unit
```

<a name="4.4"></a>
### 4.4 Considerações
- 2000 - 3.000 é razoável.
- Mais de 5.000 esta ficando alto.
- Mais de 10.000 é provavelmente um problema.
- Em dispositivos moveis esse valor é muito menor.
- Para verificar experimente executar o comando **stat RHI** e alterar o **View Mode** de **Lit** para **Unlit** e verifique os valores **Triângulos desenhados**.
- DrawCalls tem um impacto grande na performance.
- DrawCalls tem um mais impacto que a quantidade de polígonos em muitos cenários, exemplo:
  Se temos um polígono com 32 triângulos e 34 tipos de materiais diferentes aplicados na sua superfície, terá mais impacto no FPS do que um polígono de 10.000 triângulos e 1 material.
  Cada triângulo com uma superfície diferentes é renderizado por vez.

***
## Referências
- [An In-Depth Look at Real-Time Rendering](https://www.unrealengine.com/en-US/onlinelearning-courses/an-in-depth-look-at-real-time-rendering)
- [Visibility and Occlusion Culling](https://docs.unrealengine.com/en-US/RenderingAndGraphics/VisibilityCulling/index.html)
- [Cull Distance Volume](https://docs.unrealengine.com/en-US/RenderingAndGraphics/VisibilityCulling/CullDistanceVolume/index.html)
- [WTF Is? Volume - Cull Distance in Unreal Engine 4](https://www.youtube.com/watch?v=g0ML7oJll3w)
- [Process Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer)
- [Unreal’s Rendering Passes](https://unrealartoptimization.github.io/book/profiling/passes/)
- [Measuring Performance](https://unrealartoptimization.github.io/book/process/measuring-performance/)
