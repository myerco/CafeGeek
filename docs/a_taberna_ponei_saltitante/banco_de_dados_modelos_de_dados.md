---
title: Modelo de Dados e o Processo de Desenvolvimento de banco de dados
description: Sob a estrutura do banco de dados está o modelo de dados: um conjunto de ferramentas conceituais usadas para a descrição de dados, relacionamentos entre dados, semântica de dados e regras de consistência.
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
layout: page
---

Sob a estrutura do banco de dados está o modelo de dados: um conjunto de ferramentas conceituais usadas para a descrição de dados, relacionamentos entre dados, semântica de dados e regras de consistência.

## Existem diversos tipos de modelos de banco de dados, entre eles:
- Modelo de Arquivos flat;
- Modelo Relacional;
- Modelo Hierárquico;
- Modelo de Rede;
- Modelo Orientado a Objeto;

## Processo de Desenvolvimento de Banco de dados.
- Requisitos de informações de negócio - Analise e interpretação da Regra de negócio;
- Modelagem de dados Conceitual - Construção do Modelo Lógico;
- Design de Banco de dados - Construção do Modelo Relacional;
- Criação do Banco de Dados - Construção do modelo no PostgreSQL utilizando comandos SQL;

## Modelo Lógico
Tem por base a percepção de que o mundo real é formado por um conjunto de objetos chamados entidades e pelo conjunto dos relacionamentos entre esse objetos.

Tem o objetivo de facilmente ser interpretado por todos os usuários, utilizando diagramas e representações gráficas dos objetos do negócio.
Elementos.

1. Entidades;
1. Atributos e a sua opcionalidade;
1. Especialização e Generalização;
1. Relacionamentos e a sua opcionalidade e cardinalidade.

Exemplo:

## Modelo Físico
Estende detalhes do modelo de lógico e tem as seguintes características:

- Define com precisão tipos de dados e definições de tabelas;
- Identifica exibições, índices e outros objetos de banco de dados;
- Descreve como os objetos devem ser implementados no banco de dados específico;
- Apresenta chaves primárias e estrangeiras;

Exemplo:

## Comparação

| Análise             |Design               |
|:-                   |:-                   |
|**Modelo Lógico**    |**Modelo Físico**    |
|Entidade	            |Tabela               |
|Atributo	            |Coluna               |
|Instância            |Linha                |
|UID Primário         |Chave Primária       |
|UID Secundário	      |Restrição Exclusiva  |
|Relacionamento	      |Chave Estrangeira    |
|Restrição de Negócio	|Restrições de Verificação|

## Banco de Dados Relacional
- Armazena informações em tabelas com linhas e colunas;
- Uma tabela é uma coleção de registros;
- Uma linha é denominada registro ou instância;
- Uma coluna é chamada de campo ou atributo;

Regras:

- O nome das tabelas é único;
- Nas tabelas o nome das colunas é exclusivo;
- As tabelas podem contar várias linhas;
- As tabelas tem um valor para identificar as linhas de forma exclusiva;

Exemplo:

|CLIENTE ID| 	CPF |	NOME |	TIPO |	ENDERECO |	EMAIL |	SEXO_ID |	CIDADE_ID|
|:-        |:-    |:-    |:-     |:-	       |:-      |:-       |:-        |
|1         |001.546.578-04|Aragorn Passos Largos|	P	|Gondor|aragorn21@gmail.com, passos.largos@hotmail.com| 	M|	35|
|2|	698.474.456-78|	Arwen de Valfenda|	P|	Valfenda| 	arwenvalfenda@gmail.com |	F|	13|
