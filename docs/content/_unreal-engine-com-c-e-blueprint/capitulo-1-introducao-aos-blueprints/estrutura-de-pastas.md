---
title: Estrutura de Pastas
excerpt: Neste capítulo vamos entender e gerenciar as pastas do projeto.
categories: 
  - "unreal-engine-com-c-e-blueprint"
  - "capitulo-1-introducao-aos-blueprints"
permalink: /:categories/:title
sidebar:
  nav: dev_unreal_1
date: 2024-03-01T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 3
tags:
  - instalação
  - configuração
  - pastas
---

## 1. Entendendo as pastas criadas

Após criar o projeto, vamos verificar como estão as pastas criadas pela *engine*. Usando o `explorer` do Windows, navegue até a pasta do projeto para conferir os arquivos e pastas gerados:

```bash
├── .vs
├── Binaries
├── Config
├── Content
├── Intermediate
├── Saved
├── Source
├── ProjetoAula.sln
└── ProjetoAula.uproject
```

A seguir, vamos entender para que serve cada pasta do projeto.

### 1.1. Pasta de código C++ - Source

A pasta `Source` contém os arquivos com código-fonte em **C++**. O arquivo com extensão `.uproject` é o principal arquivo do projeto. Veja um exemplo de estrutura inicial:

```bash
└── Source
    ├── ProjetoAula
    |   ├── ProjetoAula.cpp
    |   ├── ProjetoAula.h
    |   └── ProjetoAula.Build.cpp    
    ├── ProjetoAulaEditor.Target.cs    
    └── ProjetoAula.Target.cs
```

### 1.2. Pasta principal do projeto - Content

A pasta `Content` é a principal do projeto, pois nela ficam todos os arquivos do jogo: imagens, sons, Blueprints, mapas, materiais, entre outros. É como a “mochila” do seu projeto, onde você guarda tudo o que será usado no jogo.

### 1.3. Pastas temporárias que podem ser removidas

As pastas abaixo são criadas para auxiliar durante o desenvolvimento e podem ser apagadas sem medo, pois serão recriadas quando você compilar novamente:

```bash
├── Binaries
├── Build
├── Intermediate
└── Saved
```

### 1.4. Nomenclatura de pastas

É recomendado adotar um padrão de nomes para arquivos e pastas, facilitando a organização e o trabalho em equipe. Consulte guias como o [UE5 Style Guide](https://github.com/Allar/ue4-style-guide/blob/master/README.md#unreal-engine-4-linter-plugin) para manter tudo padronizado.
{: .notice--info}

---

## 2. Organizando as pastas

Organizar as pastas do seu projeto é fundamental para facilitar o trabalho de todos, evitar confusões e tornar o desenvolvimento mais ágil e profissional. Em projetos de jogos, lidamos com muitos tipos de arquivos: código C++, Blueprints, imagens, sons, materiais, mapas, entre outros. Além disso, equipes multidisciplinares (programadores, artistas, músicos, level designers) podem trabalhar juntas no mesmo projeto, então uma estrutura clara faz toda a diferença!

### 2.1. Como criar pastas de trabalho?

No **Unreal Engine**, abra o `Content Drawer`, clique com o botão direito e escolha `New Folder` para criar novas pastas. Assim, você pode separar Blueprints, assets, mapas, sons e muito mais.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-content-drawer.webp"
    alt="Figura: Content Drawer."
    caption="Figura: Content Drawer."
%}

**Dica:** Use emojis ou cores nos nomes das pastas dentro do editor para facilitar a identificação visual dos tipos de conteúdo!
{: .notice--info}

---

### 2.2. Exemplos e motivos para organizar as pastas

A organização das pastas deve refletir a separação dos diferentes tipos de recursos do projeto. Por exemplo:

