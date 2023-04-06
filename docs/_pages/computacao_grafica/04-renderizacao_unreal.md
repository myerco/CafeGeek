---
title: Passos da renderizaçãos
permalink: /pages/computacao_grafica/renderizacao-unreal
excerpt: Neste capitulo vamos analisar como é realizado o processamento de imagens pela CPU e GPU pelo Unreal Engine.
last_modified_at: 2023-03-27T08:48:05-04:00
toc: true    
sidebar:
    nav: dev_computacao
---

{% include figure image_path="/assets/images/jogos_digitais/brecht-corbeel-g7JkVRANxX0-unsplash.webp" alt="Brecht Corbeel" caption="" %}

## 1. Lista de Frames e Threads

Para exemplificar o processo de renderização vamos apresentar os seguintes passos conforme as _thread_ são executas:

| Threads      |                                         |                                         |                                           |                                           |
| :----------- | :-------------------------------------- | :-------------------------------------- | :---------------------------------------- | :---------------------------------------- |
| **CPU**      | <span style="color:blue">Frame A</span> | <span style="color:red">Frame B</span>  | <span style="color:green">Frame C </span> | <span style="color:brown">Frame D</span>  |
| **DRAW CPU** |                                         | <span style="color:blue">Frame A</span> | <span style="color:red">Frame B</span>    | <span style="color:green">Frame C </span> |
| **GPU**      |                                         |                                         | <span style="color:blue">Frame A</span>   | <span style="color:red"> Frame B</span>   |
| **Time in milliseconds**     | **0**                                   | **33**                                  | **66**                                    |                                           |

Acompanhe a ordem de execução de cada Frame.

1. O <span style="color:blue">Frame A</span> é instanciado na CPU;
1. Logo em seguida o <span style="color:blue">Frame A</span> é passado para um momento onde a CPU e a GPU compartilham alguns elementos de construção. Enquanto isso ocorre a CPU carrega o <span style="color:red">Frame B</span>;
1. Após passar pelo passo de compartilhamento o <span style="color:blue">Frame A</span> é colocado inteiramente na GPU;
1. A operação se repete para todos os Frames;
1. Perceba que a cada passo que se completa são liberados recursos de CPU e GPU para serem usados com outros frames.

**Informação:** A seguir vamos abordar cada passo.
{: .notice--info}

## 2. Processamento do Frame 0 - Time 0 - CPU

**Nota:** Qualquer coisa relativa a mudança e posição dos objetos é realizado neste passo.
{: .notice--warning}

Neste passo o calculo da lógica e as transformações é realizado na CPU, como por exemplo:

**Animações** - Calcula quando as Animações iniciam e terminam;

**Posição de modelos e objetos** - Necessário para calcular a posição e sua influência;

**Física** - Calculo para determinar onde os objetos vão;

**Inteligência Artificial** - Por exemplo, em um veículo controlado por IA é necessário determinar, como ele se movimenta,  como o estado e onde o carro estará realmente;

**Cria e destrói, esconde e apresenta** - Necessário para determinar onde os objetos aparecem no mundo.

**Nota:** O Unreal Engine conhece todas as transformações e todos os objetos.
{: .notice--warning}

## 3. Processamento do Frame 1 - Time 33ms - Preparar a Thread

Antes de podermos usar as transformações para renderizar a imagem, precisamos saber o que incluir na renderização, isso é executado principalmente na CPU, mas algumas partes são manipuladas pela GPU, para tal finalidade é realizada a tarefa de :
{: .text-justify}

**Processo de oclusão** - Construção da lista de todos os objetos e modelos visíveis, sendo que o processamento é realizado por objeto e não por polígono;

**Preparação da Thread** - Uma Thread da GPU é alocada.

A seguir as 4 Etapas em ordem de execução desse processo.

`Distance Culling` - Remove quaisquer objetos além de X da câmera;

`Frustim Culling` - Verifica o que está na frente da câmera;

`Precomputed Visibility` - (Visibilidade pré-computada) Divide a cena em uma grade, cada célula da grade lembra o que está visível naquele local;

`Occlusion Culling` - Verifica com precisão o estado de visibilidade em cada modelo.

## 4. Processamento do Frame 2 - Time 66ms - GPU

A GPU agora tem uma lista de modelos e transformações, mas se apenas renderizássemos esta informação iria causar uma grande quantidade de renderização de pixels redundantes, portanto, precisamos descobrir quais modelos serão exibidos com antecedência.
{: .text-justify}

{% include imagelocal.html
    src="computacao_grafica/ue4_gemeotry_hendering.jpg"
    alt="Figura. 3 Objetos na cena."
    caption="Menu Project Settings > Rendering > Early Z-Pass."
%}

Considerando a renderização de cada pixel na cena na imagem acima não poderia renderizar os pixels que estão detrás dos cilindros e os que estão ocultos por outros objetos.
{: .text-justify}
