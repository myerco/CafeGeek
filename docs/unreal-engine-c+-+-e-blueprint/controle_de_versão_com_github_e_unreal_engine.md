---
title: Controle de versão com Github e Unreal Engine
description: Neste capítulo vamos instalar o **Git Client** com o **GitHub Desktop** para versionamento de arquivos no **Unreal Engine** e apresentar comandos básicos.
tags: [Unreal Engine,desenvolvimento, blueprint,controle de versão, github, c++]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
date: 2022-09-30 
---


***

- [Ferramentas para controle de versão](#ferramentas-para-controle-de-versão)
- [Estrutura do GIT](#estrutura-do-git)
- [Entendo o fluxo de trabalho](#entendo-o-fluxo-de-trabalho)
- [Começando a trabalhar com o Git e o Unreal Engine](#começando-a-trabalhar-com-o-git-e-o-unreal-engine)
  - [Criando uma conta e o projeto no Github](#criando-uma-conta-e-o-projeto-no-github)
  - [Instalando Git Client e GitHub Desktop](#instalando-git-client-e-github-desktop)
  - [Configurando Unreal Engine para utilizar o Git](#configurando-unreal-engine-para-utilizar-o-git)
  - [Configurando o Github Desktop e adicionando o projeto](#configurando-o-github-desktop-e-adicionando-o-projeto)
- [Criando o projeto remoto e atualizando os arquivos](#criando-o-projeto-remoto-e-atualizando-os-arquivos)
  - [Testando a configuração do Git com o Unreal Engine](#testando-a-configuração-do-git-com-o-unreal-engine)
- [Utilizando comandos do PowerShell para utilizar o Git Client](#utilizando-comandos-do-powershell-para-utilizar-o-git-client)
  - [Clonando o projeto](#clonando-o-projeto)
  - [Criando o projeto](#criando-o-projeto)
  - [Atualizando o projeto no servidor](#atualizando-o-projeto-no-servidor)
  - [Atualizando o projeto no cliente (local)](#atualizando-o-projeto-no-cliente-local)
- [Ignorando pastas e arquivos](#ignorando-pastas-e-arquivos)
  - [Exemplo de arquivo .gitignore para o Unreal Engine](#exemplo-de-arquivo-gitignore-para-o-unreal-engine)

***

{% include imagebase.html
    src="unreal/projeto/unreal_engine_git.webp"
    alt="Figura: Unreal Engine with Git."
    caption=""
%}

Quando programamos existe a necessidade de gerenciar as alterações que ocorrem durante o desenvolvimento do projeto e até mesmo depois, acompanhe o seguinte exemplo:  

Abaixo o trecho de código inicial, vamos chamá-lo de **A**.

```cpp
if (a > b) {
  resultado = (a + b)
}
```

Então, alteramos o código, vamos chamar de **B**, ou mesmo o corrigimos para :

```cpp
if (a > b) {
  resultado = (a + b * 10)
}
```

Perceba que para facilitar a manutenção e desenvolvimento em equipe e pensando em documentar a lógica temos que dispor das seguintes facilidades.

- Capacidade reverter o código atual para o estado anterior, lógica **A**.

- Necessidade de compartilhar o código como outros desenvolvedores.

- Necessidade de documentar as alterações no momento que forem compartilhadas.

## Ferramentas para controle de versão

***

Existem várias ferramentas para controle de versão disponíveis no mercado, como por exemplo :

- **GitHub** - É um serviço de armazenamento de nuvem para gerenciamento de códigos de aplicação. É possível ter uma conta gratuita e armazenar até 500Mb por projeto;

- **Gitlab** - É um serviço de armazenamento de nuvem para gerenciamento de códigos de aplicação concorrente do Github mas com o diferencial que pode ser instalado em um ambiente corporativo;

- **SVN** - Gerenciador de versão para vários tipos de arquivos, inclusive arquivos de mídia, para ambientes corporativos;

- **Git LFS** - Large File System é uma versão do git para armazenamento de arquivos de mídia ou binários, podendo armazenar de forma gratuita até 1GB.

O **Unreal Engine** trabalha de forma nativa com **SVN**, **Perforce** e **Git**, esta última até o momento em versão beta.

## Estrutura do GIT

No gráfico abaixo é apresentado a estrutura de armazenar e alguns comandos do ambiente do Git.

{% include image.html
    src="https://res.cloudinary.com/practicaldev/image/fetch/s--M_fHUEqA--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/128hsgntnsu9bww0y8sz.png"
    alt="Figura: Git, GitHub, & Workflow Fundamentals."
    caption="Figura: Git, GitHub, & Workflow Fundamentals."
%}

## Entendo o fluxo de trabalho

***

Quando utilizamos um gerenciador de versão temos que seguir um fluxo de trabalho para compartilhar o código armazenado localmente, segue abaixo os comandos iniciais do fluxo:

**Add** - Permite adicionar as alterações para um registro local.

```bash
git add .
```

**Commit** - Compromete ou confirma as alterações e criar uma etiqueta ou informação para identificar o trabalhado realizado, por exemplo:

```bash
git commit -m "feat: Adicionado lógica de movimentação do jogador com mouse X e Y em BP_HeroBase."
git commit -m "fix: Corrigido o evento MostraMenu em BP_GameInstance, anteriormente o objeto apresentava erro no momento de instanciar o objeto BP_MenuPrincipal, foi adicionado o nó IsValid antes da execução."
git commit -m "fix: Lista de correções #14,#252"
````

**Push** - Empurra e publica as alterações locais no servidor.

```bash
git push origin main
```

## Começando a trabalhar com o Git e o Unreal Engine

***

Neste passo vamos preparar o ambiente e projeto para começar a trabalhar com o gerenciamento de versões, utilizaremos o **GitHub** como repositório de arquivos e gerenciador de versões, para tal executaremos os próximos passos.

### Criando uma conta e o projeto no Github

Inscreva-se no [Github](https://github.com/) para possibilitar:

- Registro de Repositórios - Espaço de armazenamento e versionamento de arquivos e projetos;

- Registro e acompanhamento de tarefas - Registro e acompanhamento de tarefas que podem se associadas aos `commits`;

- Registro e acompanhamento de projetos e versões - Registro de versões de projeto;  

- Wiki - Publicação de um Wiki do projeto.

### Instalando Git Client e GitHub Desktop

É necessário instalar o **Git Client** no computador local para criar as estruturas de versionamento. Utilizaremos o **PowerShell** com os comandos a seguir para instalar o aplicativo cliente.

1. Instale o [Cliente GIT](https://git-scm.com/downloads);

1. Crie uma chave de autenticação (Key-Gen) com o GIT-BASH;

```shell
ssh-keygen
```

> Este passo só é necessário se no momento de envio (push) solicitar senha e o sistema operacional não gerenciar as credenciais adequadamente.

1. Adicione a chave no GitHub **Settings >SSH and GPG Keys**;

1. Para testar execute os comandos:

```shell
mkdir -p D:\temp\testegit
cd D:\temp\testegit
git init
git status
git remote -v
```

1. Após a instalação do **Git Client** vamos baixar e instalar o ambiente visual [GitHub Desktop](https://desktop.github.com/) para simplificar o fluxo de trabalho.

### Configurando Unreal Engine para utilizar o Git

Para exemplificar a conexão do **Unreal Engine** com o Github vamos criar um novo projeto com os seguintes parâmetros:

- Template : Blank;

- Project Name : TestGitHub;

- Type: Blueprint;

- Iremos manter os demais parâmetros como estão.

Para Configurar o projeto utilizaremos :

`Menu` > `Edit` > `Connect To Source Control`.

{% include imagebase.html
    src="unreal/projeto/unreal_engine_connect_to_source_control.webp"
    alt="Figura: Source Control Login."
    caption="Figura: Source Control Login."
%}

Abaixo a descrição dos parâmetros;

- `Git Path` - Caminho para o executável do **Git client**;

- `Add a .gitignore file` - Adiciona o arquivo para controle do que deve ser enviado para o servidor;

  - `Add a basic README.md file` - Adicione um arquivo em formato *Markdown* para ser utilizado como documentação inicial;

  - `Make the initial Git Commit` - Inicializa o repositório local.

Logo em seguida inicialize o projeto e clique em `Accept Settings`;

Com o `Content Drawer` cria as seguintes pastas:

- `ExampleContent`;

- `Projeto`;

  - `Projeto\Maps`;  

Salve o level atual em `Projeto\Maps` com o nome `LevelTest`.

### Configurando o Github Desktop e adicionando o projeto

Abra o GitHub Desktop e configure a sua conta do **Github** para ter acesso aos seus repositórios utilizando o menu principal `File` > `Options`;

{% include imagebase.html
    src="unreal/projeto/unreal_engine_github_desktop_options.webp"
    alt="Figura: Github Desktop Options."
    caption="Figura: Github Desktop Options."
%}

Adicione o projeto TestGitHub com `Add an Existing Repository from your hard drive...`, informe a pasta do projeto TestGitHub;

Utilizando o Explorer navegue até a pasta do projeto e edite o arquivo .gitignore e adicione o texto ExampleContent, isso impedira a pasta ser enviada para o repositório remoto, verifique `Ignorando pastas e arquivos` para mais informações;

## Criando o projeto remoto e atualizando os arquivos

***

Uma vez configurados os projetos nos sistemas **Unreal** e **GitHub Desktop**, podemos confirmar as alterações dos arquivos utilizando o comando `Commit to Master`.

{% include imagebase.html
    src="unreal/projeto/unreal_engine_github_desktop_Commit_to_master.webp"
    alt="Figura: Github Desktop Commit to Master."
    caption="Figura: Github Desktop Commit to Master."
%}

Após confirmação das alterações devemos publicá-las no repositório remoto usando o comando `Publish repository`.

{% include imagebase.html
    src="unreal/projeto/unreal_engine_github_desktop_publish_repository.webp"
    alt="Figura: Github Desktop Publish repository."
    caption="Figura: Github Desktop Publish repository."
%}

O comando acima irá criar um projeto na sua conta no Github.com e adicionar todos os arquivos criados até o momento.

### Testando a configuração do Git com o Unreal Engine

Para testar as configurações realizadas vamos adicionar o pacote `Starter Content` e um objeto **Blueprint**.

Adicione o pacote **Starter Content** utilizando o `Content Drawer`:

`Add` > `Add Feature or Content Pack` escolha `Starter Content`.

Após a instalação do pacote mova o diretório `StarterContent` para a pasta `ExampleContent`, isso deve impedir que a referida pasta seja publicada no repositório remoto, como por exemplo:

`ExampleContent\StarterContent`.

Vamos criar o objeto `BP_Ator` do tipo *Actor* e adicioná-lo na pasta `Content\Projeto\Characters`.

No painel `Changes`  do GitHub Desktop devem aparecer somente os arquivos :

- BP_Ator.usasset;

- TestGitHub.uproject.

{% include imagebase.html
    src="unreal/projeto/unreal_engine_github_desktop_commit_first_actor.webp"
    alt="Figura: Github Desktop Publish repository."
    caption="Figura: Github Desktop Publish repository."
%}

Após a confirmação vamos enviar as alterações para o servidor com o comando `Push origin`.

{% include imagebase.html
    src="unreal/projeto/unreal_engine_github_desktop_push_origin.webp"
    alt="Figura: Github Desktop Push Origin."
    caption="Figura: Github Desktop Push Origin."
%}

## Utilizando comandos do PowerShell para utilizar o Git Client

***

É interessante aprender comandos do **PowerShell** para utilizar o **Git Client** pois existem diversas situações que não estão nas ferramentas visuais, como por exemplo:

- Resolução de conflitos.

- Adicionar nome de versão para um determinado conjunto de arquivos.

Então vamos apresentar os principais comandos.

### Clonando o projeto

Clonar o projeto significa baixar o projeto do servidor para a máquina cliente (local).

```bash
mkdir -p D:\UnrealProjects
git clone https://github.com/myerco/ProjetoAula.git
cd ProjetoMP
git status
```

### Criando o projeto

Podemos criar um novo projeto no cliente e em seguida atualizar o servidor.

```bash
mkdir -p D:\UnrealProjects\ProjetoMP
cd D:\UnrealProjects\ProjetoMP
git init
git remote add origin https://github.com/myerco/ProjetoAula.git
git remote -v
```

### Atualizando o projeto no servidor

Mudanças podem ser replicadas do cliente para o servidor.

```bash
git add .
git commit -m "feat: Atualizando o projeto.. Alteração de movimentação de personagem"
git push origin master
```

### Atualizando o projeto no cliente (local)

O comando `pull` baixa os arquivos do servidor.

```shell
git status
git pull origin master
```

## Ignorando pastas e arquivos

***

É importante ignorar pastas e arquivos do cliente para que não possam ser publicadas no servidor utilizando o arquivo `.gitignore` na pasta raiz do projeto, considerando os seguintes aspectos.

**Segurança** - Arquivos de controle de senhas ou outros dados relativos a segurança não podem ficar disponíveis publicamente.

**Arquivos e pastas temporárias** - Estes arquivos podem ser recriados ao compilar o projeto.

**Arquivos grandes** Arquivos de imagens ou elementos de grande tamanho podem ser excluídos do versionamento e devemos considerar outras métodos de armazenamento como por exemplo:

- [Git LFS](https://git-lfs.github.com/)

- [SVN](https://tortoisesvn.net/)

### Exemplo de arquivo .gitignore para o Unreal Engine

```shell
# Projetos exemplo
ThirdPerson/
ThirdPersonBP/
Geometry/
Mannequin/
StarterContent/
# Visual Studio 2015 user specific files
.vs/
# Compiled Object files
*.slo
*.lo
*.o
*.obj
```
