---
title: Processamento de imagens
permalink: /pages/computacao_grafica/processamento
excerpt: Neste curso apresentaremos o processo de renderização de objetos 3D e como o Unreal Engine processa as imagens.
last_modified_at: 2023-03-27T08:48:05-04:00
toc: true    
---

## 1. Entendendo o processo de renderização

Neste capitulo serão apresentados quais são os passos para processamento de imagens no computador.

### 1.1. Entendendo como os processos são executados pelo sistema operacional

Em computação, um processo é uma instância de um programa de computador que está sendo executado. Ele contem o código do programa e sua atividade atual. Dependendo do sistema operacional, um processo pode ser feito de várias linhas de execução que executam instruções concorrentemente. O sistema operacional seleciona um processo da fila de aptos para receber o processador. O processo selecionado passa do estado de apto para o estado executando. O módulo do sistema operacional que faz essa seleção é chamado de escalonador.

{% include imagelocal.html
    src="computacao_grafica/ue4_cpu_processos.jpg"
    alt="Figura: Fila de Processos. "
    caption="Fluxo de execução de processos."
%}

- **Criado** - Enquanto o processo está sendo criado, esse é seu estado;
- **Apto** -Esse é como um estado de ponto de partida, aqui ficam os processos que estão prontos para serem processados;
- **Espera** - Esse é um estado especial que na verdade está mais para uma característica de outros estados, basta observar os processos que estão nos estado de prontidão e os que estão aguardando eventos, pois ambos também estão em um estado de espera;
- **Execução** - Quando o processo está sendo executado, seu estado passa a ser este;
- **Encerrado** -Esse é o último estado  de um processo, sua finalização, seja de forma voluntária, como quando ele não é mais necessário ou de forma involuntária, como as ocasionadas por um erro;
- **RPC** - Remote Procedure Call (Chamada de Procedimento Remoto) é uma tecnologia para a criação de programas distribuídos servidor/cliente que provê um paradigma de comunicação de alto nível no sistema operacional, á presumindo a existência de um protocolo de transporte, como TCP/IP ou UDP, para carregar a mensagem entre os programas comunicantes;
- **Threads** - Thread é um pequeno programa que trabalha como um subsistema, sendo uma forma de um processo se auto dividir em duas ou mais tarefas. É o termo em inglês para Linha ou Encadeamento de Execução. Essas tarefas múltiplas podem ser executadas simultaneamente para rodar mais rápido do que um programa em um único bloco ou praticamente juntas, mas que são tão rápidas que parecem estar trabalhando em conjunto ao mesmo tempo.

### 1.2. O processo de renderização pela GPU

A renderização GPU torna possível usar sua placa de vídeo para renderização, ao invés da CPU. Isso pode acelerar a renderização, porquê as GPUs modernas são desenhadas para fazer muito processamento de números. Por outro lado, elas também têm algumas limitações na renderização de cenas complexas devido à memória mais limitada, e questões com interatividade quando usando a mesma placa de vídeo para visualização e renderização.

A renderização ocorre mediante o envio de comandos para a GPU, que gera a tela de forma assíncrona. Em algumas situações, a GPU pode ter muito trabalho para fazer, e a CPU terá de aguardar antes de enviar novos comandos.

{% include imagelocal.html
    src="computacao_grafica/ue4_gpu_pipeline.jpg"
    alt="Figura: Pipeline de computação de gráfica."
    caption="Fluxo de trabalho do processo de renderização."
%}

### 1.3. Aplicação

Etapa de toda a lógica da mecânica dos elementos que são apresentados.

- **Animations** - Calcula quando as Animações iniciam e terminam;
- **System Coordinates** - Calcula a posição dos objetos e sua influência;
- **Artificial intelligence** - Inteligência Artificial determina como o objeto se movimenta e qual o seu estado;
- **Spawn and Hide objects** - Criar e destruir objetos é a lógica necessária para determinar onde os objetos aparecem no mundo.

### 1.4. Geometria

A etapa de geometria (com pipeline de geometria), é responsável pela maioria das operações com polígonos e seus vértices (com pipeline de vértices), pode ser dividida nas tarefas a seguir. Depende da implementação específica de como essas tarefas são organizadas em pipeline paralelo.

- **Model 3D** - Modelo 3D é o processo onde os objetos são desenhados na cena, entre eles vértices, triângulos e o sistema de coordenadas;
  
- **Distance Culling** - Ou Corte de Distância Remove objetos que estão além de um valor X da câmera;
  
- **Frustim Culling** - Ou Corte de Câmera remove objetos que não estão a frente da câmera;
  
