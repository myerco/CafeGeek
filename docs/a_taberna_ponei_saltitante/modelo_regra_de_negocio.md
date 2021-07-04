---
title: A regra de negócio
description: A regra de negócio para modelar e estruturas as informações utilizando um modelo relacional.
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
---
# A regra de negócio
A Taberna do Ponei Saltitante está ampliando o seu atendimento, buscando atender melhor sua variada clientela, Orc´s, Elfos, Hobbits e Humanos, este último com uma preferência estranha por dispositivos. Também se aliou ao Ferreiro da cidade a fim de diversificar os produtos, acrescentando espadas, escudos, elmos e outros.
Para tal, procura implementar um sistema informatizado para registrar as seguintes informações:

- Pedidos dos clientes;
- Registro de compras;
- Registro de funcionários;
- Cargos dos funcionários;
- Registro de clientes e suas classificações;
- Tabela de preços;

## 1. Detalhes
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

## 2. Necessidades
- Quantos clientes estão registrados e quais são suas raças?
- Quantos clientes por classe estão registrados?
- Qual o valor total das vendas para os clientes da classe Padrão?
- Qual o volume de vendas por período?
- Quanto cada empregado vendeu por período?
- Qual o produto mais vendido?
