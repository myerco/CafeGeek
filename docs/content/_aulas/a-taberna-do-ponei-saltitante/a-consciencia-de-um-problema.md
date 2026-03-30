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

## Estruturas das Tabelas

Agora, vamos organizar e expandir nosso modelo de banco de dados. Apresentaremos as tabelas em formato Markdown, adicionando novas tabelas essenciais para um jogo RPG, como quests, tarefas, itens e inventário.

### Tabela: Regioes

| id  | nome    | imagem | coordenadas | bio                      | tipo   | pai |
| --- | ------- | ------ | ----------- | ------------------------ | ------ | --- |
| 1   | Bree    | <>     | 10,20       | Cidade próspera no Norte | cidade | 0   |
| 2   | Condado | <>     | 5,15        | Terra dos Hobbits        | região | 0   |
| 3   | Gondor  | <>     | 50,60       | Reino do Sul             | reino  | 0   |

### Tabela: Racas

| id  | nome   | imagem |
| --- | ------ | ------ |
| 1   | Humano | <>     |
| 2   | Hobbit | <>     |
| 3   | Elfo   | <>     |
| 4   | Anão   | <>     |

### Tabela: Classes

| id  | nome      | imagem | historia                                                        |
| --- | --------- | ------ | --------------------------------------------------------------- |
| 1   | Guerreiro | <>     | Mestres do combate físico, especializados em armas e armaduras. |
| 2   | Mago      | <>     | Estudiosos da magia arcana, lançando feitiços poderosos.        |
| 3   | Paladino  | <>     | Guerreiros sagrados dedicados à proteção e justiça.             |
| 4   | Ladino    | <>     | Especialistas em furtividade, armadilhas e exploração.          |

### Tabela: Sexos

| id  | nome      | imagem |
| --- | --------- | ------ |
| 1   | Masculino | <>     |
| 2   | Feminino  | <>     |

### Tabela: Especializacoes

| id  | nome          | classe_id |
| --- | ------------- | --------- |
| 1   | Guerreiro DPS | 1         |
| 2   | Tank          | 1         |
| 3   | Mago DPS      | 2         |
| 4   | Curandeiro    | 2         |

### Tabela: Niveis

| id  | nome    | xp  | categoria_id |
| --- | ------- | --- | ------------ |
| 1   | Nível 1 | 0   | 1            |
| 2   | Nível 2 | 100 | 1            |
| 3   | Nível 3 | 300 | 1            |

### Tabela: Categorias

| id  | nome          |
| --- | ------------- |
| 1   | Iniciante     |
| 2   | Intermediário |
| 3   | Avançado      |

### Tabela: PersonagemBase

| id  | nome              | esqueleto | raca_id | classe_id | cor   | sexo_id | vitalidade | forca | agilidade | resistencia | inteligencia | protecao | bio                       | imagem_pequena | imagem_grande | nivel | regiao_id | pontos_atuais | pontos_proximo_nivel |
| --- | ----------------- | --------- | ------- | --------- | ----- | ------- | ---------- | ----- | --------- | ----------- | ------------ | -------- | ------------------------- | -------------- | ------------- | ----- | --------- | ------------- | -------------------- |
| 1   | Cevado Carrapicho | mannequim | 1       | 3         | azul  | 1       | 120        | 90    | 70        | 100         | 80           | 90       | Proprietário hospitaleiro | <>             | <>            | 5     | 1         | 450           | 550                  |
| 2   | Aragorn           | mannequim | 1       | 1         | cinza | 1       | 110        | 100   | 95        | 90          | 85           | 85       | Ranger errante            | <>             | <>            | 10    | 1         | 1200          | 1400                 |
| 3   | Gandalf           | mannequim | 1       | 2         | cinza | 1       | 100        | 70    | 80        | 80          | 120          | 70       | Mago sábio                | <>             | <>            | 15    | 1         | 2000          | 2300                 |
| 4   | Frodo Bolseiro    | mannequim | 2       | 4         | verde | 1       | 80         | 60    | 100       | 70          | 90           | 60       | Hobbit aventureiro        | <>             | <>            | 8     | 2         | 800           | 950                  |

### Tabela: PersonagemEspecializacoes

| personagem_id | especializacao_id | pontos_aprendidos | nivel_maturidade |
| ------------- | ----------------- | ----------------- | ---------------- |
| 1             | 2                 | 50                | 3                |
| 2             | 1                 | 80                | 5                |

### Tabela: PersonagemHabilidades

| personagem_id | habilidade_id |
| ------------- | ------------- |
| 1             | 1             |
| 2             | 2             |

### Tabela: Habilidades

| id  | nome            | descricao        |
| --- | --------------- | ---------------- |
| 1   | Ataque Poderoso | Causa dano extra |
| 2   | Cura            | Restaura vida    |

### Tabela: Animacoes

