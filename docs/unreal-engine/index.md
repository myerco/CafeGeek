---
title: Unreal Engine com C++ e Blueprint
description: Aprenda estruturas de desenvolvimento e lógicas de programação, utilizando Blueprints e C++.
keywords: [Desonvolvimento com Unreal Engine, Jogos com Unreal Engine]
tags: [Unreal Engine, jogos digitais, desenvolvimento, Blueprint, c++, game digital]
layout: page
---

Aprenda estruturas de desenvolvimento e lógicas de programação, utilizando *Blueprints* e *C++*, bem como a construção de elementos de apresentação de jogos como por exemplo materiais, terrenos, inteligência artificial e conexões multiplayer.  

**Habilidades que serão aprendidas**

- Configuração e organização de projetos;
- Analisar e aplicar lógica de programação utilizando *Blueprint* e *C++*;
- Implementar regras de tempo e espaço;
- Implementar interface do usuário;
- Estruturar e configurar materiais, terrenos e iluminação;
- Implementar ambientes Multijogador;
- Implementar inteligência artificial;
- Construir a animação de personagens;
- Implementar Efeitos especiais.


[**Capítulo I - O Unreal Engine e sua lógica de programação.**](#1)

1. [**Desenvolvendo jogos digitais**](#1.1)
    1. [O que é uma Engine e Framework?](#1.2)
    1. [Ciclo da lógica do desenvolvimento de um jogo](#1.3)
    1. [O que é Unreal Engine?](#1.4)
1. [Como instalar o Unreal Engine?](unreal_engine_como_instalar_o_unreal_engine.html)
1. [Organizando pastas e logo do projeto](unreal_engine_organizando_pastas_e_logo.html)
1. [Controle de versão com GitHub](unreal_engine_controle_de_versao_com_github.html)
1. [Interface e Editores](interface_e_editores.html)  
1. [Programação visual com Blueprint](unreal_engine_entendo_blueprint.html)
1. [Programação C++ no Unreal Engine](unreal_engine_entendo_cpp.html)
1. [Trabalhando com variáveis](unreal_engine_trabalhando_com_variaveis.html)  
1. [Estruturas de controle de fluxo](unreal_engine_estruturas_de_controle_de_fluxo.html)
1. [Manipulando Arrays](unreal_engine_manipulando_array.html)  
1. [Utilizando Enums](unreal_engine_enum.html)    

***
**Capítulo II - Atores e movimentação**

1. [Implementando Atores](actor_atores.html)
1. [Utilizando Eventos, funções e macros](estruturando_logica_utilizando_eventos_funcoes_macros.html)  
1. [Implementando a movimentação do personagem](trabalhando_com_logica_movimentacao_de_personagem.html)    
1. [Comunicação entre Blueprints](comunicacao_entre_blueprint.html)    
1. [Delta time e sistema de coordenadas](deltatime_sistema_coordenadas.html)

***

**Capítulo III - Estruturas de dados e Interface com usuário**

1. [Variáveis estruturadas ou Structure](structure_variaveis_estruturadas.html)  
1. [Tabelas de dados ou Data tables - ](data_tables.html)
1. [Game Instance, Game State e Game Mode](unreal_engine_gameinstance_state_mode.html)
1. [Implementando a Interface com o jogador](unreal_engine_hud_interface.html)
1. [Lógica de programação dos objetos da interface](unreal_engine_hud_logica.html)

***
**Capítulo IV - Materiais e Landscape**

1. [Introdução aos Materiais](unreal_engine_material_introducao_aos_materiais.html)
1. [Construindo Materiais e entendo a lógica](unreal_engine_material_construindo_materiais_entendendo_a_logica.html)
1. [Material Instance](unreal_engine_material_instance.html)
1. [Materiais e Blueprint](unreal_engine_material_blueprint.html)
1. [Trabalhando com Iluminação](iluminacao.html)
1. [Criando terrenos - Landscape](landscape.html)  

***
**Capítulo V - Animação de personagens**

1. [Introdução a animação de personagens](unreal_engine_animacao_introducao.html)
1. [Preparando o projeto](unreal_engine_animacao_preparando_o_projeto.html)
1. [Utilizando Blend Space](unreal_engine_animacao_blend_space.html)        
1. [Implementando a Lógica da animação](unreal_engine_animacao_animation_blueprint.html)        
1. [Implementando a mira](unreal_engine_animacao_aim_offset.html)
1. [Trabalhando com Animação 2D](unreal_engine_animacao2d.html)

***
**Capítulo VI - Inteligência Artificial**
1. [Inteligência Artificial](inteligenciaartificial.html)

***
**Capítulo VII - Multiplayer em C++**            
1. [Multiplayer](multiplayer.html)

***
**Capítulo VIII - Efeitos especiais**
1. [Sequencer](#)
1. [Utilizando Niagara](#)

<a name="1"></a>
## Capítulo I - O Unreal Engine e sua lógica de programação

<a name="1.1"></a>
## 1. Desenvolvendo jogos digitais

![Figura: So, You Want to Be a Game Developer? - https://medium.com/swlh/so-you-want-to-be-a-game-developer-e3b7f9f4ac70](https://miro.medium.com/max/875/0*OlVTuxFz-Qn7oTUn "Figura: So, You Want to Be a Game Developer? - https://medium.com/swlh/so-you-want-to-be-a-game-developer-e3b7f9f4ac70")

> *Figura: So, You Want to Be a Game Developer? - https://medium.com/swlh/so-you-want-to-be-a-game-developer-e3b7f9f4ac70 .*

O desenvolvimento de jogos digitais envolve diversas áreas de conhecimento como por exemplo:
- Programação de computadores;
- Arte 3D e 2D;
- Computação gráfica;
- Elementos de construção de Narrativas;
- Efeitos sonoros;

Na construção da mecânica de um jogo é necessário utilizar uma linguagem de programação para implementar movimento, interação de personagens, inteligência artificial e outros elementos dinâmicos.
As linguagens de programação vem evoluindo para simplificar as rotinas e comandos assim agilizando o desenvolvimento e permitindo o programador focar no que deve ser feito escondendo alguns detalhes de como é feito.

> Conhecer e entender como é feito é importante para determinar as técnicas utilizadas e ser capaz e aproveitar ou mesmo melhorar os jogos.

Existem aplicações que auxiliam na produção de programas de computador ou jogos digitais, estas ferramentas abstraem a lógica complexa que faz com os objetos sejam apresentados de forma adequada na cena, no caso de jogos digitais. Tais ferramentas são chamadas de *Frameworks* [[1](#r1)]

<a name="1.2"></a>
## 2. O que é uma Engine e Framework?

![Figura: Game Engine VS Game Framework - https://developerhouse.com/game-engine-vs-game-framework/](https://developerhouse.com/wp-content/uploads/2020/10/game-engines-and-framework.jpg "Figura: Game Engine VS Game Framework - https://developerhouse.com/game-engine-vs-game-framework/")

> *Figura: Game Engine VS Game Framework - https://developerhouse.com/game-engine-vs-game-framework/ .*

No desenvolvimento de jogos um *Framework* pode ser definido como um conjunto de bibliotecas que auxiliam a programação, sendo que uma *engine* ou motor gráfico é mais completo pois abrange outros aspectos na produção de jogos.[[2](#r2)]

Algumas *Engine*.

1. Unreal engine;
1. Unity;
1. GameMaker;

<a name="1.3"></a>
## 3. Ciclo da lógica do desenvolvimento de um jogo
A maioria das *engines* seguem um ciclo de execução da lógica de programação baseado em :

- **Inicialização** - Executado ao iniciar o jogo carregando bibliotecas básicas;
- **Carga** - Responsável por carregar os objetos ou módulos;
- **Atualização** - Estado de atualização constante responsável por apresentar todos os estados do jogo;
- **Finalização** - Executa as rotinas para descarregar o jogo;

<a name="1.4"></a>
## 4. O que é Unreal Engine?
![Figura: Unreal Engine - https://www.unrealengine.com/en-US/](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c6/Unreal%2BEngine_11_18_UE_Feed_Migration_Images_FEED_THUMB_UE_Logo_Generic-1400x788-c11642ffb55e268095321f5eb144f469beb0074f.jpg/800px-Unreal%2BEngine_11_18_UE_Feed_Migration_Images_FEED_THUMB_UE_Logo_Generic-1400x788-c11642ffb55e268095321f5eb144f469beb0074f.jpg "Figura: Unreal Engine - https://www.unrealengine.com/en-US/")

> *Figura: Unreal Engine - https://www.unrealengine.com/en-US/ .*

É uma *Engine* (motor gráfico) para desenvolvimento de jogos que engloba vários aspectos na sua produção, a segui listamos algumas funcionalidades:

1. Edição e compilação da lógica de programação;
1. Apresentação de elementos visuais da cena do jogo;
1. Editor da lógica de animações e manipulação de esqueletos e malhas;
1. Editor de interfaces para comunicação com os jogadores (HUD);
1. Editor de sequencias de animação;
1. Editor de sons;
1. Editor para construção de materiais;
1. Editor de efeitos especiais utilizando partículas;
