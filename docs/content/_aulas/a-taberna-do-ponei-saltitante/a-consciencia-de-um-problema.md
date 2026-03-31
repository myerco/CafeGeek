---
title: "A Consciência de um Problema"
excerpt: ""
categories:
  - "a-taberna-do-ponei-saltitante"
  - "prologo"
date: 2026-03-01T08:48:05-04:00
order: 5
tags:
  - banco-de-dados
sidebar:
  nav: a-taberna-do-ponei-saltitante
---

Toda grande jornada começa em um **Mundo Comum**, um lugar familiar onde a vida segue seu ritmo habitual. O herói tem uma consciência limitada de que um problema se avizinha. Para nossa aventura, nosso herói — você — chega a um lugar que precisa de ajuda, mesmo que seu gerente ainda não saiba exatamente como.

> ![thought-bubble](https://game-icons.net/icons/000000/transparent/1x1/seregacthtuf/thought-bubble.svg){: .align-left width="32"}
> Nosso "Mundo Comum" é a gestão da Taberna do Pônei Saltitante. Seu proprietário, Cevado Carrapicho, um homem ocupado e um tanto esquecido, sabe que seu negócio está crescendo, mas suas anotações em pergaminhos e sua memória já não são suficientes. Ele tem a **consciência limitada de um problema**: a desorganização. Tudo é feito "na raça", em planilhas mentais e pedidos anotados em guardanapos.
{: .notice--info}

Esta atividade consiste em ser o herói que dará o primeiro passo para trazer ordem a este caos, iniciando o desenvolvimento de um projeto de banco de dados relacional com PostgreSQL.

## Uma Hospedaria no Fim da Terra-de-Ninguém

A cidade de Bree conseguiu se manter próspera no Norte, apesar das guerras que destruíram o antigo Reino dos Dúnedain. É a única região na Terra-média onde Homens e Hobbits convivem em harmonia, servindo como um importante centro comercial para Elfos, Anões e outras raças que viajam entre reinos.

O coração pulsante de Bree é a **Taverna do Pônei Saltitante**, famosa por suas cervejas e por ser um refúgio para todo tipo de viajante.

## Os personagens

Vamos expandir nossos personagens com biografias completas, inspiradas no universo do Senhor dos Anéis, e incluir uma breve história de suas classes. Cada personagem representa um papel na taberna, mas com um toque épico.

### 1. Cevado Carrapicho (Barliman Butterbur)

- **Raça**: Humano
- **Classe**: Paladino (Guerreiro Sagrado)
- **Região**: Sul da cidade de Bree
- **Biografia**: Cevado Carrapicho é o proprietário da Taberna do Pônei Saltitante, um homem robusto e hospitaleiro que herdou o estabelecimento de seu pai. Nascido em Bree durante os tempos turbulentos das Guerras dos Anéis, Cevado sempre sonhou em manter a paz e a prosperidade em sua cidade. Ele é conhecido por sua memória afiada para rostos e histórias, mas com o crescimento do negócio, suas anotações em pergaminhos se tornaram caóticas. Como um paladino, Cevado jurou proteger os viajantes e manter a harmonia entre as raças, frequentemente intervindo em disputas com sua autoridade moral e força física. Sua vitalidade é lendária, permitindo-lhe trabalhar longas horas sem descanso, e sua resistência o torna imbatível em brigas de taverna.
- **História da Classe**: Os Paladinos são guerreiros sagrados dedicados à proteção e justiça. Originários das tradições dos Dúnedain, eles combinam força bruta com um código de honra, jurando defender os fracos e manter a paz. No mundo de RPG, paladinos ganham poderes divinos à medida que sobem de nível, curando aliados e banindo o mal.

### 2. Aragorn (como Estranho, um guerreiro errante)

- **Raça**: Humano (Dúnedain)
- **Classe**: Guerreiro (Ranger)
- **Região**: Norte da cidade de Bree
- **Biografia**: Aragorn, conhecido como Estranho na taberna, é um ranger errante que frequentemente passa por Bree em suas jornadas. Descendente dos reis de Gondor, ele vive uma vida nômade, protegendo as estradas contra orcs e lobos. Na taberna, ele ajuda Cevado com tarefas pesadas, como carregar barris ou resolver conflitos. Sua força e agilidade são excepcionais, treinadas em batalhas contra as forças das trevas. Aragorn carrega o peso de seu legado, esperando o momento de reclamar seu trono, mas por ora, encontra paz servindo cerveja e ouvindo histórias.
- **História da Classe**: Guerreiros são mestres do combate físico, especializados em armas e armaduras. Eles evoluem de recrutas a heróis lendários, ganhando habilidades como ataques poderosos e resistência a danos. Rangers, uma especialização, focam em furtividade e sobrevivência na natureza.

### 3. Gandalf (como o Velho Mago Cinzento, um conselheiro sábio)

- **Raça**: Maia (aparentando como Humano)
- **Classe**: Mago (Feiticeiro)
- **Região**: Sul da cidade de Bree
- **Biografia**: Gandalf, o mago cinzento, é um visitante frequente da taberna, onde fuma seu cachimbo e compartilha histórias antigas. Como um Istari enviado para combater Sauron, ele usa sua inteligência e magia para guiar os heróis da Terra-média. Na taberna, Gandalf ajuda com conselhos sobre organização e, ocasionalmente, lança feitiços menores para iluminar o salão ou curar ferimentos leves. Sua vitalidade parece infinita, e sua inteligência é incomparável, permitindo-lhe resolver enigmas e prever perigos.
- **História da Classe**: Magos são estudiosos da magia arcana, lançando feitiços poderosos e manipulando elementos. Eles começam como aprendizes e ascendem a arquimagos, ganhando acesso a magias cada vez mais complexas, como teleporte e controle mental.

### 4. Frodo Bolseiro (como um hobbit aventureiro)

- **Raça**: Hobbit
- **Classe**: Ladino (Explorador)
- **Região**: Sul da cidade de Bree
- **Biografia**: Frodo Bolseiro, um hobbit do Condado, é um cliente regular que traz notícias do Oeste. Após sua grande jornada, ele se estabeleceu temporariamente em Bree, ajudando na taberna com tarefas leves devido à sua agilidade. Sobrevivente do Anel, Frodo carrega cicatrizes invisíveis, mas sua resiliência e inteligência o tornam um aliado valioso. Ele organiza pequenos eventos e mantém o moral alto com suas histórias.
- **História da Classe**: Ladinos são especialistas em furtividade, armadilhas e exploração. Eles evoluem de ladrões a mestres espiões, ganhando habilidades como invisibilidade e desarmar dispositivos.
  