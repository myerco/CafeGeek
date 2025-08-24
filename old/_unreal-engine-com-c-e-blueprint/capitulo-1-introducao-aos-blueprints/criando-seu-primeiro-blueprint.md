---
title: Criando seu primeiro Blueprint
excerpt: Descubra como criar lógica de programação visual com Blueprints no Unreal Engine de forma simples e divertida!
categories: 
  - "unreal-engine-com-c-e-blueprint"
  - "capitulo-1-introducao-aos-blueprints"
permalink: /:categories/:title
sidebar:
  nav: dev_unreal_1
date: 2024-03-05T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 105
tags:
  - Visual Scripting
  - Open Level Blueprint
---

# Criando seu primeiro Blueprint

Bem-vindo ao universo dos Blueprints! Aqui você vai aprender, de forma prática e divertida, como criar lógica de programação visual no Unreal Engine, mesmo sem saber programar em C++. Vamos juntos transformar ideias em ações no seu jogo!

---

## 1. O que são Blueprints e Visual Scripting?

{% include figure
    image_path="/assets/images/unreal/actor/unreal-engine-blueprint.webp"
    alt="Figura: Unreal Engine com Blueprint"
%}

O sistema **Blueprints Visual Scripting** do Unreal Engine permite criar lógica de jogo usando uma interface visual, conectando blocos (nós) como se fossem peças de LEGO!  
Com Blueprints, qualquer pessoa da equipe pode criar interatividade, animações e comportamentos, sem precisar escrever código tradicional.

![Figura: Exemplo do conceito de objetos na programação](/assets/images/unreal/actor/uml-jogos.webp){: .align-center}

No exemplo acima, vemos uma classe que representa um objeto do tipo "gato", com seus atributos e ações. Assim como em programação tradicional, Blueprints também seguem o conceito de objetos, mas tudo é feito de forma visual.

**Por que usar Blueprints?**  
- São acessíveis para todos, mesmo para quem não é programador.
- Facilitam o entendimento e a colaboração entre diferentes áreas do projeto.
- Permitem prototipar ideias rapidamente e testar sem medo!

> **Dica:** Blueprints e C++ podem trabalhar juntos! Você pode começar com Blueprints e, quando quiser mais desempenho, converter para C++ usando a nativização.
{: .notice--info}

---

## 2. Entendendo a Hierarquia dos Blueprints

Para criar lógica visual, é importante entender como os elementos do Unreal se organizam. Veja um resumo da estrutura:

```bash
└── C++  
    ├── Herança                         # Classes derivam e herdam de suas classes pai  
    |   ├── Framework                   # Classes padrão  
    |   |   └── Actor  
    |   |       ├── GameMode
    |   |       |   ├── Pawn
    |   |       |   ├── Controller
    |   |       |   ├── GameState
    |   |       |   └── PlayerState
    |   |       └── GameInstance
    |   └── Events/Functions/Var        # Eventos, funções e variáveis.
    ├── Blueprint
    |   ├── Components
    |   |   ├── Static Mesh
    |   |   └── Emiter
    |   ├── Editores
    |   |   ├── Timeline
    |   |   ├── Componentes
    |   |   └── Editor de script
    |   └── Communication BP to BP      # Comunicação entre Blueprints
    |       ├── Casting
    |       ├── Interface
    |       └── Event Dispatcher
    ├── Compilação                      # Compilação do Bytecode.
    |   └── Nativização                 # Converter Blueprint para C++ nativo
    └── VM                              # Executado em uma máquina virtual
```

**Nativização:**  
É um recurso que transforma Blueprints em código C++ nativo na hora de empacotar o jogo, unindo facilidade e desempenho!

---

## 3. Trabalhando com Levels (Mapas)

Tudo o que aparece no seu jogo está dentro de um **Level** (ou mapa). O Level reúne iluminação, objetos, personagens e tudo mais que compõe a cena.

{% include image.html
    src="https://www.worldofleveldesign.com/images/tutorial-topics/cat-ue4-680x300.jpg"
    alt="Figura: Tutorial List."
    caption="O personagem, a grama, as árvores e os elementos de iluminação estão organizados em um level."
    idref="WORLDOFLEVELDESIGN,Home"
    ref="https://www.worldofleveldesign.com"
%}

