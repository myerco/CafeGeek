![Titulo](https://docs.google.com/drawings/d/e/2PACX-1vQ1Hn1YDYa_ZliOtpjdxVv9CZDOT5-WMhGqGUMR4hYoGKBaVpjLDvgXsHKQ0WdEaeiYVR1PVdQBXdeH/pub?w=958&h=540)
## Instalando
Dificuldade : **Nível 1**   


1. [Instalando o Uneal Engine](https://docs.unrealengine.com/en-US/GettingStarted/Installation/index.html)
1. Instalando os pacotes e o Visual Studio para programação com C++
  - [Visual Studio](https://visualstudio.microsoft.com/pt-br/?rr=https%3A%2F%2Fwww.google.com%2F)
  - [Unreal e Visual Studio](https://docs.unrealengine.com/en-US/Programming/Development/VisualStudioSetup/index.html)
  - Pacotes : Desenvolvimento para Desktop com C++ e Desenvolvimento de jogos com C++

### Criando o projeto com Blueprint
1. Criando o projeto

### Criando o projeto com C++
1. Criando o projeto:
  - Opção:  
    New Project, C++, Basic Code e C:\unrealprojects\MeuJogo
    - Parâmetros: desktop/console,Maximum Quality e With Starter Content
1. Arquivos criados na pasta do projeto:
```sh
.vs
Binaries
Config
Content
Intermediate
Saved
Source
MeuJogo.sln
MeuJogo.uproject
```
1. Visualização de Soluções no Visual Studio
```sh
Source
Meujogo.uproject
```
1. É recomendado que os arquivos e pastas devam ter um padrão de nomenclatura
para melhor organização do projeto. Abaixo o recomendado pelos desenvolvedores
[Estrutura do diretório](https://docs.unrealengine.com/en-US/Engine/Basics/DirectoryStructure/index.html)
1.  Diretórios que são construídos (build)
Os diretórios abaixo podem ser removidos pois podemos construir a qualquer momento
quando compilar o projeto
```shell
Binaries
Build
Intermediate
Saved
```
1. Para recompilar o projeto e recriar os arquivos siga os seguintes passos utilizando o
explorer no Windows:
  1. Apague as pastas *Binaries, Build, Intermediate* e *Saved*;
  1. Click com botão direito do mouse no arquivo **MeuJogo.uproject**;
  1. Escolha a opção **Generate Visual Studio project files**;
  1. Aguarde o termino da operação e abra o projeto;

1. Para verificar o editor em uso no Unreal utilize o menu :
```c
Menu/Editor Preferences/General/Source Code
```