- **Occlusion Culling** - Ou Corte de oclusão é o processo que desativa a renderização de objetos quando eles não são vistos pela câmera porque estão obscurecidos (obstruídos) por outros objetos. Isso não acontece automaticamente na computação gráfica 3D, pois na maioria das vezes os objetos mais distantes da câmera são desenhados primeiro e os objetos mais próximos são desenhados por cima deles (isso é chamado de “overdraw”).

### 1.5. Renderização

#### 1.5.1. DrawCalls

Grupo de polígonos que compartilham a mesmo material. Os desenhos de chamadas, em uma tradução pé da letra, basicamente são quantos objetos estão sendo desenhados na tela. Você deseja manter esse número baixo para manter um bom desempenho, portanto, nas luzes dos pixels, fazem os objetos serem desenhados tantas vezes quanto as luzes que os afetam.
  
{% include image.html
    src="https://unreal.tips/wp-content/uploads/2019/05/Drawcalls.jpg"
    alt="Figura: Drawcalls."
    caption="Unreal Tips."
%}  

#### 1.5.2. Vertex Shaders

É uma função de processamento gráfico usada para adicionar efeitos especiais a objetos em um ambiente 3D executando operações matemáticas nos dados de vértice dos objetos. Cada vértice pode ser definido por muitas variáveis diferentes. Por exemplo, um vértice é sempre definido por sua localização em um ambiente 3D usando as coordenadas x-, y- e z-. Os vértices também podem ser definidos por cores, texturas e características de iluminação. Os Vertex Shaders não alteram realmente o tipo de dados; eles simplesmente mudam os valores dos dados, de modo que um vértice emerge com uma cor diferente, texturas diferentes ou uma posição diferente no espaço.

{% include image.html
    src="https://upload.wikimedia.org/wikipedia/commons/8/84/Phong-shading-sample.jpg"
    alt="Figura: Flat-shading e Phong-shading."
    caption="São tipos de sombreadores 3D e são executados uma vez para cada vértice fornecido ao processador gráfico."
    ref="https://en.wikipedia.org/wiki/Shader"
%}  

#### 1.5.3. Pixel Shader

Os Pixel Shader, calculam a cor e outros atributos de cada "fragmento",uma unidade de trabalho de renderização que afeta no máximo um único pixel de saída. Os sombreadores de pixel variam desde simplesmente sempre a saída da mesma cor, até a aplicação de um valor de iluminação, até o mapeamento de saliências, sombras, realces especulares, translucidez e outros fenômenos. Eles podem alterar a profundidade do fragmento (para buffer Z) ou produzir mais de uma cor se vários destinos de renderização estiverem ativos.

{% include image.html
    src="https://upload.wikimedia.org/wikipedia/commons/0/0f/Shading_models.png"
    alt="Figura: Shading models."
    caption="Os tipos mais simples de sombreadores de pixel geram um pixel da tela como um valor de cor; sombreadores mais complexos com várias entradas / saídas também são possíveis."
%}

#### 1.5.4. Geometry Shaders

Recebe como entrada um conjunto de vértices que formam uma única primitiva, por exemplo, um ponto ou triângulo. O sombreador de geometria pode então transformar esses vértices conforme achar necessário antes de enviá-los para o próximo estágio de sombreador. O que torna o shader de geometria interessante é que ele é capaz de converter a primitiva original (conjunto de vértices) em primitivas completamente diferentes, possivelmente gerando mais vértices do que os inicialmente dados.

{% include imagelocal.html
    src="computacao_grafica/The-graphics-pipeline-in-OpenGL-consists-of-these-5-steps-in-the-new-generation-of-cards.jpg"
    alt="Figura: Pipeline OpenGL."
    caption="É uma sequência de etapas que o OpenGL executa ao renderizar objetos. Esta visão geral fornecerá uma descrição de alto nível das etapas do pipeline."
%}

#### 1.5.5. Fragment Shader

É uma unidade programável da GPU que opera em cada fragmento produzido durante a rasterização e seus dados associados.
  
#### 1.5.6. Rasterization

 O termo rasterização, em geral, pode ser aplicado a qualquer processo pelo qual informações tipo vetorial podem ser convertidas num formato de pontos ou pixels.
  
_Exemplo_: Um exemplo seria uma reta descrita matematicamente é infinitesimalmente contínua, não importa o quão pequeno um trecho da reta é observado, é impossível determinar qual é o próximo ponto depois de um determinado ponto; não existem quebras.

{% include imagelocal.html
    src="computacao_grafica/rasterização.webp"
    alt="Figura: Rasterização."
    caption="Conversão da representação de uma reta na forma vetorial para a matricial. Em B, é incluído um tratamento de anti-aliasing.."
    ref="https://portaleletronica.com.br/images/Imagens/Comp_Graf/Parte_3_Rasterizao.pdf"
%}

