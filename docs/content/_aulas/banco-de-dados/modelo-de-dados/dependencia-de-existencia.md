---
title: Dependência de Existência
excerpt: "Explore o conceito de dependência de existência em bancos de dados relacionais e sua aplicação em modelagem de dados."
categories:
  - banco-de-Dados
  - modelo-de-dados
date: 2024-03-01T08:48:05-04:00
order: 9
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

Dependência de existência ocorre quando a existência de uma entidade (subordinada) depende da existência de outra entidade (dominante). Se a entidade dominante for excluída, a subordinada também deve ser removida para manter a integridade dos dados.

**Por que é importante?**

- Garante que não haja registros "órfãos" no banco de dados.
- Mantém a consistência lógica dos dados.
- É fundamental em relacionamentos onde uma entidade não faz sentido sem a outra.

---

## Entidades Dominante e Subordinada

- **Entidade Dominante**: aquela cuja existência é independente.
- **Entidade Subordinada**: depende da dominante para existir.

---

**Exemplos:**

Considere as entidades `ALUNOS` e `NOTAS`:

- `ALUNOS` é dominante: um aluno pode existir sem notas (ex: aluno novo).
- `NOTAS` é subordinada: uma nota só faz sentido se houver um aluno correspondente.

Se um aluno for excluído, todas as suas notas devem ser removidas automaticamente. Mas excluir uma nota não afeta o aluno.

**Modelo físico:**

- Tabela `alunos` (dominante).
- Tabela `notas` (subordinada, com FK para aluno).

```sql
CREATE TABLE alunos (
    matricula INT PRIMARY KEY,
    nome VARCHAR(50)
);

CREATE TABLE notas (
    id INT PRIMARY KEY,
    matricula_aluno INT,
    disciplina VARCHAR(50),
    valor DECIMAL(4,2),
    FOREIGN KEY (matricula_aluno) REFERENCES alunos(matricula) ON DELETE CASCADE
);

-- Inserindo dados na tabela aluno
INSERT INTO alunos (matricula, nome) VALUES
(1, 'Ana Silva'),
(2, 'Bruno Souza'),
(3, 'Carla Oliveira'),
(4, 'Daniel Santos'),
(5, 'Elena Ferreira');

-- Inserindo dados na tabela nota
INSERT INTO notas (id, matricula_aluno, disciplina, valor) VALUES
(101, 1, 'Matemática', 8.5),
(102, 1, 'Português', 7.0),
(103, 2, 'Matemática', 9.0),
(104, 3, 'Português', 6.5),
(105, 3, 'História', 7.5),
(106, 5, 'Matemática', 10.0);
-- Note: O aluno 4 (Daniel) não tem notas
-- Note: O aluno 5 (Elena) tem apenas uma nota
```

A cláusula `ON DELETE CASCADE` implementa a dependência: excluir aluno remove notas automaticamente.

## Associação entre tabelas

### INNER JOIN

Retorna apenas os registros que têm correspondência em ambas as tabelas.

```sql
-- INNER JOIN: Alunos que possuem pelo menos uma nota
SELECT a.matricula, a.nome, n.disciplina, n.valor
FROM alunos a
INNER JOIN notas n ON a.matricula = n.matricula_aluno
ORDER BY a.matricula;
```

<div class="mermaid">
graph TD
    A[Aluno<br/>Ana, Bruno, Carla, Daniel, Elena] 
    B[Nota<br/>Matemática, Português, Matemática, Português, História, Matemática]
    C[INNER JOIN<br/> Alunos com notas]
    
    A ---|matrícula correspondente| C
    B ---|matrícula correspondente| C
    
    style C fill:#6959CD
</div>

### LEFT JOIN

Retorna todos os registros da tabela da esquerda (aluno), mesmo que não haja correspondência na tabela da direita (nota).

```sql
-- LEFT JOIN: Todos os alunos, com ou sem notas
SELECT a.matricula, a.nome, n.disciplina, n.valor
FROM alunos a
LEFT JOIN notas n ON a.matricula = n.matricula_aluno
ORDER BY a.matricula;
```

<div class="mermaid">
graph TD
    A[Todos Alunos<br/>Ana, Bruno, Carla, Daniel, Elena]
    B[Notas]
    C[LEFT JOIN<br/> Todos alunos + notas se houver]
    
    A ---|todos registros| C
    B ---|apenas correspondentes| C
    
    style A fill:#6959CD
    style C fill:#6959CD
</div>

### RIGHT JOIN

Retorna todos os registros da tabela da direita (nota), mesmo que não haja correspondência na tabela da esquerda (aluno).

