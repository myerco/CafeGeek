---
title: MODELO DE ENTIDADE E RELACIONAMENTO
excerpt: "**BANCO DE DADOS I** Marco Yerco Mendizabel Cabrera Analista de Sistemas"
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 14
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---
# MODELO DE ENTIDADE E RELACIONAMENTO

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Modelo de Entidade de Relacionamento
- Entidades
- Atributos

---

## M.E.R

"O Modelo Entidade-Relacionamento (E-R) tem por base a percepção de que o mundo real é formado por um conjunto de objetos chamados entidades e pelo conjunto dos relacionamentos entre esse objetos."

"Ao se utilizar a Modelagem Conceitual de Dados com a técnica de Entidades e Relacionamentos, obteremos resultados e esquemas puramente conceituais sobre a essência de um sistema. Ou melhor, sobre o negócio para qual estamos desenvolvendo um projeto, não representando procedimentos ou fluxo de dados existentes"

---

## OBJETOS CONCEITUAIS

1. Entidades
2. Atributos
3. Especialização e Generalização
4. Relacionamentos

---

## ENTIDADE

Define-se entidade como aquele objeto que existe no mundo real com uma identificação distinta e com um significado próprio. São coisas que existem no negócio, ou ainda, descrevem o negócio.

**Exemplo**:
- Pessoas na empresa
- Empréstimos
- Alunos
- Disciplinas

---

## ENTIDADE (CONTINUAÇÃO)

Uma entidade tem um conjunto de propriedades e os valores para alguns conjuntos dessas propriedades devem ser únicos.

**Exemplo**:
- **Pessoa** (CPF, Nome, Sexo, Data Nascimento, Salário)
  *CPF – Identifica uma única pessoa*

- **Aluno** (MATRICULA, nome, turma, curso)
  *MATRICULA - Identifica uma pessoa dentro do negócio*

- **Empréstimo** (Número do empréstimo, data, valor, cliente)
  *Número do empréstimo - identifica o registro*

---

## ENTIDADE - REPRESENTAÇÃO

A representação de uma Entidade no Modelo Relacional se realiza através de um retângulo, com o nome desta entidade em seu interior.

┌─────────────┐ ┌──────────┐ ┌─────────────┐ ┌──────────────┐
│ PESSOA │ │ ALUNO │ │ DISCIPLINA │ │ EMPRÉSTIMO │
└─────────────┘ └──────────┘ └─────────────┘ └──────────────┘

---

## ENTIDADE - TABELA

Devemos entender uma entidade como uma tabela de dados, onde cada linha desta tabela representa uma instância da mesma.

### ALUNO


┌────────────┬───────────────┬───────┬──────────┐
│ Matrícula │ Nome │ Turma │ Curso │
├────────────┼───────────────┼───────┼──────────┤
│ 001.201501 │ Ana Claudia │ A │ Sistemas │
│ 002.201501 │ João Silva │ B │ Direito │
└────────────┴───────────────┴───────┴──────────┘

---

## ATRIBUTOS

"Todo objeto para ser uma entidade possui propriedades que são descritas por atributos e valores."

"Toda entidade é representada por um conjunto de atributos. Atributos são propriedades descritivas de cada membro de um conjunto de entidades."

---

## ATRIBUTOS - EXEMPLO

Cada instância de **PESSOA**, cada existência de um objeto da classe pessoa, será formada por valores nestes atributos, sendo que é o conjunto destes valores representados que devemos visualizar como uma linha de uma tabela de dados.

### PESSOA


┌──────┬───────────────┬──────┬──────────┬─────────────┐
│ CPF │ Nome │ Sexo │ Salário │ Data Nasc. │
├──────┼───────────────┼──────┼──────────┼─────────────┤
│ 001 │ João │ M │ 1000.00 │ 21/06/1989 │
└──────┴───────────────┴──────┴──────────┴─────────────┘

---

## CARACTERÍSTICAS DOS ATRIBUTOS

1. **Atributos simples ou compostos**:
   - Simples - expressam um valor indivisível. Exemplo: Sexo, telefone, etc.
   - Compostos - expressam mais de um valor, pode ser dividido. Exemplo: Nome, Endereço. etc.

2. **Atributos monovalorados ou multivalorados**:
   - Monovalorado - exemplo: Idade para a entidade pessoa.
   - Multivalorado - exemplo: Salário (pode conter R$ 800,00 ou R$ 20.000,00).

3. **Atributos nulos**: Podem ser nulos. Exemplo: Estado civil, Fax.

4. **Atributo derivado**: O valor deriva de outro atributo. Exemplo: Valor da nota fiscal.

---

## Próximo tópico

- SQL entidades

### O que foi visto

- Modelo de Entidade de Relacionamento
- Entidades
- Atributos

Todos os arquivos Markdown foram criados seguindo a estrutura das apresentações originais, com títulos formatados como cabeçalhos, conteúdo estruturado em seções, e exemplos de código SQL devidamente formatados.
