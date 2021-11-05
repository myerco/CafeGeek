---
title: Relacionamentos
description: Aprenda modelos de Banco de dados relacionais
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
layout: page
---



Um relacionamento é uma associação entre uma ou várias entidades.
Por exemplo: podemos definir um relacionamento que associa o cliente ARAGORN com a cidade DOR-LÓNIM. Esse relacionamento especifica que cliente ARAGORN é um cliente que mora em DOR-LÓNIM.

Outro exemplo:

    Os clientes Compram Produtos;
    As Notas Tem Produtos;
    As Notas Tem Vendedores;
    Os Vendedores Registram Notas

Cardinalidade

No relacionamento entre duas entidades o número de ocorrências de uma entidade que está associado a outra entidade determina a cardinalidade.

    Um para Um;
    Um para Muitos;
    Muitos para Muitos;

Representação

    Ramificação - Um ou mais valores
    Tracejado - Opcional
    Ponta única - Apenas um valor
    Ponta contínua - Obrigatório

    Um para Um.

    Significa que cada elemento da entidade PEDIDO relaciona-se com somente um elemento de entidade NOTA.
    Modelo lógico.

    Um PEDIDO tem uma NOTA->

    NOTA

tem um PEDIDO
Modelo relacional.
Tabelas.
PEDIDO ID 	DATA
1	12/11/2016
3	02/04/2017
6	10/10/2017

NOTA ID 	DATA 	VALOR_TOTAL 	SERIE 	CHAVE 	PEDIDO_ID
1	12/11/2016	2.500,00	00012345	QERE001	1
3	02/04/2017	2.500,00	00012378	QERE010	3
6	10/10/2017	2.500,00	00019874	QERE022	6
Um para muitos.

Um elemento da entidade CIDADE relaciona-se com muitos elementos da entidade CLIENTE, mas cada elemento da entidade CLIENTE somente pode estar relacionado a um elemento da entidade CIDADE.
Modelo lógico

Uma CIDADE tem vários CLIENTES->

CLIENTE
pertence a uma CIDADE
Modelo Relacional
Tabelas
CIDADE ID 	DESCRICAO 	UF
1	Valfenda	CO
2	Castelo Sul	SR
3	Vento Brav	AR

CLIENTE ID 	CPF 	NOME 	TIPO 	ENDERECO 	EMAIL 	CIDADE_ID
1	001.546.578-04	Aragorn	N	Gondor	...	1
2	787.354.789-55	Legolas	N	Valfenda	...	1
3	000.000.000-00	Gandalf	E	Terra Média	...	2

    1 - Chave primária;
    2 - Chave estrangeira, referência a chave primária de outra tabela;

Muitos para muitos.

Um elemento da entidade PRODUTO relaciona-se com muitos elementos da entidade NOTA e cada elemento da entidade NOTA está relacionado a um elemento da entidade PRODUTO.
Modelo lógico.

Um PRODUTO pode estar em várias NOTAS->

NOTA
tem vários PRODUTOS
Modelo relacional.
Tabelas.
PRODUTO ID 	DESCRICAO 	VALOR
1	Espada Bronze	150,00
3	Escudo Prata	420,00
6	Arco de Madeira	100,00

PRODUTO_NOTA PRODUTO_ID 	NOTA_ID 	QUANTIDADE 	VALOR_VENDA
1	1	1,0	150,00
3	1	1,0	420,00
6	3	2,0	100,00

NOTA ID 	DATA 	VALOR_TOTAL 	SERIE 	CHAVE 	PEDIDO_ID
1	12/11/2016	2.500,00	00012345	QERE001	1
3	02/04/2017	2.500,00	00012378	QERE010	3
6	10/10/2017	2.500,00	00019874	QERE022	6

    Para a organização dos dados é construída uma tabela (tabela de relacionamento) entre as duas entidades;
    A nova tabela herda as chaves primárias das duas tabelas que ela relaciona;
    Importante verificar que a tabela tem outros atributos que expressam valores únicos do negócio , QUANTIDADE e VALOR_PRODUTO pois para cada venda eles variam;
