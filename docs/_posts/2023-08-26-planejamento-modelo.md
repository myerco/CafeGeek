---
title: "Modelo de Planejamento"
mermaid: true
categories:
  - unreal engine
tags:
  - lógica
  - blueprint
---

## Estrutura

### Acompanhamento semanal

<div class="mermaid">
gantt
    title A Gantt Diagram
    dateFormat YYYY-MM-DD
    section Section
        A task          :a1, 2014-01-01, 30d
        Another task    :after a1, 20d
    section Another
        Task in Another :2014-01-12, 12d
        another task    :24d
</div>

### Entregas mensais

<div class="mermaid">
timeline
    title History of Social Media Platform
    2002 : LinkedIn
    2004 : Facebook
         : Google
    2005 : Youtube
    2006 : Twitter
</div>

### Agenda

<div class="mermaid">
---
title: Animal example
---
classDiagram
    note "From Duck till Zebra"
    Animal <|-- Duck
    note for Duck "can fly\ncan swim\ncan dive\ncan help in debugging"
    Animal <|-- Fish
    Animal <|-- Zebra
    Animal : +int age
    Animal : +String gender
    Animal: +isMammal()
    Animal: +mate()
    class Duck{
        +String beakColor
        +swim()
        +quack()
    }
    class Fish{
        -int sizeInFeet
        -canEat()
    }
    class Zebra{
        +bool is_wild
        +run()
    }
</div>

### Indicadores

<div class="mermaid">
journey
    title My working day
    section Go to work
      Make tea: 5: Me
      Go upstairs: 3: Me
      Do work: 1: Me, Cat
    section Go home
      Go downstairs: 5: Me
      Sit down: 5: Me
</div>

## Etiquetas

### Tipos

- UX
- Design
- Front
- Back
- Install
- Config
- Report

### Projetos

- Unidade Gestor
- Linguagem (versão)
- Banco de dados (versão)

### Kanban

- Novo
- Pronto
- In Progress
- Ready for test
- Done

<div class="mermaid">
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
</div>

<div class="mermaid">
graph LR
    A --- B
    B-->C[Happy]
    B-->D(Sad);
</div>

<div class="mermaid">
graph TD
    B[peace]
    B-->C[fa:fa-ban forbidden]
    B-->D(fa:fa-spinner);
    B-->E(fa:fa-camera-retro perhaps?);
</div>