---
title: Introdução ao Unreal Engine
excerpt: Conhecendo um pouco do desenvolvimento de jogoss.
permalink: /unreal-engine-capitulo-1/introducao-ao-unreal-engine
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 101
tags:
  - Curso
  - Desenvolvimento de Jogos
  - Iniciante 
---

É impossível conseguir qualquer coisa, se você não sabe o que quer. **Fallout**.
{: .notice}

Um jogo digital é um produto de software e como muitos projetos de desenvolvimento envolve diversas áreas de conhecimento na sua construção, como por exemplo:

- Programação;

- Arte 3D e 2D;

- Computação gráfica;

- Elementos de construção de narrativas;

- Efeitos sonoros.

{% include imagelocal.html
    src="unreal/notebook.webp"
    alt="Figura: Notebooks"
%}

Se você é como a maioria das pessoas, provavelmente joga videogame. Não importa se você é um jogador competitivo de e-sports atrás de muito dinheiro com seus jogos, ou se gosta de jogar spider ou candy crush como minha mãe, todo mundo joga. Mas você já pensou em fazê-los para o seu trabalho?[REF](https://medium.com/swlh/so-you-want-to-be-a-game-developer-e3b7f9f4ac70)

## 1. Programação de computadores

[Programação](https://pt.wikipedia.org/wiki/Programa%C3%A7%C3%A3o_de_computadores) é o processo de escrita, teste e manutenção de um programa de computador. O programa é escrito em uma linguagem de programação, embora seja possível, com alguma dificuldade, o escrever diretamente em linguagem de máquina. Diferentes partes de um programa podem ser escritas em diferentes linguagens.

Exemplo:

```cpp
#include <iostream>

int main() {
    std::cout << "Hello World!";
    return 0;
}
```

## 2. Arte 3D e 2D

A arte digital (2D e 3D) é a apresentação de personagens, ambiente e outros elementos que estão presentes nos jogos eletrônicos.

{% include imagelocal.html 
  src="unreal/jogos-2d-ou-jogos-3d.webp"
  alt="É melhor criar um jogo 2D ou 3D?"
  caption="Figura: É melhor criar um jogo 2D ou 3D?"
%}

Desenvolvimento de jogos evoluiu e a geração de hoje preza bastante pelo seu design mágico, estrutura, renderização e textura. Isso tem influenciado diretamente em saber se é melhor criar um jogo 2D ou 3D.[REF](https://www.crieseusjogos.com.br/e-melhor-criar-um-jogo-2d-ou-3d/)

## 3. Computação gráfica

{% include imagelocal.html
  src="unreal/Activemarker2.webp"
  alt="3D (computação gráfica)"
  caption="figura: 3D (computação gráfica)."
%}

Computação gráfica tridimensional são gráficos que usam representações tridimensionais de dados geométricos (geralmente cartesianos) que são armazenados em um computador com o propósito de realizar cálculos e renderizar imagens 2D. [REF](https://pt.wikipedia.org/wiki/3D_%28computa%C3%A7%C3%A3o_gr%C3%A1fica%29).

## 4. Elementos de construção de Narrativas

{% include imagelocal.html 
  src="unreal/escola-brasileira-de-games-Jornada-do-Herói.webp"
  alt="Jornada do Herói: Desenvolvimento de Narrativas para Jogos"
  caption="Figura: Jornada do Herói: Desenvolvimento de Narrativas para Jogos"
%}

Toda e qualquer história seja ela de aventura, terror, ação, romance ou qualquer outro gênero, é a responsável por chamar atenção do usuário e levar o jogador de encontro com uma nova aventura, conhecer um novo mundo qual ele irá mergulhar, quem são os personagens, seus medos, conquistas e aflições. [REF](https://escolabrasileiradegames.com.br/blog/jornada-do-heroi-desenvolvimento-de-narrativas-para-jogos)

## 5. Efeitos sonoros

{% include imagelocal.html
  src="unreal/sound_main_optimized.webp"
  alt="Game sound design: soundtrack, sound effects and how to combine them"
  caption="Figura: Game sound design: soundtrack, sound effects and how to combine them"
  idref="KREONIT,Hi"
  ref="https://kreonit.com/services/game-sound-design/"
%}

O design de som é uma parte muito importante de um jogo. Os desenvolvedores de jogos concordam que a música e os sons são poderosos condutores emocionais. E nosso objetivo é usar totalmente o som para tornar o jogo ainda melhor.

Como visto acima, diversos perfis profissionais de áreas distintas estão presentes na construção de um jogo, formando diversas equipes multiculturais,  o que aumenta a complexidade desse tipo de projeto quando pensamos na organização de tarefas e comunicação dos envolvidos.

## 6. Mecânica, Dinâmica e Estética (MDA)

O projeto de desenvolvimento de um jogo pode ser estruturado dividindo-o em componentes distintos, Mecânica - Mechanics,  Dinâmica - Dynamics e Estética Aesthetics, MDA, esta divisão ajuda a trabalhar com o design do jogo.

### 6.1. Mecânica

Descreve os componentes específicos do jogo, no nível de representação de dados e algoritmos.

- Componentes: Pontos, Avatares, Distintivos, tabelas de classificação;

- Controles: Tarefas, tempo, Perfis;

- Ações: Níveis, missões e grupos.
  
### 6.2. Dinâmica

Descreve o comportamento da mecânica quando ela é executada pelas ações do jogador e cada um dos resultados ao longo do tempo.

- Contexto;

- Escolhas;

- Consequências;

- Restrições;

- Continuação;

- Competição;

- Cooperação.
  
### 6.3. Estética

Descreve as respostas emocionais desejáveis evocadas no jogador, quando ele interage com o sistema de jogo, como por exemplo:

- Desafio;
  
- Criatividade;

- Comunidade;

- Elogio;

- Confiança;

- Conhecimento;

Quanto a construção da mecânica de um jogo é necessário utilizar uma linguagem de programação para implementar movimento, interação de personagens, inteligência artificial e outros elementos dinâmicos.

As linguagens de programação vem evoluindo para simplificar as rotinas e comandos assim agilizando o desenvolvimento e permitindo o programador focar no que deve ser feito escondendo alguns detalhes de como é feito.

**Informação:** Conhecer e entender como são feitos os jogos eletrônicos, é importante para determinar as técnicas utilizadas e ser capaz de aproveitar ou mesmo melhorar os jogos.
{: .notice--info}

Existem aplicações que auxiliam na produção de programas de computador ou jogos digitais, estas ferramentas abstraem a lógica complexa que faz com os objetos sejam apresentados de forma adequada na cena, no caso de jogos digitais. Tais ferramentas são chamadas de *Frameworks*.

## 7. O que é uma Engine e Framework?

{% include imagelocal.html
  src="unreal/game-engines-and-framework.webp"
  alt="Game Engine VS Game Framework"
  caption="Figura: Game Engine VS Game Framework"
%}

Antes que os motores de jogo viessem à existência, os jogos eram escritos como uma única entidade; o que significa que, se você quisesse construir outro jogo, você tinha que reescrever códigos quase inteiros novamente. Havia muitas outras preocupações também ao escrever jogos. Por vezes, os jogos foram concebidos de baixo para cima para utilizar o hardware de vídeo de forma otimizada...[REF](https://developerhouse.com/game-engine-vs-game-framework)

No desenvolvimento de jogos um *Framework* pode ser definido como um conjunto de bibliotecas que auxiliam a programação, sendo que uma *Engine* ou motor gráfico é mais completo pois abrange outros aspectos na produção de jogos.

Algumas *Engine* disponíveis no mercado.

1. [Unreal engine](https://www.unrealengine.com/pt-BR);

1. [Unity](https://unity.com/pt);

1. [GameMaker](https://gamemaker.io/pt-BR);

1. [Godot](https://godotengine.org/).

## 8. Ciclo da lógica do desenvolvimento de um jogo

A maioria das *Engines* seguem um ciclo de execução da lógica de programação baseado em :

- **Inicialização** - Executado ao iniciar o jogo carregando bibliotecas básicas;
- **Carga** - Responsável por carregar os objetos ou módulos;
- **Atualização** - Estado de atualização constante responsável por apresentar todos os estados do jogo;
- **Finalização** - Executa as rotinas para descarregar o jogo.

## 9. O que é Unreal Engine?

{% include imagelocal.html
  src="unreal/unreal-engine-logo.webp"
  alt="Unreal Engine"
%}

É uma *Engine* (motor gráfico) para desenvolvimento de jogos que engloba vários aspectos na sua produção, a seguir listamos algumas funcionalidades:

1. Edição e compilação da lógica de programação;

1. Apresentação de elementos visuais da cena do jogo;

1. Editor da lógica de animações e manipulação de esqueletos e malhas;

1. Editor de interfaces para comunicação com os jogadores (HUD);

1. Editor de sequencias de animação;

1. Editor de sons;

1. Editor para construção de materiais;

1. Editor de efeitos especiais utilizando partículas.
