---
title: Integridade Referencial e Cardinalidade
excerpt: "Entenda integridade referencial, cardinalidade e relacionamentos em bancos de dados, com exemplos de O Senhor dos Anéis."
categories:
  - banco-de-Dados
  - modelo-de-dados
date: 2026-01-25T08:48:05-04:00
order: 19
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Objetivos

- Compreender integridade referencial e cardinalidade.
- Visualizar exemplos práticos com personagens de O Senhor dos Anéis.
- Explorar representações gráficas (Mermaid) e tabelas.

## O que é Integridade Referencial?

Integridade referencial garante que os relacionamentos entre tabelas sejam válidos, evitando registros órfãos e inconsistências.

O relacionamento efetiva-se através de uma expressão relacional que indica como deve ser feita a comparação entre os campos comuns às Entidades, só que agora com uma característica diferente.

A comparação é realizada entre campos das entidades e campos do relacionamento, formando uma expressão composta:

(sexo.id = pessoas.id_sexo)

(atendentes.id_pessoa = pessoas.id)

**Observação:** Utilize a estrutura de tabelas da aula [Restrições de Integridade](https://cafegeek.eti.br/curso/banco-de-dados/modelo-de-dados/restricoes-de-integridade/)
{: .notice}

## O que é Cardinalidade?

Cardinalidade define quantas ocorrências de uma entidade podem se relacionar com outra em um relacionamento.

**Cardinalide 1:1**

<div class="mermaid">
erDiagram
    A ||--|| B : possui
    A {
        int id_B  PK
    }
    B {
      int id_A PK
    }
</div>

**Cardinalide 1:N**

<div class="mermaid">
erDiagram
    A ||--o{ B : possui
    A {
        int id  PK
    }
    B {
      int id PK
      int id_A FK
    }
</div>

**Cardinalide N:N**

<div class="mermaid">
erDiagram
    A }o--o{ B : possui
    A {
        int id  PK
    }
    B {
      int id PK
    }
</div>

## Sintaxe dos relacionamentos

|Valor esquerda| Valor Direita|Siginificado|
|--------------|--------------|------------|

- `|o`  -  `o|` : Zero ou um
- `||`  -  `||` :Exatamente um
- `}o`  -  `o{` :Zero ou mais (sem limite)
- `}|`  -  `|{` :One ou mais (sem limite)

## Tipos de Cardinalidade

### 1:1 (Um para Um)

Cada elemento de uma entidade se relaciona com no máximo um elemento da outra.

**Exemplo - Pessoas e CPF:**

Uma pessoa tem no máximo um CPF, e um CPF pertence a no máximo uma pessoa.

<div class="mermaid">
erDiagram
    PESSOAS ||--|| CPF : possui
    PESSOAS {
        int numero_cpf  PK
        string nome
    }
    CPF {
      string numero_cpf PK
    }
</div>

**Expressão relacional:**

`(pessoas.numero_cpf = cpf.numero_cpf)`

**Exemplo - Pessoas e Foto:**

Uma pessoa tem no máximo uma foto, e um foto pertence a no máximo uma pessoa.

<div class="mermaid">
erDiagram
    PESSOAS ||--|| FOTO : possui
    PESSOAS {
        int id  PK
        string nome
    }
    FOTO {
      int id_pessoa PK
      blob imagem
     }
</div>

**Expressão relacional:**

`(pessoas.id = foto.id_pessoa)`

### 1:N (Um para Muitos)

Um elemento da entidade A se relaciona com múltiplos elementos da entidade B, mas cada elemento de B se relaciona com apenas um de A.

**Exemplo de 1:N (Sexo e pessoas)**

Um campo Sexo pode ter várias pessoas, e cada pessoa pertence a apenas um sexo.

<div class="mermaid">
erDiagram
    SEXO ||--o{ PESSOAS : possui
    SEXO {
      int id PK 
      string descricao
    }
    PESSOAS {
      int id PK
      int id_sexo FK
      string nome
    }
</div>

**Expressão relacional:**

`(sexo.id = pessoas.id_sexo)`

### N:N (Muitos para Muitos)

Instâncias de ambas as entidades podem se relacionar com múltiplas instâncias da outra.

**Exemplo de N:N (Aluno e Disciplina)** 

Um aluno pode se matricular em várias disciplinas, e uma disciplina pode ter vários alunos matriculados.

<div class="mermaid">
erDiagram
    ALUNO }o--o{ DISCIPLINA : matricula
    ALUNO {
      string nome
    }
    DISCIPLINA {
      string nome
    }
</div>

**Expressão relacional:**

`matricula.id_aluno = aluno.id`

`matricula.id_disciplina = disciplina.id`

**Exemplo  sistema acadêmico:**

<div class="mermaid">
erDiagram
    ALUNO ||--o{ MATRICULA : possui
    DISCIPLINA ||--o{ MATRICULA : recebe

    ALUNO {
        int id PK
        string nome
    }
    MATRICULA {
        int id PK
        int aluno_id FK
        int disciplina_id FK
        string semestre
        float nota
    }
    DISCIPLINA {
        int id PK
        string nome
        int professor_id FK
    }

</div>

**Expressão relacional:**

`matricula.aluno_id = aluno.id`

`matricula.disciplina_id = disciplina.id`

Perceba que a tabela MATRICULA é uma tabela associativa criada para representar o relacionamento N:N entre ALUNO e DISCIPLINA. Ela possui como chaves primárias compostas as chaves das tabelas envolvidas, permitindo registrar cada matrícula de aluno em disciplina de forma única e garantindo a integridade referencial entre as entidades.
{: .notice}

**Comandos SQL:**

```sql
CREATE TABLE professor (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100) NOT NULL
);

CREATE TABLE disciplina (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100) NOT NULL,
  professor_id INT REFERENCES professor(id)
);

CREATE TABLE aluno (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100) NOT NULL
);

CREATE TABLE matricula (
  id SERIAL PRIMARY KEY,
  aluno_id INT REFERENCES aluno(id),
  disciplina_id INT REFERENCES disciplina(id),
  semestre VARCHAR(20),
  nota NUMERIC(4,2),
  UNIQUE (aluno_id, disciplina_id, semestre)
);
```

**Exemplo clássico de N:N (Produto e Nota Fiscal)**

Um produto pode aparecer em várias notas fiscais, e uma nota fiscal pode conter vários produtos.

<div class="mermaid">
erDiagram
    PRODUTO }o--o{ NOTA_FISCAL : compoe
    PRODUTO {
      string nome
    }
    NOTA_FISCAL {
      string numero
    }
</div>

**Expressão relacional:**

produto_nota.id_produto = produto.id
produto_nota.id_nota = nota_fiscal.id

Esses exemplos mostram como cardinalidade e integridade referencial são aplicadas na modelagem de dados.

## Consultas de Relacionamento

```sql

select p.nome, s.descricao
from pessoas p
join sexo s on p.id_sexo = s.id;

select p.nome, f.imagem
from pessoas p
join foto f on p.id = f.id_pessoa;

select a.nome, d.nome, m.semestre, m.nota
from aluno a
join matricula m on a.id = m.aluno_id
join disciplina d on m.disciplina_id = d.id;

```