| id  | nome   | animacao |
| --- | ------ | -------- |
| 1   | Ataque | gif1     |
| 2   | Defesa | gif2     |

### Tabela: PersonagemAnimacoes

| personagem_id | animacao_id |
| ------------- | ----------- |
| 1             | 1           |

### Novas Tabelas para RPG

#### Tabela: Quests

| id  | nome           | descricao        | recompensa_xp | recompensa_ouro | nivel_requerido | regiao_id |
| --- | -------------- | ---------------- | ------------- | --------------- | --------------- | --------- |
| 1   | Limpar Taverna | Expulsar bêbados | 50            | 10              | 1               | 1         |
| 2   | Entregar Carta | Levar mensagem   | 100           | 20              | 2               | 1         |

#### Tabela: Tarefas

| id  | quest_id | nome      | descricao         | concluida |
| --- | -------- | --------- | ----------------- | --------- |
| 1   | 1        | Conversar | Falar com Cevado  | false     |
| 2   | 1        | Lutar     | Derrotar inimigos | false     |

#### Tabela: Itens

| id  | nome   | tipo       | descricao   | valor |
| --- | ------ | ---------- | ----------- | ----- |
| 1   | Espada | Arma       | Arma afiada | 50    |
| 2   | Poção  | Consumível | Cura vida   | 10    |

#### Tabela: Personagem_Itens

| personagem_id | item_id | quantidade |
| ------------- | ------- | ---------- |
| 1             | 1       | 1          |
| 2             | 2       | 5          |

#### Tabela: Inventario

| id  | personagem_id | item_id | quantidade | equipado |
| --- | ------------- | ------- | ---------- | -------- |
| 1   | 1             | 1       | 1          | true     |

## Diagrama do Modelo de Dados (Mermaid)

Aqui está um diagrama ER simplificado do nosso modelo de banco de dados, representando as relações entre as tabelas principais.

<div class="mermaid">
erDiagram
    PersonagemBase ||--o{ PersonagemEspecializacoes : "tem"
    PersonagemBase ||--o{ PersonagemHabilidades : "possui"
    PersonagemBase ||--o{ PersonagemAnimacoes : "usa"
    PersonagemBase ||--o{ Personagem_Itens : "carrega"
    PersonagemBase ||--o{ Inventario : "gerencia"
    PersonagemBase }o--|| Regioes : "origem"
    PersonagemBase }o--|| Racas : "pertence"
    PersonagemBase }o--|| Classes : "é"
    PersonagemBase }o--|| Sexos : "tem"
    PersonagemBase }o--|| Niveis : "está em"
    Niveis }o--|| Categorias : "classificado"
    Especializacoes }o--|| Classes : "subtipo de"
    PersonagemEspecializacoes }o--|| Especializacoes : "especializa"
    PersonagemHabilidades }o--|| Habilidades : "aprende"
    PersonagemAnimacoes }o--|| Animacoes : "anima"
    Personagem_Itens }o--|| Itens : "possui"
    Inventario }o--|| Itens : "contém"
    Quests ||--o{ Tarefas : "composta de"
    Quests }o--|| Regioes : "localizada em"
</div>

## Comandos SQL: CREATE TABLE

Agora, vamos implementar os comandos CREATE TABLE em PostgreSQL para criar nossas tabelas. Lembre-se de executar estes comandos em sequência, considerando as dependências de chaves estrangeiras.

