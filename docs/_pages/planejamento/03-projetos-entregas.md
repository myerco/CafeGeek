---
title: Acompanhamento
excerpt: Acompanhamento
permalink: /pages/planejamento/entrega
last_modified_at: 2023-08-26T08:48:05-04:00
toc: true
mermaid: true
sidebar:
    nav: planejamento
categories:
  - Planejamento
  - Entregas
tags:
  - Planejamento
---

## Level 1

<div class="mermaid">
timeline
        title Entregas 2023/02
        section 2023 N1 Avaliação
          Agaby : Protótipo
                : Personagens
                : Gameplay
          Airon : Protótipo
                : Personagens
                : Gameplay
        section 2023 N2 Avaliação
          Agaby : UI
                : Level 1
          Airon : UI
                : Level 1
</div>

<div class="mermaid">
flowchart TB
    A[Start] --> B[Recebimento]
    subgraph Abertos
    a1["Viabilidade"]-->a2["Requisitos"]
    a2 --> a3["Priorização"]
    end
    subgraph Fazer
    a3 --> b1["Elaborar Projeto"]
    end
    subgraph Fazendo
    b1 --> c1["Implementação"]
    c1 --> c2["Testes"]
    c2 --> c3["Entregas"]
    end
    subgraph Espera
    c3 --> d1["Tetes negocial"]
    d1 --> d2["Homologação"]
    d2 --> d3{"Sim/Não"}
    d3 -- Não --> c1
    d3 -- Sim --> d4{"Sim/Não"}
    d4 -- Sim --> c1
    end
    subgraph Fechado
    d4 -- Não --> e1["Termo Entrega Final"]
    end
</div>