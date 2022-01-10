---
title: Iniciando a Analise
description: Permite ao desenvolvedor/arquiteto entender o relacionamento e as restrições das entidades participantes; Ajuda a entender o procedimento de padronização seguido por uma organização ao lidar com um grande volume de dados; Devem ser simples e fáceis de entender; Devem estar atualizadas;
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
layout: page
---

Neste capitulo iremos iniciar a analise das necessidades de negócio utilizando o conceito de Regra de Negócio para orientar a análise.

![The King under the Mountain](http://tolkiengateway.net/w/images/thumb/3/3c/Alan_Lee_-_The_King_under_the_Mountain.jpg/424px-Alan_Lee_-_The_King_under_the_Mountain.jpg)

## A Regra de negócio
- Permite ao desenvolvedor/arquiteto entender o relacionamento e as restrições das entidades participantes;
- Ajuda a entender o procedimento de padronização seguido por uma organização ao lidar com um grande volume de dados;
- Devem ser simples e fáceis de entender;
- Devem estar atualizadas;

## Mãos a obra

![Celebrimbor](http://tolkiengateway.net/w/images/4/4f/Angus_McBride_-_Celebrimbor.gif)

O nosso objetivo é extrair informações da regra de negócio a fim de identificar objetos e regras conceituais. Para tal tarefa seguiremos as seguintes premissas:

1. Identificar Objetos que existem no mundo real ou representam o negócio;
1. Devemos ser capazes de detalhar as características de cada objeto identificado;
1. Os objetos devem ser de fácil construção em uma tabela/lista;

### Objetos extraídos
#### Pedidos dos clientes.

|NÚMERO|	DATA    |	PRODUTO            |CLIENTE    |
|:-    |:-        |:-                  |:-         |
|123	 |11/12/2017|	Escudo de Carvalho |Thorin     |  
|124	 |05/02/2018|	Arco Élfico dourado|Legolas    |
|125	 |21/04/2018|	Punhal de Troll    |Aragorm    |

- Existe no mundo real no formato de uma agenda;
- Pode ser detalhado : número do pedido,data do pedido, cliente, valor e produto;

#### Registro de Funcionários.

| MATRICULA |	NOME          |	SALÁRIO|
|:-         |:-             |-:      |
|480001     |	Bilbo Baggins |	1.000   |
|480453	    |Samwise Gamgee |	1.000   |
|480689	    |Peregrin Took  |	1.100   |

- Existe no mundo real
- Pode ser detalhado : identificação ou matricula, nome e salário;

#### Cargos dos Funcionários.

|CARGO ID|	NOME|
|:-      |:-    |
|01	     |Atendente|
|03	     |Gerente de Vendas|
|02	     |Contabilidade|

- Existe no mundo real no formato de uma tabela (lista), fixada na sala do gerente;
- Pode ser detalhado : nome do cargo e identificação;

#### Registro de classificação de clientes.

|ID|NOME  |
|:-|:-  |
|01|	Humano|
|02|	Elfo|
|03|	Hobbit|
|04|	Uruk Hai|

- São classificações de clientes, não existem no formato de listas mas são estão presentes no negócio pois diferenciam o atendimento e os produtos;
- Pode ser detalhado : nome da raça e uma identificação;

#### E-mail dos Clientes.

|EMAIL|
|:-|
|lurtzuruk@terramedia.com|
|passoscurtos@gmail.com|
|mariadoc.brandeduque@terramedia.com|
|elendil@hotmail.com|

- Identificam um cliente ou funcionário mas não fazem sentido isolados;
- Pode ser detalhado mas com outras informações associadas: nome do cliente ou funcionário, identificação e matricula
- Na verdade o e-mail é parte do cliente;

> **Nota**
>
>Entender os seguintes conceitos ajudam a fazer a análise:
> - Dado
> - Informação
> - Conhecimento

## Regras e restrições
![The One Ring](http://tolkiengateway.net/w/images/thumb/e/ef/One_ring.png/300px-One_ring.png)

> Um Anel para governar todos eles,     
Um Anel para encontrá-los,        
Um Anel para trazê-los todos e na escuridão prendê-los.

|Regras             |Restrições           |
|:-                 |:-                   |
|Para cada nota são registrados os produtos vendidos.| Um produto pode estar em mais de uma nota; Uma nota pode ter mais de um produto; O valor do produto pode ter descontos e acrescimentos.|
|Os Clientes tem uma determinada raça; O sexo dos clientes são registrados como M = Masculino e F = Feminino;|Um cliente tem uma raça e uma raça pode estar presente em vários clientes;Somente as letras M ou F podem ser registrados para cada cliente;|

## Referências
- [Tolkien Gateway](http://tolkiengateway.net/wiki/Main_Page)
