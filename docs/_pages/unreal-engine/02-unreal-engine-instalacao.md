---
title:  Instalação e Configuração
excerpt: O Unreal Engine é um Framework de desenvolvimento que incorpora vários editores e componentes para agilizar a construção de jogos e também um ambiente visual de programação abstraindo a lógica de programação.
permalink: /pages/unreal-engine/instalacao-configuracao
last_modified_at: 2023-03-28T08:48:05-04:00
toc: true  
sidebar:
    nav: dev_unreal
categories:
  - Unreal Engine
tags:
  - instalação
  - configuração
---


## 1. O Unreal Engine

O **Unreal Engine** é um [Framework](https://pt.wikipedia.org/wiki/Framework) de desenvolvimento que incorpora vários editores e componentes para agilizar a construção de jogos e também um ambiente visual de programação abstraindo a lógica de programação.

O **Unreal Engine** utiliza a linguagem C++ e um ambiente de programação visual denominado *Blueprint*, para que possamos habilitar a programação em linguagem **C++** é necessário instalar o **Visual Studio** ou **Visual Code** e baixar os pacotes de desenvolvimento em **C++**.

Para facilitar a instalação e atualização do ambiente de desenvolvimento dos projetos, a **Epic Games** utiliza um sistema para gerenciamento dos seus produtos, o **Inicializador da Epic Games** responsável por:

- Instalação e atualização de jogos;

- Navegação da loja de produtos;

- Instalação e atualização das versões do **Unreal Engine**;

- Instalação e atualização de uma biblioteca de *plugins* e *assets* (recursos).

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-control-version.webp"
    alt="Figura: Gerenciamento de versões."
    caption="Inicializador da Epic Games > Versões Instaladas, Lista de versões instaladas do Unreal Engine."
%}

## 2. Como instalar o Unreal Engine?

Para instalar o Unreal Engine siga os seguintes passos:

1. Baixe e instale o [Inicializador da Epic Games](https://www.epicgames.com/store/pt-BR/download);

1. Crie uma conta na Epic Games, se ainda não tiver uma;

1. Faça login no **Inicializador da Epic Games**;

1. Instale o **Unreal Engine** utilizando o menu `Unreal Engine` > `Biblioteca`.

### 2.1. Instalando o Visual Studio para programar com C++

Para instalar  os pacotes de desenvolvimento e o Visual Studio para programação com C++ baixe o Visual Studio em : [Download Visual Studio](https://visualstudio.microsoft.com/pt-br/?rr=https%3A%2F%2Fwww.google.com%2F).

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-visual-studio-installer.webp"
    alt="Figura: Visual Studio Installer - Instalação."
    caption="Permite instalar e modificar diversas versões do Visual Studio."
%}

Depois de instalar o Visual Studio é necessário selecionar os seguintes pacotes de programação:

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-visual-studio-update.webp"
    alt="Figura: Visual Studio Installer - Modificar."
    caption="Usando o Visual Studio Installer podemos instalar ou remover (modificar), os pacotes necessários para o desenvolvimento de jogos."
%}

- Desenvolvimento de jogos com C++;

- Desenvolvimento para Desktop com C++.

**Por que instalar o pacote Desktop com C++ ?** Porque muitas vezes é necessário testar uma funcionalidade ou mesmo testar um conceito da linguagem e ter o compilador disponível é uma mão na roda.
{: .notice--info}

## 3. Criando um projeto para jogos no Unreal Engine

Nesta seção vamos criar um projeto para jogos utilizando **C++**, pois, irá ajudar na compreensão da estrutura de pastas e arquivos do **Unreal Engine**. O nome do projeto será ProjetoAula e o usaremos em vários capítulos.

### 3.1. Criando um projeto no Unreal Engine 4.X

Para construção do projeto podemos clicar no versão disponível na janela do inicializador ou na opção **Inicializar** no campo superior direito, após a inicialização da **Unreal** é necessário selecionar o tipo de projeto para que a *Engine* configure alguns parâmetros iniciais.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine_select_new_project.webp"
    alt="Figura: Unreal 4 - Select or create New Project, Games."
    caption="Selecione a opção Games para construção do projeto."
%}

#### 3.1.1. Escolhendo o Template

Para este projeto vamos escolher o `template blank`, modelo vazio, significa que não vamos instalar objetos e recursos adicionais no projeto, pois, vamos realizar essa tarefa posteriormente para que possamos entender a estrutura do projeto.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-select-template.webp"
    alt="Figura: Select Template blank"
    caption="Selecionando um modelo para utilizar no projeto."
%}

**Templates:** São modelos com recursos disponíveis para cada tipo de jogo escolhido.
{: .notice--info}

#### 3.1.2. Configuração inicial do projeto

Em configuração de projeto escolha **C++** e `No Starter Content`, esta opção não vai instalar o pacote padrão de *assets* da **Epic Games** pois agora não é necessário, em seguida escolha uma pasta onde o projeto deverá ser instalado em `Select a Location for project to be stored`.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-project-settings.webp"
    alt="Figura: Unreal engine project Settings."
    caption="Configurando os parâmetros do projeto."
