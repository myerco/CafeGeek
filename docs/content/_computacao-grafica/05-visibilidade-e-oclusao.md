---
title: Visibilidade e Oclusão
permalink: /computacao-grafica/visibilidade-e-oclusao
excerpt: Neste capitulo apresentaremos o processo de visualização e oclusão de objetos.
date: 2024-03-01T08:48:05-04:00
show_date: true
last_modified_at: 2023-03-27T08:48:05-04:00
layout: single
order: 105
read_time: true
toc: true    
sidebar:
    nav: dev_computacao
---

{% include figure image_path="/assets/images/jogos-digitais/brecht-corbeel-g7JkVRANxX0-unsplash.webp" alt="Brecht Corbeel" caption="" %}

## 1. Distance Culling ou corte de distância

Este método de seleção é ideal para grandes níveis externos, onde você teria edifícios ou estruturas de algum tipo com interiores detalhados, onde você gostaria de selecionar aqueles objetos que são pequenos demais para considerar importantes a distâncias distantes.
{: .text-justify}

### 1.1. Atores na cena

Atores selecionados em um Nível ou **Blueprint** contêm configurações de distância acessadas por meio de seu painel Detalhes. Eles permitem que distâncias por instância sejam definidas ou se o Ator é selecionado usando um `Cull Distance Volume`.
{: .text-justify}

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/VisibilityCulling/PerActorDistanceCullingSettings.webp"
    alt="Figura: Selecionamos a Static Mesh do objeto para ter acesso a configuração de Renderização."
    caption="Static Mesh > Details > Rendering."
    ref="https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/VisibilityCulling/"
%}

`Min Draw Distance` - Define a distância mínima de desenho na qual o objeto será renderizado na cena. Isso é medido em unidades de espaço mundial (centímetros) do centro da esfera delimitadora do objeto até a posição da câmera.
{: .text-justify}

`Desired Max Draw Distance` - Define a distância máxima de projeção para o _Level Designer_. A distância máxima "real" é a distância mínima de tração (desconsiderando 0).
{: .text-justify}

_Exemplo_ : Valores para os atores na cena.

```cpp
Min Draw Distance = 0
Desired Max Draw Distance = 1000
```

**Nota:** O objeto vai ser renderizado quando a câmera se aproximar a uma distância **MENOR** que 1000 centímetros.
{: .notice--warning}

### 1.2. Cull Distance Volume

`Cull Distance Volumes` permitem que você especifique uma variedade de tamanhos e distâncias de seleção para que os Atores não devam mais ser desenhados.
{: .text-justify}

Adicionamos o volume `Cull Distance Volume` localizado em `Place Actors/Volumes` e alteramos as dimensões do objeto para definir a área de corte.
{: .text-justify}

{% include imagelocal.html
    src="computacao-grafica/ue4_cullDistanceVolume_size.jpg"
    alt="Figura: CullDistanceVolume Size."
    caption="Corte de volume."
%}

{% include imagelocal.html
    src="computacao-grafica/ue4_cullDistanceVolume_Array_distances.jpg"
    alt="Figura: CullDistanceVolume Cull Distance Array."
    caption="Configure a matriz de distância e tamanho, Cull Distances para o corte."
%}

**Cull Distances** - Uma lista de conjuntos de pares de Tamanho e Distância de Seleção usada para definir a distância de desenho de objetos com base em seu tamanho dentro de um `Cull Distance Volumes`. O código calculará o diâmetro da esfera da caixa delimitadora de um objeto e procurará o melhor ajuste nesta matriz para determinar qual distância de separação deve ser atribuída a um objeto.

- `Size` - O tamanho a ser associado à distância de eliminação.

- `Cull Distance` - A distância a ser associada ao tamanho dos limites de um ator.

_Exemplo_ : Valores dos cortes de distância.

