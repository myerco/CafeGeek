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

## Objetivos

- Compreender o conceito de dependência de existência.
- Identificar entidades dominantes e subordinadas.
- Aplicar o conceito em exemplos práticos de modelagem.

---

## O que é Dependência de Existência?

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

## Exemplo Prático

Considere as entidades `ALUNO` e `NOTA`:

- `ALUNO` é dominante: um aluno pode existir sem notas (ex: aluno novo).
- `NOTA` é subordinada: uma nota só faz sentido se houver um aluno correspondente.

Se um aluno for excluído, todas as suas notas devem ser removidas automaticamente. Mas excluir uma nota não afeta o aluno.

**Modelo físico:**

- Tabela `aluno` (dominante).
- Tabela `nota` (subordinada, com FK para aluno).

```sql
CREATE TABLE aluno (
    matricula INT PRIMARY KEY,
    nome VARCHAR(50)
);

CREATE TABLE nota (
    id INT PRIMARY KEY,
    matricula_aluno INT,
    disciplina VARCHAR(50),
    valor DECIMAL(4,2),
    FOREIGN KEY (matricula_aluno) REFERENCES aluno(matricula) ON DELETE CASCADE
);
```

A cláusula `ON DELETE CASCADE` implementa a dependência: excluir aluno remove notas automaticamente.

## Diagrama de Exemplo

<div class="mermaid">
erDiagram
    ALUNO ||--o{ TURMA : possui
    TURMA ||--o{ DISCIPLINA : oferece
    DISCIPLINA ||--o{ PROFESSOR : ministrada_por
    ALUNO {
      int matricula PK
      string nome
    }
    TURMA {
      int numero_turma PK
      string nome
    }
    DISCIPLINA {
      int codigo PK
      string nome
    }
    PROFESSOR {
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
