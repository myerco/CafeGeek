---
title: Acompanhamento
excerpt: Acompanhamento
permalink: /pages/planejamento/acompanhamento
last_modified_at: 2023-08-26T08:48:05-04:00
toc: true
mermaid: true
sidebar:
    nav: planejamento
categories:
  - Planejamento
  - Acompanhamento
tags:
  - Planejamento
---

## Level 1

<div class="mermaid">
gantt
    title Cronograma
    dateFormat YYYY-MM-DD
    exclude weekends
    section Agaby
        Arte 2D                                   :active,  a1, 2023-08-15, 30d
        Animações (Andar, Correr, Pular,Espera)   :         a2, after a1, 20d
    section Airon
        Desafios                                  :active, b1,2023-08-15, 30d
        Objetos                                   :        b2,after a1, 20d
</div>