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
    excludes weekends

    section Milestones
        Trabalho 1 (2pt)             :milestone, 2023-08-29, 0d
        Trabalho 2 (2pt)             :milestone, 2023-09-26, 0d        
        Avaliação N1 (6pt)           :milestone, 2023-09-26, 0d                

    section Agaby
    Arte 2D                                   :active,  a1, 2023-08-08, 7d
    Animações (Andar, Correr, Pular,Espera)   :active,  a2, 2023-08-15, 7d
    Apresentação                              :crit, a3, 2023-08-29, 1d                
    
    section Airon
    Desafios                                  :active, b1,2023-08-08, 7d
    Objetos                                   :active,  b2, 2023-08-15,7d
    Apresentação                              :crit, b3, 2023-08-29, 1d                    

    section Alefe e Lucas
    História                                  :done, c1,2023-08-08, 7d
    Mapa                                      :active,  c1, 2023-08-15,7d
    Apresentação                              :crit, c3, 2023-08-29, 1d                    

    section Gibran
    Modelos                                  :done, d1,2023-08-08, 7d
    Inimigos                                 :active,  d2, 2023-08-15,7d
    Apresentação                             :crit, d3, 2023-08-29, 1d                        

    section Luis Fernando
    Projeto                                  :done, b1,2023-08-08, 7d
    Protótipo Level 1                        :active,  a1, 2023-08-15,7d    
    Apresentação                             :milestone, m1, 2023-08-29, 0d        

    section Olímipio
    Projeto                                  :done, b1,2023-08-08, 7d
    Apresentação                             :crit, b2, 2023-08-29, 1d            
    
    section Henrique e Luis
    Projeto Endless Runner                  :done, b1,2023-08-08, 7d
    Protótipo                               :active,  a1, 2023-08-15,7d    
    Apresentação                            :milestone, m1, 2023-08-29, 0d        

    section Caio
    Projeto Semestre anterior               :done, b1,2023-08-08, 7d
    Protótipo                               :active,  a1, 2023-08-15,7d    
    Apresentação                            :crit, b2, 2023-08-29, 1d                

</div>