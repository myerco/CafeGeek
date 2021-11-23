---
title: Organizando pastas e logo do projeto
description: Neste capitulo vamos organizar as pastas do projeto ProjetoAula, construído no Unreal Engine, e vamos configurá-lo
tags: [Unreal Engine,Organizando,Blueprint,pastas,folder]
layout: page
---

Neste capitulo vamos organizar as pastas do projeto *ProjetoAula*, construído no Unreal Engine, e vamos configurá-lo.

![Figura: Content Drawer](imagens/projeto/unreal_engine_content_drawer.jpg)			

## Índice
1. **[Como criar pastas de trabalho?](#1)**
    1. [Nomenclatura e organização de pastas no Unreal Engine](#1.1)
    1. [Benefícios da organização de pastas](#1.2)    
1. **[Configurando o projeto](#2)**    
    1. [Adicionando um Level na inicialização do projeto](#2)
    1. [Configurando as imagens do projeto](#4)s
1. [Atividades](#5)s
    1. [Configure as pastas de seu projeto](#5.1)

***

<a name="1"></a>
## 1. Como criar pastas de trabalho?
No **Unreal Egnine** em `Content Drawer` utilizando botão direito do mouse clique em `New Folder` para criar pastas.

<a name="1.1"></a>
### 1.1 Nomenclatura e organização de pastas no Unreal Engine
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
- Artistas de efeitos de som e músicos;

Por conseguinte para um maior gerenciamento pelas equipes do projeto  podemos definir pastas com nomenclaturas adequadas ao projeto, abaixo vamos relacionar algumas sugestões.

1. Sugestão 1;
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

1. Sugestão 2;
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

<a name="1.2"></a>
### 1.2 Benefícios na organização das pastas 
Separar a pasta do projeto de outras pastas pode facilitar:
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

**[⬆ Volta para o início](#índice)**

<a name="2"></a>
## 2. Configurando o projeto
Neste passo vamos configurar o mapa inicial e as imagens que representam o projeto.

<a name="2.1"></a>
### 2.1 Adicionando um *Level* na inicialização do projeto
Para que um *level* ou mapa seja carregado ao iniciar o projeto siga os seguintes passos:  

1. Salve o *level* atual na pasta Maps `File` > `Save Current Level As` com o nome `LevelTest`;
1. Para configurar a inicialização do projeto utilizando o **LevelTest** utilize o menu `Edit` > `Project Settings` e depois `Maps & Modes`;   
	![Project - Maps & Modes](imagens/projeto/unreal_engine_maps_modes.jpg)			

	*Figura: Project - Maps & Modes*

- `Edit Startup Level` - Seleciona o *Level* que deverá ser carregado no início do jogo, neste caso é `LevelTest`;
- `Game default Map` - Seleciona o *Level* que é mais usado.

<a name="2.3"></a>
### 2.3 Configurando as imagens  do projeto
Para alterar as imagens de apresentação do projeto, seja ícone ou tela de apresentação (*splash*) utilizamos o menu `Project Settings` opção `Plataforms` > `Windows` e altere a imagens.

![Figura: Project icon](imagens/projeto/unreal_engine_project_icon.jpg)		

*Figura: Project icon*

> Certifique-se de produzir o ícone como um arquivo .ico (que não é PNG, mas pode ser convertido usando ferramentas online, por exemplo) e 256x256.

**[⬆ Volta para o início](#índice)**
<a name="5"></a>
## 5. Atividades
<a name="5.1"></a>
### 5.1 - Configure as pastas de seu projeto.
#### Regras
1. Configure as pastas de seu projeto escolhendo uma das sugestões e justifique a sua escolha.

#### Desafio      
1. Adicione o pacote *StarterContent*.

**[⬆ Volta para o início](#índice)**

***
## Referências
- [Directory Structure](https://docs.unrealengine.com/en-US/Engine/Basics/DirectoryStructure/index.html)  
- [Editor Preferences](https://docs.unrealengine.com/en-US/Engine/UI/index.html)  
- [Style Guide](https://github.com/Allar/ue4-style-guide/blob/master/README.md)  
- [Controles de navegação](https://docs.unrealengine.com/en-US/Engine/UI/LevelEditor/Viewports/ViewportControls/index.html)
- [How to change the icon of your game?](https://answers.unrealengine.com/questions/397901/how-to-change-the-icon-of-your-game.html)
