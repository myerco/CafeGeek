---
title:  Estrutura de pastas 
excerpt: Neste capítulo vamos entender e gerenciar as pastas do projeto.
permalink: /unreal-engine-capitulo-1/estrutura-de-pastas
last_modified_at: 2023-03-28T08:48:05-04:00
layout: single
order: 1.3
toc: true  
sidebar:
    nav: dev_unreal_1
categories:
  - Unreal Engine
tags:
  - instalação
  - configuração
  - pastas
---

## 1. Entendo as pastas criadas

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

### 1.1. Pasta de código C++ - Source

A pasta `Source` contém arquivos com código fonte em **C++** e o arquivo com extensão *uproject* é o principal arquivo do projeto, segue abaixo a configuração inicial.

```bash
└── Source
    ├── ProjetoAula
    |   ├── ProjetoAula.cpp
    |   ├── ProjetoAula.h
    |   └── ProjetoAula.Build.cpp    
    ├── ProjetoAulaEditor.Target.cs    
    └── ProjetoAula.Target.cs
```

### 1.2. Pasta principal do projeto - Content

`Content` é a principal pasta, pois nela vão ficar contidos todos os arquivos do jogo, em outras palavras esta pasta é o ponto de montagem do projeto como veremos nos próximos capítulos.

### 1.3. Pastas temporárias que podem ser removidas

As pastas abaixo podem ser removidas pois podemos construir a qualquer momento quando compilar o projeto.

```bash
├── Binaries
├── Build
├── Intermediate
└── Saved
```

### 1.4. Nomenclatura de pastas

É recomendado que os arquivos e pastas devam ter um padrão de nomenclatura para melhor organização do projeto, abaixo duas boas recomendações de organização, discutiremos mais nos próximos capítulos.

**[UE5 Style Guide](https://github.com/Allar/ue4-style-guide/blob/master/README.md#unreal-engine-4-linter-plugin "Gamemakin UE4 Style Guide() { A mostly reasonable approach to Unreal Engine 4"):** Gamemakin UE4 Style Guide() - A mostly reasonable approach to Unreal Engine 4.
{: .notice--info}

## 2. Organizando as pastas

A seguir vamos organizar as pastas do projeto *ProjetoAula*, construído no **Unreal Engine**, e vamos configurá-lo.

### 2.1. Como criar pastas de trabalho?

No **Unreal Egnine** em `Content Drawer` utilizando botão direito do mouse clique em `New Folder` para criar pastas.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-content-drawer.webp"
    alt="Figura: Content Drawer."
    caption="Usado para navegar, criar e realizar buscas nas pastas contidas no diretório de trabalho do projeto."
%}

### 2.2. Defina e utilize uma Nomenclatura e organização de pastas

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
└── Content
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
└── Content
    ├── Projeto                                         # Pasta principal do projeto
    |   ├── Art
    |   |   ├── Industrial
    |   |   |   ├── Ambient
    |   |   |   ├── Machinery
    |   |   |   └── Pipes
    |   |   ├── Nature
    |   |   |   └── Ambient
    |   |   |       ├── Foliage
    |   |   |       ├── Rocks
    |   |   |       └── Trees
    |   |   └── Office
    |   ├── Characters
    |   |   ├── Human
    |   |   |   ├── BP_Human<Child BP_CharacterBase>    # Classe filho
    |   |   |   ├── Mesh
    |   |   |   ├── Animations
    |   |   |   └── Audio
    |   |   ├── Mutant
    |   |   |   ├── BP_Mutant<Child BP_CharacterBase>   # Classe filho        
    |   |   |   ├── Mesh                                # Malha e texturas do personagem       
    |   |   |   ├── Animations
    |   |   |   |   └── Logic                           # Animation Blueprint, Blend Space
    |   |   |   |       ├── Base                        # Animações com movimento básico
    |   |   |   |       └── Aim                         # Animações usando uma arma e mirando
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

### 2.3. Os benefícios na organização das pastas

Separar a pasta do projeto `Content` de outras pastas pode facilitar e trazer vários benefícios durante o desenvolvimento do projeto, abaixo elencamos alguns:

**Versionamento** - Pastas com diferentes versões;

**Isolar pacotes** - Testes e *Marketplace*;

**DLC ou subprojetos** - Podemos administrar separadamente projetos relacionados;

**Biblioteca de Materiais** - Podemos migrar pasta de materiais e compartilhar materiais sem muitos problemas definindo um pasta de nível superior.

Exemplo:

```bash
└── Content
    ├── Projeto
    ├── ProjetoTestes
    ├── ProjetoArquitetura
    ├── StarterContent
    ├── FPS_Assault_Pack
    └── MaterialLibrary
        └── M_Master
```

## 3. Configurando o projeto

Preparar o projeto antes de começar o desenvolvimento é importante para que possamos otimizar algumas tarefas e preparar o jogo com a configuração inicial, neste passo vamos configurar alguns parâmetros do projeto.

Nos próximos capítulos vamos utilizar outras opções do menu de configuração como por exemplo o mapeamento de *Input* (teclas ou controles).

### 3.1. Adicionando um *Level* na inicialização do projeto

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

### 3.2. Configurando as imagens de apresentação do projeto

Para alterar as imagens de apresentação do projeto, seja ícone ou tela de apresentação (*splash*) utilizamos o menu : `Project Settings` opção `Plataforms` > `Windows` e altere a imagem.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-project-icon.webp"
    alt="Figura: Project Settings > Windows"
    caption="Podemos alterar o ícone do projeto e a imagem de inicialização do jogo."
%}

**Nota:** Certifique-se de produzir o ícone como um arquivo .ico (que não é PNG, mas pode ser convertido usando ferramentas online, por exemplo) e 256x256.
{: .notice--warning}
