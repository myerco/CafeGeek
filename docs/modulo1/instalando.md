[CafeGeek](https://myerco.github.io/unreal-engine)  / [Desenvolvimento de jogos utilizando Unreal Engine 4](https://myerco.github.io/unreal-engine/unreal.html)
# Instalando
Neste capítulo vamos instalar e criar um projeto apresentando a organização de pastas.

## Índice
> 1. [Instalando o Unreal e o Visual Studio](#1)
> 1. [Criando o projeto **ProjetoAula**](#2)
> 1. [Verificando as pastas criadas](#3)
> 1. [Configurando o editor de código](#4)


<a name="1"></a>
## 1. Instalando o Unreal e o Visual Studio
Devemos instalar o **Epic Games Laucnher** que gerencia a instalação e atualização de jogos e do **Unreal Engine**.

Durante a instalação é necessário baixar os pacotes de desenvolvimento em C++.

1. Guia de instalação da **Epic Games** - [Instalando o Uneal Engine](https://docs.unrealengine.com/en-US/GettingStarted/Installation/index.html).
1. Instalando os pacotes e o Visual Studio para programação com C++
  - [Visual Studio](https://visualstudio.microsoft.com/pt-br/?rr=https%3A%2F%2Fwww.google.com%2F).
  - [Unreal e Visual Studio](https://docs.unrealengine.com/en-US/Programming/Development/VisualStudioSetup/index.html).
  - Selecione os pacotes : Desenvolvimento para Desktop com C++ e Desenvolvimento de jogos com C++.  

<a name="2"></a>
## 2. Criando o projeto ProjetoAula
1. Selecionando o tipo de projeto.    
![](../imagens/projeto/projeto1.png)

1. Escolha um projeto em branco (*Blank*).  
 ![](../imagens/projeto/projeto2.png)

1. Em configuração de projeto escolha C++ e *No Starter Content* e a pasta do projeto para não instalar o pacote padrão de *assets* da **Epic Games**.  
  Escolha uma pasta onde o projeto deverá ser instalado.  
![](../imagens/projeto/projeto3.png)
1. Tela inicial.  
![](../imagens/projeto/projeto4.png)


<a name="3"></a>
## 3. Verificando as pastas criadas
Utilizando o *explorer* navegue até a pasta do projeto para verificar os arquivos criados.

```
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
  Abaixo o recomendado pelos desenvolvedores:  
  [Estrutura do diretório](https://docs.unrealengine.com/en-US/Engine/Basics/DirectoryStructure/index.html).

1.  Os diretórios abaixo podem ser removidos pois podemos construir a qualquer momento
quando compilar o projeto.
```
|-- Binaries
|-- Build
|-- Intermediate
|-- Saved
```
1. Para recompilar o projeto e recriar os arquivos siga os seguintes passos utilizando o *explorer* no Windows:

  1. Apague as pastas *Binaries, Build, Intermediate* e *Saved*.
  1. Click com botão direito do mouse no arquivo **ProjetoAula.uproject**.
  1. Escolha a opção **Generate Visual Studio project files**.
  1. Aguarde o termino da operação e abra o projeto.

<a name="4"></a>
## 4. Configurando o editor de código
Para configura o editor de código fonte **C++** acesse :
**Menu->Editor Preferences->General** e **Source Code** e escolha **Visualstudio**.

![](../imagens/projeto/projeto6.png)

***
## Referências

- [Estrutura do diretório](https://docs.unrealengine.com/en-US/Engine/Basics/DirectoryStructure/index.html)  
- [UE4 Style Guide](https://github.com/Allar/ue4-style-guide/blob/master/README.md#unreal-engine-4-linter-plugin)
- [Setting Up Visual Studio for Unreal Engine](https://docs.unrealengine.com/en-US/Programming/Development/VisualStudioSetup/index.html)
