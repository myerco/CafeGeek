---
title: Controle de versão com Git
description: Neste capítulo vamos instalar o Git com o GitHub Desktop para versionamento de arquivos no Unreal Engine e apresentar comandos básicos.
tags: [Unreal Engine,Controle de versão,GitHub]
layout: page
---

Neste capítulo vamos instalar o **Git Client** com o **GitHub Desktop** para versionamento de arquivos no **Unreal Engine** e apresentar comandos básicos.

![Figura: Unreal Engine with Git](imagens/projeto/unreal_engine_git.webp "Figura: Unreal Engine with Git")

## Índice
1. **[Para que server o controle de versão?](#1)**
1. **[Ferramentas para controle de versão](#2)**
    1. [Estrutura do GIT](#2.1)
    1. [Entendo o fluxo de trabalho](#2.2)
1. **[Começando a trabalhar com o Git e o Unreal Engine](#3)**    
    1. [Criando uma conta e o projeto no Github](#3.1)
    1. [Instalando Git Client e GitHub Desktop](#3.2)
    1. [Configurando Unreal Engine para utilizar o Git](#3.3)  
    1. [Configurando o Github Desktop e adicionando o projeto](#3.4)  
    1. [Criando o projeto remoto e atualizando os arquivos](#3.5)  
    1. [Testando a configuração do Git com o Unreal Engine](#3.6)  
1. **[Utilizando comandos do PowerShell para utilizar o Git Client](#4)**  
    1. [Clonando o projeto](#4.1)
    1. [Criando o projeto](#4.2)
    1. [Atualizando o projeto no servidor](#4.3)
    1. [Atualizando o projeto no cliente](#4.4)
1. **[Ignorando pastas e arquivos](#5)**
    1. [Exemplo de arquivo .gitignore para o Unreal Engine](#5.1)
1. [Atividades](#6)
    1. [Crie um projeto no Unreal Engine e o configure para utilizar o Git](#6.1)

***

<a name="1"></a>
## 1. Para que server o controle de versão?
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

**[⬆ Volta para o início](#índice)**

<a name="2"></a>
## 2. Ferramentas para controle de versão
Existem várias ferramentas para controle de versão disponíveis no mercado, como por exemplo :
- **GitHub** - É um serviço de armazenamento de nuvem para gerenciamento de códigos de aplicação. É possível ter uma conta gratuita e armazenar até 500Mb por projeto;
- **Gitlab** - É um serviço de armazenamento de nuvem para gerenciamento de códigos de aplicação concorrente do Github mas com o diferencial que pode ser instalado em um ambiente corporativo;
- **SVN** - Gerenciador de versão para vários tipos de arquivos, inclusive arquivos de mídia, para ambientes corporativos;
- **Git LFS** - Large File System é uma versão do git para armazenamento de arquivos de mídia ou binários, podendo armazenar de forma gratuita até 1GB.


 O **Unreal Engine** trabalha de forma nativa com **SVN**, **Perforce** e **Git**, esta última até o momento em versão beta.      

<a name="2.1"></a>
### 2.1 Estrutura do GIT
No gráfico abaixo é apresentado a estrutura de armazenar e alguns comandos do ambiente do Git.

![Git, GitHub, & Workflow Fundamentals ](https://res.cloudinary.com/practicaldev/image/fetch/s--M_fHUEqA--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/128hsgntnsu9bww0y8sz.png "Git, GitHub, & Workflow Fundamentals")

*Figura: Git, GitHub, & Workflow Fundamentals.*

<a name="2.2"></a>
### 2.2 Entendo o fluxo de trabalho
Quando utilizamos um gerenciador de versão temos que seguir um fluxo de trabalho para compartilhar o código armazenado localmente, segue abaixo os comandos iniciais do fluxo:

1. `Add` - Permite adicionar as alterações para um registro local.
  ```bash
git add .
  ```
1. `Commit` - Compromete ou confirma as alterações e criar uma etiqueta ou informação para identificar o trabalhado realizado, por exemplo:    
  ```bash
git commit -m "feat: Adicionado lógica de movimentação do jogador com mouse X e Y em BP_HeroBase."
git commit -m "fix: Corrigido o evento MostraMenu em BP_GameInstance, anteriormente o objeto apresentava erro no momento de instanciar o objeto BP_MenuPrincipal, foi adicionado o nó IsValid antes da execução."
git commit -m "fix: Lista de correções #14,#252"
  ```
1. `Push` - Empurra e publica as alterações locais no servidor.
   ```bash
git push origin main
   ```

**[⬆ Volta para o início](#índice)**

<a name="3"></a>
## 3. Começando a trabalhar com o Git e o Unreal Engine
Neste passo vamos preparar o ambiente e projeto para começar a trabalhar com o gerenciamento de versões, utilizaremos o **GitHub** como repositório de arquivos e gerenciador de versões, para tal executaremos os próximos passos.

<a name="3.1"></a>
### 3.1 Criando uma conta e o projeto no Github
Inscreva-se no [Github](https://github.com/) para ter possibilitar:
- Registro de Repositórios;
- Registro e acompanhamento de tarefas;
- Registro e acompanhamento de projetos e versões.  

<a name="3.2"></a>
### 3.2 Instalando Git Client e GitHub Desktop
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
1. Após a instalação do Git Client vamos baixar e instalar o ambiente visual [GitHub Desktop](https://desktop.github.com/) para simplificar o fluxo de trabalho.

<a name="3.3"></a>
### 3.3 Configurando Unreal Engine para utilizar o Git
Para exemplificar a conexão do Unreal Engine com o Github vamos criar um novo projeto com os seguintes parâmetros:
- Template : Blank;
- Project Name : TestGitHub;
- Type: Blurprint;
- Iremos manter os demais parâmetros como estão.

1. Para Configurar o projeto utilizaremos :   
  - O Menu principal `Edit` > `Connect To Source Control`.

   ![Figura: Source Control Login.](imagens/projeto/unreal_engine_connect_to_source_control.webp "Figura: Source Control Login")

    *Figura: Source Control Login.*
1. Abaixo a descrição dos parâmetros;
  - `Git Path` - Caminho para o executável do **Git client**;
  - `Add a .gitignore file` - Adiciona o arquivo para controle do que deve ser enviado para o servidor;
  - `Add a basic README.md file` - Adicione um arquivo em formato *Markdown* para ser utilizado como documentação inicial;
  - `Make the initial Git Commit` - Inicializa o repositório local.

1. Logo em seguida inicialize o projeto e clique em `Accept Settings`;
1. Com o `Content Drawer` cria as seguintes pastas:
  - `ExampleContent`;
  - `Projeto`;
  - `Projeto\Maps`;  
1. Salve o level atual em `Projeto\Maps` com o nome `LevelTest`.

<a name="3.4"></a>
### 3.4 Configurando o Github Desktop e adicionando o projeto
1. Abra o GitHub Desktop;
1. Configure a sua conta do **Github** para ter acesso aos seus repositórios;
  - Menu principal `File` > `Options`
   ![Figura: Github Desktop Options.](imagens/projeto/unreal_engine_github_desktop_options.webp "Figura: Github Desktop Options.")

       *Figura: Github Desktop Options.*
1. Adicione o projeto TestGitHub com :
     - `Add an Existing Repository from your hard drive...` - Informe a pasta do projeto TestGitHub;
1. Utilizando o Explorer navegue até a pasta do projeto e edite o arquivo .gitignore e adicione o texto ExampleContent, isso impedira a pasta ser enviada para o repositório remoto, verifique [Ignorando pastas e arquivos](#6) para mais informações;

<a name="3.5"></a>
### 3.5 Criando o projeto remoto e atualizando os arquivos
Uma vez configurados os projetos nos sistemas **Unreal** e **GitHub Desktop**, podemos confirmar as alterações dos arquivos utilizando o comando `Commit to Master`.

![Figura: Github Desktop Commit to Master.](imagens/projeto/unreal_engine_github_desktop_Commit_to_master.webp "Figura: Github Desktop Commit to Master.")

*Figura: Github Desktop Commit to Master.*

Após confirmação das alterações devemos publicá-las no repositório remoto usando o comando `Publish repository`.

![Figura: Github Desktop Publish repository.](imagens/projeto/unreal_engine_github_desktop_publish_repository.webp "Figura: Github Desktop Publish repository.")

*Figura: Github Desktop Publish repository.*

O comando acima irá criar um projeto na sua conta no Github.com e adicionar todos os arquivos criados até o momento.

<a name="3.6"></a>
### 3.6 Testando a configuração do Git com o Unreal Engine
Para testar as configurações realizadas vamos adicionar o pacote `Starter Content` e um objeto **Blueprint**.

1. Adicione o pacote **Starter Content** utilizando o `Content Drawer`;
  - `Add` > `Add Feature or Content Pack` escolha `Starter Content`.
1. Após a instalação do pacote mova o diretório `StarterContent` para a pasta `ExampleContent`, isso deve impedir que a referida pasta seja publicada no repositório remoto;
  - `ExampleContent\StarterContent`.
1. Vamos criar o objeto `BP_Ator` do tipo *Actor* e adicioná-lo na pasta `Content\Projeto\Characters`.
1. No painel `Changes`  do GitHub Desktop devem aparecer somente os arquivos :
  ![Figura: Github Desktop Publish repository.](imagens/projeto/unreal_engine_github_desktop_commit_first_actor.webp "Figura: Github Desktop Publish repository.")

    *Figura: Github Desktop Publish repository.*
     - BP_Ator.usasset;
     - TestGitHub.uproject.
1. Após a confirmação vamos enviar as alterações para o servidor com o comando `Push origin`.
  ![Figura: Github Desktop Publish repository.](imagens/projeto/unreal_engine_github_desktop_push_origin.webp "Figura: Github Desktop Publish repository.")

    *Figura: Github Desktop Publish repository.*

**[⬆ Volta para o início](#índice)**

<a name="4"></a>
## 4. Utilizando comandos do PowerShell para utilizar o Git Client
É interessante aprender comandos do **PowerShell** para utilizar o **Git Client** pois existem diversas situações que não estão nas ferramentas visuais, como por exemplo:
- Resolução de conflitos.
- Adicionar nome de versão para um determinado conjunto de arquivos.

Então vamos apresentar os principais comandos.

<a name="4.1"></a>
### 4.1 Clonando o projeto
Clonar o projeto significa baixar o projeto do servidor para a máquina cliente (local).

```shell
mkdir -p D:\UnrealProjects
git clone https://github.com/myerco/ProjetoAula.git
cd ProjetoMP
git status
```
<a name="4.2"></a>
### 4.2. Criando o projeto
Podemos criar um novo projeto no cliente e em seguida atualizar o servidor.     
```shell
mkdir -p D:\UnrealProjects\ProjetoMP
cd D:\UnrealProjects\ProjetoMP
git init
git remote add origin https://github.com/myerco/ProjetoAula.git
git remote -v
```
<a name="4.3"></a>
### 4.3 Atualizando o projeto no servidor
Mudanças podem ser replicadas do cliente para o servidor.
```shell
git add .
git commit -m "feat: Atualizando o projeto.. Alteração de movimentação de personagem"
git push origin master
```
<a name="4.4"></a>
### 4.4 Atualizando o projeto no cliente (local)
O comando `pull` baixa os arquivos do servidor.
```shell
git status
git pull origin master
```

**[⬆ Volta para o início](#índice)**

<a name="5"></a>
## 5. Ignorando pastas e arquivos
É importante ignorar pastas e arquivos do cliente para que não possam ser publicadas no servidor utilizando o arquivo `.gitignore` na pasta raiz do projeto, considerando os seguintes aspectos.

**Segurança**  
Arquivos de controle de senhas ou outros dados relativos a segurança não podem ficar disponíveis publicamente.

**Arquivos e pastas temporárias**  
Estes arquivos podem ser recriados ao compilar o projeto.

**Arquivos grandes**  
Arquivos de imagens ou elementos de grande tamanho podem ser excluídos do versionamento e devemos considerar outras métodos de armazenamento como por exemplo:
- [Git LFS](https://git-lfs.github.com/)
- [SVN](https://tortoisesvn.net/)

<a name="5.1"></a>
### 5.1 Exemplo de arquivo .gitignore para o Unreal Engine
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

<a name="6"></a>
## 6. Atividades
<a name="6.1"></a>
### 6.1 - Crie um projeto no Unreal Engine e o configure para utilizar o Git.

#### Regras
1. Instale todo o ambiente e crie um projeto com  a  última versão do Unreal Engine.
1. Configure o GitHub Desktop e publique o projeto criado.
1. Implemente pastas e adicione três atores para testar a publicação.

#### Desafio      
1. Crie um branch para Testes e adicione alterações.

**[⬆ Volta para o início](#índice)**

***
## Referências
- [Top 20 Git commands with examples](https://dzone.com/articles/top-20-git-commands-with-examples)
- [Source Control](https://docs.unrealengine.com/en-US/Basics/UI/SourceControl/index.html)
- [Using SVN as Source Control](https://docs.unrealengine.com/en-US/ProductionPipelines/SourceControl/SVN/index.html)
- [Git, GitHub, & Workflow Fundamentals ]([https://dev.to/mollynem/git-github--workflow-fundamentals-5496)
- [Git with Unreal Engine 5](https://www.anchorpoint.app/blog/git-with-unreal-engine-5)
- [Git for UE4 / Unreal Engine 4](https://www.youtube.com/watch?v=FXMTHrLWFKQ)