```cpp
// 0 - Os objetos de tamanho 300 centímetros não sofreram corte.
  Size = 300
  Cull Distance = 0
// 1 - Objetos de tamanho 200 centímetros serão cortados a partir de 1200 centímetros de distância.
  Size = 200
  Cull Distance = 1200
// 2 - Objetos de tamanho 100 centímetros serão cortados a partir de 1500 centímetros de distância.
  Size = 100
  Cull Distance = 1500  
```

## 2. Frustum Culling ou corte de câmera

A seleção de **View Frustum** usa a área visível da tela do campo de visão (FOV) da câmera para selecionar objetos fora deste espaço.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/VisibilityCulling/ViewFrustumDiagram.webp"
    alt="Figura: View Frustum."
    caption="O tronco da visão é uma forma piramidal que inclui um plano de recorte próximo e distante que define o mais próximo e o mais distante que qualquer objeto deve ser visível dentro deste espaço. Todos os outros objetos são removidos para economizar tempo de processamento."
%}

**1.** O plano de recorte próximo é o ponto mais próximo da câmera em que os objetos ficarão visíveis;

**2.** A **Camera Frustum** é a representação em formato piramidal da área de visualização visível entre os planos de clipe próximo e distante;

**3.** O plano de recorte distante é o ponto mais distante da câmera em que os objetos serão visíveis.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/VisibilityCulling/SceneViewBase.webp"
    alt="Figura: View Frustum Culled."
    caption=" Os objetos fora do campo de visão da câmera (o tronco de visão) não são visíveis e podem ser selecionados (objetos delineados em vermelho)."
%}

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/VisibilityCulling/SceneViewWithOnlyOccludedObjects.webp"
    alt="Figura: Occlued Objects Remover."
    caption="Objetos selecionados fora do tronco de visão da câmera não são mais renderizados, deixando apenas um punhado de objetos dentro desta visão que são obstruídos por outro objeto que precisam ser verificados para visibilidade. Portanto, durante essa passagem, uma consulta será enviada à GPU para testar o estado de visibilidade de cada um desses objetos. Aqueles que são ocluídos por outro são retirados da vista (objetos delineados em azul)."
%}

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/VisibilityCulling/Vis_FinalSceneView.webp"
    alt="Figura: View Occlued Scene View."
    caption="Todos os objetos que estão fora do tronco da vista ou que estão ocluídos são agora eliminados da vista. A vista final da cena agora corresponde aos objetos que sabemos serem visíveis na cena a partir da posição da câmera.
."
%}

Configurando o Unreal Engine para visualizar o corte de câmera.

{% include imagelocal.html
    src="computacao-grafica/ue4_camera_frustum.jpg"
    alt="Figura: Camera Frustum."
    caption="Show > Advanced > Camera frustum."
%}

## 3. Precomputed Visibility - Visibilidade pré-computada

Armazenam o estado de visibilidade de atores não móveis (**Static**) em células colocadas acima de superfícies de projeção de sombras. Este método de seleção gera dados de visibilidade _offline_ (durante uma construção de iluminação) e funciona melhor para níveis de tamanho pequeno a médio.

A **Precomputed Visibility** é ideal para hardware inferior e dispositivos móveis. Para tais hardwares e dispositivos, ao considerar os custos de desempenho, você obterá o máximo negociando custos de Thread de renderização que são mais caros por aqueles com memória de tempo de execução, onde há mais flexibilidade em relação ao desempenho.

**Informação:** Divide a cena em um grid, onde cada célula do grid registra o que é visível naquele local. O tamanho das células é configurado no arquivo .ini do projeto.
{: .notice--info}

{% include image.html
    src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/VisibilityCulling/PrecomputedVisibilityVolume/WS_EnablePVIS.webp"
    alt="Figura: World Settings > Precompute Visibility."
    caption="Configurando em World Settings o atributo Precomputed Visibility para verdadeiro."
%}

{% include image.html
    src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/VisibilityCulling/PrecomputedVisibilityVolume/PVIS_AddVolume.webp"
    alt="Figura: World Settings > Precompute Visibility."
    caption="Adicionando na cena o volume Precomputed Visibility Volume que está em Place Actors > Volumes."
%}