- **Código C++**: Fica na pasta `Source`, separado dos demais recursos.
- **Blueprints**: Pastas específicas para scripts visuais.
- **Imagens e Texturas**: Pastas como `Assets/Images` ou `Art/Textures`.
- **Sons**: Pastas como `Assets/Audio` ou `Art/Audio`.
- **Materiais**: Pastas como `Assets/Materials` ou `Art/Materials`.
- **Mapas**: Pastas como `Maps` ou `Levels`.
- **UI**: Pastas para elementos de interface.

Isso facilita encontrar rapidamente o que você precisa, evita misturar arquivos de naturezas diferentes e permite que cada membro da equipe trabalhe em sua área sem atrapalhar os outros.

Veja duas sugestões de organização:

**Sugestão simples:**

```bash
└── Content
    ├── Blueprints
    |  ├── Core
    |  ├── Characters
    |  └── Elements
    ├── Assets
    |  ├── Images
    |  ├── StructureMesh
    |  └── Materials
    ├── Maps
    |  └── Level1
    ├── UI
    └── Animations
```

**Sugestão avançada e comentada:**

```bash
└── Content
    ├── Projeto                                         # Pasta principal do projeto
    |   ├── Art                                         # Imagens, texturas, materiais, sons
    |   |   ├── Industrial
    |   |   |   ├── Ambient
    |   |   |   ├── Machinery
    |   |   |   └── Pipes
    |   |   ├── Nature
    |   |   |   └── Ambient
    |   |   |       ├── Foliage
    |   |   |       ├── Rocks
    |   |   |       └── Trees
    |   |   └── Office
    |   ├── Characters                                 # Personagens e suas variações
    |   |   ├── Human
    |   |   |   ├── BP_Human<Child BP_CharacterBase>    # Classe filho
    |   |   |   ├── Mesh
    |   |   |   ├── Animations
    |   |   |   └── Audio
    |   |   ├── Mutant
    |   |   |   ├── BP_Mutant<Child BP_CharacterBase>   # Classe filho        
    |   |   |   ├── Mesh                                # Malha e texturas do personagem       
    |   |   |   ├── Animations
    |   |   |   |   └── Logic                           # Animation Blueprint, Blend Space
    |   |   |   |       ├── Base                        # Animações com movimento básico
    |   |   |   |       └── Aim                         # Animações usando uma arma e mirando
    |   |   |   └── Audio                               # Sons do personagem
    |   |   ├── Steve
    |   |   └── Zoe
    |   ├── Core                                       # Lógica central do projeto
    |   |   ├── Characters
    |   |   |   └── BP_CharacterBase                    # Classe principal dos personagens
    |   |   ├── Engine
    |   |   |   └── BP_PlayerController
    |   |   ├── GameModes
    |   |   |   └── BP_GameMode    
    |   |   ├── Interactables
    |   |   ├── Pickups
    |   |   ├── DataSets
    |   |   |   └── ECharacterState                     # Enum para registro de estados do personagem
    |   |   └── Weapons                                 # Classe principal de armas
    |   ├── Maps
    |   |   ├── Level1
    |   |   └── Level2
    └── ExampleContent                                  # Pacotes de exemplo, separados da lógica do projeto
        ├── AnimStarterPack                             # Não devem estar no versionamento
        └── ThirdPerson
```

**Por que organizar assim?**

- **Separação por tipo:** Facilita encontrar sons, imagens, Blueprints e código C++ rapidamente.
- **Pastas de exemplo:** Conteúdo de exemplo, como pacotes do Marketplace ou Starter Content, ficam separados em `ExampleContent` para não misturar com o projeto principal.
- **DLC, versões e testes:** Você pode criar pastas específicas para DLCs, versões alternativas, testes ou subprojetos, mantendo tudo isolado e organizado.
- **Biblioteca de materiais:** Ter uma pasta dedicada para materiais facilita o reaproveitamento e compartilhamento entre projetos.

