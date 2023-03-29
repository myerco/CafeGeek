---
title: Unreal Engine
excerpt: Aprenda estruturas de desenvolvimento e lógicas de programação, utilizando Blueprints e C++.
permalink: /pages/unreal_engine/
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true  
---
## 1. Como é o desenvolvimento de jogos digitais?

{% include image.html
    src="https://miro.medium.com/max/875/0*OlVTuxFz-Qn7oTUn"
    alt="Figura: So, You Want to Be a Game Developer?"
    title="Figura: So, You Want to Be a Game Developer?"
    caption="Se você é como a maioria das pessoas, provavelmente joga videogame. Não importa se você é um jogador competitivo de e-sports atrás de muito dinheiro com seus jogos, ou se gosta de jogar spider ou candy crush como minha mãe, todo mundo joga. Mas você já pensou em fazê-los para o seu trabalho?"
    ref="https://medium.com/swlh/so-you-want-to-be-a-game-developer-e3b7f9f4ac70"
%}

Um jogo digital é um produto de software e como muitos projetos de desenvolvimento envolve diversas áreas de conhecimento na sua construção, como por exemplo:

### 1.1. Programação de computadores

{% include image.html
    src="https://upload.wikimedia.org/wikipedia/commons/1/1f/Primoc.png"
    alt="Figura: Programação de computadores"
    title="Figura: Programação de computadores."
    caption="Programação é o processo de escrita, teste e manutenção de um programa de computador. O programa é escrito em uma linguagem de programação, embora seja possível, com alguma dificuldade, o escrever diretamente em linguagem de máquina. Diferentes partes de um programa podem ser escritas em diferentes linguagens."
    ref="https://pt.wikipedia.org/wiki/Programa%C3%A7%C3%A3o_de_computadores"
%}

### 1.2. Arte 3D e 2D

{% include image.html
    src="https://i2.wp.com/www.crieseusjogos.com.br/wp-content/uploads/2018/08/jogos-2d-ou-jogos-3d.jpeg?w=1200&ssl=1"
    alt="Figura: É melhor criar um jogo 2D ou 3D? "
    title="Figura: É melhor criar um jogo 2D ou 3D? "
    caption="Desenvolvimento de jogos evoluiu e a geração de hoje preza bastante pelo seu design mágico, estrutura, renderização e textura. Isso tem influenciado diretamente em saber se é melhor criar um jogo 2D ou 3D."
    ref="https://www.crieseusjogos.com.br/e-melhor-criar-um-jogo-2d-ou-3d/"
%}

### 1.3. Computação gráfica

{% include image.html
    src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Activemarker2.PNG/330px-Activemarker2.PNG"
    alt="3D (computação gráfica)"
    title="3D (computação gráfica)."
    caption="Computação gráfica tridimensional são gráficos que usam representações tridimensionais de dados geométricos (geralmente cartesianos) que são armazenados em um computador com o propósito de realizar cálculos e renderizar imagens 2D."
    ref="https://pt.wikipedia.org/wiki/3D_%28computa%C3%A7%C3%A3o_gr%C3%A1fica%29"
%}

### 1.4. Elementos de construção de Narrativas

{% include image.html
    src="https://escolabrasileiradegames.com.br/wp2016/wp-content/uploads/2020/06/escola-brasileira-de-games-Jornada-do-Her%C3%B3i.jpg"
    alt="Figura: Jornada do Herói: Desenvolvimento de Narrativas para Jogos"
    title="Figura: Jornada do Herói: Desenvolvimento de Narrativas para Jogos."
    caption="Toda e qualquer história seja ela de aventura, terror, ação, romance ou qualquer outro gênero, é a responsável por chamar atenção do usuário e levar o jogador de encontro com uma nova aventura, conhecer um novo mundo qual ele irá mergulhar, quem são os personagens, seus medos, conquistas e aflições…"
    ref="https://escolabrasileiradegames.com.br/blog/jornada-do-heroi-desenvolvimento-de-narrativas-para-jogos"
%}

### 1.5. Efeitos sonoros

{% include image.html
    src="https://sp-ao.shortpixel.ai/client/to_webp,q_lossy,ret_img/https://kreonit.com/wp-content/uploads/2020/08/sound_main_optimized.jpg"
    alt="Figura: Game sound design: soundtrack, sound effects and how to combine them"
    caption="O design de som é uma parte muito importante de um jogo. Os desenvolvedores de jogos concordam que a música e os sons são poderosos condutores emocionais. E nosso objetivo é usar totalmente o som para tornar o jogo ainda melhor."
    ref="https://kreonit.com/our-services/mobile-game-development/game-sound-design/"
%}

Como visto acima, diversos perfis profissionais de áreas distintas estão presentes na construção de um jogo, formando diversas equipes multiculturais,  o que aumenta a complexidade desse tipo de projeto quando pensamos na organização de tarefas e comunicação dos envolvidos.

***

## 2. Mecânica, Dinâmica e Estética (MDA)

O projeto de desenvolvimento de um jogo pode ser estruturado dividindo-o em componentes distintos, Mecânica - Mechanics,  Dinâmica - Dynamics e Estética Aesthetics, MDA, esta divisão ajuda a trabalhar com o design do jogo.

