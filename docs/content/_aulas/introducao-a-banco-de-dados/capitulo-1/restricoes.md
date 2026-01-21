---

title: RestriÇÕES
excerpt: "Entenda conceitos fundamentais de bancos de dados relacionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 18
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

# RESTRIÇÕES

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Restrições
- Cardinalidade

---

## RESTRIÇÕES

"O esquema E-R de uma empresa pode definir certas restrições, as quais o conteúdo do banco de dados deve respeitar."

### Tipos de restrições:

1. Cardinalidade
2. Dependência de Existência

---

## CARDINALIDADE

No relacionamento entre duas entidades o número de ocorrências de uma entidade que esta associado a outra entidade determina a **cardinalidade**.

### Graus de Cardinalidade:

- Um para Um (1:1)
- Um para Muitos (1:N)
- Muitos para Um (N:1)
- Muitos para Muitos (N:N)

---

## UM PARA UM (1:1)

Significa que cada elemento de uma entidade relaciona-se com somente um elemento de outra entidade.

HOMEM ─── MULHER
1 1

*UM HOMEM SOMENTE PODE TER UMA MULHER
UMA MULHER SOMENTE PODE TER UM HOMEM*

### TABELAS:

**HOMEM**
**MULHER**

---

## UM PARA MUITOS (1:N)

Um elemento da entidade 1 relaciona-se com muitos elementos da entidade 2, mas cada elemento da entidade 2 somente pode estar relacionado a um elemento da entidade 1.

CLIENTE ─── EMPRÉSTIMO
1 N

*UM HOMEM TEM VÁRIOS EMPRESTIMOS
UM EMPRÉSTIMO SOMENTE TEM UM CLIENTE*

### TABELAS:

**CLIENTE**
**EMPRÉSTIMO**

---

## MUITOS PARA MUITOS (N:N)

Um elemento da entidade 1 relaciona-se com muitos elementos da entidade 2 e cada elemento da entidade 2 está relacionado a um elemento da entidade 1.

PRODUTOS ─── NOTA FISCAL
N N

*UM PRODUTO APARECE EM MAIS DE UMA NOTA FISCAL
UMA NOTA FISCAL TEM MAIS DE UM PRODUTO*

---

## MUITOS PARA MUITOS (IMPLEMENTAÇÃO)

Para este tipo de relacionamento é necessário construir uma tabela no meio.

Esta nova tabela deverá conter os dois atributos Chaves de ambas as tabelas.

PRODUTOS ─── NOTA FISCAL
N N
PRODUTO-NOTA

### TABELAS:

**PRODUTO**
**NOTA FISCAL**
**PRODUTO-NOTA** (tabela associativa)

---

## Próximo tópico

- Dependência de Existência

### O que foi visto

- Restrições
- Cardinalidade
