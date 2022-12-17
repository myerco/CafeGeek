---
title: Desenvolvimento jogos digitais
description: Na construção da mecânica de um jogo é necessário utilizar uma linguagem de programação para implementar movimento, interação de personagens, inteligência artificial e outros elementos dinâmicos.
tags: [Unreal Engine,desenvolvimento, blueprint]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
date: 2022-09-21 
---

***

- [Como é o desenvolvimento de jogos digitais?](#como-é-o-desenvolvimento-de-jogos-digitais)
- [Mecânica, Dinâmica e Estética (MDA)](#mecânica-dinâmica-e-estética-mda)
- [O que é uma Engine e Framework?](#o-que-é-uma-engine-e-framework)
- [Ciclo da lógica do desenvolvimento de um jogo](#ciclo-da-lógica-do-desenvolvimento-de-um-jogo)
- [O que é Unreal Engine?](#o-que-é-unreal-engine)
- [O curso de Unreal Engine com C++ e Blueprint](#o-curso-de-unreal-engine-com-c-e-blueprint)
  - [Habilidades que serão aprendidas](#habilidades-que-serão-aprendidas)
  - [Categoria do Curso](#categoria-do-curso)

***

## Como é o desenvolvimento de jogos digitais?

***

{% include image.html
    src="https://miro.medium.com/max/875/0*OlVTuxFz-Qn7oTUn"
    alt="Figura: So, You Want to Be a Game Developer?"
    caption=" Figura: So, You Want to Be a Game Developer? - <https://medium.com/swlh/so-you-want-to-be-a-game-developer-e3b7f9f4ac70> ."
%}

O desenvolvimento de jogos digitais envolve diversas áreas de conhecimento como por exemplo:

- Programação de computadores;

{% include image.html
    src="https://upload.wikimedia.org/wikipedia/commons/1/1f/Primoc.png"
    alt="Figura: Programação de computadores "
    caption=" Figura: Programação de computadores - "Programação é o processo de escrita, teste e manutenção de um programa de computador. O programa é escrito em uma linguagem de programação, embora seja possível, com alguma dificuldade, o escrever diretamente em linguagem de máquina. Diferentes partes de um programa podem ser escritas em diferentes linguagens." <https://pt.wikipedia.org/wiki/Programa%C3%A7%C3%A3o_de_computadores>."
%}

- Arte 3D e 2D;

{% include image.html
    src="https://i2.wp.com/www.crieseusjogos.com.br/wp-content/uploads/2018/08/jogos-2d-ou-jogos-3d.jpeg?w=1200&ssl=1"
    alt="Figura: É melhor criar um jogo 2D ou 3D? "
    caption=" Figura: É melhor criar um jogo 2D ou 3D? - "Desenvolvimento de jogos evoluiu e a geração de hoje preza bastante pelo seu design mágico, estrutura, renderização e textura. Isso tem influenciado diretamente em saber se é melhor criar um jogo 2D ou 3D." <https://www.crieseusjogos.com.br/e-melhor-criar-um-jogo-2d-ou-3d/>."
%}

- Computação gráfica;

{% include image.html
    src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Activemarker2.PNG/330px-Activemarker2.PNG"
    alt="3D (computação gráfica)"
    caption=" Figura: 3D (computação gráfica) - "Computação gráfica tridimensional são gráficos que usam representações tridimensionais de dados geométricos (geralmente cartesianos) que são armazenados em um computador com o propósito de realizar cálculos e renderizar imagens 2D." <https://pt.wikipedia.org/wiki/3D_%28computa%C3%A7%C3%A3o_gr%C3%A1fica%29>."
%}

- Elementos de construção de Narrativas;

{% include image.html
    src="https://escolabrasileiradegames.com.br/wp2016/wp-content/uploads/2020/06/escola-brasileira-de-games-Jornada-do-Her%C3%B3i.jpg"
    alt="Figura: Jornada do Herói: Desenvolvimento de Narrativas para Jogos"
    caption=" Figura: Jornada do Herói: Desenvolvimento de Narrativas para Jogos - "Toda e qualquer história seja ela de aventura, terror, ação, romance ou qualquer outro gênero, é a responsável por chamar atenção do usuário e levar o jogador de encontro com uma nova aventura, conhecer um novo mundo qual ele irá mergulhar, quem são os personagens, seus medos, conquistas e aflições…" <https://escolabrasileiradegames.com.br/blog/jornada-do-heroi-desenvolvimento-de-narrativas-para-jogos>."
%}

- Efeitos sonoros;

Como visto acima, diversos perfis profissionais de áreas distintas estão presentes na construção de um jogo o que aumenta a complexidade desse tipo de projeto, afinal, temos diversas equipes multiculturais envolvidas compartilhando tarefas.

## Mecânica, Dinâmica e Estética (MDA)

O projeto de desenvolvimento de um jogo pode ser estruturado dividindo-o em componentes distintos, Mecânica - Mechanics,  Dinâmica - Dynamics e Estética Aesthetics, MDA, esta divisão ajuda a trabalhar com o design do jogo.

- Mecânica: descreve os componentes específicos do jogo, no nível de representação de dados e algoritmos;
  - Componentes: Pontos, Avatares, Distintivos, tabelas de classificação.
  - Controles: Tarefas, tempo, Perfis.
  - Ações: Níveis, missões e grupos.
  
- Dinâmica: descreve o comportamento da mecânica quando ela é executada pelas ações do jogador e cada um dos resultados ao longo do tempo.
  - Contexto;
  - Escolhas;
  - Consequências;
  - Restrições;
  - Continuação;
  - Competição;
  - Cooperação.
  
- Estética: descreve as respostas emocionais desejáveis evocadas no jogador, quando ele interage com o sistema de jogo.
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

## O que é uma Engine e Framework?

***

{% include image.html
    src="https://developerhouse.com/wp-content/uploads/2020/10/game-engines-and-framework.jpg"
    alt="Figura: Game Engine VS Game Framework."
    caption=" Figura: Game Engine VS Game Framework - <https://developerhouse.com/game-engine-vs-game-framework/> ."
%}

No desenvolvimento de jogos um *Framework* pode ser definido como um conjunto de bibliotecas que auxiliam a programação, sendo que uma *Engine* ou motor gráfico é mais completo pois abrange outros aspectos na produção de jogos.

Algumas *Engine* disponíveis no mercado.

1. Unreal engine;

1. Unity;

1. GameMaker;

## Ciclo da lógica do desenvolvimento de um jogo

A maioria das *Engines* seguem um ciclo de execução da lógica de programação baseado em :

- **Inicialização** - Executado ao iniciar o jogo carregando bibliotecas básicas;

- **Carga** - Responsável por carregar os objetos ou módulos;

- **Atualização** - Estado de atualização constante responsável por apresentar todos os estados do jogo;

- **Finalização** - Executa as rotinas para descarregar o jogo;

## O que é Unreal Engine?

***

{% include image.html
    src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c6/Unreal%2BEngine_11_18_UE_Feed_Migration_Images_FEED_THUMB_UE_Logo_Generic-1400x788-c11642ffb55e268095321f5eb144f469beb0074f.jpg/800px-Unreal%2BEngine_11_18_UE_Feed_Migration_Images_FEED_THUMB_UE_Logo_Generic-1400x788-c11642ffb55e268095321f5eb144f469beb0074f.jpg"
    alt="Figura: Unreal Engine."
    caption="Figura: Unreal Engine - <https://www.unrealengine.com/en-US/>."
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

## O curso de Unreal Engine com C++ e Blueprint

***

Aprenda estruturas de desenvolvimento e lógicas de programação, utilizando *Blueprints* e *C++*.  O curso está associado a construção **Mecânica** do jogo pois nele definimos elementos como mecanismos de controle e elementos do conteúdo do jogo.  

### Habilidades que serão aprendidas

- Configuração e organização de projetos;
  
- Analisar e aplicar lógica de programação utilizando *Blueprint* e *C++*;
  
- Implementar regras de tempo e espaço;
  
- Implementar interface do usuário;
  
- Estruturar e configurar materiais, terrenos e iluminação;
  
- Implementar ambientes Multijogador;
  
- Implementar inteligência artificial;
  
- Construir a animação de personagens;
  
- Implementar Efeitos especiais.

### Categoria do Curso

| M             | D             | A         |
| :------------ | :------------ | :-------- |
| **Mecânicas** | **Dinâmicas** | Estéticas |
