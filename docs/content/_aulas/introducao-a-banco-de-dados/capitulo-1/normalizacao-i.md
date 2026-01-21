---
title: NORMALIZAÇÃO I
excerpt: "**BANCO DE DADOS I** Marco Yerco Mendizabel Cabrera Analista de Sistemas"
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 15
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---
# NORMALIZAÇÃO I

**BANCO DE DADOS I**
Marco Yerco Mendizabel Cabrera
Analista de Sistemas

## Objetivos

- Normalização
- Anomalias
- 1FN
- Dependência funcional total ou parcial
- Dependência funcional transitiva

---

## NORMALIZAÇÃO

"O conceito de normalização foi introduzido por E. F. Codd em 1970 (primeira forma normal). Esta técnica é um processo matemático formal, que tem seus fundamentos na teoria dos conjuntos. Através deste processo pode-se, gradativamente, substituir um conjunto de entidades e relacionamentos por um outro, o qual se apresenta 'purificado' em relação às anomalias de atualização (inclusão, alteração e exclusão) as quais podem causar certos problemas, tais como: grupos repetitivos (atributos multivalorados) de dados, dependências parciais em relação a uma chave concatenada, redundância de dados desnecessárias, perdas acidentais de informação, dificuldade na representação de fatos da realidade observada e dependências transitivas entre atributos."

---

## ANOMALIAS

Considere o formulário de Pedido apresentado a seguir. Podemos entender que uma entidade formada com os dados presentes neste documento, terá a seguinte apresentação:

### PEDIDO (formulário)


---

## ENTIDADE PEDIDOS

Caso esta entidade fosse implementada como uma tabela em um banco de dados, as seguintes anomalias iriam aparecer:

1. **Anomalia de inclusão**: ao ser incluído um novo cliente, o mesmo tem que estar relacionado a uma venda.
2. **Anomalia de exclusão**: ao ser excluído um cliente, os dados referentes as suas compras serão perdidos.
3. **Anomalia de alteração**: caso algum fabricante de produto altere a faixa de preço de uma determinada classe de produtos, será preciso percorrer toda a entidade para realizar múltiplas alterações.

---

## FORMAS NORMAIS

1. Primeira Forma Normal (1FN)
2. Dependência Funcional
   - Total e parcial
   - Transitiva
3. Segunda Forma Normal (2FN)
4. Terceira Forma Normal (3FN)
5. Forma Normal de BOYCE/CODD (FNBC)
6. Quarta forma normal (4FN)

---

## PRIMEIRA FORMA NORMAL (1FN)

A 1FN diz que: cada ocorrência da chave primária deve corresponder a uma e somente uma informação de cada atributo, ou seja, a entidade não deve conter grupos repetitivos.

Para se obter entidades na 1FN, é necessário decompor cada entidade não normalizada em tantas entidades quanto for o número de conjuntos de atributos repetitivos.

Nas novas entidades criadas, a chave primária é a concatenação da chave primária da entidade original mais o(s) atributo(s) do grupo repetitivo visualizado(s) como chave primária deste grupo.

---

## 1FN - ENTIDADE PEDIDO

Considere a entidade pedido:
- Chave primária é Nº do pedido
- Identificamos o grupo de atributos que se repetem
- Criamos uma nova entidade ITEM-DE_PEDIDO que herdará os atributos repetitivos e destacados da entidade PEDIDO

### DIAGRAMA:


PEDIDO ─── ITEM-PEDIDO
1 N

PEDIDO:
PK - Nº do pedido

    Entrega

    Cliente

    Endereço

    Cidade

    UF

ITEM-PEDIDO:
PK - Nº Pedido + PK - Cod Prod

    Unid.

    Qtd.

    Descrição

    Valor Unit. Prod

---

## DEPENDÊNCIA FUNCIONAL

Dada uma entidade qualquer, dizemos que um atributo ou conjunto de atributos **A** é dependente funcional de um outro atributo **B** contido na mesma entidade se, a cada valor B existir nas linhas da entidade em que aparece, um único valor de A. Em outras palavras, **A depende funcionalmente de B**.

**Exemplo**:
Na entidade PEDIDO, o atributo **ENTREGA** depende funcionalmente de **NUMERO-DO-PEDIDO**.

O exame das relações existentes entre os atributos de uma entidade deve ser feito a partir do conhecimento (conceitual) que se tem sobre a realidade a ser modelada.

---

## DEPENDÊNCIA FUNCIONAL TOTAL OU PARCIAL

Na ocorrência de uma chave primária concatenada, dizemos que um atributo ou conjunto de atributos depende de forma **completa ou total** desta chave primária concatenada, se e somente se, a cada valor da chave (e não parte dela) está associado a um valor para cada atributo.

Quando um atributo só depende de **parte da chave primária concatenada** e não dela como um todo é dito "dependente parcial".

A dependência total ou parcial só acontece quando a chave primária é concatenada.

---

## DEPENDÊNCIA FUNCIONAL TOTAL OU PARCIAL - EXEMPLO

**Dependência total**: Na Entidade ITEM-DE-PEDIDO, o atributo **QUANTIDADE** depende de forma total da chave primária concatenada **Nº-PEDIDO + COD.PROD**.

---

## DEPENDÊNCIA FUNCIONAL TRANSITIVA

Quando um atributo ou conjunto de atributos **A** depende de outro atributo **B** que **não pertence à chave primária** (mas é dependente funcional desta) dizemos que **A é Dependente Transitivo de B**.

**Exemplos**:
1. Na entidade PEDIDO, os atributos **ENDEREÇO, CIDADE e UF** são dependentes transitivos do atributo **CLIENTE**
2. O atributo **NOME-DO-VENDEDOR** é dependente transitivo do atributo **CODIGO-DO-VENDEDOR**

---

## Próximo tópico

- Normalização II

### O que foi visto

- Normalização
- Anomalias
- 1FN
- Dependência funcional total ou parcial
- Dependência funcional transitiva
