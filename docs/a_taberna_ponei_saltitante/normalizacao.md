---
title: Normalização
description: Aprenda modelos de Banco de dados relacionais
tags: [Banco de Dados, Oracle, Oracle SQLDeveloper, MER, modelo relacional,PostgreSQL]
layout: page
---


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
