---
title: Conhecendo a taberna
description: Neste projeto iremos utilizar como exemplo de negócio um empreendimento famoso conhecido na literatura que é a Taberna do Pônei Saltitante localizada na cidade de Bree presente nas obras de J.R.R. Tolkien.
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
layout: page
---

Neste projeto iremos utilizar como exemplo de negócio um empreendimento famoso conhecido na literatura que é a Taberna do Pônei Saltitante localizada na cidade de Bree presente nas obras de J.R.R. Tolkien.

![The Lord of the Ring](https://i.pinimg.com/originals/3b/31/e3/3b31e34debef0e079a148d8941af59de.jpg)

## O projeto

Para conseguir representar a organização e armazenamento dos dados vamos implementar o seguinte:

- Modelo Lógico;
- Modelo Relacional;
- Comandos para construção.

## A cidade de Bree

![http://tolkiengateway.net/wiki/Bree](http://tolkiengateway.net/w/images/thumb/1/13/Darek_Zabrocki_-_Morning.jpg/250px-Darek_Zabrocki_-_Morning.jpg)

A cidade de Bree conseguiu se manter prospéra próspera no Norte, apesar das guerras e tumultos que destruíram o Reino dos Dúnedain do Norte. Dizem que quando os homens foram para o Ocidente, Bree já estava lá e quando os antigos reis retornaram, encontraram Bree os esperando. Dizem que foi fundada pors homens que não voltaram para Beleriand na Primeira Era, e após a queda do Reino de Cardolan na guerra conta Angmar se tornou uma cidade independente.

![Map of Bree](http://tolkiengateway.net/w/images/thumb/1/16/The_Lord_of_the_Rings_Online_-_Bree_map.gif/180px-The_Lord_of_the_Rings_Online_-_Bree_map.gif)

É a única região na Terra-média, onde Homens e Hobbits convivem em harmonia e e um importante centro comercial para elfos e anões, que são bens de comércio ou viagens de um reino para outro. O centro econômico e social é a **Taverna do Pônei Saltitante**, conhecida por ter as melhores bebidas do Norte.

## Taverna do Pônei Saltitante e o projeto
![tabernaponeisaltitante](https://3.bp.blogspot.com/-bbFXtl8DLsM/WhswXoihJKI/AAAAAAAANa4/vOl3JpqLHJY9-rgkRmd87yTkF1vUZ2hAgCLcBGAs/s320/tabernaponeisaltitante.jpg)

A Taberna do Ponei Saltitante está ampliando o seu atendimento, buscando atender melhor sua variada clientela, Orc´s, Elfos, Hobbits e Humanos, este último com uma preferência estranha por dispositivos. Também se aliou ao Ferreiro da cidade a fim de diversificar os produtos, acrescentando espadas, escudos, elmos e outros.

![The Inn at Bree](http://tolkiengateway.net/w/images/thumb/2/2b/Alan_Lee_-_The_Inn_at_Bree.jpg/369px-Alan_Lee_-_The_Inn_at_Bree.jpg)

Para tal, procura implementar um sistema informatizado para registrar as seguintes informações:

- Pedidos dos clientes;
- Registro de compras;
- Registro de funcionários;
- Cargos dos funcionários;
- Registro de clientes e suas classificações;
- Tabela de preços;

## Detalhes
- Os cargos tem um valor para ser acrescido no salário do empregado;
- Os cargos estão hierarquicamente organizados;
- Empregados são registrados com um número de matricula;
- Empregados tem um salário base;
- E-mail´s dos clientes são registrados;
- Raças dos clientes são registrados a fim de personalizar o atendimento;
- Endereço dos clientes são registrados;
- Clientes são classificados por tipos (Padrão, Especial e Classe A);
- Os pedidos dos clientes são feitos em um caderno e nem sempre resultam em uma venda;
- Produtos podem ser compostos de outros itens, como por exemplo uma espada com pedras preciosas, aumentando a sua eficácia. Vendemos as pedras em separado também;

## Necessidades
![At the Sign of the Prancing Pony](http://tolkiengateway.net/w/images/f/fa/Ted_Nasmith_-_At_the_Sign_of_the_Prancing_Pony.jpg)

- Quantos clientes estão registrados e quais são suas raças?
- Quantos clientes por classe estão registrados?
- Qual o valor total das vendas para os clientes da classe Padrão?
- Qual o volume de vendas por período?
- Quanto cada empregado vendeu por período?
- Qual o produto mais vendido?


## Referências
- [Tolkien Gataway](http://tolkiengateway.net/wiki/Bree)