**Dica:** Pastas de conteúdo extra, como DLCs, versões alternativas, testes e biblioteca de materiais, ajudam a manter o projeto limpo e organizado. Assim, você pode experimentar à vontade sem bagunçar o projeto principal!
{: .notice--info}

**Nota:** A estrutura acima será usada em todos os projetos do curso.
{: .notice--warning}

---

### 2.3. Os benefícios na organização das pastas

Separar a pasta do projeto `Content` de outras pastas pode facilitar e trazer vários benefícios durante o desenvolvimento do projeto, como:

- **Versionamento:** Permite manter diferentes versões do projeto organizadas.
- **Isolamento de pacotes:** Facilita testes e uso de recursos do *Marketplace* sem misturar com o projeto principal.
- **DLC ou subprojetos:** Possibilita administrar projetos relacionados de forma independente.
- **Biblioteca de Materiais:** Permite migrar e compartilhar materiais facilmente, usando uma pasta de nível superior.

Exemplo:

```bash
└── Content
    ├── Projeto
    ├── ProjetoTestes
    ├── ProjetoArquitetura
    ├── StarterContent
    ├── FPS_Assault_Pack
    └── MaterialLibrary
        └── M_Master
```

**Dica:** Sempre que baixar assets do Marketplace, coloque-os em pastas separadas. Assim, fica fácil atualizar, remover ou até mesmo compartilhar com outros projetos!
{: .notice--info}

---

## 3. Configurando o projeto

Preparar o projeto antes de começar o desenvolvimento é importante para otimizar tarefas e garantir uma configuração inicial adequada. Nos próximos capítulos, vamos explorar outras opções do menu de configuração, como o mapeamento de *Input* (teclas ou controles).

### 3.1. Adicionando um *Level* na inicialização do projeto

Para que um *level* ou mapa seja carregado ao iniciar o projeto, siga os passos:

- Salve o *level* atual na pasta `Maps`: `File` > `Save Current Level As` com o nome `LevelTest`;
- Para configurar a inicialização do projeto usando o `LevelTest`, acesse: `Edit` > `Project Settings` > `Maps & Modes`;

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-maps-modes.webp"
    alt="Figura: Project Settings > Maps & Modes."
    caption="Figura: Project Settings > Maps & Modes."
%}

- `Edit Startup Level`: Seleciona o *Level* que será carregado no início do jogo, neste caso `LevelTest`;
- `Game Default Map`: Seleciona o *Level* mais usado.

### 3.2. Configurando as imagens de apresentação do projeto

Para alterar as imagens de apresentação do projeto, como ícone ou tela de apresentação (*splash*), utilize o menu: `Project Settings` > `Platforms` > `Windows` e altere a imagem.

{% include imagelocal.html
    src="unreal/projeto/unreal-engine-project-icon.webp"
    alt="Figura: Project Settings > Windows"
    caption="Figura: Project Settings > Windows"
%}

Podemos alterar o ícone do projeto e a imagem de inicialização do jogo.

**Nota:** Certifique-se de produzir o ícone como um arquivo `.ico` (não PNG), preferencialmente 256x256 pixels. Ferramentas online podem ajudar na conversão.
{: .notice--warning}

---

## 4. Dicas para sua jornada

- Crie uma pasta `README.md` dentro de `Content` para documentar a estrutura do seu projeto.
- Use nomes claros e evite espaços ou acentos nos nomes das pastas.
- Separe conteúdo experimental ou de protótipo em pastas próprias.
- Compartilhe sua organização com a equipe e mantenha todos alinhados!

---

## 5. Próximos passos sugeridos

- Como navegar e usar o Content Browser do Unreal Engine.
- Dicas para versionamento de projetos (Git/SVN).
- Como importar assets e organizar recursos gratuitos.
- Boas práticas para equipes trabalhando no mesmo projeto.

---

**Organização é o segredo para criar jogos incríveis e se divertir no processo! Bora deixar tudo em ordem e partir para a próxima aventura? 🚀**
