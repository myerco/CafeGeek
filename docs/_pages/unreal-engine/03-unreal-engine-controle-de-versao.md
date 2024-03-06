---
title: Controle de versão
excerpt: Neste capítulo vamos instalar o **Git Client** com o **GitHub Desktop**.
permalink: /pages/unreal-engine/controle-versao
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal_8
toc: true  
categories:
  - Unreal Engine
tags:
  - controle de versão
  - git
---

## 1. Controle de Versão

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-git.webp"
    alt="Figura: Unreal Engine with Git."
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

- Capacidade reverter o código atual para o estado anterior, lógica **A**;

- Necessidade de compartilhar o código como outros desenvolvedores;

- Necessidade de documentar as alterações no momento que forem compartilhadas.

## 2. Ferramentas para controle de versão

Existem várias ferramentas para controle de versão disponíveis no mercado, como por exemplo :

**GitHub** - É um serviço de armazenamento de nuvem para gerenciamento de códigos de aplicação. É possível ter uma conta gratuita e armazenar até 500Mb por projeto;

**Gitlab** - É um serviço de armazenamento de nuvem para gerenciamento de códigos de aplicação concorrente do Github mas com o diferencial que pode ser instalado em um ambiente corporativo;

**SVN** - Gerenciador de versão para vários tipos de arquivos, inclusive arquivos de mídia, para ambientes corporativos;

**Git LFS** - Large File System é uma versão do git para armazenamento de arquivos de mídia ou binários, podendo armazenar de forma gratuita até 1GB.

O **Unreal Engine** trabalha de forma nativa com **SVN**, **Perforce** e **Git**, esta última até o momento em versão beta.

## 3. Estrutura do GIT

No gráfico abaixo é apresentado a estrutura de armazenar e alguns comandos do ambiente do Git.

{% include image.html
    src="https://res.cloudinary.com/practicaldev/image/fetch/s--M_fHUEqA--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/128hsgntnsu9bww0y8sz.png"
    alt="Figura: Git, GitHub, & Workflow Fundamentals."
    caption="Vamos revisar um fluxo de trabalho de projeto simples e os comandos da CLI que nos ajudam a passar de uma etapa para a seguinte. Abaixo está um diagrama de um fluxo de trabalho, incluindo Git e Github. Este diagrama representa mais de perto o fluxo do meu projeto de grupo."
    ref="https://dev.to/mollynem/git-github--workflow-fundamentals-5496"
%}

## 4. Entendo o fluxo de trabalho

Quando utilizamos um gerenciador de versão temos que seguir um fluxo de trabalho para compartilhar o código armazenado localmente, segue abaixo os comandos iniciais do fluxo:

`Add` - Permite adicionar as alterações para um registro local.

```bash
git add .
```

`Commit` - Compromete ou confirma as alterações e criar uma etiqueta ou informação para identificar o trabalhado realizado, por exemplo:

