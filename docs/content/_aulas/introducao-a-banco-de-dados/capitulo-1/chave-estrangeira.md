---

title: Chave Estrangeira
excerpt: "Aprenda o que é uma chave estrangeira, sua importância para integridade referencial e como aplicá-la em bancos de dados relacionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 8
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Objetivos

- Compreender o conceito de chave estrangeira.
- Entender sua função na integridade referencial.
- Aplicar chaves estrangeiras em exemplos práticos.

---

## O que é uma Chave Estrangeira?

Uma chave estrangeira (foreign key) é um campo ou conjunto de campos em uma tabela que faz referência à chave primária de outra tabela (ou da mesma tabela, em auto-relacionamentos). Ela garante a integridade dos dados, impedindo que registros "órfãos" sejam criados.

**Por que é importante?**

- Mantém a consistência entre tabelas relacionadas.
- Evita dados desconectados (por exemplo, um aluno em uma turma inexistente).
- Permite a navegação e junção eficiente de dados.

---

## Termos Importantes

- **Chave Referenciada**: a chave primária que está sendo apontada.
- **Tabela dependente (filha)**: contém a chave estrangeira.
- **Tabela referenciada (pai)**: é referenciada pela chave estrangeira.

---

## Exemplo Prático

Considere duas tabelas: `ALUNO` e `TURMA`.

| ALUNO          | TURMA             |
| -------------- | ----------------- |
| matricula (PK) | numero_turma (PK) |
| nome           | nome              |
| turma (FK)     | ...               |

No exemplo acima, o campo `turma` em `ALUNO` é uma chave estrangeira que referencia `numero_turma` em `TURMA`.

```sql
CREATE TABLE turma (
  numero_turma INT PRIMARY KEY,
  nome VARCHAR(50)
);

CREATE TABLE aluno (
  matricula INT PRIMARY KEY,
  nome VARCHAR(50),
  turma INT,
  FOREIGN KEY (turma) REFERENCES turma(numero_turma)
);
```

### Exemplo de Dados nas Tabelas

#### TURMA

| numero_turma | nome         |
|--------------|--------------|
| 1            | Matemática   |
| 2            | História     |
| 3            | Biologia     |

#### ALUNO

| matricula | nome           | turma |
|-----------|----------------|-------|
| 101       | Ana Souza      | 1     |
| 102       | Bruno Lima     | 2     |
| 103       | Carla Mendes   | 1     |
| 104       | Diego Pereira  | 3     |
| 105       | Elisa Martins  | 2     |

## Diagrama de Relacionamento

```text
┌─────────────┐    ┌──────────┐    
│  ALUNO      │─── │  TURMA   │ 
└─────────────┘    └──────────┘ 
    PK/FK             PK        
```

Legenda: PK = chave primária, FK = chave estrangeira

## Benefícios da Chave Estrangeira

- Garante integridade referencial automaticamente.
- Facilita consultas entre tabelas relacionadas (JOINs).
- Permite modelar relacionamentos 1:N e N:N.