```sql
-- Tabela Regioes
CREATE TABLE Regioes (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    imagem VARCHAR(255),
    coordenadas VARCHAR(50),
    bio TEXT,
    tipo VARCHAR(50),
    pai INTEGER REFERENCES Regioes(id)
);

-- Tabela Racas
CREATE TABLE Racas (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    imagem VARCHAR(255)
);

-- Tabela Classes
CREATE TABLE Classes (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    imagem VARCHAR(255),
    historia TEXT
);

-- Tabela Sexos
CREATE TABLE Sexos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    imagem VARCHAR(255)
);

-- Tabela Especializacoes
CREATE TABLE Especializacoes (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    classe_id INTEGER REFERENCES Classes(id)
);

-- Tabela Categorias
CREATE TABLE Categorias (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);

-- Tabela Niveis
CREATE TABLE Niveis (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    xp INTEGER NOT NULL,
    categoria_id INTEGER REFERENCES Categorias(id)
);

-- Tabela PersonagemBase
CREATE TABLE PersonagemBase (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    esqueleto VARCHAR(50),
    raca_id INTEGER REFERENCES Racas(id),
    classe_id INTEGER REFERENCES Classes(id),
    cor VARCHAR(50),
    sexo_id INTEGER REFERENCES Sexos(id),
    vitalidade INTEGER,
    forca INTEGER,
    agilidade INTEGER,
    resistencia INTEGER,
    inteligencia INTEGER,
    protecao INTEGER,
    bio TEXT,
    imagem_pequena VARCHAR(255),
    imagem_grande VARCHAR(255),
    nivel INTEGER,
    regiao_id INTEGER REFERENCES Regioes(id),
    pontos_atuais INTEGER,
    pontos_proximo_nivel INTEGER
);

-- Tabela PersonagemEspecializacoes
CREATE TABLE PersonagemEspecializacoes (
    personagem_id INTEGER REFERENCES PersonagemBase(id),
    especializacao_id INTEGER REFERENCES Especializacoes(id),
    pontos_aprendidos INTEGER,
    nivel_maturidade INTEGER,
    PRIMARY KEY (personagem_id, especializacao_id)
);

-- Tabela Habilidades
CREATE TABLE Habilidades (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    descricao TEXT
);

-- Tabela PersonagemHabilidades
CREATE TABLE PersonagemHabilidades (
    personagem_id INTEGER REFERENCES PersonagemBase(id),
    habilidade_id INTEGER REFERENCES Habilidades(id),
    PRIMARY KEY (personagem_id, habilidade_id)
);

-- Tabela Animacoes
CREATE TABLE Animacoes (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    animacao VARCHAR(255)
);

-- Tabela PersonagemAnimacoes
CREATE TABLE PersonagemAnimacoes (
    personagem_id INTEGER REFERENCES PersonagemBase(id),
    animacao_id INTEGER REFERENCES Animacoes(id),
    PRIMARY KEY (personagem_id, animacao_id)
);

-- Tabela Itens
CREATE TABLE Itens (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    tipo VARCHAR(50),
    descricao TEXT,
    valor INTEGER
);

-- Tabela Personagem_Itens
CREATE TABLE Personagem_Itens (
    personagem_id INTEGER REFERENCES PersonagemBase(id),
    item_id INTEGER REFERENCES Itens(id),
    quantidade INTEGER,
    PRIMARY KEY (personagem_id, item_id)
);

-- Tabela Inventario
CREATE TABLE Inventario (
    id SERIAL PRIMARY KEY,
    personagem_id INTEGER REFERENCES PersonagemBase(id),
    item_id INTEGER REFERENCES Itens(id),
    quantidade INTEGER,
    equipado BOOLEAN DEFAULT FALSE
);

-- Tabela Quests
CREATE TABLE Quests (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    descricao TEXT,
    recompensa_xp INTEGER,
    recompensa_ouro INTEGER,
    nivel_requerido INTEGER,
    regiao_id INTEGER REFERENCES Regioes(id)
);

-- Tabela Tarefas
CREATE TABLE Tarefas (
    id SERIAL PRIMARY KEY,
    quest_id INTEGER REFERENCES Quests(id),
    nome VARCHAR(100) NOT NULL,
    descricao TEXT,
    concluida BOOLEAN DEFAULT FALSE
);
```

## Comandos SQL: INSERT INTO

Agora, vamos inserir dados iniciais em nossas tabelas, usando personagens e elementos do Senhor dos Anéis para tornar o exemplo mais imersivo.

