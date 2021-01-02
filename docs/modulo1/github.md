[Home](https://myerco.github.io/unreal-engine) / [Unreal](https://myerco.github.io/unreal-engine/unreal.html)

# Versionando
Neste capítulo vamos instalar o *git* para versionamento de código e apresentar
os comandos básicos.

## Índices
> 1. [Instalação **Git**](#1)
> 1. [Clonando o projeto](#2)
> 1. [Criando o projeto](#3)
> 1. [Atualizando o projeto no servidor](#4)
> 1. [Atualizando o projeto no cliente](#5)
> 1. [Ignorando pastas e arquivos](#6)

<a name="1"></a>
## 1. Instalação Git
Nesta passo utilizaremos comandos do **PowerShell** para executar comandos de versionamento.

1. Instale o [GIT](https://git-scm.com/downloads);
1. Instale o [GIT-Desktop](https://desktop.github.com/) ou [Sourcetree](https://www.sourcetreeapp.com/);
1. Crie uma conta no [Github](https://github.com/);
1. Crie uma chave de autenticação (Key-Gen) com o GIT-BASH;
```shell
ssh-keygen
```
1. Adicione a chave no GitHub **Settings->SSH and GPG Keys**;
1. Para testar execute os comandos:
```shell
mkdir -p D:\temp\testegit
cd D:\temp\testegit
git init
git status
git remote -v
```
1. Ou use o **GitDesktop** para adicionar um repositório existente;

<a name="2"></a>
## 2. Clonando o projeto
Clonar o projeto significa baixar o projeto do servidor para a máquina cliente (local).

```shell
    mkdir -p D:\UnrealProjects
    git clone https://github.com/myerco/ProjetoMP.git
    cd ProjetoMP
    git status
```
<a name="3"></a>
## 3. Criando o projeto
Podemos criar um novo projeto no cliente e log em seguida atualizar o servidor.

```shell
    mkdir -p D:\UnrealProjects\ProjetoMP
    cd D:\UnrealProjects\ProjetoMP
    git init
    git remote add origin https://github.com/myerco/ProjetoMP.git
    git remote -v
```

<a name="4"></a>
## 4. Atualizando o projeto no servidor
Mudanças podem ser replicadas do cliente para o servidor.
```shell
    git add .
    git commit -m "feat: Atualizando o projeto.. Alteração de movimentação de personagem"
    git push origin master
```
<a name="5"></a>
## 5. Atualizando o projeto no cliente (local)
```shell
    git status
    git pull origin master
```
<a name="6"></a>
## 6. Ignorando pastas e arquivos
É importante ignorar pastas e arquivos do cliente para que não possam ser publicadas no servidor utilizando o arquivo **.gitignore** na pasta raiz do projeto, considerando os seguintes aspectos.

**Segurança**  
Arquivos de controle de senhas ou outros dados relativos a segurança não podem ficar disponíveis publicamente.

**Arquivos e pastas temporárias**  
Estes arquivos podem ser recriados ao compilar o projeto.

**Arquivos grandes**  
Arquivos de imagens ou elementos de grande tamanho podem ser excluídos do versionamento e devemos considerar outras métodos de armazenamento como por exemplo:
  - [Git LFS](https://git-lfs.github.com/)
  - [SVN](https://tortoisesvn.net/)

### Exemplo de arquivo .gitignore  
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

***

## Referências
- [Top 20 Git commands with examples](https://dzone.com/articles/top-20-git-commands-with-examples)
- [Source Control](https://docs.unrealengine.com/en-US/Basics/UI/SourceControl/index.html)
- [Using SVN as Source Control](https://docs.unrealengine.com/en-US/ProductionPipelines/SourceControl/SVN/index.html)
