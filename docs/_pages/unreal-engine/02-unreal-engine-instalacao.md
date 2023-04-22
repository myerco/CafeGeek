---
title:  Instalação e Configuração
excerpt: Neste capítulo vamos instalar e configurar o ambiente de desenvolvimento.
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

[Iniciante](/collection-archive/){: .btn .btn--success}

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
    src="unreal/projeto/unreal-engine-select-new-project.webp"
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