### 2.1. Mecânica

Descreve os componentes específicos do jogo, no nível de representação de dados e algoritmos.

- Componentes: Pontos, Avatares, Distintivos, tabelas de classificação;
  
- Controles: Tarefas, tempo, Perfis;
  
- Ações: Níveis, missões e grupos.
  
### 2.2. Dinâmica

Descreve o comportamento da mecânica quando ela é executada pelas ações do jogador e cada um dos resultados ao longo do tempo.

- Contexto;

- Escolhas;
  
- Consequências;
  
- Restrições;

- Continuação;

- Competição;

- Cooperação.
  
### 2.3. Estética

Descreve as respostas emocionais desejáveis evocadas no jogador, quando ele interage com o sistema de jogo.

- Desafio;
  
- Criatividade;

- Comunidade;
  
- Elogio;
  
- Confiança;
  
- Conhecimento;

Quanto a construção da mecânica de um jogo é necessário utilizar uma linguagem de programação para implementar movimento, interação de personagens, inteligência artificial e outros elementos dinâmicos.

As linguagens de programação vem evoluindo para simplificar as rotinas e comandos assim agilizando o desenvolvimento e permitindo o programador focar no que deve ser feito escondendo alguns detalhes de como é feito.

> Conhecer e entender como é feito é importante para determinar as técnicas utilizadas e ser capaz e aproveitar ou mesmo melhorar os jogos.

Existem aplicações que auxiliam na produção de programas de computador ou jogos digitais, estas ferramentas abstraem a lógica complexa que faz com os objetos sejam apresentados de forma adequada na cena, no caso de jogos digitais. Tais ferramentas são chamadas de *Frameworks*.

***

## 3. O que é uma Engine e Framework?

{% include image.html
    src="https://developerhouse.com/wp-content/uploads/2020/10/game-engines-and-framework.jpg"
    alt="Figura: Game Engine VS Game Framework."
    title="Figura: Game Engine VS Game Framework"
    ref="https://developerhouse.com/game-engine-vs-game-framework/"
%}

No desenvolvimento de jogos um *Framework* pode ser definido como um conjunto de bibliotecas que auxiliam a programação, sendo que uma *Engine* ou motor gráfico é mais completo pois abrange outros aspectos na produção de jogos.

Algumas *Engine* disponíveis no mercado.

1. Unreal engine;

1. Unity;

1. GameMaker;

## 4. Ciclo da lógica do desenvolvimento de um jogo

***

A maioria das *Engines* seguem um ciclo de execução da lógica de programação baseado em :

- **Inicialização** - Executado ao iniciar o jogo carregando bibliotecas básicas;

- **Carga** - Responsável por carregar os objetos ou módulos;

- **Atualização** - Estado de atualização constante responsável por apresentar todos os estados do jogo;

- **Finalização** - Executa as rotinas para descarregar o jogo;

***

## 5. O que é Unreal Engine?

{% include image.html
    src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c6/Unreal%2BEngine_11_18_UE_Feed_Migration_Images_FEED_THUMB_UE_Logo_Generic-1400x788-c11642ffb55e268095321f5eb144f469beb0074f.jpg/800px-Unreal%2BEngine_11_18_UE_Feed_Migration_Images_FEED_THUMB_UE_Logo_Generic-1400x788-c11642ffb55e268095321f5eb144f469beb0074f.jpg"
    alt="Figura: Unreal Engine."
    ref="https://www.unrealengine.com/en-US/"
%}

É uma *Engine* (motor gráfico) para desenvolvimento de jogos que engloba vários aspectos na sua produção, a seguir listamos algumas funcionalidades:

1. Edição e compilação da lógica de programação;

1. Apresentação de elementos visuais da cena do jogo;

1. Editor da lógica de animações e manipulação de esqueletos e malhas;

1. Editor de interfaces para comunicação com os jogadores (HUD);

1. Editor de sequencias de animação;

1. Editor de sons;

1. Editor para construção de materiais;

1. Editor de efeitos especiais utilizando partículas;

***

## 6. O curso de Unreal Engine com C++ e Blueprint

Aprenda estruturas de desenvolvimento e lógicas de programação, utilizando *Blueprints* e *C++*.  O curso está associado a construção **Mecânica** do jogo pois nele definimos elementos como mecanismos de controle e elementos do conteúdo do jogo.  

### 6.1. Habilidades que serão aprendidas

- Configuração e organização de projetos;
  
- Analisar e aplicar lógica de programação utilizando *Blueprint* e *C++*;
  
- Implementar regras de tempo e espaço;
  
- Implementar interface do usuário;
  
- Estruturar e configurar materiais, terrenos e iluminação;
  
- Implementar ambientes Multijogador;
  
- Implementar inteligência artificial;
  
- Construir a animação de personagens;
  
- Implementar Efeitos especiais.

### 6.2. Categoria do Curso

| M             | D             | A         |
| :------------ | :------------ | :-------- |
| **Mecânicas** | **Dinâmicas** | Estéticas |
