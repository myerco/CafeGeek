---
title: Renderização
permalink: /computacao-grafica/renderizacao
excerpt: Neste capítulo apresentaremos o processo de renderização de objetos 3D.
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-27T08:48:05-04:00
order: 103
---

## 1. Entendendo o processo de renderização

A renderização de imagens 3D é um processo complexo que envolve várias etapas. Em geral, o processo de renderização envolve a conversão de dados de modelos 3D em imagens 2D usando técnicas de iluminação, sombreamento e texturização para criar uma imagem final realista.

Mas antes de abordar o processo de renderização é necessário entender como os processos ou tarefas são executados pelos sistemas operacionais.

## 2. Entendendo como os processos são executados pelo sistema operacional

Em computação, um processo é uma instância de um programa de computador que está sendo executado. Ele contem o código do programa e sua atividade atual. Dependendo do sistema operacional, um processo pode ser feito de várias linhas de execução que executam instruções concorrentemente. O sistema operacional seleciona um processo da fila de aptos para receber o processador. O processo selecionado passa do estado de apto para o estado executando. O módulo do sistema operacional que faz essa seleção é chamado de escalonador.
{: .text-justify}

{% include imagelocal.html
    src="computacao-grafica/ue4_cpu_processos.jpg"
    alt="Figura: Fila de Processos. "
    caption="Fluxo de execução de processos."
%}

**Criado** - Enquanto o processo está sendo criado, esse é seu estado;

**Apto** -Esse é como um estado de ponto de partida, aqui ficam os processos que estão prontos para serem processados;

**Espera** - Esse é um estado especial que na verdade está mais para uma característica de outros estados, basta observar os processos que estão nos estado de prontidão e os que estão aguardando eventos, pois ambos também estão em um estado de espera;

**Execução** - Quando o processo está sendo executado, seu estado passa a ser este;

**Encerrado** -Esse é o último estado  de um processo, sua finalização, seja de forma voluntária, como quando ele não é mais necessário ou de forma involuntária, como as ocasionadas por um erro;

**RPC** - Remote Procedure Call (Chamada de Procedimento Remoto) é uma tecnologia para a criação de programas distribuídos servidor/cliente que provê um paradigma de comunicação de alto nível no sistema operacional, á presumindo a existência de um protocolo de transporte, como TCP/IP ou UDP, para carregar a mensagem entre os programas comunicantes;

**Threads** - Thread é um pequeno programa que trabalha como um subsistema, sendo uma forma de um processo se auto dividir em duas ou mais tarefas. É o termo em inglês para Linha ou Encadeamento de Execução. Essas tarefas múltiplas podem ser executadas simultaneamente para rodar mais rápido do que um programa em um único bloco ou praticamente juntas, mas que são tão rápidas que parecem estar trabalhando em conjunto ao mesmo tempo.

## 3. O processo de renderização pela GPU

A renderização GPU torna possível usar sua placa de vídeo para renderização, ao invés da CPU. Isso pode acelerar a renderização, porquê as GPUs modernas são desenhadas para fazer muito processamento de números. Por outro lado, elas também têm algumas limitações na renderização de cenas complexas devido à memória mais limitada, e questões com interatividade quando usando a mesma placa de vídeo para visualização e renderização.
{: .text-justify}

A renderização ocorre mediante o envio de comandos para a GPU, que gera a tela de forma assíncrona. Em algumas situações, a GPU pode ter muito trabalho para fazer, e a CPU terá de aguardar antes de enviar novos comandos.
{: .text-justify}

{% include imagelocal.html
    src="computacao-grafica/ue4_gpu_pipeline.jpg"
    alt="Figura: Pipeline de computação de gráfica."
    caption="Fluxo de trabalho do processo de renderização."
%}

### 3.1. Aplicação

Etapa de toda a lógica da mecânica dos elementos que são apresentados.

**Animations** - Calcula quando as Animações iniciam e terminam;

**System Coordinates** - Calcula a posição dos objetos e sua influência;

**Artificial intelligence** - Determina como o objeto se movimenta e qual o seu estado;

**Spawn and Hide objects** - É a lógica necessária para determinar onde os objetos aparecem no mundo.

### 3.2. Geometria

A etapa de geometria (com pipeline de geometria), é responsável pela maioria das operações com polígonos e seus vértices (com pipeline de vértices), pode ser dividida nas tarefas a seguir. Depende da implementação específica de como essas tarefas são organizadas em pipeline paralelo.
{: .text-justify}

**Model 3D** - É o processo onde os objetos são desenhados na cena, entre eles vértices, triângulos e o sistema de coordenadas;
  
**Distance Culling** - Ou Corte de Distância Remove objetos que estão além de um valor X da câmera;
  
**Frustim Culling** - Ou Corte de Câmera remove objetos que não estão a frente da câmera;

**Occlusion Culling** - Ou Corte de oclusão é o processo que desativa a renderização de objetos quando eles não são vistos pela câmera porque estão obscurecidos (obstruídos) por outros objetos. Isso não acontece automaticamente na computação gráfica 3D, pois na maioria das vezes os objetos mais distantes da câmera são desenhados primeiro e os objetos mais próximos são desenhados por cima deles (isso é chamado de “overdraw”).
{: .text-justify}

### 3.3. Renderização

**DrawCalls** - Grupo de polígonos que compartilham a mesmo material. Os desenhos de chamadas, em uma tradução ao pé da letra, basicamente são quantos objetos estão sendo desenhados na tela. Você deseja manter esse número baixo para manter um bom desempenho, portanto, nas luzes dos pixels, fazem os objetos serem desenhados tantas vezes quanto as luzes que os afetam.
{: .text-justify}
  
