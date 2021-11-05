---
title: As Entidades
description: Iniciando a Analise
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
layout: page
---

## Entidade.

Define-se entidade como aquele objeto que existe no mundo real com uma identificação distinta e com um significado próprio.

São coisas que existem no negócio, ou ainda, descrevem o negócio.

Uma entidade tem um conjunto de propriedades e os valores para alguns conjuntos dessas propriedades devem ser únicos.

Exemplo :

- Notas fiscais (numero, data, valor total)
- Clientes (cpf, nome, sexo,endereço)
- Produtos (código, endereço, valor)
- Cidade (id,nome, estado)

## Representação no modelo lógico.

## Representação no modelo relacional (Tabela).

    Tabela Cliente.
    CLIENTE ID 	CPF 	Nome 	Tipo 	Endereco 	...
    1	001.546.578-04	Aragorn	N	Gondor	...
    2	787.354.789-55	Legolas	N	Valfenda	...
    3	000.000.000-00	Gandalf	E	Terra Média	...

## Restrições

- Os nomes não podem conter espaços em branco;
- Não usar caracteres especiais "@#$%¨&*";
- Não usar palavras reservadas: INSERT, UPDATE, DELETE, SELECT e etc;
- Tamanho de 30 caracteres;
