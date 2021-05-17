---
title: Como instalar o Unreal Engine 4?
description: Neste capítulo vamos instalar e criar um projeto apresentando a organização de suas pastas.
tags: [Unreal Engine,instalando]
---

[CafeGeek](http://CafeGeek.eti.br)  / [Desenvolvimento de jogos utilizando Unreal Engine 4](http://cafeGeek.eti.br/ue4_blueprint/index.html)
# Como instalar o Unreal Engine 4?
Neste capítulo vamos instalar e criar um projeto apresentando a organização de suas pastas.

## Índice
1. [Instalando o Unreal e o Visual Studio](#1)
    1. [Siga o passos recomendados pela Epic Games](#11)
    1. [Instalando os pacotes e o Visual Studio para programação com C++](#12)    
1. [Criando o projeto **ProjetoAula**](#2)
1. [Verificando as pastas criadas](#3)
    1. [Pastas temporárias que podem ser removidas](#31)
1. [Compilando o projeto usando o Windows Explorer](#4)    
1. [Configurando o editor de código](#5)

<a name="1"></a>
## 1. Instalando o Unreal e o Visual Studio
Para instalar a **Unreal Engine 4** devemos instalar o **Epic Games Laucnher**, responsável pelo gerenciamento, instalação e atualização de jogos e do Framework.

Sim, o **Unreal Enegine 4** é um [Framework](https://pt.wikipedia.org/wiki/Framework) de desenvolvimento que incorpora vários editores e componentes para agilizar a construção de jogos.

Durante a instalação é necessário baixar os pacotes de desenvolvimento em C++.

<a name="11"></a>
### 1.1 Siga o passos recomendados pela Epic Games
Siga o guia de instalação da **Epic Games** pois é bem fácil.   

[Instalando o Uneal Engine](https://docs.unrealengine.com/en-US/GettingStarted/Installation/index.html).

<a name="12"></a>
### 1.2 Instalando os pacotes e o Visual Studio para programação com C++
1. [Visual Studio](https://visualstudio.microsoft.com/pt-br/?rr=https%3A%2F%2Fwww.google.com%2F).
1. [Unreal e Visual Studio](https://docs.unrealengine.com/en-US/Programming/Development/VisualStudioSetup/index.html).
1. Selecione os pacotes :
  - Desenvolvimento de jogos com C++.
  - Desenvolvimento para Desktop com C++   
  > **Por que instalei este pacote?**    
  Porque muitas vezes foi necessário testar uma funcionalidade ou mesmo testar um conceito da linguagem e ter o compilador disponível foi uma mão na roda.

<a name="2"></a>
## 2. Criando o projeto ProjetoAula
Neste passo vamos criar um projeto utilizando **C++** como linguagem de desenvolvimento pois ajuda para compreender a organização e construção de pastas e arquivos da *Unreal Engine**.  

1. Selecionando o tipo de projeto.    
![blueprint_select_new_project](projeto/blueprint_ue_select_new_project.jpg)

1. Escolha um projeto em branco (*Blank*).  
 ![blueprint_ue_select_template](projeto/blueprint_ue_select_template.jpg)

1. Em configuração de projeto escolha **C++** e *No Starter Content*, este opção não vai instalar o pacote padrão de *assets* da **Epic Games** pois agora não é necessário.    
Logo em seguida escolha uma pasta onde o projeto deverá ser instalado em **Select a Location for project to be stored**.       
![blueprint_ue_project_settings](projeto/blueprint_ue_project_settings.jpg)

1. Se deu certo a tela inicial da **Engine** deve aparecer.  
![blueprint_ue_tela_inicial](projeto/blueprint_ue_tela_inicial.jpg)

<a name="3"></a>
## 3. Verificando as pastas criadas
Utilizando o *explorer* do Windows, navegue até a pasta do projeto para verificar os arquivos criados.

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
1. A pasta *Source* contém arquivos com código
fonte em **C++** e o arquivo com extensão *uproject* é o principal arquivo do projeto.    
1. É recomendado que os arquivos e pastas devam ter um padrão de nomenclatura para melhor organização do projeto.
  Abaixo duas boas recomendações de organização, discutiremos mais nos próximos capítulos.    
  - [Estrutura do diretório](https://docs.unrealengine.com/en-US/Engine/Basics/DirectoryStructure/index.html).
  - [UE4 Style Guide](https://github.com/Allar/ue4-style-guide/blob/master/README.md#unreal-engine-4-linter-plugin)

<a name="31"></a>
### 3.1 Pastas temporárias que podem ser removidas
As pastas abaixo podem ser removidas pois podemos construir a qualquer momento quando compilar o projeto.
```bash
|-- Binaries
|-- Build
|-- Intermediate
|-- Saved
```
<a name="4"></a>
## 4 Compilando o projeto usando o Windows Explorer
Para recompilar o projeto e recriar os arquivos siga os seguintes passos utilizando o *explorer* no Windows:
1. Apague as pastas *Binaries, Build, Intermediate* e *Saved*.
1. Click com botão direito do mouse no arquivo **ProjetoAula.uproject**.
1. Escolha a opção **Generate Visual Studio project files**.  
![blueprint_explorer_generate_vs](projeto/blueprint_explorer_generate_vs.jpg)
1. Aguarde o termino da operação e abra o projeto.

<a name="5"></a>
## 5. Configurando o editor de código
Você tem que escolher qual editor de código **C++** utilizar usando :
**Menu->Editor Preferences->General** e **Source Code** e escolha **Visualstudio**.

![blueprint_ue_editor_codigo](https://myerco.github.io/CafeGeek//ue4_blueprint/imagens/projeto/blueprint_ue_editor_codigo.jpg)

>**Qual editor eu escolho, Visual Code ou Visual Studio?**
Os dois são ótimos editores de código mas o Visual Code tem uma apresentação mais enxuta e quando se trata de utilizar ele para outras lingagens, como por exemplo Pyhton, ou mesmo editar um arquivo de formato Markdown é uma boa escolha.

***
## Referências

- [Estrutura do diretório](https://docs.unrealengine.com/en-US/Engine/Basics/DirectoryStructure/index.html)  
- [UE4 Style Guide](https://github.com/Allar/ue4-style-guide/blob/master/README.md#unreal-engine-4-linter-plugin)
- [Setting Up Visual Studio for Unreal Engine](https://docs.unrealengine.com/en-US/Programming/Development/VisualStudioSetup/index.html)

***
## Tags
[Blueprint](https://myerco.github.io/CafeGeek/ue4_blueprint/blueprint.html), [Unreal Engine](https://myerco.github.io/CafeGeek/ue4_blueprint/index.html), [CafeGeek](https://myerco.github.io/CafeGeek/)
