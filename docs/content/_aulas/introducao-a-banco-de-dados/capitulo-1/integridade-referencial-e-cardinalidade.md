---
title: Integridade Referencial e Cardinalidade
excerpt: "Entenda integridade referencial, cardinalidade e relacionamentos em bancos de dados, com exemplos de O Senhor dos Anéis."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
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

(aluno.matricula = turma.matriculaAluno)
(aluno.sexo = sexo.descricao)

## O que é Cardinalidade?

Cardinalidade define quantas ocorrências de uma entidade podem se relacionar com outra em um relacionamento.

## Tipos de Cardinalidade e Exemplos

### 1:1 (Um para Um)

Cada elemento de uma entidade se relaciona com no máximo um elemento da outra.

#### Exemplo de 1:1 (Pessoa e CPF)

Uma pessoa tem no máximo um CPF, e um CPF pertence a no máximo uma pessoa.

<div class="mermaid">
erDiagram
    PESSOA ||--|| CPF : possui
    PESSOA {
      string nome
    }
    CPF {
      string numero
    }
</div>

**Expressão relacional:**

pessoa.id_cpf = cpf.id

### 1:N (Um para Muitos)

Um elemento da entidade A se relaciona com múltiplos elementos da entidade B, mas cada elemento de B se relaciona com apenas um de A.

#### Exemplo de 1:N (Cliente e Empréstimos)

Um cliente pode ter vários empréstimos, e cada empréstimo pertence a apenas um cliente.

<div class="mermaid">
erDiagram
    CLIENTE ||--o{ EMPRESTIMO : possui
    CLIENTE {
      string nome
    }
    EMPRESTIMO {
      int valor
    }
</div>

**Expressão relacional:**

emprestimo.id_cliente = cliente.id

### N:N (Muitos para Muitos)

Instâncias de ambas as entidades podem se relacionar com múltiplas instâncias da outra.

#### Exemplo de N:N (Aluno e Disciplina)

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

matricula.id_aluno = aluno.id
matricula.id_disciplina = disciplina.id

#### Exemplo prático de sistema acadêmico

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

matricula.aluno_id = aluno.id
matricula.disciplina_id = disciplina.id

Perceba que a tabela MATRICULA é uma tabela associativa criada para representar o relacionamento N:N entre ALUNO e DISCIPLINA. Ela possui como chaves primárias compostas as chaves das tabelas envolvidas, permitindo registrar cada matrícula de aluno em disciplina de forma única e garantindo a integridade referencial entre as entidades.
{: .notice}

## Exemplo prático de sistema acadêmico: Comandos SQL (PostgreSQL)

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

## Exemplo clássico de N:N (Produto e Nota Fiscal)

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
