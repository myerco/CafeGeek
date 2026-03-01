---
title: Mundo Comum
excerpt: "Conciência limitada de um problema : Esta atividade consiste em iniciar o desenvolvimento de um projeto de banco de dados relacional utilizando o PostgreSQL. O objetivo é criar a estrutura inicial do projeto, sem detalhar regras de negócio ou requisitos avançados neste momento."
categories:
  - "banco-de-dados"
  - "a-jornada-do-heroi"
  - "ato-i"
date: 2026-01-31T08:48:05-04:00
order: 2
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

Neste projeto iremos utilizar como exemplo de negócio um empreendimento famoso conhecido na literatura que é a Taberna do Pônei Saltitante 
localizada na cidade de Bree presente nas obras de J.R.R. Tolkien.

Esta atividade consiste em iniciar o desenvolvimento de um projeto de banco de dados relacional utilizando o PostgreSQL. O objetivo é criar a estrutura inicial do projeto, sem detalhar regras de negócio ou requisitos avançados neste momento.

O aluno chega sem saber nada de banco de dados. É o "povoado pacato" onde tudo é feito "na raça", em planilhas bagunçadas ou sem persistência.
{: .notice}

## A cidade de Bree

{% include imagelocal.html
    src="a-taberna-ponei-saltitante/250px-Darek_Zabrocki_-_Morning.webp"
    alt="Figura: A cidade de Bree."
    caption="Figura: A cidade de Bree."
    idref="TOLKIEN GATEWAY, Bree"
    ref="http://tolkiengateway.net/wiki/Bree"
%}

![image-left](/assets/images/a-taberna-ponei-saltitante/treasure-map.png){: .align-left} A cidade de Bree conseguiu se manter prospera próspera no Norte, apesar das guerras e tumultos que destruíram o Reino dos Dúnedain do Norte. Dizem que quando os homens foram para o Ocidente, Bree já estava lá e quando os antigos reis retornaram, encontraram Bree os esperando. Dizem que foi fundada pors homens que não voltaram para Beleriand na Primeira Era, e após a queda do Reino de Cardolan na guerra conta Angmar se tornou uma cidade independente.

{% include imagelocal.html
    src="a-taberna-ponei-saltitante/Map_of_Bree_-_LOTRO.webp"
    alt="Figura: Mapa da cidade de Bree."
    caption="Figura: Mapa da cidade de Bree."
    idref="TOLKIEN GATEWAY, Bree"
    ref="https://lotr.fandom.com/wiki/Bree"
%}

É a única região na Terra-média, onde Homens e Hobbits convivem em harmonia e e um importante centro comercial para elfos e anões, que são bens de comércio ou viagens de um reino para outro. O centro econômico e social é a **Taverna do Pônei Saltitante**, conhecida por ter as melhores bebidas do Norte.

## Taverna do Pônei Saltitante e o projeto

{% include image.html
    src="https://3.bp.blogspot.com/-bbFXtl8DLsM/WhswXoihJKI/AAAAAAAANa4/vOl3JpqLHJY9-rgkRmd87yTkF1vUZ2hAgCLcBGAs/s320/tabernaponeisaltitante.jpg"
    alt="Figura: A Taberna do Pônei Saltitante."
    caption="Figura: A Taberna do Pônei Saltitante."
%}

![image-left](/assets/images/a-taberna-ponei-saltitante/tavern-sign-150x150.png){: .align-left} A Taberna do Ponei Saltitante está ampliando o seu atendimento, buscando atender melhor sua variada clientela, Orc´s, Elfos, Hobbits e Humanos, este último com uma preferência estranha por dispositivos. Também se aliou ao Ferreiro da cidade a fim de diversificar os produtos, acrescentando espadas, escudos, elmos e outros.

## Os Objetivos

- Definir o escopo geral do projeto: criar um sistema para uma taberna que atende diversas raças e agora se aliou a um ferreiro para vender equipamentos de combate.
- A Preparação: O herói prepara sua "mochila de equipamentos", criando o repositório no GitHub e desenhando o primeiro mapa da região através de um diagrama MERMAID inicial.

## Regras  

Siga o passo a passo abaixo para implementar e apresentar seu projeto:

1. Crie ou utilize uma conta existente no GitHub.
2. Crie um repositório com o nome do projeto escolhido.
3. No README.md do repositório, inclua:
   - Breve apresentação do projeto (tema e objetivo geral)
   - Estrutura inicial do projeto (pastas, arquivos principais)
   - Versão inicial do projeto
   - Modelo de dados do projeto (utilize o diagrama MERMAID para representar as tabelas e relações)
4. Faça o commit inicial com o README.md e o diagrama do modelo de dados.
5. Compartilhe o link do repositório no ambiente da disciplina para avaliação.

## Referências

- [Mermaid Live](https://mermaid.live/)
- [Mermaid Tutorials](https://mermaid.js.org/ecosystem/tutorials.html)
- [Mermaid Entity Relationships Diagrams  - ER](https://mermaid.js.org/syntax/entityRelationshipDiagram.html)
- [Github](https://github.com/)
- [Banco PostgreSQL para implementações](https://comp-pga.qute.com.br/login?next=/)