```sql
-- Inserir Regioes
INSERT INTO Regioes (nome, coordenadas, bio, tipo, pai) VALUES
('Bree', '10,20', 'Cidade próspera no Norte da Terra-média', 'cidade', NULL),
('Condado', '5,15', 'Terra pacífica dos Hobbits', 'região', NULL),
('Gondor', '50,60', 'Reino do Sul, lar dos Homens', 'reino', NULL);

-- Inserir Racas
INSERT INTO Racas (nome) VALUES
('Humano'),
('Hobbit'),
('Elfo'),
('Anão');

-- Inserir Classes
INSERT INTO Classes (nome, historia) VALUES
('Guerreiro', 'Mestres do combate físico, especializados em armas e armaduras.'),
('Mago', 'Estudiosos da magia arcana, lançando feitiços poderosos.'),
('Paladino', 'Guerreiros sagrados dedicados à proteção e justiça.'),
('Ladino', 'Especialistas em furtividade, armadilhas e exploração.');

-- Inserir Sexos
INSERT INTO Sexos (nome) VALUES
('Masculino'),
('Feminino');

-- Inserir Especializacoes
INSERT INTO Especializacoes (nome, classe_id) VALUES
('Guerreiro DPS', 1),
('Tank', 1),
('Mago DPS', 2),
('Curandeiro', 2);

-- Inserir Categorias
INSERT INTO Categorias (nome) VALUES
('Iniciante'),
('Intermediário'),
('Avançado');

-- Inserir Niveis
INSERT INTO Niveis (nome, xp, categoria_id) VALUES
('Nível 1', 0, 1),
('Nível 2', 100, 1),
('Nível 3', 300, 1),
('Nível 5', 700, 2),
('Nível 8', 1200, 2),
('Nível 10', 1800, 2),
('Nível 15', 3000, 3);

-- Inserir Personagens
INSERT INTO PersonagemBase (nome, esqueleto, raca_id, classe_id, cor, sexo_id, vitalidade, forca, agilidade, resistencia, inteligencia, protecao, bio, nivel, regiao_id, pontos_atuais, pontos_proximo_nivel) VALUES
('Cevado Carrapicho', 'mannequim', 1, 3, 'azul', 1, 120, 90, 70, 100, 80, 90, 'Proprietário hospitaleiro da Taberna do Pônei Saltitante, dedicado à paz em Bree.', 5, 1, 450, 550),
('Aragorn', 'mannequim', 1, 1, 'cinza', 1, 110, 100, 95, 90, 85, 85, 'Ranger errante, herdeiro do trono de Gondor, protetor das estradas.', 10, 1, 1200, 1400),
('Gandalf', 'mannequim', 1, 2, 'cinza', 1, 100, 70, 80, 80, 120, 70, 'Mago sábio, Istari enviado para combater o mal na Terra-média.', 15, 1, 2000, 2300),
('Frodo Bolseiro', 'mannequim', 2, 4, 'verde', 1, 80, 60, 100, 70, 90, 60, 'Hobbit aventureiro, portador do Anel, sobrevivente de grandes jornadas.', 8, 2, 800, 950);

-- Inserir Habilidades
INSERT INTO Habilidades (nome, descricao) VALUES
('Ataque Poderoso', 'Causa dano extra com armas'),
('Cura', 'Restaura pontos de vida'),
('Invisibilidade', 'Torna o personagem invisível temporariamente'),
('Teleporte', 'Move o personagem instantaneamente');

-- Inserir PersonagemHabilidades
INSERT INTO PersonagemHabilidades (personagem_id, habilidade_id) VALUES
(1, 1),
(2, 1),
(3, 4),
(4, 3);

-- Inserir Itens
INSERT INTO Itens (nome, tipo, descricao, valor) VALUES
('Espada de Aragorn', 'Arma', 'Espada ancestral dos reis de Gondor', 200),
('Cajado de Gandalf', 'Arma', 'Cajado mágico com poderes arcanos', 300),
('Anel Único', 'Artefato', 'O Anel do Poder, fonte de grande mal', 10000),
('Poção de Cura', 'Consumível', 'Restaura 50 pontos de vida', 20);

-- Inserir Personagem_Itens
INSERT INTO Personagem_Itens (personagem_id, item_id, quantidade) VALUES
(2, 1, 1),
(3, 2, 1),
(4, 3, 1),
(1, 4, 10);

-- Inserir Inventario
INSERT INTO Inventario (personagem_id, item_id, quantidade, equipado) VALUES
(2, 1, 1, TRUE),
(3, 2, 1, TRUE),
(4, 3, 1, TRUE),
(1, 4, 10, FALSE);

-- Inserir Quests
INSERT INTO Quests (nome, descricao, recompensa_xp, recompensa_ouro, nivel_requerido, regiao_id) VALUES
('Limpar a Taverna', 'Expulsar bêbados e manter a ordem na Taberna do Pônei Saltitante', 50, 10, 1, 1),
('Entregar Mensagem', 'Levar uma carta importante de Bree ao Condado', 100, 20, 2, 1),
('Derrotar Orcs', 'Eliminar uma patrulha de Orcs nas estradas próximas', 200, 50, 5, 1);

-- Inserir Tarefas
INSERT INTO Tarefas (quest_id, nome, descricao, concluida) VALUES
(1, 'Conversar com Cevado', 'Falar com o proprietário sobre a situação', FALSE),
(1, 'Lutar contra bêbados', 'Derrotar os perturbadores', FALSE),
(2, 'Pegar a carta', 'Receber a carta de Cevado', FALSE),
(2, 'Viajar ao Condado', 'Entregar a carta em Bolsão', FALSE);
```

## Conclusão da Aula

Parabéns, alunos! Vocês deram o primeiro passo para organizar o caos da Taberna do Pônei Saltitante. Agora, pratiquem criando o banco de dados no PostgreSQL:

1. Conecte-se ao seu servidor PostgreSQL (usando psql ou uma ferramenta como pgAdmin).
2. Execute os comandos CREATE TABLE em ordem.
3. Insira os dados com os INSERTs.
4. Façam consultas SELECT para explorar os dados, como `SELECT * FROM PersonagemBase;`.
5. Experimentem JOINs, como `SELECT p.nome, c.nome AS classe FROM PersonagemBase p JOIN Classes c ON p.classe_id = c.id;`.

Lembrem-se: um bom modelo de banco de dados é a base de qualquer aplicação. Na próxima aula, exploraremos consultas avançadas e otimização!

Se tiverem dúvidas, perguntem!
```
