![Titulo](https://docs.google.com/drawings/d/e/2PACX-1vQ1Hn1YDYa_ZliOtpjdxVv9CZDOT5-WMhGqGUMR4hYoGKBaVpjLDvgXsHKQ0WdEaeiYVR1PVdQBXdeH/pub?w=958&h=540)
## Instalando e configurando o projeto
Dificuldade : **Nível 1**   

### Instalando e configurando o Visual Studio
  - [Visual Studio](https://visualstudio.microsoft.com/pt-br/?rr=https%3A%2F%2Fwww.google.com%2F)
  - [Unreal e Visual Studio](https://docs.unrealengine.com/en-US/Programming/Development/VisualStudioSetup/index.html)
  - Pacotes : Desenvolvimento para Desktop com C++ e Desenvolvimento de jogos com C++
  - Verificando o editor em uso no Unreal  
  ```c
  Menu/Editor Preferences/General/Source Code
  ```
### Diretórios e arquivos
  1. Criando o projeto:
    - Opção:  
    New Project, C++, Basic Code e C:\unrealprojects\TAOc
    - Parâmetros: desktop/console,Maximum Quality e With Starter Content
  1. Arquivos criados na pasta do projeto:
```shell
.vs
Binaries
Config
Content
Intermediate
Saved
Source
TAOc.sln
TAOc.uproject
```
  1. Visualização de Soluções no Visual Studio
```shell
Source
TAOc.uproject
```
  1. [Estrutura do diretório](https://docs.unrealengine.com/en-US/Engine/Basics/DirectoryStructure/index.html)

### 3.  Diretórios que são construídos (build)
Os diretórios abaixo podem ser removidos pois podemos construir a qualquer momento
quando compilar o projeto
```shell
Binaries
Build
Intermediate
Saved
```