### 1.6. Conclusão

**Nota:** Componentes = `DrawCalls`
{: .notice--warning}

**1.** O custo para renderizar muitos polígonos é muitas vezes menor que o Drawcall;

**2.** 50.000 triângulos podem rodar pior que 50 milhões dependendo da implementação;

**3.** `Drawcall` tem uma despesa básica, portanto, otimizar poli de baixo para super poli pode fazer nenhuma diferença;  

**4.** Componentes ocluem e são renderizados um por um;

**5.** Mesclar em um único ator geralmente não faz diferença para a renderização;

**6.** Para diminuir o `Drawcalls` é melhor usar menos modelos maiores do que muitos modelos pequenos, você não pode fazer muito isso, no entanto, isso afeta todo o resto negativamente;

- Pior para oclusão - A oclusão é mais rápida por si só, mas não será capaz de fazer um trabalho bom o suficiente, tem menos objetos que precisam ser verificados quanto à oclusão, mas tem uma chance menor de realmente ocluir alguma coisa;
- Pior para o lightmapping - `Lightmap` tem uma quantidade limite de espaço, a quantidade máxima de espaço é a textura do mapa de luz, independentemente da resolução, o mapa de luz também tem um limite de resolução superior;

    _Exemplo_: Imagens de 4k, 4.096 já são enormes para um `Lightmap`.

- Se você fizer modelos muito grandes, eventualmente eles simplesmente ficarão sem espaço UV.
  - Pior para calculo de colisão.
  - Pior para memoria.

***

## 2. Processamento de imagens com Unreal Engine

Neste capitulo vamos analisar como é realizado o processamento de imagens pela CPU e GPU pelo Unreal Engine.

### 2.1. O processo de renderização no Unreal Engine

Para exemplificar o processo de renderização vamos apresentar os seguintes passos conforme as _thread_ são executas:

| Threads      |                                         |                                         |                                           |                                           |
| :----------- | :-------------------------------------- | :-------------------------------------- | :---------------------------------------- | :---------------------------------------- |
| **CPU**      | <span style="color:blue">Frame A</span> | <span style="color:red">Frame B</span>  | <span style="color:green">Frame C </span> | <span style="color:brown">Frame D</span>  |
| **DRAW CPU** |                                         | <span style="color:blue">Frame A</span> | <span style="color:red">Frame B</span>    | <span style="color:green">Frame C </span> |
| **GPU**      |                                         |                                         | <span style="color:blue">Frame A</span>   | <span style="color:red"> Frame B</span>   |
| **Time**     | **0**                                   | **33**                                  | **66**                                    |                                           |

Acompanhe a ordem de execução de cada Frame.

1. O <span style="color:blue">Frame A</span> é instanciado na CPU;
1. Logo em seguida o <span style="color:blue">Frame A</span> é passado para um momento onde a CPU e a GPU compartilham alguns elementos de construção. Enquanto isso ocorre a CPU carrega o <span style="color:red">Frame B</span>;
1. Após passar pelo passo de compartilhamento o <span style="color:blue">Frame A</span> então é colocado inteiramente na GPU;
1. A operação se repete para todos os Frames;
1. Perceba que a cada passo que se completa são liberados recursos de CPU e GPU para serem usados com outros frames;

**Informação:** A seguir vamos abordar cada passo.
{: .notice--info}

### 2.2. Processamento do Frame 0 - Time 0 - CPU

Neste passo é realizado o calculo é realizado na CPU de toda a lógica e as transformações:

**Nota:** Qualquer coisa relativa a mudança e posição dos objetos.
{: .notice--warning}

1. **Animações** - Calcula quando as Animações iniciam e terminam;
1. **Posição de modelos e objetos** - Necessário para calcular a posição e sua influência;
1. **Física** - Calculo para determinar onde os objetos vão;
1. **Inteligência Artificial** - Por exemplo, em um veículo controlado por IA é necessário determinar, como ele se movimenta,  como o estado e onde o carro estará realmente;
1. **Cria e destrói, esconde e apresenta** - Necessário para determinar onde os objetos aparecem no mundo.

**Nota:** O Unreal Engine conhece todas as transformações e todos os objetos.
{: .notice--warning}

### 2.3. Processamento do Frame 1 - Time 33ms - Preparar a Thread

Antes de podermos usar as transformações para renderizar a imagem, precisamos saber o que incluir na renderização, isso é executado principalmente na CPU, mas algumas partes são manipuladas pela GPU, para tal finalidade é realizada a tarefa de :

