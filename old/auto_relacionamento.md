---
title: Auto-relacionamento
description: Aprenda modelos de Banco de dados relacionais
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
layout: page
---

É um tipo especial de relacionamento onde as entidades se relacionam com elas mesmas.
Tipos de auto-relacionamentos.

    Auto-relacionamento Um-para-Muitos;
    Auto-relacionamento Muitos-para-Muitos.

    Um para muitos

    Considere a entidade CARGOS, observe que alguns cargos são filhos de outros cargos (ordem hierárquica).
    Modelo lógico.
    Modelo relacional.
    Tabela.
    CARGO ID 	DESCRICAO 	VALOR 	CARGO_ID
    1	Gerente Comercial	1.000,00
    2	Atendente	500,00	1
    3	Embalador	500,00	1
    4	Gerente de Negócio	4.000,00
    5	Contador	2.000,00	4
    Muitos para muitos

    Observe que os itens registrados na entidade PRODUTO podem ser compostos de vários outros itens, componentes. Por outro lado, um item componente pode participar da composição de muitos itens
    Modelo lógico.
    Modelo relacional.
    Tabelas.
    PRODUTO ID 	DESCRICAO 	VALOR 	CATEGORIA_ID
    1	Espada de aço da montanha da perdição	200,00	2
    2	Poder de gelo	300,00	4
    3	Escudo de Carvalho	180,00	6
    4	Pedra azul	20,00	5
    5	Garrafa de Bafo de Yeti	10,00	5

    COMPONENTE PRODUTO_ID 	PRODUTO_ID1
    1	2

32 24 25
