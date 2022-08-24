---
title: Trabalhando como Unreal Engine e Visual Studio
description: O Unreal Engine é um Framework de desenvolvimento que incorpora vários editores e componentes para agilizar a construção de jogos e também um ambiente visual de programação abstraindo a lógica de programação.
tags: [Unreal Engine,desenvolvimento, visual studio]
layout: page
---

***

O **Unreal Engine** é um [Framework](https://pt.wikipedia.org/wiki/Framework) de desenvolvimento que incorpora vários editores e componentes para agilizar a construção de jogos e também um ambiente visual de programação abstraindo a lógica de programação.

Para que possamos programar em linguagem **C++** com **Unreal Engine** é necessário instalar o **Visual Studio** ou **Visual Code** e baixar os pacotes de desenvolvimento em **C++**.

A **Epic Games** utiliza um sistema para gerenciamento dos seus produtos, o **Inicializador da Epic Games** responsável por:

- Instalação e atualização de jogos;

- Navegação da loja de produtos;

- Instalação e atualização das versões do **Unreal Engine**;

![Figura: Gerenciamento de versões.](https://cafegeek.eti.br/unreal-engine/imagens/projeto/unreal_engine_control_version.webp "Figura: Gerenciamento de versões.")   

> Figura: Gerenciamento de versões.

## Como instalar o Unreal Engine?

Para instalar o **Unreal Engine** siga os seguintes passos:

1. Baixe e instale o [Inicializador da Epic Games](https://www.epicgames.com/store/pt-BR/download);

2. Inscreva-se para uma conta da Epic Games, se ainda não tiver uma;

3. Faça login no **Inicializador da Epic Games**;

4. Instale o **Unreal Engine** utilizando o menu `Unreal Engine` > `Biblioteca`.

5. Para instalar  os pacotes de desenvolvimento e o Visual Studio para programação com C++ baixe o Visual Studio em : [Download Visual Studio](https://visualstudio.microsoft.com/pt-br/?rr=https%3A%2F%2Fwww.google.com%2F);

6. Selecione os pacotes de programação:

    - Desenvolvimento de jogos com C++;

    - Desenvolvimento para Desktop com C++.

<img src="https://cafegeek.eti.br/unreal-engine/imagens/projeto/unreal_engine_visual_studio_update.webp" width="1265" height="auto" alt="Figura: Visual Studio Update para desenvolvimento de jogos." title="Figura: Visual Studio Update para desenvolvimento de jogos.">

> Figura: Visual Studio Update para desenvolvimento de jogos.

### Por que instalar o pacote Desktop com C++ ?

Porque muitas vezes é necessário testar uma funcionalidade ou mesmo testar um conceito da linguagem e ter o compilador disponível é uma mão na roda.

## Criando um projeto para jogos no Unreal Engine

Nesta seção vamos criar um projeto para jogos utilizando **C++** pois irá ajudar na compreensão da estrutura de pastas e arquivos do **Unreal Engine**. O nome do projeto será ProjetoAula e o usaremos em vários capítulos.

### Selecionando o tipo de projeto

Para construção do projeto vamos selecionar a categoria *Games* para que a Engine configure alguns parâmetros iniciais.

![Figura: Unreal 4 - Select or create New Project, Games.](https://cafegeek.eti.br/unreal-engine/imagens/projeto/blueprint_ue_select_new_project.webp "Figura: Unreal 4 - Select or create New Project, Games.")  

> Figura: Unreal 4 - Select or create New Project, Games.

### Escolhendo o Template

Para este projeto vamos escolher o `template blank` para que possamos entender os elementos do projeto e adicionar posteriormente outros pacotes.

![Figura: Select Template blank.](https://cafegeek.eti.br/unreal-engine/imagens/projeto/blueprint_ue_select_template.webp "Figura: Select Template blank.")

> Figura: Select Template blank.

**Templates** são modelos com elementos disponíveis para cada tipo de jogo escolhido.

## Configurando o projeto inicialmente

Em configuração de projeto escolha **C++** e `No Starter Content`, esta opção não vai instalar o pacote padrão de *assets* da **Epic Games** pois agora não é necessário, em seguida escolha uma pasta onde o projeto deverá ser instalado em `Select a Location for project to be stored`.

![Figura: Unreal engine project Settings.](https://cafegeek.eti.br/unreal-engine/imagens/projeto/blueprint_ue_project_settings.webp "Figura: Unreal engine project Settings.")

> Figura: Unreal engine project Settings.

### Tela inicial do Unreal Engine

Quando todos os passos anteriores forem concluídos corretamente a tela inicial deve aparecer.  

<img src="https://cafegeek.eti.br/unreal-engine/imagens/projeto/blueprint_ue_tela_inicial.webp" width="1265" height="auto" alt="Figura: Unreal Engine tela inicial." title="Figura: Unreal Engine tela inicial.">

> Figura: Unreal Engine tela inicial.

## Iniciando um projeto no Unreal Engine 5

A versão 5 tem uma apresentação um pouco diferente mas o conceito ainda é o mesmo dos passos anteriores.

<!--![Figura: Unreal 5 - Select or create New Project, Games.](https://cafegeek.eti.br/unreal-engine/imagens/projeto/unreal_engine_select_new_project.webp "Figura: Unreal 5 - Select or create New Project, Games")-->

<figure>
  <img src="https://cafegeek.eti.br/unreal-engine/imagens/projeto/unreal_engine_select_new_project.webp"
  alt="Figura: Unreal 5 - Select or create New Project, Games" title="Figura: Unreal 5 - Select or create New Project, Games">
  <figcaption>Figura: Unreal 5 - Select or create New Project, Games</figcaption>
</figure>

> Figura: Unreal 5 - Select or create New Project, Games.

<!-- ![Figura: Unreal 5 - Tela inicial.](https://cafegeek.eti.br/unreal-engine/imagens/projeto/unreal_engine_home_screen.webp "Figura: Unreal 5 - Tela inicial.") -->

<img src="https://cafegeek.eti.br/unreal-engine/imagens/projeto/unreal_engine_home_screen.webp" width="1265" height="auto" alt="Figura: Unreal 5 - Tela inicial." title="Figura: Unreal Engine tela inicial.">

> Figura: Unreal 5 - Tela inicial.

## Configurando o editor de código

Para programar utilizando **C++** no Unreal devemos configurar um editor de código para ser responsável pela compilação, organização e edição da linguagem. A configuração esta em :

`Menu` > `Editor Preferences` > `General` e `Source Code`, então escolha `Visualstudio`.   

![Figura: General - Source Code, Definindo o editor de código.](https://cafegeek.eti.br/unreal-engine/imagens/projeto/unreal_engine_editor_codigo.webp "Figura: General - Source Code, Definindo o editor de código.")   

> Figura: General - Source Code, Definindo o editor de código.

### Qual editor eu escolho, Visual Code ou Visual Studio?

Os dois são ótimos editores de código mas o Visual Code tem uma apresentação mais enxuta e quando se trata de utilizar ele para outras lingagens, como por exemplo Pyhton, ou mesmo editar um arquivo de formato Markdown é uma boa escolha.

## Entendo as pastas criadas

Após criar o projeto vamos verificar como estão as pastas criadas pela *engine*, utilizando o `explorer` do Windows, navegue até a pasta do projeto para verificar os arquivos criados, devem aparecer as seguintes pastas e arquivos:

```bash
|-- .vs
|-- Binaries
|-- Config
|-- Content
|-- Intermediate
|-- Saved
|-- Source
|-- ProjetoAula.sln
|-- ProjetoAula.uproject
```

A seguir vamos entender as pastas do projeto.

### Pasta de código C++ - Source

A pasta `Source` contém arquivos com código fonte em **C++** e o arquivo com extensão *uproject* é o principal arquivo do projeto, segue abaixo a configuração inicial.

```bash
|-- Source
		|-- ProjetoAula
		|		|-- ProjetoAula.cpp
		|		|-- ProjetoAula.h
		|		|-- ProjetoAula.Build.cpp    
		|-- ProjetoAulaEditor.Target.cs    
		|-- ProjetoAula.Target.cs
```

### Pasta principal do projeto - Content

`Content` é a principal pasta, pois nela vão ficar contidos todos os arquivos do jogo, em outras palavras esta pasta é o ponto de montagem do projeto como veremos nos próximos capítulos.

### Pastas temporárias que podem ser removidas

As pastas abaixo podem ser removidas pois podemos construir a qualquer momento quando compilar o projeto.

```bash
|-- Binaries
|-- Build
|-- Intermediate
|-- Saved
```

### Nomenclatura de pastas

É recomendado que os arquivos e pastas devam ter um padrão de nomenclatura para melhor organização do projeto, abaixo duas boas recomendações de organização, discutiremos mais nos próximos capítulos.    
- [Directory Structure](https://docs.unrealengine.com/en-US/Engine/Basics/DirectoryStructure/index.html "Directory Structure Overview of the directories that make up the engine and game projects.");

- [UE5 Style Guide](https://github.com/Allar/ue4-style-guide/blob/master/README.md#unreal-engine-4-linter-plugin "Gamemakin UE4 Style Guide() { A mostly reasonable approach to Unreal Engine 4").

## Compilando o projeto usando o Windows Explorer

Para recompilar o projeto e recriar os arquivos podemos utilizar o `explorer` do Windows seguindo os passos abaixo:

1. Apague as pastas `Binaries`, `Build`, `Intermediate` e `Saved`;

1. Click com botão direito do mouse no arquivo **ProjetoAula.uproject**;

1. Escolha a opção `Generate Visual Studio project files`;

    ![Figura: Recriando os arquivos do projeto, Generate Visual Studio Project files](https://cafegeek.eti.br/unreal-engine/imagens/projeto/blueprint_explorer_generate_vs.webp "Figura: Recriando os arquivos do projeto, Generate Visual Studio Project files")

    > Figura: Recriando os arquivos do projeto, Generate Visual Studio Project files.

1. Aguarde o termino da operação e abra o projeto.

## Organizando pastas e logo do projeto

A seguir vamos organizar as pastas do projeto *ProjetoAula*, construído no **Unreal Engine**, e vamos configurá-lo.

### Como criar pastas de trabalho?

No **Unreal Egnine** em `Content Drawer` utilizando botão direito do mouse clique em `New Folder` para criar pastas.

![Figura: Content Drawer](https://cafegeek.eti.br/unreal-engine/imagens/projeto/unreal_engine_content_drawer.webp "Figura: Content Drawer")

> Figura: Content Drawer.

### Defina e utilize uma Nomenclatura e organização de pastas

A organização de arquivos e pastas dentro dos projetos de desenvolvimento de softwares é bastante relevante para reduzir o tempo de programação e custo.

Em projetos de desenvolvimento de jogos, no **Unreal Engine**, temos diversos tipos de arquivos com caraterísticas distintas que influenciam na sua forma de armazenamento, como por exemplo:

- Código **C++**;

- Lógica de desenvolvimento utilizando Blueprints;

- Arquivos de imagens, como texturas e outros;

- Arquivos de som;

- Arquivos binários em geral.  

Temos também equipes heterogêneas trabalhando no mesmo projeto e até na mesma estrutura de pastas, como por exemplo:

- Programadores;

- Level Design;

- Artistas gráficos;

- Artistas de efeitos de som e músicos.

Por conseguinte para um maior gerenciamento pelas equipes do projeto  podemos definir pastas com nomenclaturas e organização adequadas ao projeto, abaixo vamos relacionar algumas sugestões.

1. Sugestão 1.
```bash
|-- Content
		|-- Blueprints
		|		|-- Core
		|		|-- Characters
		|		|-- Elements
		|-- Assets
		|		|-- Images
		|		|-- StructureMesh
		|		|-- Materials
		|-- Maps
		|		|-- Level1
		|-- UI
		|-- Animations
```

1. Sugestão 2.
```bash
|-- Content
		|-- ProjetoAula
			|-- Art
			|	|-- Industrial
			|	|	|-- Ambient
			|	|	|-- Machinery
			|	|	|-- Pipes
			|	|-- Nature
			|	|	|-- Ambient
			|	|	|	|-- Foliage
			|	|	|	|-- Rocks
			|	|	|	|-- Trees
			|	|-- Office
			|-- Characters
			|  |-- Bob
			|  |-- Common
			|  |  |-- Animations
			|  |  |-- Audio
			|  |-- Jack
			|  |-- Steve
			|  |-- Zoe						
			|-- Core
			|	|-- Characters
			|	|-- Engine
			|	|-- GameModes
			|	|-- Interactables
			|	|-- Pickups
			|	|-- Weapons
			|-- Maps
			|	|-- Level1
			|	|-- Level2
```

### Os benefícios na organização das pastas

Separar a pasta do projeto `Content` de outras pastas pode facilitar e trazer vários benefícios durante o desenvolvimento do projeto, abaixo elencamos alguns:

1. Versionamento - pastas com diferentes versões;

1. Isolar pacotes de testes e *Marketplace*;

1. DLC ou subprojetos - podemos administrar separadamente projetos relacionados;

1. Biblioteca de Materiais - podemos migrar pasta de materiais e compartilhar materiais sem muitos problemas definindo um pasta de nível superior.

Exemplo:
```bash
|-- Content
	|-- ProjetoAula
	|-- ProjetoAulaTestes
	|-- ProjetoAulaArquitetura
	|-- StarterContent
	|-- FPS_Assault_Pack
	|-- MaterialLibrary
	|	|-- M_Master
```		

## Configurando o projeto

Preparar o projeto antes de começar o desenvolvimento é importante para que possamos otimizar algumas tarefas e preparar o jogo com a configuração inicial, neste passo vamos configurar alguns parâmetros do projeto.

Nos próximos capítulos vamos utilizar outras opções do menu de configuração como por exemplo o [mapeamento de *Input* (teclas ou controles)](http://cafegeek.eti.br/unreal-engine/trabalhando_com_logica_movimentacao_de_personagem.html#13).

### Adicionando um *Level* na inicialização do projeto

Para que um *level* ou mapa seja carregado ao iniciar o projeto siga os seguintes passos:  

1. Salve o *level* atual na pasta `Maps` :
    `File` > `Save Current Level As` com o nome `LevelTest`;
1. Para configurar a inicialização do projeto utilizando o `LevelTest` utilize o menu :     
    `Edit` > `Project Settings` e depois `Maps & Modes`;   

	![Figura: Project - Maps & Modes.](https://cafegeek.eti.br/unreal-engine/imagens/projeto/unreal_engine_maps_modes.webp "Figura: Project - Maps & Modes.")

	> Figura: Project - Maps & Modes.

- `Edit Startup Level` - Seleciona o *Level* que deverá ser carregado no início do jogo, neste caso é `LevelTest`;
- `Game default Map` - Seleciona o *Level* que é mais usado.

### Configurando as imagens  do projeto

Para alterar as imagens de apresentação do projeto, seja ícone ou tela de apresentação (*splash*) utilizamos o menu :

`Project Settings` opção `Plataforms` > `Windows` e altere a imagens.

<!-- ![Figura: Project icon.](https://cafegeek.eti.br/unreal-engine/imagens/projeto/unreal_engine_project_icon.webp "Figura: Project icon.")		-->

<figure>
  <img src="https://cafegeek.eti.br/unreal-engine/imagens/projeto/unreal_engine_project_icon.webp"  
alt="Figura: Project icon." title="Figura: Project icon.">
  <figcaption>Figura: Project icon.</figcaption>
</figure>

> Figura: Project icon.

Certifique-se de produzir o ícone como um arquivo .ico (que não é PNG, mas pode ser convertido usando ferramentas online, por exemplo) e 256x256.