- Processo de oclusão - Construção de lista de todos os objetos e modelos visíveis, sendo que o processamento é realizado por objeto e não por polígono;
- Preparação da Thread - Uma Thread da GPU é alocada.

A seguir as 4 Etapas em ordem de execução desse processo.

1. `Distance Culling` - Remove quaisquer objetos além de X da câmera;
1. `Frustim Culling` - Verifica o que está na frente da câmera;
1. `Precomputed Visibility` - (Visibilidade pré-computada) Divide a cena em uma grade, cada célula da grade lembra o que está visível naquele local;
1. `Occlusion Culling` - Verifica com precisão o estado de visibilidade em cada modelo.

### 2.4. Distance Culling ou corte de distância

Este método de seleção é ideal para grandes níveis externos, onde você teria edifícios ou estruturas de algum tipo com interiores detalhados, onde você gostaria de selecionar aqueles objetos que são pequenos demais para considerar importantes a distâncias distantes.

#### 2.4.1. Atores na cena

Atores selecionados em um Nível ou Blueprint contêm configurações de distância acessadas por meio de seu painel Detalhes. Eles permitem que distâncias por instância sejam definidas ou se o Ator é selecionado usando um `Cull Distance Volume`.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/VisibilityCulling/PerActorDistanceCullingSettings.webp"
    alt="Figura: A seleção de distância do objeto."
    caption="Details > Rendering."
    ref="https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/VisibilityCulling/"
%}

- `Min Draw Distance` - Define a distância mínima de desenho na qual o objeto será renderizado na cena. Isso é medido em unidades de espaço mundial (centímetros) do centro da esfera delimitadora do objeto até a posição da câmera.
- `Desired Max Draw Distance` - Define a distância máxima de projeção para o *Level Designer*. A distância máxima "real" é a distância mínima de tração (desconsiderando 0).

#### 2.4.2. Exemplo de atores na cena

```cpp
Min Draw Distance = 0
Desired Max Draw Distance = 1000
```

**Nota:** O objeto vai ser renderizado quando a câmera se aproximar a uma distância **MENOR** que 1000 centímetros.
{: .notice--warning}

#### 2.4.3. Cull Distance Volume

`Cull Distance Volumes` permitem que você especifique uma variedade de tamanhos e distâncias de seleção para que os Atores não devam mais ser desenhados.

**1.** Adicione o volume `Cull Distance Volume` localizado em `Place Actors/Volumes`;

**2.** Altere as dimensões do objeto para definir a área de corte.

{% include imagelocal.html
    src="computacao_grafica/ue4_cullDistanceVolume_size.jpg"
    alt="Figura: CullDistanceVolume Size."
    caption="Corte de volume."
%}

{% include imagelocal.html
    src="computacao_grafica/ue4_cullDistanceVolume_Array_distances.jpg"
    alt="Figura: CullDistanceVolume Cull Distance Array."
    caption="Configure a matriz de distância e tamanho, Cull Distances para o corte."
%}

- **Cull Distances** - Uma lista de conjuntos de pares de Tamanho e Distância de Seleção usada para definir a distância de desenho de objetos com base em seu tamanho dentro de um **Cull Distance Volumes**. O código calculará o diâmetro da esfera da caixa delimitadora de um objeto e procurará o melhor ajuste nesta matriz para determinar qual distância de separação deve ser atribuída a um objeto.
  - `Size` - O tamanho a ser associado à distância de eliminação.
  - `Cull Distance` - A distância a ser associada ao tamanho dos limites de um ator.

#### 2.4.4. Exemplo de código

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

### 2.5. Frustum Culling ou corte de câmera

A seleção de **View Frustum** usa a área visível da tela do campo de visão (FOV) da câmera para selecionar objetos fora deste espaço.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/RenderingAndGraphics/VisibilityCulling/ViewFrustumDiagram.webp"
    alt="Figura: View Frustum."
    caption="O tronco da visão é uma forma piramidal que inclui um plano de recorte próximo e distante que define o mais próximo e o mais distante que qualquer objeto deve ser visível dentro deste espaço. Todos os outros objetos são removidos para economizar tempo de processamento."
%}

1. O plano de recorte próximo é o ponto mais próximo da câmera em que os objetos ficarão visíveis;

2. A **Camera Frustum** é a representação em formato piramidal da área de visualização visível entre os planos de clipe próximo e distante;

3. O plano de recorte distante é o ponto mais distante da câmera em que os objetos serão visíveis.

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
    src="computacao_grafica/ue4_camera_frustum.jpg"
    alt="Figura: Camera Frustum."
    caption="`Show` > `Advanced` > `Camera frustum`."
%}

### 2.6. Precomputed Visibility - Visibilidade pré-computada

