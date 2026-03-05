---
title: "O Mundo Comum"
excerpt: "A Jornada do Herói começa. Nesta atividade, o aluno inicia o desenvolvimento de um projeto de banco de dados, criando a estrutura inicial para a Taberna do Pônei Saltitante."
categories:
  - "banco-de-dados"
  - "a-jornada-do-heroi"
  - "ato-i"
date: 2026-03-01T08:48:05-04:00
order: 2
tags:
  - banco-de-dados
sidebar:
  nav: a-taberna-do-ponei-saltitante
---

{% include image.html
    src="https://i.pinimg.com/originals/3b/31/e3/3b31e34debef0e079a148d8941af59de.jpg"
    alt="Figura: O Condado, o mundo comum de onde muitos heróis partem."
    caption="O Condado de J.R.R. Tolkien, um perfeito 'Mundo Comum' antes da aventura começar."
    idref="WIKIPEDIA,O Senhor dos Anéis."
    ref="https://pt.wikipedia.org/wiki/O_Senhor_dos_An%C3%A9is"
%}

## Prólogo: A Consciência de um Problema

Toda grande jornada começa em um **Mundo Comum**, um lugar familiar onde a vida segue seu ritmo habitual. O herói tem uma consciência limitada de que um problema se avizinha. Para nossa aventura, nosso herói — você — chega a um lugar que precisa de ajuda, mesmo que seu gerente ainda não saiba exatamente como.