%}

#### 3.1.3. Tela inicial do Unreal Engine

Quando todos os passos anteriores forem concluídos corretamente a tela inicial deve aparecer.  

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-tela-inicial.webp"
    alt="Figura: Unreal Engine tela inicial."
    caption="Ambiente de desenvolvimento integrado com editor visual de cena, paletas de objetos e suas propriedades."
%}

### 3.2. Iniciando um projeto no Unreal Engine 5

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-5-select-new-project.webp"
    alt="Figura: Unreal 5 - Select or create New Project, Games"
    caption="A versão 5 tem uma apresentação um pouco diferente mas o conceito ainda é o mesmo dos passos anteriores."
%}

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-home-screen.webp"
    alt="Figura: Unreal 5 - Tela inicial."
    caption="Paleta de comandos com ícones menores o novo navegador de conteúdo (Content Drawer)."
%}

## 4. Configurando o editor de código

Para programar utilizando **C++** no Unreal devemos configurar um editor de código para ser responsável pela compilação, organização e edição da linguagem. A configuração esta em :

`Menu` > `Editor Preferences` > `General` e `Source Code`, então escolha `Visualstudio`.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-editor-codigo.webp"
    alt="Figura: Editor Preferences > General > Source Code."
    caption="Em Source Code Editor escolha o editor da sua preferência."
%}

**Qual editor eu escolho, Visual Code ou Visual Studio?**  Os dois são ótimos editores de código mas o Visual Code tem uma apresentação mais enxuta e quando se trata de utilizar ele para outras linguagens, como por exemplo Pyhton, ou mesmo editar um arquivo de formato Markdown é uma boa escolha.
{: .notice--info}

## 5. Entendo as pastas criadas

Após criar o projeto vamos verificar como estão as pastas criadas pela *engine*, utilizando o `explorer` do Windows, navegue até a pasta do projeto para verificar os arquivos criados, devem aparecer as seguintes pastas e arquivos:

```bash
├── .vs
├── Binaries
├── Config
├── Content
├── Intermediate
├── Saved
├── Source
├── ProjetoAula.sln
└── ProjetoAula.uproject
```

A seguir vamos entender as pastas do projeto.

### 5.1. Pasta de código C++ - Source

A pasta `Source` contém arquivos com código fonte em **C++** e o arquivo com extensão *uproject* é o principal arquivo do projeto, segue abaixo a configuração inicial.

```bash
├── Source
  ├── ProjetoAula
  |  ├── ProjetoAula.cpp
  |  ├── ProjetoAula.h
  |  └── ProjetoAula.Build.cpp    
  ├── ProjetoAulaEditor.Target.cs    
  └── ProjetoAula.Target.cs
```

### 5.2. Pasta principal do projeto - Content

`Content` é a principal pasta, pois nela vão ficar contidos todos os arquivos do jogo, em outras palavras esta pasta é o ponto de montagem do projeto como veremos nos próximos capítulos.

### 5.3. Pastas temporárias que podem ser removidas

As pastas abaixo podem ser removidas pois podemos construir a qualquer momento quando compilar o projeto.

```bash
├── Binaries
├── Build
├── Intermediate
└── Saved
```

### 5.4. Nomenclatura de pastas

É recomendado que os arquivos e pastas devam ter um padrão de nomenclatura para melhor organização do projeto, abaixo duas boas recomendações de organização, discutiremos mais nos próximos capítulos.

**[UE5 Style Guide](https://github.com/Allar/ue4-style-guide/blob/master/README.md#unreal-engine-4-linter-plugin "Gamemakin UE4 Style Guide() { A mostly reasonable approach to Unreal Engine 4"):** Gamemakin UE4 Style Guide() - A mostly reasonable approach to Unreal Engine 4.
{: .notice--info}

## 6. Organizando as pastas

A seguir vamos organizar as pastas do projeto *ProjetoAula*, construído no **Unreal Engine**, e vamos configurá-lo.

### 6.1. Como criar pastas de trabalho?

No **Unreal Egnine** em `Content Drawer` utilizando botão direito do mouse clique em `New Folder` para criar pastas.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-content-drawer.webp"
    alt="Figura: Content Drawer."
    caption="Usado para navegar, criar e realizar buscas nas pastas contidas no diretório de trabalho do projeto."
%}

### 6.2. Defina e utilize uma Nomenclatura e organização de pastas

A organização de arquivos e pastas dentro dos projetos de desenvolvimento de softwares é bastante relevante para reduzir o tempo e custo de programação.

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

Primeira Sugestão de organização de pastas no Unreal Engine.

```bash
├── Content
  ├── Blueprints
  |  ├── Core
  |  ├── Characters
  |  └── Elements
  ├── Assets
  |  ├── Images
  |  ├── StructureMesh
  |  └── Materials
  ├── Maps
  |  └── Level1
  ├── UI
  └── Animations
```

