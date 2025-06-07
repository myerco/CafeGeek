---
title:  Instalação e Configuração
excerpt: Neste capítulo vamos instalar e configurar o ambiente de desenvolvimento.
permalink: /unreal-engine-capitulo-1/instalacao-e-configuracao
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 102
tags:
  - Unreal Engine
  - Framework
---

## 1. O Unreal Engine

O **Unreal Engine** é um [Framework](https://pt.wikipedia.org/wiki/Framework) de desenvolvimento que incorpora vários editores e componentes para agilizar a construção de jogos e também um ambiente visual de programação abstraindo a lógica de programação.

O **Unreal Engine** emprega a linguagem C++ juntamente com um ambiente de programação visual chamado *Blueprint*. Para habilitar a programação em C++, é imprescindível instalar o Visual Studio ou Visual Code, e também fazer o download dos pacotes de desenvolvimento em C++.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-control-version.webp"
    alt="Figura: Inicializador da Epic Games."
    caption="Figura: Inicializador da Epic Games."
%}

Para facilitar a instalação e atualização do ambiente de desenvolvimento dos projetos, a **Epic Games** utiliza um sistema para gerenciamento dos seus produtos, o **Inicializador da Epic Games** responsável por:

- Instalação e atualização de jogos;

- Navegação da loja de produtos;

- Instalação e atualização das versões do **Unreal Engine**;

- Instalação e atualização de uma biblioteca de *plugins* e *assets* (recursos).

## 2. Como instalar o Unreal Engine?

Para instalar o Unreal Engine siga os seguintes passos:

1. Baixe e instale o [Inicializador da Epic Games](https://www.epicgames.com/store/pt-BR/download);

1. Crie uma conta na Epic Games, se ainda não tiver uma;

1. Faça login no **Inicializador da Epic Games**;

1. Instale o **Unreal Engine** utilizando o menu `Unreal Engine` > `Biblioteca`.

## 3. Instalando o Visual Studio para programar com C++

Para instalar  os pacotes de desenvolvimento e o Visual Studio para programação com C++ baixe o Visual Studio em : [Download Visual Studio](https://visualstudio.microsoft.com/pt-br/?rr=https%3A%2F%2Fwww.google.com%2F).

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-visual-studio-installer.webp"
    alt="Figura: Visual Studio Installer - Instalação."
    caption="Figura: Visual Studio Installer - Instalação."
 %}

Depois de instalar o Visual Studio é necessário selecionar os seguintes pacotes de programação:

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-visual-studio-update.webp"
    alt="Figura: Visual Studio Installer - Modificar."
    caption="Figura: Visual Studio Installer - Modificar."
%}

Usando o Visual Studio Installer podemos instalar ou remover (modificar), os pacotes necessários para o desenvolvimento de jogos.

- Desenvolvimento de jogos com C++;

- Desenvolvimento para Desktop com C++.

**Por que instalar o pacote Desktop com C++ ?** Porque frequentemente é necessário testar funcionalidades ou mesmo explorar conceitos da linguagem. Ter o compilador disponível é extremamente útil nessas situações.
{: .notice--info}

## 4. Criando um projeto para jogos no Unreal Engine

Nesta seção vamos criar um projeto para jogos utilizando **C++**, pois, irá ajudar na compreensão da estrutura de pastas e arquivos do **Unreal Engine**. O nome do projeto será ProjetoAula e o usaremos em vários capítulos.

### 4.1. Criando um projeto no Unreal Engine 4.27

Para construção do projeto podemos clicar no versão disponível na janela do inicializador ou na opção **Inicializar** no campo superior direito, após a inicialização da **Unreal** é necessário selecionar o tipo de projeto para que a *Engine* configure alguns parâmetros iniciais.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-select-new-project.webp"
    alt="Figura: Unreal 4 - Select or create New Project, Games."
    caption="Figura: Unreal 4 - Select or create New Project, Games."
%}

Selecione a opção Games para construção do projeto.

#### 4.1.1. Escolhendo o Template

Para este projeto vamos escolher o `template blank`, modelo vazio, significa que não vamos instalar objetos e recursos adicionais no projeto, pois, vamos realizar essa tarefa posteriormente para que possamos entender a estrutura do projeto.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-select-template.webp"
    alt="Figura: Selecionando um modelo para utilizar no projeto."
    caption="Figura: Selecionando um modelo para utilizar no projeto."
%}

**Templates:** São modelos com recursos disponíveis para cada tipo de jogo escolhido.
{: .notice--info}

#### 4.1.2. Configuração inicial do projeto

Em configuração de projeto escolha **C++** e `No Starter Content`, esta opção não vai instalar o pacote padrão de *assets* da **Epic Games** pois agora não é necessário, em seguida escolha uma pasta onde o projeto deverá ser instalado em `Select a Location for project to be stored`.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-project-settings.webp"
    alt="Figura: Unreal engine project Settings."
    caption="Figura: Unreal engine project Settings."
%}

#### 4.1.3. Tela inicial do Unreal Engine

Quando todos os passos anteriores forem concluídos corretamente a tela inicial deve aparecer o ambiente de desenvolvimento integrado com editor visual de cena, paletas de objetos e suas propriedades  

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-tela-inicial.webp"
    alt="Figura: Unreal Engine tela inicial."
    caption="Figura: Unreal Engine tela inicial."
%}

### 4.2. Iniciando um projeto no Unreal Engine 5

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-5-select-new-project.webp"
    alt="Figura: Unreal 5 - Select or create New Project, Games"
    caption="Figura: Unreal 5 - Select or create New Project, Games"
%}

A versão 5 tem uma apresentação um pouco diferente mas o conceito ainda é o mesmo dos passos anteriores.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-home-screen.webp"
    alt="Figura: Unreal 5 - Tela inicial."
    caption="Figura: Unreal 5 - Tela inicial."
%}

Paleta de comandos com ícones menores o novo navegador de conteúdo (Content Drawer).

## 5. Configurando o editor de código

Para programar utilizando **C++** no Unreal devemos configurar um editor de código para ser responsável pela compilação, organização e edição da linguagem. A configuração esta em :

`Menu` > `Editor Preferences` > `General` e `Source Code`, então escolha `Visualstudio`.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-editor-codigo.webp"
    alt="Figura: Editor Preferences > General > Source Code."
    caption="Figura: Editor Preferences > General > Source Code."
%}

**Qual editor eu escolho, Visual Code ou Visual Studio?**  Os dois são ótimos editores de código, mas o Visual Code tem uma apresentação mais enxuta e quando se trata de utilizar ele para outras linguagens, como por exemplo Pyhton, ou mesmo editar um arquivo de formato Markdown é uma boa escolha.
{: .notice--info}
