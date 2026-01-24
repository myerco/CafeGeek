---
title: Modelo de Dados
excerpt: "Explore os tipos de modelos de dados, linguagens DDL e DML, e a definição de SQL em bancos de dados relacionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2026-01-22T08:48:05-04:00
order: 13
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Objetivos

- Compreender o conceito de modelo de dados.
- Identificar tipos de modelos (lógicos e físicos).
- Explorar linguagens DDL e DML.
- Entender a definição e uso de SQL.

## O que é um Modelo de Dados?

Um modelo de dados é um conjunto de ferramentas conceituais para descrever dados, relacionamentos, semântica e regras de consistência. Ele serve como ponte entre o mundo real e a implementação técnica do banco de dados.

**Classificações principais:**

1. **Modelos lógicos com base em objetos**: Focam em entidades e relacionamentos.
2. **Modelos lógicos com base em registros**: Usam tabelas e campos.
3. **Modelos físicos**: Descrevem armazenamento em disco, índices, etc.

---

## Modelos Lógicos com Base em Objetos

### Modelo de Entidade de Relacionamento (E-R)

O mais usado. Representa entidades, atributos e relacionamentos.

<div class="mermaid">
erDiagram
    ALUNO {
        int id_aluno PK
        string nome
        string matricula
        date data_nascimento
        string email
    }
    DISCIPLINA {
        int id_disciplina PK
        string codigo
        string nome
        int carga_horaria
        string ementa
    }

    TURMA {
        int id_turma PK
        string codigo_turma
        string horario
        string sala
        int ano_semestre
    }
    
    PROFESSOR {
        int id_professor PK
        string nome
        string departamento
    }
    
    ALUNO ||--o{ MATRICULA : "faz"
    DISCIPLINA ||--o{ TURMA : "oferece"
    TURMA }o--|| PROFESSOR : "ministrada_por"
    TURMA ||--o{ MATRICULA : "contém"
    
    MATRICULA {
        int id_matricula PK
        date data_matricula
        string situacao
        float nota_final
    }
    ALUNO }o--o{ DISCIPLINA : "pode_cursar_via"
</div>

### Modelo Orientado a Objetos

Integra conceitos de OOP (herança, encapsulamento).

<div class="mermaid">
classDiagram
    note "Diagrama de Classes OO com herança e composição"
    class Pessoa {
        <<abstract>>
        -id: int
        -nome: string
        -email: string
        +getInfo() string
    }
    class Aluno {
        -matricula: string
        -dataIngresso: date
        -historico: List~DisciplinaCursada~
        +matricularEmTurma(turma: Turma) boolean
        +calcularCR() float
    }
    class Professor {
        -departamento: string
        -titulacao: string
        -turmasMinistradas: List~Turma~
        +criarTurma(disciplina: Disciplina) Turma
        +lancarNota(aluno: Aluno, nota: float) void
    }
    class Disciplina {
        -codigo: string
        -nome: string
        -cargaHoraria: int
        -ementa: string
        -preRequisitos: List~Disciplina~
        +verificarPreRequisitos(aluno: Aluno) boolean
    }
    class Turma {
        -codigoTurma: string
        -horario: string
        -sala: string
        -anoSemestre: int
        -vagasDisponiveis: int
        -alunosMatriculados: List~Aluno~
        +matricularAluno(aluno: Aluno) boolean
        +verificarLotacao() boolean
    }
    class DisciplinaCursada {
        -disciplina: Disciplina
        -turma: Turma
        -nota: float
        -situacao: string
        +calcularAprovacao() boolean
    }
    class Matricula {
        -dataMatricula: date
        -situacao: string
        +cancelar() boolean
        +confirmar() boolean
    }
    Pessoa <|-- Aluno
    Pessoa <|-- Professor
    Aluno "1" *-- "*" DisciplinaCursada : histórico
    Aluno "1" --> "*" Matricula : possui
    Professor "1" --> "*" Turma : ministra
    Turma "1" --> "1" Disciplina : é de
    Turma "1" --> "*" Matricula : contém
    DisciplinaCursada "1" --> "1" Disciplina : referente a
    DisciplinaCursada "1" --> "1" Turma : cursada em
    Disciplina "1" --> "*" Disciplina : pré-requisitos
</div>

Esta disciplina foca no **Modelo E-R** devido à sua simplicidade e poder para bancos relacionais.

---

## Linguagens de Banco de Dados

Duas linguagens principais interagem com o modelo de dados:

1. **Linguagem de Definição de Dados (DDL)**: Define a estrutura do banco (tabelas, índices, restrições).
2. **Linguagem de Manipulação de Dados (DML)**: Manipula os dados (inserir, consultar, atualizar, excluir).

---

## DDL - Principais Comandos

- `CREATE`: Cria objetos (tabelas, índices).
- `DROP`: Remove objetos.
- `ALTER`: Modifica objetos existentes.

**Exemplo:**

```sql
CREATE TABLE aluno (
    id_aluno INT,
    nome VARCHAR(50)
);

ALTER TABLE aluno ADD data_nascimento DATE;

DROP TABLE aluno;
```

## DML - Principais Comandos

- `INSERT`: Adiciona registros.
- `UPDATE`: Modifica registros.
- `DELETE`: Remove registros.
- `SELECT`: Consulta dados.

**Exemplo:**

```sql
INSERT INTO aluno VALUES (1, 'Aragorn');

UPDATE aluno SET data_nascimento ='2025-01-24' WHERE id_aluno = 1;

DELETE FROM aluno WHERE id = 1;

SELECT * FROM aluno;
```

## O que é SQL?

SQL (Structured Query Language) é a linguagem padrão para bancos de dados relacionais. Declarativa, permite consultas e manipulações inspiradas na álgebra relacional.

**Ferramentas como SQL Developer** oferecem interface gráfica para executar comandos SQL, facilitando o aprendizado e depuração.

## Benefícios dos Modelos de Dados

- Estruturação clara dos dados.
- Facilita comunicação entre desenvolvedores e usuários.
- Suporte a integridade e consistência.
- Base para implementação eficiente em SGBDs.