### 3.1. Criando um Level

Para criar um novo Level, vá em `File > New Level`.

{% include imagelocal.html
    src="unreal/actor/unreal-engine-new-level.webp"
    alt="Figura: New Level."
    caption="Figura: New Level."
%}

Escolha um modelo para começar:

- **Default:** Um Level básico, já com luz, céu e um ponto de início.
- **TimeofDay:** Um Level com sistema de iluminação dinâmica para testar diferentes horários.
- **VR-Basic:** Um Level pronto para experiências em realidade virtual.
- **Empty Level:** Um Level completamente vazio, para criar tudo do zero!

### 3.2. Salvando e Abrindo Levels

- Para salvar: `File > Save Current`
- Para abrir: `File > Open Level`

{% include imagelocal.html
    src="unreal/actor/unreal-engine-save-level.webp"
    alt="Figura: Save Current."
    caption="Figura: Save Current."
%}

{% include imagelocal.html
    src="unreal/actor/unreal-engine-open-level.webp"
    alt="Figura: Open Level."
    caption="Figura: Open Level."
%}

---

## 4. O que é Level Blueprint?

O **Level Blueprint** é um tipo especial de Blueprint que controla a lógica do Level inteiro.  
Cada Level tem seu próprio Level Blueprint, onde você pode criar eventos, interações e scripts que afetam tudo no mapa.

Para abrir: `Blueprints > Open Level Blueprint`

{% include imagelocal.html
    src="unreal/actor/unreal-engine-open-level-blueprint.webp"
    alt="Figura:  Open Level Blueprint."
    caption="Figura: Open Level Blueprint."
%}

> **Informação:** O Level Blueprint é ideal para lógica global do mapa, como abrir portas, acionar eventos ou mostrar mensagens.
{: .notice--info}

---

## 5. Escrevendo sua Primeira Lógica com Blueprint

Vamos criar um exemplo simples: mostrar uma mensagem na tela quando o Level começar!

1. Abra o Level Blueprint.
2. Adicione o evento **BeginPlay** (executado quando o Level inicia).
3. Conecte ao nó **Print String** (escreve uma mensagem na tela).

{% include imagelocal.html
    src="unreal/actor/unreal-engine-blueprint-beginplay-printstring.webp"
    alt="Figura: Iniciando o level e escrevendo uma mensagem na tela."
    caption="Figura: Iniciando o level e escrevendo uma mensagem na tela."
%}

- **BeginPlay:** Executa quando o Level é carregado.
- **Print String:** Mostra um texto na tela.

> **Dica:** Use o Print String para testar ideias rapidamente e ver mensagens durante o jogo!
{: .notice--info}

---

### 5.1. Exemplo Visual: BeginPlay e Tick

Veja um exemplo visual de como BeginPlay e Tick funcionam no Blueprint:

{% include iframe.html
    src="https://blueprintue.com/render/46vsgoyi/"
    title="Cafegeek - Exemplo de BeginPlay e Tick."
    caption="BeginPlay é executado ao carregar o level; Tick é executado a cada quadro da cena."
    ref="https://blueprintue.com/render/46vsgoyi/"
%}

---

### 5.2. Exemplo de Mensagem com C++

Se quiser fazer o mesmo usando C++, veja como é fácil:

**No Console (Log):**
```cpp
UE_LOG(LogTemp, Warning, TEXT("Escreva aqui sua mensagem!"));
```

**Na tela (Screen):**
```cpp
GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Red, TEXT("Escreva aqui sua mensagem!"));
```

---

## Resumindo

- Blueprints permitem criar lógica visual sem programar em C++.
- Levels organizam tudo que aparece no seu jogo.
- O Level Blueprint controla a lógica global do mapa.
- Com poucos cliques, você já pode mostrar mensagens e criar interatividade!

---

**Agora é sua vez! Experimente criar seu próprio Blueprint e veja a mágica acontecer no seu jogo!**