Armazenam o estado de visibilidade de atores não móveis em células colocadas acima de superfícies de projeção de sombras. Este método de seleção gera dados de visibilidade *offline* (durante uma construção de iluminação) e funciona melhor para níveis de tamanho pequeno a médio.

A **Precomputed Visibility** é ideal para hardware inferior e dispositivos móveis. Para tais hardwares e dispositivos, ao considerar os custos de desempenho, você obterá o máximo negociando custos de Thread de renderização que são mais caros por aqueles com memória de tempo de execução, onde há mais flexibilidade em relação ao desempenho.

**Informação:** Divide a cena em um grid, onde cada célula do grid registra o que é visível naquele local. O tamanho das células é configurado .ini do projeto.
{: .notice--info}

{% include image.html
    src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/VisibilityCulling/PrecomputedVisibilityVolume/WS_EnablePVIS.webp"
    alt="Figura: World Settings > Precompute Visibility."
    caption="Configurando em World Settings o atributo Precomputed Visibility para verdadeiro."
%}

{% include image.html
    src="https://docs.unrealengine.com/4.26/Images/RenderingAndGraphics/VisibilityCulling/PrecomputedVisibilityVolume/PVIS_AddVolume.webp"
    alt="Figura: World Settings > Precompute Visibility."
    caption="- Adicionando na cena o volume Precomputed Visibility Volume que está em Place Actors > Volumes."
%}

Defina o tamanho do Volume para abranger a área analisada;

{% include imagelocal.html
    src="computacao_grafica/ue4_precomputed_visibility_volume.jpg"
    alt="Figura: Precomputed Visibility Cells, em azul as células."
    caption="Para visualizar o Grid de células na cena, Show > Visualize > Precomputed Visibility Cells."
%}

**Nota:** Se você já construiu a iluminação (`Bluid` > `Lighting`), pode usar o menu suspenso Construir na barra de ferramentas principal(**Show**) e selecionar `Precompute Static Visibility` para gerar células de visibilidade sem reconstruir a iluminação todas as vezes.
{: .notice--warning}

A câmera ao entrar na célula pergunta:

- "O que pode ser ocluído?";
- "O que pode ser renderizando e o que eu não devo renderizar?";
- "Neste local, lembramos que esses objetos eram visíveis e estes outros não eram".

### 2.7. Occlusion Culling

O sistema de oclusão dinâmica em UE4 vem com vários métodos de abate para escolher. Cada um desses métodos rastreia os estados de visibilidade dos Atores em um nível dentro do tronco de visão da câmera (ou campo de visão) que são obstruídos por outro Ator. As consultas são emitidas para a GPU ou CPU para verificar o estado de visibilidade de cada ator. Uma heurística é usada para reduzir o número de verificações de visibilidade necessárias, por sua vez, aumentando a eficácia geral de seleção e o desempenho.

**1.** A seleção de oclusão verifica com precisão o estado de visibilidade em cada modelo;

**2.** Use o comando do console `freezerendering` que força a renderização para congelar ou retomar. Permite a visualização da cena conforme foi renderizada a partir do ponto em que o comando foi inserido;

```bash
    freezerendering
```

**3.** Comando do console `Stat initviews` exibe informações sobre quanto tempo levou a seleção de visibilidade e quão eficaz foi. A contagem de seções visíveis é a estatística mais importante com relação ao desempenho do thread de renderização e é dominada por **Visible Static Mesh Elements** em `Stat initviews`.

```bash
    Stat initviews
```

### 2.8. Exemplo Occlusion Culling

{% include imagelocal.html
    src="computacao_grafica/ue4_freezerendering_before.jpg"
    alt="Figura: Freezerendering before."
    caption="Marque a posição da camera com o comando Ctrl + 1."
%}

{% include imagelocal.html
    src="computacao_grafica/ue4_stat_initviews_complete_scene.jpg"
    alt="Figura: Stat initviews."
    caption="Com comando Stat initviews apresente as estatistas."
%}

{% include imagelocal.html
    src="computacao_grafica/ue4_camera_actor.jpg"
    alt="Figura: Perspective > Camera Actor."
    caption="Alterne para a visualização e controle de câmera."
%}

Perceba que a média de objetos cortados na cena aumentou (`Frustum Culled Primitives`) e os objetos visíveis diminuiu (`Visible static mesh elements`).

{% include imagelocal.html
    src="computacao_grafica/ue4_stat_initviews_complete_scene_camera.jpg"
    alt="Figura: Stat initviews."
    caption="Complete scene camera."
%}

Com o comando `freezerendering` congele a renderização.

