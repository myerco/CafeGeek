---
title: Os atributos
description: Iniciando a Analise
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
layout: page
---

Toda entidade é representada por um conjunto de atributos.

Exemplo modelo relacional:

Atributos são propriedades descritivas de entidades. Cada instância de CLIENTE será formada por valores nestes atributos, e o conjunto destes valores devemos visualizar como uma linha de uma tabela.
ID 	CPF 	NOME 	TIPO 	ENDERECO 	EMAIL 	SEXO_ID 	CIDADE_ID
1	001.546.578-04	Aragorn Passos Largos	P	Gondor 	aragorn21@gmail.com, passos.largos@hotmail.com 	M	35
2	698.474.456-78	Arwen de Valfenda	P	Valfenda 	arwenvalfenda@gmail.com 	F	13
3	000.000.000-00	Gandalf o Cinzento	E	Terra Média 		M	35
Tipos de atributos

    Simples.

    Expressam um valor indivisível. Exemplo : SEXO_ID
    Compostos.

    Expressam mais de um valor, pode ser dividido. Exemplo: NOME e ENDERECO
    Monovalorados.

    Exemplo : CIDADE_ID para a entidade cliente
    Multivalorado.

    Pode contar vários valores. Exemplo : EMAIL
    Atributos nulos.

    Podem ser nulos. Exemplo : EMAIL
    Atributo derivado.
        O valor deriva de outro atributo. Exemplo : VALOR TOTAL
        O VALOR TOTAL é construído com outros objetos ou atributos como descontos, acréscimos e A SOMA TOTAL DE TODOS OS PRODUTOS daquela venda.

Restrições

    Os nomes não podem conter espaços em branco;
    Não usar caracteres especiais "@#$%¨&*";
    Não usar palavras reservadas: VARCHAR,CHAR,INTEGER e etc;
    Tamanho de 30 caracteres;

Representação

    # - Chave primária ou (P) no modelo relacional;
    F - Chave estrangeira, somente no modelo relacional;
    O - Atributo;
    * - Obrigatório;
