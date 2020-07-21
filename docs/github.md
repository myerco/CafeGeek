![Titulo](https://docs.google.com/drawings/d/e/2PACX-1vQ1Hn1YDYa_ZliOtpjdxVv9CZDOT5-WMhGqGUMR4hYoGKBaVpjLDvgXsHKQ0WdEaeiYVR1PVdQBXdeH/pub?w=958&h=540)
### Dificuldade : **Nível 1**

## 1. Instalação Git
> Utilize PowerShell para executar comandos

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
1. Ou use o GitDesktop para adicionar um repositório existente;

## 2. Clonando o projeto
```shell
    mkdir -p D:\UnrealProjects
    git clone https://github.com/myerco/ProjetoMP.git
    cd ProjetoMP
    git status
```
## 3. Criando o projeto
```shell
    mkdir -p D:\UnrealProjects\ProjetoMP
    cd D:\UnrealProjects\ProjetoMP
    git init
    git remote add origin https://github.com/myerco/ProjetoMP.git
    git remote -v
```
## 4. Atualizando o projeto no servidor
```shell
    git add .
    git commit -m "Atualizando o projeto.. Alteração de movimentação de personagem"
    git push origin master
```
## 5. Atualizando o projeto no cliente (local)
```shell
    git status
    git pull origin master
```