Após congelar a cena, ejete a câmera para poder navegar pela cena e aperte a tecla **1**, que foi utilizada para marcar a posição da câmera antes.

{% include imagelocal.html
    src="computacao_grafica/ue4_freezerendering_after.jpg"
    alt="Figura: Stat initviews after."
    caption="Rendering frozen."
%}

Como resultado temos dois objetos sendo renderizados, pois se um pixel de um objeto estiver presente na cena, o caso do objeto mais longe da câmera, todo o objeto é renderizado.
  
**Informação:** Se os objetos grandes fossem divididos em vários pedaços isso poderia diminuir o processo de renderização pois não teríamos que renderizar objetos gigantes que não aparecem totalmente na cena, mas sobrecarregaria a verificação de cada objeto visível na cena, então devemos balancear entre os dois métodos.
{: .notice--warning}

### 2.9. Occlusion Culling é um processo pesado a partir de 10.000 objetos na cena

Abaixo um exemplo em uma cena com 10.000 objetos:

1. Distance Culling remove 3.000 restando 7.000;
1. Frustum Culling remove e renderiza 4.000;
1. Precomputed Visibility remove 1.000;
1. Occlusion Culling remove 1.000.  

A necessidade do sistema executar os passos acima e efetuar vários cálculos para cada um pode tornar o processo pesado.

#### 2.9.1. Performance

- Configure distance Culling;
- Mais de 10-15k objetos pode ter impacto;
- Maior parte na CPU mas tem algum impacto na GPU;
- Grandes ambientes não ocluem bem;
- A mesma coisa para as partículas;
- Modelos grandes raramente irão ocluir e, assim, aumentar GPU;
- Mas combinar modelos com modelos grandes irá diminuir o custo da CPU.

#### 2.9.2. Resultado

- (Cubo) Modelos A  Visível;
- (Cubo) Modelos B Visível;
- (Esfera) Modelos C Não Visível;
- (Cilindro) Modelos D Visível;
- (Cubo) Modelos E Não Visível.

A,B,D são processados na GPU.

### 2.10. Processamento do Frame 2 - Time 66ms - GPU

A GPU agora tem uma lista de modelos e transformações, mas se apenas renderizássemos esta informação iria causar uma grande quantidade de renderização de pixels redundantes, portanto, precisamos descobrir quais modelos serão exibidos com antecedência.

{% include imagelocal.html
    src="computacao_grafica/ue4_gemeotry_hendering.jpg"
    alt="Figura. 3 Objetos na cena."
    caption="Menu Project Settings > Rendering > Early Z-Pass."
%}

Considerando a renderização de cada pixel na cena na imagem acima não poderia renderizar os pixels que estão detrás dos cilindros e os que estão ocultos por outros objetos;

### 2.11. Drawcalls

A GPU agora começa a renderizar, sendo feito objeto por objeto (DrawCall).

Um grupo de poligonos compartilha as mesmas propriedades em um `Drawcall`, abaixo um exemplo de como é feita a renderização.

{% include imagelocal.html
    src="computacao_grafica/ue4_gemeotry_hendering_drawcall_2.jpg"
    alt="Figura: 3 Objetos na cena."
    caption="A imagem acima renderiza 5 vezes."
%}

1. Chão;
1. Objetos 1, 2 e 3;
1. Céu.

{% include imagelocal.html
    src="computacao_grafica/ue4_gemeotry_hendering_drawcall.jpg"
    alt="Figura: 3 Objetos na cena."
    caption="A imagem acima renderiza 6 vezes."
%}

1. Chão;
2. Objetos 1, 2 e parte do objeto 3;
3. Parte do Objeto 3;
4. Céu.

{% include imagelocal.html
    src="computacao_grafica/ue4_gemeotry_hendering_drawcall_3.jpg"
    alt="Figura: Gemeotry Hendering Drawcall."
    caption="Acima o passo a passo, a ordem de renderização depende da importância dos objetos na cena."
%}

O chão é renderizado primeiro e depois os cilindos, isto se deve porque a cena é classificada por tipo de material, isso é mais rápido do contrário, pois tem que fazer uma mudança de estado de renderização no hardware.

**Nota:** A ordem de renderização não tem impacto no processamento.
{: .notice--warning}

### 2.12. Comando Stat RHI

RHI significa Rendering Hardware Interface. Este comando exibe várias estatísticas exclusivas:

{% include imagelocal.html
    src="computacao_grafica/ue4_stat_rhi.jpg"
    alt="Figura: Stat RHI."
    caption="No Viewport aparece o relatório com as estatísticas."
%}