Segunda Sugestão de organização de pastas no Unreal Engine.

```bash
├── Content
    ├── Projeto                                         # Pasta principal do projeto
    |   ├── Art
    |   |   ├── Industrial
    |   |   |   ├── Ambient
    |   |   |   ├── Machinery
    |   |   |   └── Pipes
    |   |   ├── Nature
    |   |   |   ├── Ambient
    |   |   |   |   ├── Foliage
    |   |   |   |   ├── Rocks
    |   |   |   |   └── Trees
    |   |   └── Office
    |   ├── Characters
    |   |   ├── Human
    |   |   |   └── BP_Human<Child BP_CharacterBase>    # Classe filho
    |   |   |   ├── Mesh
    |   |   |   ├── Animations
    |   |   |   └── Audio
    |   |   ├── Mutant
    |   |   |   └── BP_Mutant<Child BP_CharacterBase>   # Classe filho        
    |   |   |   ├── Mesh                                # Malha e texturas do personagem       
    |   |   |   ├── Animations
    |   |   |   |   ├── Logic                           # Animation Blueprint, Blend Space
    |   |   |   |   |   ├── Base                        # Animações com movimento básico
    |   |   |   |   |   └── Aim                         # Animações usando uma arma e mirando
    |   |   |   └── Audio                               # Sons do personagem
    |   |   ├── Steve
    |   |   └── Zoe
    |   ├── Core
    |   |   ├── Characters
    |   |   |   └── BP_CharacterBase                    # Classe principal dos personagens
    |   |   ├── Engine
    |   |   |   └── BP_PlayerController
    |   |   ├── GameModes
    |   |   |   └── BP_GameMode    
    |   |   ├── Interactables
    |   |   ├── Pickups
    |   |   ├── DataSets
    |   |   |   └── ECharacterState                     # Enum para registro de estados do personagem
    |   |   └── Weapons                                 # Classe principal de armas
    |   ├── Maps
    |   |   ├── Level1
    |   |   └── Level2
    └── ExampleContent                                  # Pacotes de exemplo
        ├── AnimStarterPack                             # Não devem estar no versionamento
        └── ThirdPerson                                 # Separados da lógica do projeto
```

**Nota:** A estrutura acima será usada em todos os projetos do curso.
{: .notice--warning}

### 6.3. Os benefícios na organização das pastas

Separar a pasta do projeto `Content` de outras pastas pode facilitar e trazer vários benefícios durante o desenvolvimento do projeto, abaixo elencamos alguns:

**Versionamento** - Pastas com diferentes versões;

**Isolar pacotes** - Testes e *Marketplace*;

**DLC ou subprojetos** - Podemos administrar separadamente projetos relacionados;

**Biblioteca de Materiais** - Podemos migrar pasta de materiais e compartilhar materiais sem muitos problemas definindo um pasta de nível superior.

Exemplo:

```bash
├── Content
  ├── Projeto
  ├── ProjetoTestes
  ├── ProjetoArquitetura
  ├── StarterContent
  ├── FPS_Assault_Pack
  └── MaterialLibrary
      └── M_Master
```

## 7. Configurando o projeto

Preparar o projeto antes de começar o desenvolvimento é importante para que possamos otimizar algumas tarefas e preparar o jogo com a configuração inicial, neste passo vamos configurar alguns parâmetros do projeto.

Nos próximos capítulos vamos utilizar outras opções do menu de configuração como por exemplo o mapeamento de *Input* (teclas ou controles).

### 7.1. Adicionando um *Level* na inicialização do projeto

Para que um *level* ou mapa seja carregado ao iniciar o projeto siga os seguintes passos:  

Salve o *level* atual na pasta `Maps` :  `File` > `Save Current Level As` com o nome `LevelTest`;

Para configurar a inicialização do projeto utilizando o `LevelTest` utilize o menu : `Edit` > `Project Settings` e depois `Maps & Modes`;

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-maps-modes.webp"
    alt="Figura: Project Settings > Maps & Modes."
    caption="Parâmetros globais de configuração do level e classes."
%}

`Edit Startup Level` - Seleciona o *Level* que deverá ser carregado no início do jogo, neste caso é `LevelTest`;

`Game default Map` - Seleciona o *Level* que é mais usado.

### 7.2. Configurando as imagens de apresentação do projeto

Para alterar as imagens de apresentação do projeto, seja ícone ou tela de apresentação (*splash*) utilizamos o menu : `Project Settings` opção `Plataforms` > `Windows` e altere a imagem.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-project-icon.webp"
    alt="Figura: Project Settings > Windows"
    caption="Podemos alterar o ícone do projeto e a imagem de inicialização do jogo."
%}

**Nota:** Certifique-se de produzir o ícone como um arquivo .ico (que não é PNG, mas pode ser convertido usando ferramentas online, por exemplo) e 256x256.
{: .notice--warning}
