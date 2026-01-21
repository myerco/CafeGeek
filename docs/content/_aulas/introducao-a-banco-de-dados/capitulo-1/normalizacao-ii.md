---
title: NORMALIZAÇÃO II
excerpt: "**BANCO DE DADOS I** Marco Yerco Mendizabel Cabrera Analista de Sistemas"
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 16
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---
# NORMALIZAÇÃO II

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- 2FN
- 3FN
- Boyce / CODD
- 4FN
- 5FN

---

## SEGUNDA FORMA NORMAL (2FN)

A segunda forma normal assegura que **não exista dependência funcional parcial** no modelo de dados. Para aplicarmos a segunda forma normal em um modelo de dados devemos observar se alguma entidade do modelo possui chave primária concatenada e verificar se existe algum atributo ou conjunto de atributos com dependência parcial em relação a algum atributo da chave primária concatenada.

**Exemplo**: A entidade ITEM-DO-PEDIDO apresenta uma chave primária concatenada e por observação, notamos que os atributos **UNIDADE, DESCRIÇÃO e VALOR-UNITÁRIO** dependem de forma parcial do atributo **COD. PROD**, que faz parte da chave primária.

---

## DIAGRAMA 2FN


PEDIDO ─── ITEM-PEDIDO ─── PRODUTO
1 N 1

PEDIDO:
PK - Nº do pedido

    Entrega

    Cliente

    Endereço

    Cidade

    UF

ITEM-PEDIDO:
PK - Nº Pedido + PK - Cod Prod

    Qtd.

    Valor Total

PRODUTO:
PK - Cod. Prod.

    Descricao

    Valor Unitário

    Unidade

---

## TERCEIRA FORMA NORMAL (3FN)

A terceira forma normal assegura que **nenhuma entidade do modelo de dados possui atributos com dependência transitiva**. Assim, uma entidade está na 3FN se nenhum de seus atributos possui dependência transitiva em relação a outro atributo da entidade que não participe da chave primária, ou seja, não existe nenhum atributo intermediário entre a chave primária e o próprio atributo observado.

Ao retirarmos a dependência funcional transitiva, devemos criar uma nova entidade que contenha os atributos que dependem transitivamente de outro e a sua chave primária é o atributo que causou esta dependência.

Também não devem conter atributos derivados, como por exemplo VALOR TOTAL.

---

## DIAGRAMA 3FN


PEDIDO ─── ITEM-PEDIDO ─── PRODUTO
1 N 1
│
└── CLIENTE
1

PEDIDO:
PK - Nº do pedido

    Entrega

ITEM-PEDIDO:
PK - Nº Pedido + PK - Cod Prod

    Qtd.

    Valor Total

PRODUTO:
PK - Cod. Prod.

    Descrição

    Valor Unitário

    Unidade

CLIENTE:
PK - Cliente

    Endereço

    Cidade

    UF

---

## FORMA NORMAL DE BOYCE / CODD

A forma normal Boyce/Codd foi desenvolvida com o objetivo de resolver algumas situações que não eram inicialmente cobertas pelas três formas normais, em especial quando haviam várias chaves na entidade, formadas por mais de um atributo (chaves compostas) e que ainda compartilham ao menos um atributo.

Isso nos leva a concluir que, o problema se devia ao fato de até agora as formas normais tratarem de atributos dependentes de **chaves primárias**. Assim, para estar na FNBC, uma entidade precisa possuir somente atributos que são chaves candidatas.

---

## EXEMPLO FNBC

Um mesmo professor pode ministrar aulas entre cursos e turmas diferentes. Sendo assim podemos identificar três chaves candidatas que são determinantes nessa entidade:

1. **COD_CURSO + TURMA**
2. **COD_CURSO + MATRICULA_PROFESSOR**
3. **TURMA + MATRICULA_PROFESSOR**

O atributo **MATRICULA_PROFESSOR** é parcialmente dependente do **COD_CURSO** e de **TURMA**, mas é totalmente dependente da chave candidata composta **COD_CURSO + TURMA**. Dessa forma a entidade deve ser desmembrada, resultando em duas: uma que contém os atributos que descrevem o aluno em si e outra cujos atributos designam um professor.

---

## DIAGRAMA FNBC


---

## QUARTA FORMA NORMAL (4FN)

Uma tabela está na 4FN, se e somente se, estiver na 3FN e não existirem dependências multivaloradas.

### PEDIDO (antes da 4FN)


---

## QUARTA FORMA NORMAL (4FN) - CONTINUAÇÃO


### PEDIDO (após normalização para 4FN)


---

## QUINTA FORMA NORMAL (5FN)

A 5FN trata de casos particulares que ocorrem com pouca frequência na modelagem de dados e que são os relacionamentos múltiplos (ternários, quaternários, n-nários...).

Ela fala que uma entidade está na sua 5FN quando o conteúdo desta entidade não puder ser reconstruído a partir de outras entidades menores, extraídas desta entidade. Ou seja, ao se fazer a decomposição de uma entidade em outras entidades perde-se o conteúdo (a informação da entidade original) pois as entidades geradas pela decomposição não conseguem representar a informação original.

---

## Próximo tópico

- Encerramento

### O que foi visto

- 2FN
- 3FN
- Boyce / CODD
- 4FN
- 5FN
