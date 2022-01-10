---
title: A taberna do Pônei Saltitante
description: Neste projeto serão apresentadas técnicas de modelagem de banco de dados e dicas importantes para construir uma base de dados organizada evitando redundâncias.
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
layout: page
---


## Habilidades que serão aprendidas
Neste projeto serão apresentadas técnicas de modelagem de banco de dados e dicas importantes para construir uma base de dados organizada evitando redundâncias.

- Identificar e descrever objetos conceituais a partir da regra de negócio;
- Construir relacionamentos entre os objetos;
- Aplicar regras de normalização;
- Diagramar modelos de dados lógico e relacional;
- Implementar comandos para construção do banco de dados relacional utilizando PostgreSQL;

> Manipular e construir objetos conceituais facilita a documentação e apresentação de projetos de banco de dados.

**CapítuloI - Conhecendo a Taberna**

1. [Conhecendo a Taberna](banco_de_dados_conhecendo_a_taberna.html)
1. [Modelo de dados e o Processo de Desenvolvimento de Banco de Dados](banco_de_dados_modelos_de_dados.html)
1. [Iniciando a Analise](banco_de_dados_iniciando_analise.html)
1. [O SQLDeveloper](banco_de_dados_sqldeveloper_com_postgresql.html)
1. [As Entidades](as_entidades.html)
1. [Os Atributos](os_atributos.html)
1. [A Chave primária](a_chave_primaria.html)
1. [Especialização e Generalização](especializacao_generalizacao.html)
1. [Relacionamentos](relacionamentos.html)
1. [O Auto-relacionamento](auto_relacionamento.html)
1. [Normalização](normalizacao.html)
1. O banco de dados PostgreSQL
1. Construção do modelo no PostgreSQL

## 1. Introdução
Neste projeto iremos utilizar como exemplo de negócio um empreendimento famoso conhecido na literatura que é a Taberna do Pônei Saltitante localizada na cidade de Bree presente nas obras de J.R.R. Tolkien.

