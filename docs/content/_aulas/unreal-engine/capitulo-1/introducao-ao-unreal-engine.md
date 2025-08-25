---
title: Introdução ao Unreal Engine
categories: 
  - "unreal-engine"
  - "capitulo-1"
excerpt: Conhecendo um pouco do desenvolvimento de jogos.
date: 2024-03-01T08:48:05-04:00
num: 1
order: 1
sidebar:
  nav: unreal-engine
---

> É impossível conseguir qualquer coisa se você não sabe o que quer.  
> — *Fallout*

Este capítulo apresenta uma visão geral do desenvolvimento de jogos digitais, abordando as principais áreas envolvidas, conceitos fundamentais e o papel das engines e frameworks. Ao final, você entenderá o que é a Unreal Engine e por que ela é uma das ferramentas mais utilizadas na indústria.

Um jogo digital é um produto de software e, como muitos projetos de desenvolvimento, envolve diversas áreas de conhecimento em sua construção, como:

- Programação
- Arte 3D e 2D
- Computação gráfica
- Elementos de construção de narrativas
- Efeitos sonoros

## 1. Programação de computadores

[Programação](https://pt.wikipedia.org/wiki/Programa%C3%A7%C3%A3o_de_computadores) é o processo de escrita, teste e manutenção de um programa de computador. O programa é escrito em uma linguagem de programação, embora seja possível, com alguma dificuldade, escrevê-lo diretamente em linguagem de máquina. Diferentes partes de um programa podem ser escritas em diferentes linguagens.

Exemplo:

```cpp
#include <iostream>

int main() {
    std::cout << "Hello World!";
    return 0;
}
```

## 2. Arte 3D e 2D

A arte digital (2D e 3D) é a apresentação de personagens, ambientes e outros elementos presentes nos jogos eletrônicos.

{% include imagelocal.html 
  src="unreal/jogos-2d-ou-jogos-3d.webp"
  alt="É melhor criar um jogo 2D ou 3D?"
  caption="Figura: É melhor criar um jogo 2D ou 3D?"
%}

O desenvolvimento de jogos evoluiu e a geração atual valoriza bastante o design, a estrutura, a renderização e as texturas. Isso influencia diretamente na decisão entre criar um jogo 2D ou 3D. [REF](https://www.crieseusjogos.com.br/e-melhor-criar-um-jogo-2d-ou-3d/)

## 3. Computação gráfica

{% include imagelocal.html
  src="unreal/Activemarker2.webp"
  alt="3D (computação gráfica)"
  caption="Figura: 3D (computação gráfica)."
%}

Computação gráfica tridimensional são gráficos que usam representações tridimensionais de dados geométricos (geralmente cartesianos) que são armazenados em um computador com o propósito de realizar cálculos e renderizar imagens 2D. [REF](https://pt.wikipedia.org/wiki/3D_%28computa%C3%A7%C3%A3o_gr%C3%A1fica%29)

## 4. Elementos de construção de narrativas

{% include imagelocal.html 
  src="unreal/escola-brasileira-de-games-Jornada-do-Herói.webp"
  alt="Jornada do Herói: Desenvolvimento de Narrativas para Jogos"
  caption="Figura: Jornada do Herói: Desenvolvimento de Narrativas para Jogos"
%}

Toda história, seja de aventura, terror, ação, romance ou qualquer outro gênero, é responsável por chamar a atenção do usuário e levar o jogador a uma nova aventura, conhecer um novo mundo, descobrir quem são os personagens, seus medos, conquistas e aflições. [REF](https://escolabrasileiradegames.com.br/blog/jornada-do-heroi-desenvolvimento-de-narrativas-para-jogos)

## 5. Efeitos sonoros

{% include imagelocal.html
  src="unreal/sound_main_optimized.webp"
  alt="Game sound design: soundtrack, sound effects and how to combine them"
  caption="Figura: Game sound design: soundtrack, sound effects and how to combine them"
  idref="KREONIT,Hi"
  ref="https://kreonit.com/services/game-sound-design/"
%}

O design de som é uma parte muito importante de um jogo. Desenvolvedores concordam que a música e os sons são poderosos condutores emocionais. O objetivo é usar o som para tornar o jogo ainda melhor.

Como visto acima, diversos perfis profissionais de áreas distintas estão presentes na construção de um jogo, formando equipes multidisciplinares, o que aumenta a complexidade desse tipo de projeto quando pensamos na organização de tarefas e comunicação dos envolvidos.

## 6. Mecânica, Dinâmica e Estética (MDA)

O projeto de desenvolvimento de um jogo pode ser estruturado dividindo-o em componentes distintos: Mecânica (*Mechanics*), Dinâmica (*Dynamics*) e Estética (*Aesthetics*), conhecidos como MDA. Essa divisão ajuda a trabalhar com o design do jogo.

### 6.1. Mecânica

Descreve os componentes específicos do jogo, no nível de representação de dados e algoritmos.

- Componentes: Pontos, avatares, distintivos, tabelas de classificação
- Controles: Tarefas, tempo, perfis
- Ações: Níveis, missões e grupos

### 6.2. Dinâmica

Descreve o comportamento da mecânica quando ela é executada pelas ações do jogador e os resultados ao longo do tempo.

- Contexto
- Escolhas
- Consequências
- Restrições
- Continuação
- Competição
- Cooperação

### 6.3. Estética

Descreve as respostas emocionais desejáveis evocadas no jogador ao interagir com o sistema de jogo, como por exemplo:

- Desafio
- Criatividade
- Comunidade
- Elogio
- Confiança
- Conhecimento

Quanto à construção da mecânica de um jogo, é necessário utilizar uma linguagem de programação para implementar movimento, interação de personagens, inteligência artificial e outros elementos dinâmicos.

As linguagens de programação vêm evoluindo para simplificar as rotinas e comandos, agilizando o desenvolvimento e permitindo ao programador focar no que deve ser feito, abstraindo detalhes de implementação.

**Informação:** Conhecer e entender como são feitos os jogos eletrônicos é importante para determinar as técnicas utilizadas e ser capaz de aproveitar ou mesmo melhorar os jogos.
{: .notice--info}

Existem aplicações que auxiliam na produção de programas de computador ou jogos digitais. Essas ferramentas abstraem a lógica complexa que faz com que os objetos sejam apresentados de forma adequada na cena. No caso de jogos digitais, tais ferramentas são chamadas de *frameworks*.

## 7. O que é uma Engine e Framework?

{% include imagelocal.html
  src="unreal/game-engines-and-framework.webp"
  alt="Game Engine VS Game Framework"
  caption="Figura: Game Engine VS Game Framework"
%}

Antes que os motores de jogo viessem à existência, os jogos eram escritos como uma única entidade; ou seja, se você quisesse construir outro jogo, teria que reescrever quase todo o código novamente. Havia muitas outras preocupações ao escrever jogos, como otimizar o uso do hardware de vídeo. [REF](https://developerhouse.com/game-engine-vs-game-framework)

No desenvolvimento de jogos, um *framework* pode ser definido como um conjunto de bibliotecas que auxiliam a programação, enquanto uma *engine* ou motor gráfico é mais completa, pois abrange outros aspectos da produção de jogos.

Algumas *engines* disponíveis no mercado:

1. [Unreal Engine](https://www.unrealengine.com/pt-BR)
2. [Unity](https://unity.com/pt)
3. [GameMaker](https://gamemaker.io/pt-BR)
4. [Godot](https://godotengine.org/)

## 8. Ciclo da lógica do desenvolvimento de um jogo

A maioria das *engines* segue um ciclo de execução da lógica de programação baseado em:

- **Inicialização** – Executado ao iniciar o jogo, carregando bibliotecas básicas
- **Carga** – Responsável por carregar os objetos ou módulos
- **Atualização** – Estado de atualização constante responsável por apresentar todos os estados do jogo
- **Finalização** – Executa as rotinas para descarregar o jogo

## 9. O que é Unreal Engine?

{% include imagelocal.html
  src="unreal/unreal-engine-logo.webp"
  alt="Unreal Engine"
%}

A Unreal Engine é uma *engine* (motor gráfico) para desenvolvimento de jogos que engloba vários aspectos da produção. A seguir, listamos algumas funcionalidades:

1. Edição e compilação da lógica de programação
2. Apresentação de elementos visuais da cena do jogo
3. Editor da lógica de animações e manipulação de esqueletos e malhas
4. Editor de interfaces para comunicação com os jogadores (HUD)
5. Editor de sequências de animação
6. Editor de sons
7. Editor para construção de materiais
8. Editor de efeitos especiais utilizando partículas

## Resumo

Neste capítulo, você conheceu as principais áreas do desenvolvimento de jogos, o conceito de engine e framework, e o ciclo de desenvolvimento de um jogo. Também foi apresentada a Unreal Engine, que será explorada em detalhes nos próximos capítulos.

Este capítulo apresenta uma visão geral do desenvolvimento de jogos digitais, abordando as principais áreas envolvidas, conceitos fundamentais e o papel das engines e frameworks. Ao final, você entenderá o que é a Unreal Engine e por que ela é uma das ferramentas mais utilizadas na indústria.
