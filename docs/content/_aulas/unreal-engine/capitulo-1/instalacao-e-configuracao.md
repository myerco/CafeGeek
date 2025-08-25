---
title: Instalação e Configuração
categories: 
  - "unreal-engine"
  - "capitulo-1"
excerpt: Aprenda a instalar e configurar o Unreal Engine de forma simples e divertida!
date: 2024-03-02T08:48:05-04:00
num: 2
order: 2
sidebar:
  nav: unreal-engine
---

## 1. O que é o Unreal Engine?

O **Unreal Engine** é uma poderosa ferramenta para criar jogos incríveis! Ele reúne vários editores e componentes que facilitam a vida de quem quer desenvolver, seja você iniciante ou já experiente. Além disso, oferece um ambiente visual chamado *Blueprint*, que permite programar sem precisar escrever código, mas também suporta a linguagem C++ para quem gosta de colocar a mão na massa.

Para programar em C++, é necessário instalar o Visual Studio ou o Visual Studio Code, além dos pacotes de desenvolvimento em C++.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-control-version.webp"
    alt="Figura: Inicializador da Epic Games."
    caption="Figura: Inicializador da Epic Games."
%}

A **Epic Games** facilita tudo com o **Inicializador da Epic Games**, um aplicativo que gerencia a instalação e atualização dos seus jogos e do próprio Unreal Engine. Com ele, você pode:

- Instalar e atualizar jogos;
- Navegar pela loja de produtos;
- Instalar e atualizar diferentes versões do Unreal Engine;
- Gerenciar uma biblioteca de *plugins* e *assets* (recursos extras para seus projetos).

---

## 2. Instalando o Unreal Engine

Vamos colocar a mão na massa! Siga os passos abaixo para instalar o Unreal Engine:

1. Baixe e instale o [Inicializador da Epic Games](https://www.epicgames.com/store/pt-BR/download).
2. Crie uma conta na Epic Games, se ainda não tiver uma.
3. Faça login no Inicializador da Epic Games.
4. No menu `Unreal Engine` > `Biblioteca`, escolha a versão desejada e clique para instalar.

Pronto! Agora você já tem o Unreal Engine instalado e pronto para criar.

---

## 3. Instalando o Visual Studio para programar com C++

Se você quer explorar o lado da programação, será necessário instalar o Visual Studio. Siga estes passos:

1. Baixe o Visual Studio em: [Download Visual Studio](https://visualstudio.microsoft.com/pt-br/).
2. Durante a instalação, selecione os seguintes pacotes:
   - **Desenvolvimento de jogos com C++**
   - **Desenvolvimento para Desktop com C++**

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-visual-studio-installer.webp"
    alt="Figura: Visual Studio Installer - Instalação."
    caption="Figura: Visual Studio Installer - Instalação."
%}

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-visual-studio-update.webp"
    alt="Figura: Visual Studio Installer - Modificar."
    caption="Figura: Visual Studio Installer - Modificar."
%}

**Dica:** Instalar o pacote Desktop com C++ é útil para testar funcionalidades e explorar conceitos da linguagem, mesmo fora do Unreal.
{: .notice--info}

---

## 4. Criando seu primeiro projeto no Unreal Engine

Vamos criar juntos um projeto chamado **ProjetoAula**! Ele será nosso companheiro nos próximos capítulos.

### 4.1. Criando um projeto no Unreal Engine 4.27

1. Abra o Inicializador da Epic Games e selecione a versão 4.27.
2. Clique em **Inicializar**.
3. Escolha o tipo de projeto: selecione **Games**.
4. Escolha o template `Blank` (modelo vazio) para começar do zero.
5. Selecione **C++** e marque `No Starter Content` (sem conteúdo inicial).
6. Escolha a pasta onde o projeto será salvo.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-select-new-project.webp"
    alt="Figura: Unreal 4 - Select or create New Project, Games."
    caption="Figura: Unreal 4 - Select or create New Project, Games."
%}

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-select-template.webp"
    alt="Figura: Selecionando um modelo para utilizar no projeto."
    caption="Figura: Selecionando um modelo para utilizar no projeto."
%}

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-project-settings.webp"
    alt="Figura: Unreal engine project Settings."
    caption="Figura: Unreal engine project Settings."
%}

Quando tudo estiver pronto, você verá a tela inicial do Unreal Engine, com o editor visual, paletas de objetos e propriedades.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-tela-inicial.webp"
    alt="Figura: Unreal Engine tela inicial."
    caption="Figura: Unreal Engine tela inicial."
%}

---

### 4.2. Criando um projeto no Unreal Engine 5

A versão 5 tem uma interface um pouco diferente, mas o processo é parecido:

1. Abra o Inicializador da Epic Games e selecione a versão 5.
2. Clique em **Inicializar**.
3. Siga os mesmos passos para criar um projeto em branco com C++.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-5-select-new-project.webp"
    alt="Figura: Unreal 5 - Select or create New Project, Games"
    caption="Figura: Unreal 5 - Select or create New Project, Games"
%}

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-home-screen.webp"
    alt="Figura: Unreal 5 - Tela inicial."
    caption="Figura: Unreal 5 - Tela inicial."
%}

A interface traz ícones menores e um novo navegador de conteúdo, chamado **Content Drawer**.

---

## 5. Configurando o editor de código

Para programar em C++ no Unreal, é importante configurar o editor de código preferido. No Unreal, vá em:

`Menu` > `Editor Preferences` > `General` > `Source Code` e escolha `Visual Studio` ou `Visual Studio Code`.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-editor-codigo.webp"
    alt="Figura: Editor Preferences > General > Source Code."
    caption="Figura: Editor Preferences > General > Source Code."
%}

**Qual editor escolher?**  
O Visual Studio é completo e recomendado para projetos grandes, mas o Visual Studio Code é mais leve e ótimo para quem gosta de praticidade ou trabalha com várias linguagens.
{: .notice--info}

---

## 6. Dicas para uma jornada divertida

- Explore os menus e não tenha medo de experimentar!
- Personalize o Unreal Engine com temas e extensões.
- Procure tutoriais em vídeo para complementar sua leitura.
- Compartilhe dúvidas e descobertas com a comunidade.

---

## 7. Próximos passos sugeridos

- Como organizar a estrutura de pastas do seu projeto.
- Conhecendo a interface do Unreal Engine.
- Primeiros passos com Blueprints.
- Como importar assets e recursos gratuitos.

---

**Agora que seu ambiente está pronto, vamos juntos criar mundos incríveis! 🚀**