![The Lord of the Ring](https://i.pinimg.com/originals/3b/31/e3/3b31e34debef0e079a148d8941af59de.jpg)

## 2. O projeto

Para conseguir representar a organização e armazenamento dos dados vamos implementar o seguinte:

- Modelo Lógico;
- Modelo Relacional;
- Comandos para construção.

## 3. A cidade de Bree

![http://tolkiengateway.net/wiki/Bree](http://tolkiengateway.net/w/images/thumb/1/13/Darek_Zabrocki_-_Morning.jpg/250px-Darek_Zabrocki_-_Morning.jpg)

A cidade de Bree conseguiu se manter prospéra próspera no Norte, apesar das guerras e tumultos que destruíram o Reino dos Dúnedain do Norte. Dizem que quando os homens foram para o Ocidente, Bree já estava lá e quando os antigos reis retornaram, encontraram Bree os esperando. Dizem que foi fundada pors homens que não voltaram para Beleriand na Primeira Era, e após a queda do Reino de Cardolan na guerra conta Angmar se tornou uma cidade independente.

![Map of Bree](http://tolkiengateway.net/w/images/thumb/1/16/The_Lord_of_the_Rings_Online_-_Bree_map.gif/180px-The_Lord_of_the_Rings_Online_-_Bree_map.gif)

É a única região na Terra-média, onde Homens e Hobbits convivem em harmonia e e um importante centro comercial para elfos e anões, que são bens de comércio ou viagens de um reino para outro. O centro econômico e social é a **Taverna do Pônei Saltitante**, conhecida por ter as melhores bebidas do Norte.

## 4. Taverna do Pônei Saltitante e o projeto
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

## 5. Detalhes dos atributos
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

## 6. Necessidades
![At the Sign of the Prancing Pony](http://tolkiengateway.net/w/images/f/fa/Ted_Nasmith_-_At_the_Sign_of_the_Prancing_Pony.jpg)

- Quantos clientes estão registrados e quais são suas raças?
- Quantos clientes por classe estão registrados?
- Qual o valor total das vendas para os clientes da classe Padrão?
- Qual o volume de vendas por período?
- Quanto cada empregado vendeu por período?
- Qual o produto mais vendido?

--------------------
Sob a estrutura do banco de dados está o modelo de dados: um conjunto de ferramentas conceituais usadas para a descrição de dados, relacionamentos entre dados, semântica de dados e regras de consistência.

![The Pillars of the Kings](http://tolkiengateway.net/w/images/9/97/Ted_Nasmith_-_The_Pillars_of_the_Kings.jpg)

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

### Elementos
1. Entidades;
1. Atributos e a sua opcionalidade;
1. Especialização e Generalização;
1. Relacionamentos e a sua opcionalidade e cardinalidade.

Exemplo:

![Modelo lógico](https://1.bp.blogspot.com/-su8B-5NlNq8/WhzflZ1dmnI/AAAAAAAANcc/NB8CnwX7xFMzzMuXhFCKlfvKwTz5dQ8xgCLcBGAs/s320/Logical.png)

## Modelo Físico
Estende detalhes do modelo de lógico e tem as seguintes características:

- Define com precisão tipos de dados e definições de tabelas;
- Identifica exibições, índices e outros objetos de banco de dados;
- Descreve como os objetos devem ser implementados no banco de dados específico;
- Apresenta chaves primárias e estrangeiras;

Exemplo:

![](https://2.bp.blogspot.com/-4WkXSYf00_s/WiCd-gdpBrI/AAAAAAAANdo/54VhOg6_iWU1enoF9rKl4shhVCT0_nAmwCPcBGAYYCw/s320/Relacional.pngs)

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


-------------------

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


-----

## Características
- Ferramenta gráfica desenvolvida pela ORACLE;
- Permite a implementação de estruturas de banco de dados executando comandos SQL;
- Construção de modelos lógicos e físicos;

## Instalação
1. Instalando no linux Ubuntu
  - Instalando Java 8;
  - Baixando o  SQLDeveloper Oracle;
  - Descompactando o SQLDeveloper.
  - Descompacte o programa no diretório /opt para padronizar as instalação
  ```bash
  sudo unzip ~/Downloads/sqldeveloper-*-no-jre.zip -d /opt/
  sudo chmod +x /opt/sqldeveloper/sqldeveloper.sh
  sudo ln -s /opt/sqldeveloper/sqldeveloper.sh /usr/local/bin/sqldeveloper
  ```  
  - Alterando o arquivo sqldeveloper.sh
  ```bash
  #!/bin/bash
  unset -v GNOME_DESKTOP_SESSION_ID<
  cd /opt/sqldeveloper/sqldeveloper/bin && bash sqldeveloper $*
  ```
  - Testando.
  ```bash
  sqldeveloper.sh
  ```
  - ADICIONANDO AO DESKTOP

  Arquivo : `/usr/share/applications/sqldeveloper.desktop`
  ```bash
  [Desktop Entry]
  Exec=sqldeveloper
  Terminal=false
  StartupNotify=true
  Categories=GNOME;Oracle;Utility;Development;
  Type=Application
  Icon=/opt/sqldeveloper/icon.png
  Name=Oracle SQL Developer
  Comment=SQLDeveloper Oracle
  Version=?
  GenericName=ORACLE SQL DEVELOPER
  ```
1. Instalando no Windows
  - Baixe o aplicativo de preferência com JDK incluído
  - Descompacte em uma pasta de trabalho, por exemplo: `c:\desenvolvimento\SQLDeveloper`
  - Baixe o driver JDBC para [PostgreSQL](https://jdbc.postgresql.org/download.html);
  - Execute o `SQLDeveloper.exe`;
  - Adicione o driver do PostgreSQL : Menu->Ferramentas->Banco de Dados->Drivers JDBC de Terceiros;

## Data Modeler
- `Menu` > `Exibir` > `Data Modeler` > `Browser`;
- Na janela Browser clique no Modelo Lógico com botão direito e escolha Mostrar para que barra de menu apresente as opções de construção de modelos;

-----
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

-----

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

------

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

----

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

----

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

--------------

É um processo matemático formal, que tem seus fundamentos na teoria dos conjuntos. Através deste processo pode-se, gradativamente, substituir um conjunto de entidades e relacionamentos por um outro, o qual se apresenta “purificado” em relação às anomalias de atualização (inclusão, alteração e exclusão) as quais podem causar certos problemas, tais como: grupos repetitivos (atributos multivalorados) de dados, dependências parciais em relação a uma chave concatenada, redundância de dados desnecessárias, perdas acidentais de informação, dificuldade na representação de fatos da realidade observada e dependências transitivas entre atributos.
Anomalias.

Considere o formulário de NOTAS apresentado a seguir. Podemos considerar que uma entidade formada com os dados presentes neste documento, terá a seguinte apresentação:
NOTAS ID 	DATA 	CLIENTE 	EMAIL 	ENDERECO 	CIDADE 	UF 	PRODUTO_ID 	DESCRICAO 	UNID. 	QUANTIDADE 	VALOR
1	12/11/2016	Elendur 	elendur@hotmail.com, elendur12r@gmail.com 	Rua das Flores	LAGO	VL 	1	Espada de fogo	P	1	200,00
1	02/04/2017	Elendur 	elendur@hotmail.com, elendur12r@gmail.com 	Rua das Flores	LAGO	VL 	2	Escudo de Carvalho	P	1	180,00
3	10/10/2017	Durin II 	durinii@yahoo.com.br 	Caverna de Orgrimar	Floresta Negra	GO 	8	Cajado de Gelo	P	1	1.200,00
3	30/11/2017	Eldacar 	el65@gmail.com, jhon65@gmail.com 	Caverna de Orgrimar	Floresta Negra	GO 	12	Cajado de Fogo do Vulcão	P	1	1.300,00


Caso a entidade fosse implementada como uma tabela em um banco de dados, as seguintes anomalias iriam aparecer:

   Anomalia de inclusão: ao ser incluído um novo cliente, o mesmo tem que estar relacionado a uma venda;
   Anomalia de exclusão: ao ser excluído um cliente, os dados referentes as suas compras serão perdidos;
   Anomalia de alteração: caso algum fabricante de produto altere a faixa de preço de uma determinada classe de produtos, será preciso percorrer toda a entidade para realizar múltiplas alterações;

Formas Normais.

   Primeira Forma Normal (1FN);
   Dependência Funcional;
       Total e parcial;
       Transitiva;
   Segunda Forma Normal (2FN);
   Terceira Forma Normal (3FN);
   Forma Normal de BOYCE/CODD (FNBC);
   Quarta forma normal (4FN).

   Primeira forma normal (1FN).

   Uma tabela está na 1FN se e somente se:
       Todos seus atributos forem atômicos, atributos compostos não são permitidos EMAIL;
       Cada ocorrência da chave primária (ID) deve corresponder a uma e somente uma informação de cada atributo, ou seja, a entidade não deve conter grupos repetitivos;
   NOTAS ID 	DATA 	CLIENTE 	EMAIL 	ENDERECO 	CIDADE 	UF 	PRODUTO_ID 	DESCRICAO 	UNID. 	QUANTIDADE 	VALOR
   1	12/11/2016	Elendur 	elendur@hotmail.com, elendur12r@gmail.com 	Rua das Flores	LAGO	VL 	1	Espada de fogo	P	1	200,00
   1	02/04/2017	Elendur 	elendur@hotmail.com, elendur12r@gmail.com 	Rua das Flores	LAGO	VL 	2	Escudo de Carvalho	P	1	180,00
   3	10/10/2017	Durin II 	durinii@yahoo.com.br 	Caverna de Orgrimar	Floresta Negra	GO 	8	Cajado de Gelo	P	1	1.200,00
   3	30/11/2017	Eldacar 	el65@gmail.com, jhon65@gmail.com 	Caverna de Orgrimar	Floresta Negra	GO 	12	Cajado de Fogo do Vulcão	P	1	1.300,00
   Dependência funcional.

   Dizemos que um atributo ou conjunto de atributos A é dependente funcional de um outro atributo B contido na mesma entidade se, a cada valor B existir nas linhas da entidade em que aparece, um único valor de A . Em outras palavras, A depende funcionalmente de B, Exemplo : Na entidade NOTA, o atributo DATA depende funcionalmente de ID.

   O exame das relações existentes entre os atributos de uma entidade deve ser feito a partir do conhecimento (conceitual) que se tem sobre a realidade a ser modelada.
   Dependência funcional parcial ou total.

   Na ocorrência de uma chave primária concatenada, dizemos que um atributo ou conjunto de atributos depende de forma completa ou total desta chave primária concatenada, se e somente se, a cada valor da chave (e não parte dela) está associado a um valor para cada atributo. Quando um atributo só depende de parte da chave primária concatenada e não dela como um todo é dito "dependente parcial". A dependência total ou parcial só acontece quando a chave primária é concatenada.

   Exemplo:

   Dependência total: Na Entidade PRODUTO, o atributo QUANTIDADE depende de forma total da chave primária concatenada PRODUTO_ID + NOTA_ID
   Dependência funcional transitiva

   Quando um atributo ou conjunto de atributos A depende de outro atributo B que não pertence à chave primária (mas é dependente funcional desta) dizemos que A é Dependente Transitivo de B. Exemplos: Na entidade NOTA, os atributos ENDERECO, CIDADE e UF são dependentes transitivos do atributo CLIENTE;
   NOTAS ID 	DATA 	CLIENTE 	EMAIL 	ENDERECO 	CIDADE 	UF 	PRODUTO_ID 	DESCRICAO 	UNID. 	QUANTIDADE 	VALOR
   1	12/11/2016	Elendur 	elendur@hotmail.com, elendur12r@gmail.com 	Rua das Flores	LAGO	VL 	1	Espada de fogo	P	1	200,00
   1	02/04/2017	Elendur 	elendur@hotmail.com, elendur12r@gmail.com 	Rua das Flores	LAGO	VL 	2	Escudo de Carvalho	P	1	180,00
   3	10/10/2017	Durin II 	durinii@yahoo.com.br 	Caverna de Orgrimar	Floresta Negra	GO 	8	Cajado de Gelo	P	1	1.200,00
   3	30/11/2017	Eldacar 	el65@gmail.com, jhon65@gmail.com 	Caverna de Orgrimar	Floresta Negra	GO 	12	Cajado de Fogo do Vulcão	P	1	1.300,00
   Segunda forma normal (2FN).

   A segunda forma normal assegura que não exista dependência funcional parcial no modelo de dados. Para aplicarmos a segunda forma normal em um modelo de dados devemos observar se alguma entidade do modelo possui chave primária concatenada e verificar se existe algum atributo ou conjunto de atributos com dependência parcial em relação a algum atributo da chave primária concatenada. Exemplo: A entidade PRODUTO_NOTA apresenta uma chave primária concatenada e por observação, notamos que os atributos QUANTIDADE e VALOR_VENDA dependem de forma parcial do atributo PRODUTO_ID, que faz parte da chave primária.
   Terceira forma normal (3FN).

   A terceira forma normal assegura que nenhuma entidade do modelo de dados possui atributos com dependência transitiva. Assim, uma entidade está na 3FN se nenhum de seus atributos possui dependência transitiva em relação a outro atributo da entidade que não participe da chave primária, ou seja, não existe nenhum atributo intermediário entre a chave primária e o próprio atributo observado. Ao retirarmos a dependência funcional transitiva, devemos criar uma nova entidade que contenha os atributos que dependem transitivamente de outro e a sua chave primária é o atributo que causou esta dependência. Também não devem conter atributos derivados, como por exemplo VALOR TOTAL.
   Forma Normal de Boyce/Codd.

   A forma normal Boyce/Codd foi desenvolvida com o objetivo de resolver algumas situações que não eram inicialmente cobertas pelas três formas normais, em especial quando haviam várias chaves na entidade, formadas por mais de um atributo (chaves compostas) e que ainda compartilham ao menos um atributo. Isso nos leva a concluir que, o problema se devia ao fato de até agora as formas normais tratarem de atributos dependentes de chaves primárias. Assim, para estar na FNBC, uma entidade precisa possuir somente atributos que são chaves candidatas. Vamos analisar o caso em que temos uma entidade formada pelos seguintes atributos:
   TURMA_CURSO ALUNO_ID 	TURMA 	CURSO_ID 	PROFESSOR_ID
   0012015	0101	SIS-01	0072003
   0022015	8901	DIR-01	4592005
   0032015	9001	PSI-01	0072003

   Um mesmo professor pode ministrar aulas entre cursos e turmas diferentes. Sendo assim podemos identificar três chaves candidatas que são determinantes nessa entidade: CURSO_ID+TURMA, CURSO_ID+PROFESSOR_ID e TURMA+PROFESSOR_ID. O atributo PROFESSOR_ID é parcialmente dependente do CURSO_ID e de TURMA, mas é totalmente dependente da chave candidata composta CURSO_ID+TURMA. Dessa forma a entidade deve ser desmembrada, resultando em duas: uma que contém os atributos que descrevem o aluno em si e outra cujos atributos designam um professor.
   TURMA_ALUNO TURMA 	CURSO_ID 	ALUNO_ID
   0101	SIS-01	0012015
   8901	DIR-01	0022015
   9001	PSI-01	0032015
   TURMA_PROFESSOR TURMA 	CURSO_ID 	PROFESSOR_ID
   0101	SIS-01	0072003
   8901	DIR-01	4592005
   9001	PSI-01	0072003
   Quarta Forma Normal (4FN).

   Uma tabela está na 4FN, se e somente se, estiver na 3FN e não existirem dependências multivaloradas.



## Referências
- [Tolkien Gataway](http://tolkiengateway.net/wiki/Bree)