```sql
-- RIGHT JOIN: Todas as notas com informações do aluno
SELECT a.matricula, a.nome, n.disciplina, n.valor
FROM alunos a
RIGHT JOIN notas n ON a.matricula = n.matricula_aluno;
```

<div class="mermaid">
graph TD
    A[Alunos]
    B[ Todas Notas<br/> Matemática, Português, Matemática, Português, História, Matemática]
    C[RIGHT JOIN<br/>Todas notas + aluno se houver]
    
    A ---|apenas correspondentes| C
    B ---|todos registros| C
    
    style B fill:#6959CD
    style C fill:#6959CD
</div>

## Operações de Conjuntos

Para operações de conjuntos, precisamos de queries que retornem estruturas compatíveis. Vamos criar duas visões:

Alunos com nota em Matemática vs Alunos com nota em Português

```sql
-- Query 1: Alunos com nota em Matemática
SELECT a.matricula, a.nome, 'Matemática' as tipo
FROM alunos a
INNER JOIN notas n ON a.matricula = n.matricula_aluno
WHERE n.disciplina = 'Matemática';

-- Query 2: Alunos com nota em Português
SELECT a.matricula, a.nome, 'Português' as tipo
FROM alunos a
INNER JOIN notas n ON a.matricula = n.matricula_aluno
WHERE n.disciplina = 'Português';
```

### UNION - União de conjuntos

Retorna todos os registros de ambas as queries, removendo duplicatas.

```sql
-- UNION: Alunos que têm nota em Matemática OU em Português
SELECT a.matricula, a.nome, 'Matemática' as disciplina
FROM alunos a
INNER JOIN notas n ON a.matricula = n.matricula_aluno
WHERE n.disciplina = 'Matemática'

UNION

SELECT a.matricula, a.nome, 'Português' as disciplina
FROM alunos a
INNER JOIN notas n ON a.matricula = n.matricula_aluno
WHERE n.disciplina = 'Português'
ORDER BY matricula;
```

<div class="mermaid">
graph TD
    A[Matemática<br/>Ana, Bruno, Elena]
    B[Português<br/>Ana, Carla]
    C[UNION<br/> Ana, Bruno, Carla, Elena]
    
    A ---|união| C
    B ---|união| C
    
    style C fill:#6959CD
</div>

### INTERSECT - Interseção de conjuntos

Retorna apenas os registros que estão presentes em ambas as queries.

```sql
-- INTERSECT: Alunos que têm nota em Matemática E em Português
SELECT matricula, nome
FROM alunos
WHERE matricula IN (
    SELECT matricula_aluno 
    FROM notas 
    WHERE disciplina = 'Matemática'
)

INTERSECT

SELECT matricula, nome
FROM alunos
WHERE matricula IN (
    SELECT matricula_aluno 
    FROM notas
    WHERE disciplina = 'Português'
);
```

<div class="mermaid">
graph TD
    A[Matemática<br/>Ana, Bruno, Elena]
    B[Português<br/>Ana, Carla]
    C[INTERSECT<br/> Ana]
    
    A ---|interseção| C
    B ---|interseção| C
    
    style C fill:#6959CD
</div>

### EXCEPT Diferença de conjuntos

```sql
-- EXCEPT: Alunos que têm nota em Matemática mas NÃO em Português
SELECT matricula, nome
FROM alunos
WHERE matricula IN (
    SELECT matricula_aluno 
    FROM notas 
    WHERE disciplina = 'Matemática'
)

EXCEPT

SELECT matricula, nome
FROM alunos
WHERE matricula IN (
    SELECT matricula_aluno 
    FROM notas 
    WHERE disciplina = 'Português'
);
```

<div class="mermaid">
graph TD
    A[Matemática<br/>Ana, Bruno, Elena]
    B[Português<br/>Ana, Carla]
    C[EXCEPT<br/> Bruno, Elena]
    
    A ---|diferença| C
    B -.->|exclui interseção| C
    
    style C fill:#6959CD
</div>

**Tabelas completas:**

<div class="mermaid">
erDiagram
    ALUNOS ||--o{ TURMAS : possui
    TURMAS ||--o{ DISCIPLINAS : oferece
    DISCIPLINAS ||--o{ PROFESSORES : ministrada_por
    ALUNOS {
      int matricula PK
      string nome
    }
    TURMAS {
      int numero_turma PK
      string nome
    }
    DISCIPLINAS {
      int codigo PK
      string nome
    }
    PROFESSORES {
      int id PK
      string nome
    }
</div>

Se o ALUNO é excluído, os dados da TURMA também serão removidos para manter consistência.
{: .notice--info}

## Benefícios

- Evita inconsistências (ex: notas sem aluno).
- Facilita manutenção e integridade referencial.
- Suportado por SGBDs via chaves estrangeiras e triggers.
