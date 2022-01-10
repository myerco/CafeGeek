---
title: Especialização e generalização
description: Aprenda modelos de Banco de dados relacionais
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
layout: page
---


Especialização

Considere a entidade CLIENTE, ela pode ser definida em um conjunto de entidades classificados como :

    PADRÃO (P);
    ESPECIAL (E);
    CLASSE A (A);

CLIENTE ID 	CPF 	NOME 	TIPO 	ENDERECO 	EMAIL 	SEXO_ID 	CIDADE_ID
1	001.546.578-04	Aragorn Passos Largos	P	Gondor 	aragorn21@gmail.com, passos.largos@hotmail.com 	M	35
2	698.474.456-78	Arwen de Valfenda	P	Valfenda 	arwenvalfenda@gmail.com 	F	13
3	000.000.000-00	Gandalf o Cinzento	E	Terra Média 		M	35

O processo de projetar os subgrupos dentro de um conjunto de entidades é chamado de especialização, o qual nos permite distinguir os tipos de clientes.
CLIENTE - Tipo (P) ID 	CPF 	NOME 	TIPO 	ENDERECO 	EMAIL 	SEXO_ID 	CIDADE_ID
1	001.546.578-04	Aragorn Passos Largos	P	Gondor 	aragorn21@gmail.com, passos.largos@hotmail.com 	M	35
2	698.474.456-78	Arwen de Valfenda	P	Valfenda 	arwenvalfenda@gmail.com 	F	13

Auxilia na segurança dos dados, pois restringe a sua visualização e acesso.

Podemos restringir o acesso as colunas e linhas de uma tabela,
como por exemplo :
CLIENTE - Somente algumas colunas NOME 	TIPO 	ENDERECO 	EMAIL
Gandalf o Cinzento	E	Terra Média 	
Generalização

Praticamente a generalização é o inverso da especialização.
Por exemplo: a entidade PRODUTO é na realidade uma generalização para diversas entidades de dados de PRODUTOS (registrados em várias filias).
PRODUTOS - Todos os produtos ID	NOME
11	Espada de Eldor
12	Espada Élfica
21	Escudo de carvalho
22	Escudo de Mitrill
PRODUTO - Espadas ID	NOME
11	Espada de Eldor
12	Espada Élfica
PRODUTOS - Escudos ID	NOME
21	Escudo de carvalho
22	Escudo de Mitrill

Em Sistemas Distribuídos podemos resumir a visualização de diferentes entidades em somente uma.

Exemplo: Espadas podem estar armazenadas em uma cidade e escudos em outra.
