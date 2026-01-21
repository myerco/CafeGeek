---

title: DependÊNCIA DE EXISTÊNCIA
excerpt: "Entenda conceitos fundamentais de bancos de dados relacionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 9
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# DEPENDÊNCIA DE EXISTÊNCIA

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Dependência de existência

---

## DEPENDÊNCIA DE EXISTÊNCIA

Quando uma entidade **X** depende da existência da entidade **Y**, então X é dito **dependente da existência de Y**. Se Y for excluído, o mesmo deve acontecer com X.

- A entidade **Y** é chamada de **entidade dominante**.
- A entidade **X** é chamada de **entidade subordinada**.

---

## EXEMPLO

Vamos considerar uma entidade **aluno** e outra entidade **nota**:
- A entidade nota armazena todas as notas de todas as disciplinas de cada aluno
- Se um aluno for excluído da entidade aluno, então todas as ocorrências do aluno serão excluídas na entidade nota
- Se uma nota for excluída da entidade nota não afetará a entidade aluno

---

## DIAGRAMA DE EXEMPLO


ALUNO ─── TURMA ─── DISCIPLINA ─── PROFESSOR
1 1 N N
N 1

*SE O ALUNO É EXCLUÍDO OS DADOS DA TURMA TAMBÉM SERÃO*

---

## Próximo tópico

- Chave estrangeira

### O que foi visto

- Dependência de Existência
