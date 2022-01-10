---
title: A chave primária
description: Aprenda modelos de Banco de dados relacionais
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
layout: page
---

    Este(s) atributo(s) cujos valores nunca se repetem, sempre tem(têm) a função de atuar(em) como identificador(es) único(s) das instâncias da entidade.
    Chave primária então é o atributo (ou conjunto de atributos concatenados) que identifica uma única ocorrência dentro de uma tabela.

Representação no modelo lógico (#).
Representação no modelo relacional (P).
A coluna ID é a chave primária da tabela e apresenta as seguintes características:

    Não se repete
    Não é nula
    É um índice (estrutura de acesso mais rápida)


CLIENTE ID 	CPF 	NOME 	TIPO 	ENDERECO 	EMAIL 	SEXO_ID 	CIDADE_ID
1	001.546.578-04	Aragorn Passos Largos	P	Gondor 	aragorn21@gmail.com, passos.largos@hotmail.com 	M	35
2	698.474.456-78	Arwen de Valfenda	P	Valfenda 	arwenvalfenda@gmail.com 	F	13
3	000.000.000-00	Gandalf o Cinzento	E	Terra Média 		M	35
