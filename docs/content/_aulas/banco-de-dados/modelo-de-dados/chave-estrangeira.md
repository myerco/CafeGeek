---

title: Chave Estrangeira
excerpt: "Aprenda o que é uma chave estrangeira, sua importância para integridade referencial e como aplicá-la em bancos de dados relacionais."
categories:
  - banco-de-Dados
  - modelo-de-dados
date: 2024-03-01T08:48:05-04:00
order: 8
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## O que é uma Chave Estrangeira?

Uma chave estrangeira (foreign key) é um campo ou conjunto de campos em uma tabela que faz referência à chave primária de outra tabela (ou da mesma tabela, em auto-relacionamentos). Ela garante a integridade dos dados, impedindo que registros "órfãos" sejam criados.

**Por que é importante?**

- Mantém a consistência entre tabelas relacionadas.
- Evita dados desconectados (por exemplo, um aluno em uma turma inexistente).
- Permite a navegação e junção eficiente de dados.

## Termos Importantes

- **Chave Referenciada**: a chave primária que está sendo apontada.
- **Tabela dependente (filha)**: contém a chave estrangeira.
- **Tabela referenciada (pai)**: é referenciada pela chave estrangeira.

## Exemplo Prático

Considere duas tabelas: `PESSOAS` e `SEXO`.

| PESSOAS      | SEXO      |
| ------------ | --------- |
| id (PK)      | id (PK)   |
| nome         | descricao |
| id_sexo (FK) | ...       |

No exemplo acima, o campo `id_sexo` em `PESSOAS` é uma chave estrangeira que referencia `id` em `SEXO`.

**Expressão:**

`(sexo.id = pessoas.id_sexo)`

## Diagrama de Relacionamento

<div class="mermaid">
erDiagram
    SEXO ||--o{ PESSOAS : possui
    SEXO {
      int id PK
      string descricao
    }
    PESSOAS {
      int id PK
      string nome
      int id_sexo FK
    }
</div>

Legenda: PK = chave primária, FK = chave estrangeira

## Benefícios da Chave Estrangeira

- Garante integridade referencial automaticamente.
- Facilita consultas entre tabelas relacionadas (JOINs).
- Permite modelar relacionamentos 1:N e N:N.