{% include image.html
    src="https://unreal.tips/wp-content/uploads/2019/05/Drawcalls.jpg"
    alt="Figura: Drawcalls."
    caption="Unreal Tips."
%}  

**Vertex Shaders** - É uma função de processamento gráfico usada para adicionar efeitos especiais a objetos em um ambiente 3D executando operações matemáticas nos dados de vértice dos objetos. Cada vértice pode ser definido por muitas variáveis diferentes. Por exemplo, um vértice é sempre definido por sua localização em um ambiente 3D usando as coordenadas x-, y- e z-. Os vértices também podem ser definidos por cores, texturas e características de iluminação. Os Vertex Shaders não alteram realmente o tipo de dados; eles simplesmente mudam os valores dos dados, de modo que um vértice emerge com uma cor diferente, texturas diferentes ou uma posição diferente no espaço.
{: .text-justify}

{% include image.html
    src="https://upload.wikimedia.org/wikipedia/commons/8/84/Phong-shading-sample.jpg"
    alt="Figura: Flat-shading e Phong-shading."
    caption="São tipos de sombreadores 3D e são executados uma vez para cada vértice fornecido ao processador gráfico."
    ref="https://en.wikipedia.org/wiki/Shader"
%}  

**Pixel Shader** - Os Pixel Shader, calculam a cor e outros atributos de cada "fragmento",uma unidade de trabalho de renderização que afeta no máximo um único pixel de saída. Os sombreadores de pixel variam desde simplesmente sempre a saída da mesma cor, até a aplicação de um valor de iluminação, até o mapeamento de saliências, sombras, realces especulares, translucidez e outros fenômenos. Eles podem alterar a profundidade do fragmento (para buffer Z) ou produzir mais de uma cor se vários destinos de renderização estiverem ativos.
{: .text-justify}

{% include image.html
    src="https://upload.wikimedia.org/wikipedia/commons/0/0f/Shading_models.png"
    alt="Figura: Shading models."
    caption="Os tipos mais simples de sombreadores de pixel geram um pixel da tela como um valor de cor; sombreadores mais complexos com várias entradas / saídas também são possíveis."
%}

**Geometry Shaders** - Recebe como entrada um conjunto de vértices que formam uma única primitiva, por exemplo, um ponto ou triângulo. O sombreador de geometria pode então transformar esses vértices conforme achar necessário antes de enviá-los para o próximo estágio de sombreador. O que torna o shader de geometria interessante é que ele é capaz de converter a primitiva original (conjunto de vértices) em primitivas completamente diferentes, possivelmente gerando mais vértices do que os inicialmente dados.
{: .text-justify}

{% include imagelocal.html
    src="computacao-grafica/The-graphics-pipeline-in-OpenGL-consists-of-these-5-steps-in-the-new-generation-of-cards.jpg"
    alt="Figura: Pipeline OpenGL."
    caption="É uma sequência de etapas que o OpenGL executa ao renderizar objetos. Esta visão geral fornecerá uma descrição de alto nível das etapas do pipeline."
%}

**Fragment Shader** - É uma unidade programável da GPU que opera em cada fragmento produzido durante a rasterização e seus dados associados.
  
**Rasterization** -  O termo rasterização, em geral, pode ser aplicado a qualquer processo pelo qual informações tipo vetorial podem ser convertidas num formato de pontos ou pixels.
  
_Exemplo_: Um exemplo seria uma reta descrita matematicamente é infinitesimalmente contínua, não importa o quão pequeno um trecho da reta é observado, é impossível determinar qual é o próximo ponto depois de um determinado ponto; não existem quebras.

{% include imagelocal.html
    src="computacao-grafica/rasterização.webp"
    alt="Figura: Rasterização."
    caption="Conversão da representação de uma reta na forma vetorial para a matricial. Em B, é incluído um tratamento de anti-aliasing.."
    ref="https://portaleletronica.com.br/images/Imagens/Comp_Graf/Parte_3_Rasterizao.pdf"
%}

## 4. O custo da renderização

**Nota:** Componentes = `DrawCalls`
{: .notice--warning}

**1.** O custo para renderizar muitos polígonos é muitas vezes menor que o `Drawcall`;

**2.** 50.000 triângulos podem rodar pior que 50 milhões dependendo da implementação;

**3.** `Drawcall` tem uma despesa básica, portanto, otimizar _low poli_  para _super poli_ pode ser que não faça nenhuma diferença;  

**4.** Componentes ocluem e são renderizados um por um;

**5.** Mesclar em um único ator geralmente não faz diferença para a renderização;

**6.** Para diminuir o `Drawcalls` é melhor usar menos modelos maiores do que muitos modelos pequenos, você não pode fazer muito isso, no entanto, isso afeta todo o resto negativamente;
{: .text-justify}

- Pior para oclusão - A oclusão é mais rápida por si só, mas não será capaz de fazer um trabalho bom o suficiente, tem menos objetos que precisam ser verificados quanto à oclusão, mas tem uma chance menor de realmente ocluir alguma coisa;
{: .text-justify}

- Pior para o lightmapping - `Lightmap` tem uma quantidade limite de espaço, a quantidade máxima de espaço é a textura do mapa de luz, independentemente da resolução, o mapa de luz também tem um limite de resolução superior;
{: .text-justify}

    _Exemplo_: Imagens de 4k, 4.096 já são enormes para um `Lightmap`.

- Se você fizer modelos muito grandes, eventualmente eles simplesmente ficarão sem espaço UV.
  - Pior para calculo de colisão.
  - Pior para memoria.