> ![thought-bubble](https://game-icons.net/icons/000000/transparent/1x1/seregacthtuf/thought-bubble.svg){: .align-left width="48"}
> Nosso "Mundo Comum" é a gestão da Taberna do Pônei Saltitante. Seu proprietário, Cevado Carrapicho, um homem ocupado e um tanto esquecido, sabe que seu negócio está crescendo, mas suas anotações em pergaminhos e sua memória já não são suficientes. Ele tem a **consciência limitada de um problema**: a desorganização. Tudo é feito "na raça", em planilhas mentais e pedidos anotados em guardanapos.
{: .notice--info}

Esta atividade consiste em ser o herói que dará o primeiro passo para trazer ordem a este caos, iniciando o desenvolvimento de um projeto de banco de dados relacional com PostgreSQL.

## Capítulo 1: Uma Hospedaria no Fim da Terra-de-Ninguém

{% include imagelocal.html
    src="a-taberna-ponei-saltitante/250px-Darek_Zabrocki_-_Morning.webp"
    alt="Figura: A cidade de Bree."
    caption="A cidade de Bree ao amanhecer."
    idref="TOLKIEN GATEWAY, Bree"
    ref="http://tolkiengateway.net/wiki/Bree"
%}

A cidade de Bree conseguiu se manter próspera no Norte, apesar das guerras que destruíram o antigo Reino dos Dúnedain. É a única região na Terra-média onde Homens e Hobbits convivem em harmonia, servindo como um importante centro comercial para Elfos, Anões e outras raças que viajam entre reinos.

O coração pulsante de Bree é a **Taverna do Pônei Saltitante**, famosa por suas cervejas e por ser um refúgio para todo tipo de viajante.

{% include image.html
    src="https://3.bp.blogspot.com/-bbFXtl8DLsM/WhswXoihJKI/AAAAAAAANa4/vOl3JpqLHJY9-rgkRmd87yTkF1vUZ2hAgCLcBGAs/s320/tabernaponeisaltitante.jpg"
    alt="Figura: A Taberna do Pônei Saltitante."
    caption="A famosa Taberna do Pônei Saltitante."
%}

## Capítulo 2: O Chamado à Aventura

![image-left](/assets/images/a-taberna-ponei-saltitante/tavern-sign-150x150.png){:width="48" .align-left} O Pônei Saltitante está expandindo seus negócios! Para melhor atender sua clientela variada de Anões, Elfos, Hobbits e Homens, a taverna agora se aliou ao Ferreiro da cidade. Além das bebidas e da hospitalidade, agora também venderá espadas, escudos e elmos.

Cevado Carrapicho está sobrecarregado. Como gerenciar o estoque de bebidas e de armas? Como registrar os pedidos de clientes tão diferentes? Ele precisa de um sistema, uma forma de organizar tudo antes que sua taverna se afogue em pergaminhos perdidos e barris não contabilizados.

Este é o seu **Chamado à Aventura**: usar suas habilidades para criar a estrutura de um banco de dados que salvará o Pônei Saltitante.

---

## Sua Missão: O Primeiro Mapa do Território

Como um aventureiro preparando sua mochila, seu primeiro passo é criar as ferramentas e o mapa inicial para esta jornada. Sua missão é estruturar o projeto e desenhar o primeiro diagrama do modelo de dados.

Siga os passos abaixo:

1. ![quill-ink](https://game-icons.net/icons/000000/transparent/1x1/lorc/quill-ink.svg){:width="48" .align-left}
**Forje seu Diário de Bordo:** Crie ou utilize sua conta no **GitHub**. Este será o registro de toda a sua jornada.
2. ![bookshelf](https://game-icons.net/icons/000000/transparent/1x1/delapouite/bookshelf.svg){:width="48" .align-left}
**Nomeie sua Aventura:** Crie um novo repositório com um nome para o projeto (ex: `taverna-ponei-saltitante-db`).
3. ![treasure-map](https://game-icons.net/icons/000000/transparent/1x1/lorc/treasure-map.svg){:width="48" .align-left} **Desenhe o Primeiro Mapa (`README.md`):** No arquivo `README.md` do seu repositório, você irá detalhar o plano da sua missão. Ele deve incluir:
    - **Apresentação da Missão:** Um breve resumo do tema (gerenciar a Taberna do Pônei Saltitante) e seu objetivo (criar um banco de dados para controlar clientes, produtos e vendas).
    - **O Mapa do Mundo (Diagrama MERMAID):** Crie um **Modelo de Entidade e Relacionamento (MER)** inicial usando a sintaxe do Mermaid. Este diagrama representará as primeiras tabelas e suas relações. Pense nas entidades principais: `Clientes`, `Produtos`, `Pedidos`... Como elas se conectam?
4. ![position-marker](https://game-icons.net/icons/000000/transparent/1x1/delapouite/position-marker.svg){:width="48" .align-left} **Marque seu Ponto de Partida:** Faça o `commit` inicial no seu repositório com o `README.md` contendo o diagrama. Esta será a versão "0.1" da sua jornada.
5. ![mailbox](https://game-icons.net/icons/000000/transparent/1x1/delapouite/mailbox.svg){:width="48" .align-left}
**Compartilhe suas Intenções:** Compartilhe o link do seu repositório no ambiente da disciplina para que seu progresso possa ser avaliado.

## Ferramentas do Aventureiro

Recursos essenciais para completar sua missão:

- ![compass](https://game-icons.net/icons/000000/transparent/1x1/lorc/compass.svg){:width="32"} **Cartografia (Diagramas):**
  - [Mermaid Live](https://mermaid.live/) (Editor online para criar seu diagrama)
  - [Mermaid ERD Syntax](https://mermaid.js.org/syntax/entityRelationshipDiagram.html)
- ![book](https://game-icons.net/icons/000000/transparent/1x1/delapouite/stabbed-note.svg){:width="32"} **Diário de Bordo:**
  - [Github](https://github.com/)
- ![scroll-unfurled](https://game-icons.net/icons/000000/transparent/1x1/lorc/scroll-unfurled.svg){:width="32"} **Conhecimento Ancestral:**
  - [A Jornada do Herói](https://viverdeblog.com/jornada-do-heroi/)
  - [Modelo de Entidade e Relacionamento](https://cafegeek.eti.br/curso/banco-de-dados/modelo-de-dados/modelo-de-entidade-e-relacionamento/)
- ![anvil](https://game-icons.net/icons/000000/transparent/1x1/lorc/anvil.svg){:width="32"} **A Forja (Onde a magia acontece):**
  - [Banco PostgreSQL para implementações](https://comp-pga.qute.com.br/login?next=/)
