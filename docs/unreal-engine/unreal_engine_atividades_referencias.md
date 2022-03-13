---
title: Unreal Engine Atividades e Referências
description: Unreal Engine - Seção de atividades e Referências
tags: [Unreal Engine, Atividades]
layout: page
---

**[Atividades](#atividades)**

- [2.1 Instale o Unreal Engine com Visual Studio](#21-instale-o-unreal-engine-com-visual-studio)
- [2.2 Configure as pastas de seu projeto](#22-configure-as-pastas-de-seu-projeto)
- [2.3 A Cena](#23-a-cena)
- [3.1 Crie um projeto no Unreal Engine e o configure para utilizar o Git](#31-crie-um-projeto-no-unreal-engine-e-o-configure-para-utilizar-o-git)
- [4.1 Crie um level para apresentar uma mensagem na tela.](#41-crie-um-level-para-apresentar-uma-mensagem-na-tela)
- [4.2 Level Blueprint.](#42-level-blueprint)
- [4.3 A cena da Década - EQUIPE](#43-a-cena-da-década---equipe)
- [6.1 Crie um projeto que implemente vários tipos de variáveis](#61-crie-um-projeto-que-implemente-vários-tipos-de-variáveis)
- [6.2 Implemente um projeto que crie vários atores na cena e os posicione em áreas diferentes da cena](#62-implemente-um-projeto-que-crie-vários-atores-na-cena-e-os-posicione-em-áreas-diferentes-da-cena)
- [6.3 O controle](#63-o-controle)
- [7.1 Apresentando mensagens para interagir com o personagem](#71-apresentando-mensagens-para-interagir-com-o-personagem)
- [7.2 Implementando o menu do jogo usando Game Instance](#72-implementando-o-menu-do-jogo-usando-game-instance)
- [9.1 O meu primeiro material no Unreal Engine](#91-o-meu-primeiro-material-no-unreal-engine)
- [9.2 A cortina](#92-a-cortina)
- [9.3 A grama do vizinho](#93-a-grama-do-vizinho)
- [9.4 A esfera transparente](#94-a-esfera-transparente)
- [9.5 Uma base para vários materiais](#95-uma-base-para-v-rios-materiais)

**[Referências](#refer-ncias)**
  * [Livros](#livros)
  * [Internet](#internet)

**[Recursos](#recursos)**

***

## Atividades

### 2.1 Instale o Unreal Engine com Visual Studio
**Regras.**

1. Instale todo o ambiente e crie um projeto de nome MeuPrimeiroProjeto.

**Desafio.**

1. Configure o Visual Studio para ser o editor padrão.

### 2.2 Configure as pastas de seu projeto
**Regras.**

1. Configure as pastas de seu projeto escolhendo uma das sugestões e justifique a sua escolha.

**Desafio.**

1. Adicione o pacote *StarterContent*.

### 2.3 A Cena
**Regras.**

1. Construa elementos usando Geomtry;

2. Use a imagem de referência em anexo;

3. Adicione um ícone no seu jogo;

4. Adicione uma imagem splash;


**Desafio.**

1. Crie um ambiente personalizado que harmonize com a igreja

2. Implemente mais elementos na sua cena (casas, fonte, barris, lápides, árvores)


### 3.1 Crie um projeto no Unreal Engine e o configure para utilizar o Git
**Regras.**

1. Instale todo o ambiente e crie um projeto com  a  última versão do Unreal Engine.
1. Configure o GitHub Desktop e publique o projeto criado.
1. Implemente pastas e adicione três atores para testar a publicação.

**Desafio.**

1. Crie um branch para Testes e adicione alterações.

***

### 4.1 Crie um level para apresentar uma mensagem na tela.
**Regras.**

1. Utilize variáveis para parametrizar a mensagem.

**Desafio.**

1. Adicione vários objetos de diferentes tipos.


### 4.2 Level Blueprint.

**Regras.**

1. Implemente no Level Blueprint os seguintes comandos:
  1. Ao iniciar o level é apresentado a mensagem : "tem Alguém ai?
  2. A cada "tick" apresente a mensagem : Tic, Tac, não é tik tok..
2. Mapeie uma referência de um objeto na cena e apresente o nome no objeto, exemplo : adicione um cubo na cena e ao iniciar o level escreva o nome do OBJETO CUBO na tela;
3. Explique como funcionam os eventos e seus parâmetros básicos: BeginPlay, Tick, BeginOverlap, EndOverLap ;

**Desafio.**

1. Crie um objeto do tipo peão e o adicione na tela;
2. Explique o que é um objeto do tipo peão (pawn) e seus eventos básicos;
3. No evento Tick do peão escreva mensagem  : Tik Rock é melhor que...

### 4.3 A cena da Década - EQUIPE

**Regras**

1. Implemente um protótipo de cena do seu jogo definido na disciplina de Jogatina das Décadas

2. Sinalize na cena os objetos que foram criados por cada um dos integrantes da equipe;

3. Organizem as pastas trabalho para compartilhar melhor os objetos.

**Desafio**

1. Cada elemento da equipe deve apresentar o seu objeto.


### 6.1 Crie um projeto que implemente vários tipos de variáveis
**Regras.**
1. Implemente variáveis para armazenar o Nome do personagem, a vida do personagem e força do personagem;
1. Aumente a vida e a força do personagem;
2. Altere o nome do personagem e escreva na cena.

**Desafio.**

1. Implemente uma lógica para calcular o maior valor entre três números.

  Exemplo:
```bash
x = 3;
y = 5;
z = 2;
O maior valor é Y = 5;
```

### 6.2 Implemente um projeto que crie vários atores na cena e os posicione em áreas diferentes da cena
**Regras.**

1. Adicione diferentes tipos de atores.

**Desafio.**

1. Adicione um *array* para controlar melhor os objetos.

### 6.3 O controle
**Regras.**

1. Implemente lógica que permita alternar o controle do gamemode de terceira pessoa para primeira pessoa.

**Desafio.**

1. Apresente um ambiente personalizado.


### 7.1 Apresentando mensagens para interagir com o personagem
**Regras.**

1. Implemente um objeto *Widget* com um texto colorido e formatado.
1. O *Widget* é acionado pressionando a tecla F quando o personagem ficar próximo.

**Desafio.**

1. Implemente um gameplay em primeira pessoa dentro de uma casa.


### 7.2 Implementando o menu do jogo usando Game Instance
**Regras.**

1. Implemente o menu principal do jogo com as opções : Play e Quit.
1. Implemente o menu de Resumo do jogo com as opções : Resume, Load, Save, Home e Quit. O menu é acionado com a tecla M durante a *gameplay*. Implemente também toda a lógica das ações dos botões Load, Save e Quit.
1. Implemente uma Game Instance e adicione os seguintes objetos:
  - **Open Menu Principal** para abrir o menu principal;
  - **Open Menu Resume** para abrir o menu de pausa e resumo do jogo;

### 9.1 O meu primeiro material no Unreal Engine
**Regras.**

1. Utilize os parâmetros Base Color, Roughness e Metallic

**Desafio.**

1. Escolha um objeto da internet para tentar simular a sua textura com seguintes parâmetros: uma cor, reflexivo e que possa ser aplicado em superfícies simples.

  1. Escolha um objeto qualquer para aplicar o material, exemplo: cadeira, mesa ou parede.

### 9.2 A cortina
**Regras.**

1. Implemente uma malha em formato de cortina e adicione um material para simular movimento.

**Desafio.**

1. Apresente um ambiente com vários elementos, como por exemplo sofá, paredes, janelas e etc.

1. Adicione som ambiente na cena.

### 9.3 A grama do vizinho
**Regras.**

1. Implemente um objeto para representar grama.

**Desafio.**

1. Apresente um ambiente com vários elementos, como por exemplo pedra, flores e etc.
1. Adicione som de vento.

### 9.4 A esfera transparente
**Regras.**

1. Implemente um objeto transparente simulando vidro.

**Desafio.**

1. Apresente um ambiente com vários elementos, como por exemplo pedra, flores e etc.

1. Adicione um som especial ao se aproximar da esfera.

### 9.5 Uma base para vários materiais
**Regras.**

1. Implemente um material base e 3 instancias de materiais (Material Instance).
1. Defina texturas e cores diferentes para cada instância.

**Desafio.**

1. Implemente um parâmetro para aumentar ou diminuir a mistura de várias texturas a fim de simular por exemplo pisos com pouca ou muita grama.

***

## Referências

### Internet

**CAPT 1,2**

- [Estrutura do diretório](https://docs.unrealengine.com/en-US/Engine/Basics/DirectoryStructure/index.html)

- [UE4 Style Guide](https://github.com/Allar/ue4-style-guide/blob/master/README.md#unreal-engine-4-linter-plugin)

- [Setting Up Visual Studio for Unreal Engine](https://docs.unrealengine.com/en-US/Programming/Development/VisualStudioSetup/index.html)

- [Installing Unreal Engine](https://docs.unrealengine.com/en-US/GettingStarted/Installation/index.html)

- [Documentação Unreal e Visual Studio](https://docs.unrealengine.com/en-US/Programming/Development/VisualStudioSetup/index.html)

- [Directory Structure](https://docs.unrealengine.com/en-US/Engine/Basics/DirectoryStructure/index.html)  

- [Unreal Editor Interface](https://docs.unrealengine.com/en-US/Engine/UI/index.html)  

- [Gamemakin UE4 Style Guide() {](https://github.com/Allar/ue4-style-guide/blob/master/README.md)  

- [Viewport Controls](https://docs.unrealengine.com/en-US/Engine/UI/LevelEditor/Viewports/ViewportControls/index.html)

- [How to change the icon of your game?](https://answers.unrealengine.com/questions/397901/how-to-change-the-icon-of-your-game.html)

**CAPT 3**

- [Top 20 Git commands with examples](https://dzone.com/articles/top-20-git-commands-with-examples)

- [Source Control](https://docs.unrealengine.com/en-US/Basics/UI/SourceControl/index.html)

- [Using SVN as Source Control](https://docs.unrealengine.com/en-US/ProductionPipelines/SourceControl/SVN/index.html)

- [Git, GitHub, & Workflow Fundamentals ]([https://dev.to/mollynem/git-github--workflow-fundamentals-5496)

- [Git with Unreal Engine 5](https://www.anchorpoint.app/blog/git-with-unreal-engine-5)

- [Git for UE4 / Unreal Engine 4](https://www.youtube.com/watch?v=FXMTHrLWFKQ)


**CAPT 4**

- [Blueprint](https://docs.unrealengine.com/en-US/Engine/Blueprints/index.html)

- [Level Blurprint](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Types/LevelBlueprint/index.html)

- [Actors](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Actors/index.html)

- [Components](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Actors/Components/index.html)

- [Event Graph](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/EventGraph/index.html)

- [Placing Actors](https://docs.unrealengine.com/en-US/Engine/Actors/Placement/index.html)

- [Blueprint Class](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Types/ClassBlueprint/index.html)

- [Comments](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Comments/index.html)

- [Events](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/Events/index.html)

- [Nativização](https://bibliotecadigital.ipb.pt/bitstream/10198/18264/4/pauta-relatorio-9.pdf)

- [Levels](https://docs.unrealengine.com/4.27/en-US/Basics/Levels/)

- [Blueprint Variables](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Variables/index.html)

- [Coding Standard](https://docs.unrealengine.com/en-US/Programming/Development/CodingStandard/index.html)

- [Properties](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Reference/Properties/index.html)

- [String](https://docs.unrealengine.com/en-US/BlueprintAPI/Utilities/String/index.html)

- [Srting Tables](https://docs.unrealengine.com/en-US/Gameplay/Localization/StringTables/index.html)

- [Integer](https://docs.unrealengine.com/en-US/BlueprintAPI/Math/Integer/index.html)

- [Float](https://docs.unrealengine.com/en-US/BlueprintAPI/Math/Float/index.html)

- [Designer's guide to Unreal Engine keyboard shortcuts](https://www.unrealengine.com/en-US/tech-blog/designer-s-guide-to-unreal-engine-keyboard-shortcuts "Designer's guide to Unreal Engine keyboard shortcuts")

- [View Modes](https://docs.unrealengine.com/en-US/BuildingWorlds/LevelEditor/Viewports/ViewModes/index.html "View Modes")

- [Viewport Basics](https://docs.unrealengine.com/en-US/BuildingWorlds/LevelEditor/Viewports/Basics/index.html "Viewport Basics")

- [Transforming Actors](https://docs.unrealengine.com/en-US/Basics/Actors/Transform/index.html "Transforming Actors")

**CAPT 5**

- [Unreal Property System (Reflection)](https://www.unrealengine.com/en-US/blog/unreal-property-system-reflection?sessionInvalidated=true)

- [The UCLASS() macro ](https://romeroblueprints.blogspot.com/2020/10/the-uclass-macro.html)

- [Exposing Gameplay Elements to Blueprints](https://docs.unrealengine.com/en-US/Engine/Blueprints/TechnicalGuide/ExtendingBlueprints/index.html)

- [Macros](
https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Macros/index.html)

- [UFunctions](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Reference/Functions/index.html)

- [UPROPERTY](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Reference/Properties/index.html)

- [Access modifiers in C++](https://www.geeksforgeeks.org/access-modifiers-in-c/)

- [Virtual Function in C++](https://www.geeksforgeeks.org/virtual-function-cpp/)

- [Inheritance](https://www.youtube.com/watch?v=X8nYM8wdNRE&list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb&index=27)


- [Virtual Functions in C++](https://www.youtube.com/watch?v=oIV2KchSyGQ&list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb&index=28)

- [Default IntelliSense and UE4](https://docs.wholetomato.com/default.asp?W805)

**CAPT 6**

- [Unreal Engine Blueprints Array](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Arrays/index.html)   

- [Unreal Engine Array Nodes](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Arrays/ArrayNodes/index.html)    

- [C++](https://www.codegrepper.com/code-examples/cpp/ue4+c%2B%2B+array)

- [Dynamic Arrays](https://michaeljcole.github.io/wiki.unrealengine.com/Dynamic_Arrays_in_UE4_C++/)

- [TArray: Arrays in Unreal Engine](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/TArrays/)


**CAPT 7**

- [Arms](https://docs.unrealengine.com/en-US/Gameplay/HowTo/UsingCameras/SpringArmComponents/index.html)  

- [Spawned no cliente](https://docs.unrealengine.com/en-US/Gameplay/HowTo/SpawnAndDestroyActors/Blueprints/index.html)  

- [Editor](https://docs.unrealengine.com/en-US/Engine/Content/Types/StaticMeshes/Editor/index.html)  

- [Static Mesh](https://www.youtube.com/watch?v=8WvwFPN1XNA)  

- [Static Mesh Actors](https://docs.unrealengine.com/en-US/Engine/Actors/StaticMeshActor/index.html)

- [Skeletal Mesh Actors](https://docs.unrealengine.com/en-US/Engine/Actors/SkeletalMeshActors/index.html)  

- [Componentes](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Actors/Components/index.html)

- [Brushes](https://docs.unrealengine.com/en-US/Basics/Actors/Brushes/index.html)

- [Actors](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/Actors/index.html)

- [Collsion Overview](https://docs.unrealengine.com/en-US/InteractiveExperiences/Physics/Collision/Overview/index.html)

- [Best Practices](https://docs.unrealengine.com/en-US/Engine/Blueprints/BestPractices/index.html)

- [Managing complexity in Blueprints](https://www.unrealengine.com/en-US/blog/managing-complexity-in-blueprints?sessionInvalidated=true)

- [Events](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Events/index.html)

- [Methods vs. Functions in C++ with Examples](https://www.geeksforgeeks.org/methods-vs-functions-in-c-with-examples/)

- [PlayerInput](https://docs.unrealengine.com/en-US/Programming/Tutorials/PlayerInput/index.html)

- [Enabled Input](https://docs.unrealengine.com/en-US/Gameplay/HowTo/ActorInput/Blueprints/index.html)  

- [Mapeando de comandos](https://docs.unrealengine.com/en-US/Gameplay/Input/index.html)  

- [CharacterMovement](https://docs.unrealengine.com/en-US/Gameplay/HowTo/CharacterMovement/Blueprints/index.html)  

- [Create a Free camera pawn with custom inputs](https://isaratech.com/ue4-create-a-free-camera-pawn-with-custom-inputs/)

- [Setting Up Character Movement](https://docs.unrealengine.com/en-US/InteractiveExperiences/HowTo/CharacterMovement/index.html)

- [Grabbing Objects](https://www.youtube.com/watch?v=HnR1Gf5gXcY)

- [Types of Blueprints](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/Types/index.html)

- [Blueprint interface](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/Types/Interface/index.html)

- [Event Dispatcher](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/EventDispatcher/index.html)

- [Binding and Unbind](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/EventDispatcher/BindingAndUnbinding/index.html)

- [Unreal Engine 4 em Português - Event Dispatcher](https://www.youtube.com/watch?v=qHYA4dLnVAA)

- [Delta timing](https://en.wikipedia.org/wiki/Delta_timing)

- [Understanding Delta time in Games](https://dev.to/dsaghliani/understanding-delta-time-in-games-3olf)

- [How to use delta time](https://answers.unrealengine.com/questions/38798/how-to-use-delta-time.html)

- [Tutorial enentendo o que é o deltatime](https://www.fabricadejogos.net/posts/tutorial-entendo-o-que-o-deltatime/)

- [fps vs capacidade humana](http://teclab.net.br/fps-vs-capacidade-humana/)

- [Timelines](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/Timelines/index.html)

- [Vectors and Unity](http://staffwww.fullcoll.edu/dcraig/csharp/Vectors%20and%20Unity.pdf)

- [Stat Commands](https://docs.unrealengine.com/en-US/TestingAndOptimization/PerformanceAndProfiling/StatCommands/index.html)

**CAPT 8**

- [Struct Variables in Blueprints](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/Variables/Structs/index.html)

- [How to use Structs in Unreal Engine 4](https://couchlearn.com/how-to-use-structs-in-unreal-engine-4/)

- [Using structs in Blueprints ](https://romeroblueprints.blogspot.com/2015/08/using-structs-in-blueprints.html)

- [Unreal Engine 4 em Português - Estrutura - Olha Que Fácil #47](https://www.youtube.com/watch?v=IWAhdY6Vlzo)

- [Set value of a struct-member](https://answers.unrealengine.com/questions/807996/set-value-of-a-struct-member.html)

- [Data Driven Gameplay Elements](https://docs.unrealengine.com/en-US/InteractiveExperiences/DataDriven/index.html)

- [Get Data Table Row](https://docs.unrealengine.com/en-US/BlueprintAPI/Utilities/GetDataTableRow/index.html)

- [Game Mode and Game State](https://docs.unrealengine.com/en-US/InteractiveExperiences/Framework/GameMode/index.html)

- [PlayerController vs Character](https://answers.unrealengine.com/questions/216113/playercontroller-vs-character.html)

- [UE4_Network_Compendium_by_Cedric_eXi_Neukirchen](https://cedric-neukirchen.net/Downloads/Compendium/UE4_Network_Compendium_by_Cedric_eXi_Neukirchen.pdf)

- [1.1 - HUD Example](https://docs.unrealengine.com/en-US/Resources/ContentExamples/Blueprints_HUD/1_1/index.html)

- [User Interfaces & HUDs](https://docs.unrealengine.com/en-US/InteractiveExperiences/Framework/UIAndHUD/index.html)

-[Anchors](https://docs.unrealengine.com/en-US/InteractiveExperiences/UMG/UserGuide/Anchors/index.html)

- [Quick Start](https://docs.unrealengine.com/en-US/InteractiveExperiences/UMG/QuickStart/index.html)

- [1.1 - HUD Example](https://docs.unrealengine.com/en-US/Resources/ContentExamples/Blueprints_HUD/1_1/index.html)

- [User Interfaces & HUDs](https://docs.unrealengine.com/en-US/InteractiveExperiences/Framework/UIAndHUD/index.html)

- [Anchors](https://docs.unrealengine.com/en-US/InteractiveExperiences/UMG/UserGuide/Anchors/index.html)

- [Quick Start](https://docs.unrealengine.com/en-US/InteractiveExperiences/UMG/QuickStart/index.html)


**CAPT 9**

- [Physically Based Materials](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Materials/PhysicallyBased/index.html)

- [Texture Import Guide](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Textures/Importing/index.html)

- [Curso Material Essential Concepts](https://www.unrealengine.com/en-US/onlinelearning-courses/materials---exploring-essential-concepts)

- [![Intro Material Unreal Engine](http://img.youtube.com/vi/lngF4VVNER4/0.webp)](https://www.youtube.com/watch?v=lngF4VVNER4")

- [Texture Import Guide](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Textures/Importing/index.html)

- [Material Expression Reference](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Materials/ExpressionReference/index.html)

- [Coordinates Expressions](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Materials/ExpressionReference/Coordinates/index.html)

- [Math Expressions](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Materials/ExpressionReference/Math/index.html#power)

- [1.10 - World Position Offset](https://docs.unrealengine.com/en-US/Resources/ContentExamples/MaterialNodes/1_10/index.html)

- [1.9 - Normal](https://docs.unrealengine.com/en-US/Resources/ContentExamples/MaterialNodes/1_9/index.html)

- [Material Blend Modes](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Materials/MaterialProperties/BlendModes/index.html)

- [Texture maps](https://conceptartempire.com/texture-maps/)

- [Creating and Using Material Instances](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Materials/HowTo/Instancing/index.html)

- [Material Parameter Collections](https://www.unrealengine.com/en-US/blog/material-parameter-collections)

- [Material Parameter Collections](https://www.unrealengine.com/en-US/blog/material-parameter-collections)

- [Creating Material Functions](https://docs.unrealengine.com/4.26/en-US/RenderingAndGraphics/Materials/HowTo/Making_Functions/)

**CAPT 10**

- [Importing Animations](https://docs.unrealengine.com/4.26/en-US/WorkingWithContent/Importing/FBX/Animations/)

- [Skeleton Editor](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/Skeleton/index.html)   

- [FBX Import Options Reference](https://docs.unrealengine.com/en-US/Engine/Content/Importing/FBX/ImportOptions/index.html)   

- [Animations Tools](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/index.html)  

- [AnimGraph](https://docs.unrealengine.com/en-US/Engine/Animation/AnimBlueprints/AnimGraph/index.html)

- [Importing Animations](https://docs.unrealengine.com/4.26/en-US/WorkingWithContent/Importing/FBX/Animations/)

- [Skeleton Editor](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/Skeleton/index.html)   

- [FBX Import Options Reference](https://docs.unrealengine.com/en-US/Engine/Content/Importing/FBX/ImportOptions/index.html)   

- [Animations Tools](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/index.html)  

- [AnimGraph](https://docs.unrealengine.com/en-US/Engine/Animation/AnimBlueprints/AnimGraph/index.html)

- [Creating Transition Rules](https://docs.unrealengine.com/4.27/en-US/AnimatingObjects/SkeletalMeshAnimation/StateMachines/TransitionRules/)

- [Skeleton Editor](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/Skeleton/index.html)   

- [FBX Import Options Reference](https://docs.unrealengine.com/en-US/Engine/Content/Importing/FBX/ImportOptions/index.html)   

- [Animations Tools](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/index.html)  

- [AnimGraph](https://docs.unrealengine.com/en-US/Engine/Animation/AnimBlueprints/AnimGraph/index.html)

- [Animating Objects](https://docs.unrealengine.com/4.26/en-US/AnimatingObjects/SkeletalMeshAnimation/AnimMontage/Overview/)

- [Blend depth](https://answers.unrealengine.com/questions/387906/what-does-the-blend-depth-parameter-in-layered-ble.html?sort=oldest)

- [Importing Animations](https://docs.unrealengine.com/4.26/en-US/WorkingWithContent/Importing/FBX/Animations/)

- [Skeleton Editor](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/Skeleton/index.html)   

- [FBX Import Options Reference](https://docs.unrealengine.com/en-US/Engine/Content/Importing/FBX/ImportOptions/index.html)   

- [Animations Tools](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/index.html)  

- [AnimGraph](https://docs.unrealengine.com/en-US/Engine/Animation/AnimBlueprints/AnimGraph/index.html)

- [Using Layered Animations](https://docs.unrealengine.com/4.26/en-US/AnimatingObjects/SkeletalMeshAnimation/AnimHowTo/AdditiveAnimations/)

- [Blend Nodes](https://docs.unrealengine.com/4.26/en-US/AnimatingObjects/SkeletalMeshAnimation/NodeReference/Blend/)

- [O que é animação 2D e o que a difere dos outros tipos de animações?](https://blog.saga.art.br/animacao-2d/)

- [Getting Started with Paper 2D  Community Led Training  Unreal Engine Livestream](https://www.youtube.com/watch?v=Tf9Qd4isHTM)

- [Introduction to Paper2D v4.4  Unreal Engine](https://www.youtube.com/playlist?list=PLZlv_N0_O1gauJh60307mE_67jqK42twB)

- [Paper 2D](https://docs.unrealengine.com/4.26/en-US/AnimatingObjects/Paper2D/)

- [Texture Properties](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Textures/Properties/)

- [Paper 2D Tile Sets / Tile Maps](https://docs.unrealengine.com/4.27/en-US/AnimatingObjects/Paper2D/TileMaps/)

- [Introduction to Paper2D](https://www.youtube.com/playlist?list=PLZlv_N0_O1gauJh60307mE_67jqK42twB)

**CAPT 11**

- [Playlist IA](https://www.youtube.com/playlist?list=PLMRuH4-akjpSxkYxilTbg78pP-ybQwcy9)

- [Unreal IA documetação](https://docs.unrealengine.com/en-US/Gameplay/AI/index.html)

- [Unreal Start Guide](https://docs.unrealengine.com/en-US/Engine/ArtificialIntelligence/BehaviorTrees/BehaviorTreeQuickStart/index.html)

- [Raywenderlich Tutorial](https://www.raywenderlich.com/238-unreal-engine-4-tutorial-artificial-intelligence)

**CAPT 12**

- [Getting Started with Unreal Multiplayer in C++](https://www.unrealengine.com/en-US/tech-blog/getting-started-with-unreal-multiplayer-in-cpp?sessionInvalidated=true)   

- [Multiplayer Prorgamming Quick Start](https://docs.unrealengine.com/en-US/Gameplay/Networking/QuickStart/index.html)   

- [Networking Guide](http://www.zachmetcalfgames.com/wp-content/uploads/2014/12/zmg_Unreal_Networking_Guide.pdf)   

- [Multiplayer Damage and Health System in Unreal Engine 4](https://couchlearn.com/multiplayer-damage-and-health-system-in-unreal-engine-4/)  

- [Replication](https://docs.unrealengine.com/en-US/Gameplay/HowTo/Networking/ReplicateFunction/Blueprints/index.html)

- [Networking Overview](https://docs.unrealengine.com/en-US/InteractiveExperiences/Networking/Overview/index.html)

### Livros

- SANDERS, Andrew. An Introduction to Unreal Engine 4. Boca Raton,FL. Taylor & Francis Group. 2017;

- SEWELL, Brenden. Blueprints Visual Scripting for Unreal Engine. Birminghan UK. Pack Publishing.2015;

- SEWELL, Brenden. Blueprints Visual Scripting for Unreal Engine. Birminghan UK. Pack Publishingtlh;

- PV, Satheesh. Unreal Engine 4 Game Development Essentials. Birminghan-Mumbai. Packt Publishing. 2016;

- SHERIF, Willian, Stephen Whittle. Unreal Engine 4 Scripting with C++ Cookbook. Birminghan-Mumbai. Packt Publishing. 2016;

## Recursos

- Framework  de desenvolvimento da Epic Games Unreal Engine;

- Laboratório de Jogos;