É necessário definir o tamanho do volume para abranger a área analisada.

{% include imagelocal.html
    src="computacao-grafica/ue4_precomputed_visibility_volume.jpg"
    alt="Figura: Precomputed Visibility Cells, em azul as células."
    caption="Para visualizar o Grid de células na cena, Show > Visualize > Precomputed Visibility Cells."
%}

**Nota:** Se você já construiu a iluminação (`Build` > `Lighting`), pode usar o menu suspenso `Build` na barra de ferramentas principal e selecionar `Precompute Static Visibility` para gerar células de visibilidade sem reconstruir a iluminação todas as vezes.
{: .notice--warning}

A câmera ao entrar na célula pergunta:

- O que pode ser ocluído?;
- O que pode ser renderizando e o que eu não devo renderizar?;
- Neste local, lembramos que esses objetos eram visíveis e estes outros não eram.

## 4. Occlusion Culling

O sistema de oclusão dinâmica no Unreal Engine vem com vários métodos de abate para escolher. Cada um desses métodos rastreia os estados de visibilidade dos Atores em um nível dentro do tronco de visão da câmera (ou campo de visão) que são obstruídos por outro Ator. As consultas são emitidas para a GPU ou CPU para verificar o estado de visibilidade de cada ator. Uma heurística é usada para reduzir o número de verificações de visibilidade necessárias, por sua vez, aumentando a eficácia geral de seleção e o desempenho.
{: .text-justify}

**1.** A seleção de oclusão verifica com precisão o estado de visibilidade em cada modelo;

**2.** Use o comando do console `freezerendering` que congela ou retomar a renderização. Permite a visualização da cena conforme foi renderizada a partir do ponto em que o comando foi inserido;

```bash
    freezerendering
```

**3.** Comando do console `Stat initviews` exibe informações sobre quanto tempo levou a seleção de visibilidade e quão eficaz foi. A contagem de seções visíveis, é a estatística mais importante com relação ao desempenho do Thread de renderização e é dominada por `Visible Static Mesh Elements`, `Visible Dynamic Primitives` também influenciam.