- `Render target memory` -  Mostra o peso total de alvos de renderização como o GBuffer (que armazena as informações finais sobre iluminação e materiais) ou mapas de sombras. O tamanho dos buffers depende da resolução de renderização do jogo, enquanto as sombras são controladas pelas configurações de qualidade das sombras. É útil verificar esse valor periodicamente em sistemas com várias quantidades de RAM de vídeo e, em seguida, ajustar as predefinições de qualidade do seu projeto de acordo.
- `Triangles drawn` - Este é o número final de triângulos. É após o abate de _frustum_ e oclusão. Pode parecer muito grande em comparação com o _polycount_ de suas malhas. É porque o número real inclui sombras (que "copiam" malhas para desenhar mapas de sombras) e mosaico. No editor, também é afetado pela seleção.
- `DrawPrimitive calls` -  As chamadas _Draw_ podem ser um sério gargalo nos programas DirectX 11 e OpenGL4. São os comandos emitidos pela CPU para a GPU e, infelizmente, devem ser traduzidos pelo driver. Esta linha em **stat RHI** mostra a quantidade de chamadas de _draw_ emitidas no quadro atual (excluindo apenas a IU do Slate - Interface do Editor). Este é o valor total, portanto, além da geometria (normalmente o maior número), também inclui decalques, sombras, volumes de iluminação translúcida, pós-processamento e muito mais.

#### 2.12.1. Comando do console

```bash
stat RHI
```

### 2.13. O comando Stat unit e Stat FPS

**Stat fps** nos mostra o número final de _fps_ e o tempo que levou para renderizar o último quadro. É o tempo total. Mas ainda não sabemos se o custo foi causado pela CPU ou pela GPU. Como explicado antes, um tem que esperar o outro. A renderização rápida na placa de vídeo não ajudará, se a CPU precisar de mais tempo para terminar o trabalho de jogabilidade, desenho (gerenciando a GPU) ou física.

{% include imagelocal.html
    src="computacao_grafica/ue4_stat_unit.jpg"
    alt="Figura: Stat Unit."
    caption="Podemos obter informações mais específicas usando o comando stat unit. A hora do último quadro é mostrada com 4 números."
%}

- **Frame** - é igual ao FPS, o custo final;
- **Game** - é o trabalho da CPU no código do jogo;
- **Draw** -  é o trabalho da CPU na preparação de dados para a placa gráfica;
- **GPU** - é o tempo bruto necessário para renderizar um quadro na placa de vídeo.

#### 2.13.1. Comandos do console FPS

```bash
stat fps
stat unit
```

### 2.14. Considerações

**1.** 2000 - 3.000 é razoável;

**2.**Mais de 5.000 esta ficando alto;

**3.** Mais de 10.000 é provavelmente um problema;

**4.** Em dispositivos moveis esse valor é muito menor;

**5.** Para verificar experimente executar o comando **stat RHI** e alterar o **View Mode** de **Lit** para **Unlit** e verifique os valores **Triângulos desenhados**;

**6.** **DrawCalls** tem um impacto grande na performance;

**7.** **DrawCalls** tem um mais impacto que a quantidade de polígonos em muitos cenários.

_Exemplo_: Se temos um polígono com 32 triângulos e 34 tipos de materiais diferentes aplicados na sua superfície, terá mais impacto no FPS do que um polígono de 10.000 triângulos e 1 material. Cada triângulo com uma superfície diferentes é renderizado por vez.

## 3. ATIVIDADES

### 3.1. Renderização de materiais

1. Implemente os seguintes elementos e seus materiais.

   - Pedra;

   - Mesa;

   - Cadeira;

1. Apresente as seguintes informações.

   - Média de Drawcalls;

   - Quantidade de triângulos;

   - Quantidade de memória;

1. Utilizando os mesmos elementos tente reduzir o processo de renderização.

1. Justifique a possibilidade de executar a cena em hardware de baixo processamento (mobile).

***

## 4. Referências