```bash
git commit -m "feat: Adicionado lógica de movimentação do jogador com mouse X e Y em BP_HeroBase."
git commit -m "fix: Corrigido o evento MostraMenu em BP_GameInstance, anteriormente o objeto apresentava erro no momento de instanciar o objeto BP_MenuPrincipal, foi adicionado o nó IsValid antes da execução."
git commit -m "fix: Lista de correções #14,#252"
````

`Push` - "Empurra" e publica as alterações locais no servidor.

```bash
git push origin main
```

## 5. Começando a trabalhar com o Git e o Unreal Engine

Neste passo vamos preparar o ambiente e projeto para começar a trabalhar com o gerenciamento de versões, utilizaremos o **GitHub** como repositório de arquivos e gerenciador de versões, para tal executaremos os próximos passos.

### 5.1. Criando uma conta e o projeto no Github

Inscreva-se no [Github](https://github.com/) para possibilitar:

- Registro de Repositórios - Espaço de armazenamento e versionamento de arquivos e projetos;

- Registro e acompanhamento de tarefas - Registro e acompanhamento de tarefas que podem se associadas aos `commits`;

- Registro e acompanhamento de projetos e versões - Registro de versões de projeto;  

- Wiki - Publicação de um Wiki do projeto.

### 5.2. Instalando Git Client e GitHub Desktop

É necessário instalar o **Git Client** no computador local para criar as estruturas de versionamento. Utilizaremos o **PowerShell** com os comandos a seguir para instalar o aplicativo cliente.

**1.** Instale o [Cliente GIT](https://git-scm.com/downloads);

**2.** Crie uma chave de autenticação (Key-Gen) com o GIT-BASH;

```shell
ssh-keygen
```

**Nota:** Este passo só é necessário se no momento de envio (push) solicitar senha e o sistema operacional não gerenciar as credenciais adequadamente.
{: .notice--warning}

- Adicione a chave no GitHub **Settings >SSH and GPG Keys**;

- Para testar execute os comandos:

```shell
mkdir -p D:\temp\testegit
cd D:\temp\testegit
git init
git status
git remote -v
```

**3.** Após a instalação do **Git Client** vamos baixar e instalar o ambiente visual [GitHub Desktop](https://desktop.github.com/) para simplificar o fluxo de trabalho.

### 5.3. Configurando Unreal Engine para utilizar o Git

Para exemplificar a conexão do **Unreal Engine** com o Github vamos criar um novo projeto com os seguintes parâmetros:

- Template : Blank;

- Project Name : TestGitHub;

- Type: Blueprint;

**Nota:** Iremos manter os demais parâmetros como estão.
{: .notice--info}

Para Configurar o projeto utilizaremos  `Menu` > `Edit` > `Connect To Source Control`.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-connect-to-source-control.webp"
    alt="Figura: Source Control Login."
    caption="Configuração do usuário, servidor remoto e pasta do projeto."
%}

Abaixo a descrição dos parâmetros;

`Git Path` - Caminho para o executável do **Git client**;

`Add a .gitignore file` - Adiciona o arquivo para controle do que deve ser enviado para o servidor;

`Add a basic README.md file` - Adicione um arquivo em formato *Markdown* para ser utilizado como documentação inicial;

`Make the initial Git Commit` - Inicializa o repositório local.

Logo em seguida inicialize o projeto e clique em `Accept Settings`;

Com o `Content Drawer` crie as pastas de trabalho.

**Nota:** Utilize a estrutura de pastas definidas em [Organizando as Pastas](https://cafegeek.eti.br/pages/unreal-engine/instalacao-configuracao#6-organizando-as-pastas).
{: .notice--warning}

Salve o level atual em `Projeto\Maps` com o nome `LevelTest`.

### 5.4. Configurando o Github Desktop e adicionando o projeto

Abra o GitHub Desktop e configure a sua conta do **Github** para ter acesso aos seus repositórios utilizando o menu principal `File` > `Options`;

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-github-desktop-options.webp"
    alt="Figura: Github Desktop > Options."
    caption="Configuração de conta no Github."
%}

Adicione o projeto TestGitHub com `Add an Existing Repository from your hard drive...`, informe a pasta do projeto TestGitHub;

Utilizando o Explorer navegue até a pasta do projeto e edite o arquivo .gitignore e adicione o texto ExampleContent, isso impedira a pasta ser enviada para o repositório remoto, verifique `Ignorando pastas e arquivos` para mais informações;

## 6. Criando o projeto remoto e atualizando os arquivos

Uma vez configurados os projetos nos sistemas **Unreal** e **GitHub Desktop**, podemos confirmar as alterações dos arquivos utilizando o comando `Commit to Master`.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-github-desktop-commit-to-master.webp"
    alt="Figura: Github Desktop Commit to Master."
    caption="A aba Changes lista as mudanças e a descrição da atualização. A aba Current branch apresenta o branch atual."
%}

Após confirmação das alterações devemos publicá-las no repositório remoto usando o comando `Publish repository`.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-github-desktop-publish-repository.webp"
    alt="Figura: Github Desktop Publish repository."
    caption="Envia os dados para o repositório remoto."
%}

O comando acima irá criar um projeto na sua conta no Github.com e adicionar todos os arquivos criados até o momento.

### 6.1. Testando a configuração do Git com o Unreal Engine

Para testar as configurações realizadas vamos adicionar o pacote `Starter Content` e um objeto **Blueprint**.

Adicione o pacote **Starter Content** utilizando o `Content Drawer`: `Add` > `Add Feature or Content Pack` escolha `Starter Content`.

Após a instalação do pacote mova o diretório `StarterContent` para a pasta `ExampleContent`, isso deve impedir que a referida pasta seja publicada no repositório remoto, como por exemplo:

`ExampleContent\StarterContent`.

Vamos criar o objeto `BP_Ator` do tipo *Actor* e adicioná-lo na pasta `Content\Projeto\Characters`.

No painel `Changes`  do GitHub Desktop devem aparecer somente os arquivos :

- BP_Ator.usasset;

- TestGitHub.uproject.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-github-desktop-commit-first-actor.webp"
    alt="Figura: Github Desktop Publish repository."
    caption="No exemplo acima foi inserido um novo ator no projeto."
%}

Após a confirmação vamos enviar as alterações para o servidor com o comando `Push origin`.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-github-desktop-push-origin.webp"
    alt="Figura: Github Desktop Push Origin."
    caption="A janela da direita informa que é necessário realizar o envio de dados para o servidor remoto com o comando Push."
%}

## 7. Utilizando comandos do PowerShell para utilizar o Git Client

É interessante aprender comandos do **PowerShell** para utilizar o **Git Client** pois existem diversas situações que não estão nas ferramentas visuais, como por exemplo:

- Resolução de conflitos.

- Adicionar nome de versão para um determinado conjunto de arquivos.

Então vamos apresentar os principais comandos.

### 7.1. Clonando o projeto

Clonar o projeto significa baixar o projeto do servidor para a máquina cliente (local).

```bash
mkdir -p D:\UnrealProjects
git clone https://github.com/myerco/ProjetoAula.git
cd ProjetoMP
git status
```

### 7.2. Criando o projeto

Podemos criar um novo projeto no cliente e em seguida atualizar o servidor.

```bash
mkdir -p D:\UnrealProjects\ProjetoMP
cd D:\UnrealProjects\ProjetoMP
git init
git remote add origin https://github.com/myerco/ProjetoAula.git
git remote -v
```

### 7.3. Atualizando o projeto no servidor

Mudanças podem ser replicadas do cliente para o servidor.

```bash
git add .
git commit -m "feat: Atualizando o projeto.. Alteração de movimentação de personagem"
git push origin master
```

### 7.4. Atualizando o projeto no cliente (local)

O comando `pull` baixa os arquivos do servidor.

```shell
git status
git pull origin master
```

## 8. Ignorando pastas e arquivos

É importante ignorar pastas e arquivos do cliente para que não possam ser publicadas no servidor utilizando o arquivo `.gitignore` na pasta raiz do projeto, considerando os seguintes aspectos.

**Segurança** - Arquivos de controle de senhas ou outros dados relativos a segurança não podem ficar disponíveis publicamente.

**Arquivos e pastas temporárias** - Estes arquivos podem ser recriados ao compilar o projeto.

**Arquivos grandes** Arquivos de imagens ou elementos de grande tamanho podem ser excluídos do versionamento e devemos considerar outras métodos de armazenamento como por exemplo:

- [Git LFS](https://git-lfs.github.com/)

- [SVN](https://tortoisesvn.net/)

### 8.1. Exemplo de arquivo .gitignore para o Unreal Engine

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

### 8.2. Exemplo de arquivo . gitattributes

O arquivo .gitattributes é utilizado para que o Github identifique e armazene de forma estruturada arquivos binários, como por exemplo, vídeos, imagens e outros, para saber como utilizar visite [Git Large File Storage - Git LFS](https://git-lfs.com/).

```shell
# Auto detect text files and perform LF normalization
* text=auto
*.jpg filter=lfs diff=lfs merge=lfs -text
*.fbx filter=lfs diff=lfs merge=lfs -text
*.png filter=lfs diff=lfs merge=lfs -text
*.hdr filter=lfs diff=lfs merge=lfs -text
*.mp3 filter=lfs diff=lfs merge=lfs -text
*.wav filter=lfs diff=lfs merge=lfs -text
*.exr filter=lfs diff=lfs merge=lfs -text
*.mp4 filter=lfs diff=lfs merge=lfs -text
*.tga filter=lfs diff=lfs merge=lfs -text
*.cubemap filter=lfs diff=lfs merge=lfs -text
*.tif filter=lfs diff=lfs merge=lfs -text
*.bin.fbx filter=lfs diff=lfs merge=lfs -text
*.umap filter=lfs diff=lfs merge=lfs -text
*.duf filter=lfs diff=lfs merge=lfs -text
*.uasset filter=lfs diff=lfs merge=lfs -text
*.upk filter=lfs diff=lfs merge=lfs -text
*.udk filter=lfs diff=lfs merge=lfs -text
*.blend filter=lfs diff=lfs merge=lfs -text
```