**Dynamic Primitives :** Um componente de contém ou gera algum tipo de geometria, geralmente pode ser renderizado ou usado para dados de colisão. [UPrimitiveComponent](https://medium.com/realities-io/creating-a-custom-mesh-component-in-ue4-part-3-the-mesh-components-scene-proxy-6965a3ea4cc9)
{: .notice--info}

```bash
    Stat initviews
```

_Exemplo_: Occlusion Culling

{% include imagelocal.html
    src="computacao-grafica/ue4_freezerendering_before.jpg"
    alt="Figura: Freezerendering before."
    caption="Marque a posição da camera com o comando Ctrl + 1."
%}

{% include imagelocal.html
    src="computacao-grafica/ue4_stat_initviews_complete_scene.jpg"
    alt="Figura: Stat initviews."
    caption="Com comando Stat initviews apresente as estatistas."
%}

{% include imagelocal.html
    src="computacao-grafica/ue4_camera_actor.jpg"
    alt="Figura: Perspective > Camera Actor."
    caption="Alterne para a visualização e controle de câmera."
%}

Perceba que a média de objetos cortados na cena aumentou (`Frustum Culled Primitives`) e os objetos visíveis diminuiu (`Visible static mesh elements`).

{% include imagelocal.html
    src="computacao-grafica/ue4_stat_initviews_complete_scene_camera.jpg"
    alt="Figura: Stat initviews."
    caption="Complete scene camera."
%}

Com o comando `freezerendering` congele a renderização.

Após congelar a cena, ejete a câmera para poder navegar pela cena e aperte a tecla **1**, que foi utilizada para marcar a posição da câmera antes.

{% include imagelocal.html
    src="computacao-grafica/ue4_freezerendering_after.jpg"
    alt="Figura: Stat initviews after."
    caption="Rendering frozen."
%}

Como resultado temos dois objetos sendo renderizados, pois se um pixel de um objeto estiver presente na cena, o caso do objeto mais longe da câmera, todo o objeto é renderizado.
  
**Informação:** Se os objetos grandes fossem divididos em vários pedaços isso poderia diminuir o processo de renderização pois não teríamos que renderizar objetos gigantes que não aparecem totalmente na cena, mas sobrecarregaria a verificação de cada objeto visível na cena, então devemos balancear entre os dois métodos.
{: .notice--warning}

Occlusion Culling é um processo pesado a partir de 10.000 objetos na cena, abaixo um exemplo em uma cena com 10.000 objetos:

`Distance Culling` remove 3.000 restando 7.000;

`Frustum Culling` remove e renderiza 4.000;

`Precomputed Visibility` remove 1.000;

`Occlusion Culling` remove 1.000.  

A necessidade do sistema executar os passos acima e efetuar vários cálculos para cada um pode tornar o processo pesado.

### 4.1. Implicações de desempenho de oclusão

- Configurando `Distance Culling` os objetos não vão ser renderizados na cena mas o calculo de oclusão ainda é realizado;
- Mais de 10-15k objetos podem ter grande impacto;
- Maior parte nos processos que usam muita CPU, mas tem algum impacto na GPU;
- Grandes ambientes não ocluem bem, pois a cena apresenta qualquer coisa e não podemos esconder os objetos, se você pode ver qualquer coisa não podemos ocluir algo;
- A mesma coisa para as partículas, pois as partículas usam `Bounding Box` e esse elemento é alterado várias vezes por segundo, se o elemento é visível ele vai ser renderizado;
- Modelos grandes raramente irão ocluir e, assim, aumentar GPU;
- Combinar modelos com modelos grandes irá diminuir o custo da CPU.
  
  _Exemplo:_

  Se um pedaço pequeno de um objeto grande está visível, TODO o objeto será renderizado, o que aumenta o processamento, mas se esse pedaço for somente uma parte de um conjunto de objetos agrupados, somente esse pedaço será renderizado.

**Informação:** Os objetos grandes que estão atrás de objetos são renderizados por inteiro.
{: .notice--warning}

_Exemplo_: Abaixo temos uma lista de modelos para renderizar:

- (Cubo) Modelos A  Visível;
- (Cubo) Modelos B Visível;
- (Esfera) Modelos C Não Visível;
- (Cilindro) Modelos D Visível;
- (Cubo) Modelos E Não Visível.

O resultado é que somente os modelos A,B,D são processados na GPU.

### 4.2. Drawcalls

A GPU agora começa a renderizar, sendo feito objeto por objeto (DrawCall).

Um grupo de polígonos compartilha as mesmas propriedades em um `Drawcall`, abaixo um exemplo de como é feita a renderização.

{% include imagelocal.html
    src="computacao-grafica/ue4_gemeotry_hendering_drawcall_2.jpg"
    alt="Figura: 3 Objetos na cena."
    caption="A imagem acima renderiza 5 vezes."
%}

1. Chão;
1. Objetos 1, 2 e 3;
1. Céu.

{% include imagelocal.html
    src="computacao-grafica/ue4_gemeotry_hendering_drawcall.jpg"
    alt="Figura: 3 Objetos na cena."
    caption="A imagem acima renderiza 6 vezes."
%}

1. Chão;
2. Objetos 1, 2 e parte do objeto 3;
3. Parte do Objeto 3;
4. Céu.

{% include imagelocal.html
    src="computacao-grafica/ue4_gemeotry_hendering_drawcall_3.jpg"
    alt="Figura: Gemeotry Hendering Drawcall."
    caption="Acima o passo a passo, a ordem de renderização depende da importância dos objetos na cena."
%}

O chão é renderizado primeiro e depois os cilindos, isto se deve porque a cena é classificada por tipo de material, isso é mais rápido do contrário, pois tem que fazer uma mudança de estado de renderização no hardware.

**Nota:** A ordem de renderização não tem impacto no processamento.
{: .notice--warning}

### 4.3. Comando Stat RHI

RHI significa Rendering Hardware Interface. Este comando exibe várias estatísticas exclusivas:

{% include imagelocal.html
    src="computacao-grafica/ue4_stat_rhi.jpg"
    alt="Figura: Stat RHI."
    caption="No Viewport aparece o relatório com as estatísticas."
%}

`Render target memory` -  Mostra o peso total de alvos de renderização como o GBuffer (que armazena as informações finais sobre iluminação e materiais) ou mapas de sombras. O tamanho dos buffers depende da resolução de renderização do jogo, enquanto as sombras são controladas pelas configurações de qualidade das sombras. É útil verificar esse valor periodicamente em sistemas com várias quantidades de RAM de vídeo e, em seguida, ajustar as predefinições de qualidade do seu projeto de acordo.
{: .text-justify}

`Triangles drawn` - Este é o número final de triângulos. É após o abate de _frustum_ e oclusão. Pode parecer muito grande em comparação com o _polycount_ de suas malhas. É porque o número real inclui sombras (que "copiam" malhas para desenhar mapas de sombras) e mosaico. No editor, também é afetado pela seleção.
{: .text-justify}

`DrawPrimitive calls` -  As chamadas _Draw_ podem ser um sério gargalo nos programas DirectX 11 e OpenGL4. São os comandos emitidos pela CPU para a GPU e, infelizmente, devem ser traduzidos pelo driver. Esta linha em **stat RHI** mostra a quantidade de chamadas de _draw_ emitidas no quadro atual (excluindo apenas a IU do Slate - Interface do Editor). Este é o valor total, portanto, além da geometria (normalmente o maior número), também inclui decalques, sombras, volumes de iluminação translúcida, pós-processamento e muito mais.
{: .text-justify}

Comando do console:

```bash
stat RHI
```

### 4.4. O comando Stat unit e Stat FPS

**Stat fps** nos mostra o número final de _fps_ e o tempo que levou para renderizar o último quadro. É o tempo total. Mas ainda não sabemos se o custo foi causado pela CPU ou pela GPU. Como explicado antes, um tem que esperar o outro. A renderização rápida na placa de vídeo não ajudará, se a CPU precisar de mais tempo para terminar o trabalho de jogabilidade, desenho (gerenciando a GPU) ou física.

{% include imagelocal.html
    src="computacao-grafica/ue4_stat_unit.jpg"
    alt="Figura: Stat Unit."
    caption="Podemos obter informações mais específicas usando o comando stat unit. A hora do último quadro é mostrada com 4 números."
%}

**Frame** - é igual ao FPS, o custo final;

**Game** - é o trabalho da CPU no código do jogo;

**Draw** -  é o trabalho da CPU na preparação de dados para a placa gráfica;

**GPU** - é o tempo bruto necessário para renderizar um quadro na placa de vídeo.

Comandos do console FPS:

```bash
stat fps
stat unit
```

## 5. Considerações

**1.** 2000 - 3.000 é razoável;

**2.**Mais de 5.000 esta ficando alto;

**3.** Mais de 10.000 é provavelmente um problema;

**4.** Em dispositivos moveis esse valor é muito menor;

**5.** Para verificar experimente executar o comando **stat RHI** e alterar o **View Mode** de **Lit** para **Unlit** e verifique os valores **Triângulos desenhados**;

**6.** **DrawCalls** tem um impacto grande na performance;

**7.** **DrawCalls** tem um mais impacto que a quantidade de polígonos em muitos cenários.

_Exemplo_: Se temos um polígono com 32 triângulos e 34 tipos de materiais diferentes aplicados na sua superfície, terá mais impacto no FPS do que um polígono de 10.000 triângulos e 1 material. Cada triângulo com uma superfície diferentes é renderizado por vez.