- [O que é computação gráfica](http://www.um.pro.br/index.php?c=/computacao/definicao)
- [Computação gráfica](https://pt.wikipedia.org/wiki/Computa%C3%A7%C3%A3o_gr%C3%A1fica)
- [Computação Gráfica e Jogos Digitais](https://medium.com/@bitsgrupo/computa%C3%A7%C3%A3o-gr%C3%A1fica-e-jogos-digitais-1e15f0febf7c)
- [Introduction to Computer Graphics](http://math.hws.edu/graphicsbook/)
- [An In-Depth Look at Real-Time Rendering](https://www.unrealengine.com/en-US/onlinelearning-courses/an-in-depth-look-at-real-time-rendering)
- [Visibility and Occlusion Culling](https://docs.unrealengine.com/en-US/RenderingAndGraphics/VisibilityCulling/index.html)
- [Visibilty Culling Reference](https://docs.unrealengine.com/en-US/RenderingAndGraphics/VisibilityCulling/VisibilityCullingReference/index.html)
- [Cull Distance Volume](https://docs.unrealengine.com/en-US/RenderingAndGraphics/VisibilityCulling/CullDistanceVolume/index.html)
- [WTF Is? Volume - Cull Distance in Unreal Engine 4](https://www.youtube.com/watch?v=g0ML7oJll3w)
- [Process Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer)
- [Unreal’s Rendering Passes](https://unrealartoptimization.github.io/book/profiling/passes/)
- [Measuring Performance](https://unrealartoptimization.github.io/book/process/measuring-performance/)
- [Understanding Culling Methods - Live Training - Inside Unreal](https://youtu.be/6WtE3CoFMXU)
- [how unreal renders a frame](https://interplayoflight.wordpress.com/2017/10/25/how-unreal-renders-a-frame/)
- [Real-Time Rendering Fundamentals](https://www.unrealengine.com/en-US/onlinelearning-courses/real-time-rendering-fundamentals)
- [How Unreal Renders a Frame](https://interplayoflight.wordpress.com/2017/10/25/how-unreal-renders-a-frame/)
- [Introduction to Decal Rendering](https://samdriver.xyz/article/decal-render-intro)
- [Vertex Shaders](https://www.nvidia.com/en-us/drivers/feature-vertexshader/)
- [Verttex Shaders](https://pt.wikipedia.org/wiki/Vertex_shader)
- [Deferred Shading](https://learnopengl.com/Advanced-Lighting/Deferred-Shading)
- [Normal Mapping](https://learnopengl.com/Advanced-Lighting/Normal-Mapping)
- [General-purpose computing on graphics processing units](https://en.wikipedia.org/wiki/General-purpose_computing_on_graphics_processing_units)
- [gpu-rendering-and-game-graphics-explained](https://www.gamersnexus.net/guides/2429-gpu-rendering-and-game-graphics-explained)
- [feature-vertexshader](https://www.nvidia.com/en-us/drivers/feature-vertexshader/)
- [General-purpose_computing_on_graphics_processing_units](https://en.wikipedia.org/wiki/General-purpose_computing_on_graphics_processing_units)
- [articles/forward-rendering-vs-deferred-rendering--gamedev-12342](https://gamedevelopment.tutsplus.com/articles/forward-rendering-vs-deferred-rendering--gamedev-12342)
- [Graphics_pipeline](https://en.wikipedia.org/wiki/Graphics_pipeline)
- [Vertex_pipeline](https://en.wikipedia.org/wiki/Vertex_pipeline)
- [vertex-shader](https://www.pcmag.com/encyclopedia/term/vertex-shader)
- [video-game-e-jogos/863-o-que-e-vertex-shading](https://www.tecmundo.com.br/video-game-e-jogos/863-o-que-e-vertex-shading-.htm)
- [Geometry_Shader](https://www.khronos.org/opengl/wiki/Geometry_Shader)
- [Fragment_Shader](https://www.khronos.org/opengl/wiki/Fragment_Shader)
- [computer_graphics](https://en.wikipedia.org/wiki/Rendering_(computer_graphics))
- [what-are-draw-calls](https://unreal.tips/en/what-are-draw-calls/)
- [RPC](https://deinfo.uepg.br/~alunoso/2017/RPC/)
- [pixels](https://bassemtodary.wordpress.com/tag/pixels/)
- [Interplay of Light](https://interplayoflight.wordpress.com/2017/10/25/how-unreal-renders-a-frame-part-2/)
- [Game Engine Overview](https://www.slideshare.net/sharadmitra/game-engine-overview)
- [Polygon Mesh](https://pt.qaz.wiki/wiki/Polygon_mesh)
- [How to Prepare Textures](https://vvvv.org/documentation/howto-prepare-textures)
- [Computer Graphics. image treatment](https://www.petervaldivia.com/computer-graphics/)
- [Maya tutorial : How to move your Pivot Point ( 2 methods )](https://www.youtube.com/watch?v=V4DwKcik4yU)
- [UE4 Tutorial: Change Pivot Point on BSP or Static Mesh](https://www.youtube.com/watch?v=N1h5mMviSKs)
- [HSV to RGB Material Function in Unreal Engine](https://ferkizue.blogspot.com/2018/06/hsv-to-rgb-material-function-in-unreal.html)
- [Alpha compositing](https://en.wikipedia.org/wiki/Alpha_compositing)
- [Alpha (alpha channel)](https://developer.mozilla.org/en-US/docs/Glossary/Alpha)
- [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html)
