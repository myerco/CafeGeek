---
title: Normalização de Banco de Dados
excerpt: "Explore os conceitos fundamentais da normalização de bancos de dados: anomalias, 1FN e dependências funcionais."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 15
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Objetivos

- Compreender o conceito de normalização em bancos de dados.
- Identificar anomalias em tabelas não normalizadas.
- Aplicar a Primeira Forma Normal (1FN).
- Entender dependências funcionais: total, parcial e transitiva.

## O que é Normalização?

A normalização é um processo matemático formal introduzido por E. F. Codd em 1970. Consiste em decompor tabelas complexas em estruturas mais simples, eliminando anomalias de atualização e redundâncias desnecessárias.

**Objetivo principal:** Criar esquemas relacionais "puros" que evitem problemas como:

- Grupos repetitivos de dados
- Dependências parciais em chaves concatenadas
- Redundância desnecessária
- Perda acidental de informação
- Dificuldade na representação da realidade

## Anomalias em Tabelas Não Normalizadas

### Tabela de pedidos

| Nº Pedido | Entrega | Cliente | Endereço       | Cidade | UF  | Cod. Prod. | Unid. Prod. | Qtd. Prod. | Descrição Prod. | Valor Unit Prod |
| --------- | ------- | ------- | -------------- | ------ | --- | ---------- | ----------- | ---------- | --------------- | --------------- |
| 001       | 05/12   | JOÃO    | RUA DAS FLORES | JARÚ   | RO  | 001        | P           | 10         | MOUSE           | 200             |
| 001       | 05/12   | JOÃO    | RUA DAS FLORES | JARÚ   | RO  | 002        | P           | 15         | TECLADO         | 500             |
| 002       | 10/12   | ANA     | RUA X          | JIPA   | RO  | 005        | P           | 100        | MODEM           | 5000            |

Quando uma tabela não está adequadamente estruturada, podem ocorrer três tipos principais de anomalias:

### Anomalia de Inclusão

Não é possível incluir um novo registro sem que ele esteja relacionado a outro dado existente.

**Exemplo:** Não se pode cadastrar um cliente que ainda não fez compras.

### Anomalia de Exclusão

Ao excluir um registro, informações importantes podem ser perdidas.

**Exemplo:** Excluir um cliente remove também o histórico de suas compras.

### Anomalia de Alteração

Alterações em um campo podem exigir múltiplas modificações na mesma tabela.

**Exemplo:** Alterar o preço de um produto requer atualizar todas as vendas desse produto.

## Formas Normais

A normalização é aplicada através de uma série de regras chamadas Formas Normais:

1. **Primeira Forma Normal (1FN)**
2. **Segunda Forma Normal (2FN)**
3. **Terceira Forma Normal (3FN)**
4. **Forma Normal de Boyce-Codd (FNBC)**
5. **Quarta Forma Normal (4FN)**
6. **Quinta Forma Normal (5FN)**

## Primeira Forma Normal (1FN)

A 1FN estabelece que **cada atributo deve conter apenas valores atômicos** (indivisíveis), não permitindo grupos repetitivos.

**Regra:** Uma tabela está na 1FN se todos os seus atributos contêm apenas valores simples, sem listas ou estruturas complexas.

### Aplicando 1FN - Exemplo Prático

Considere uma tabela PEDIDO com itens repetitivos:

**Tabela original (não normalizada):**

| Nº Pedido | Cliente | Produto1 | Qtd1 | Produto2 | Qtd2 |
| --------- | ------- | -------- | ---- | -------- | ---- |
| 001       | João    | Caneta   | 2    | Lápis    | 1    |

**Após 1FN - Duas tabelas:**
**PEDIDO:**

| Nº Pedido | Cliente | Endereço               | Cidade      | UF  |
| --------- | ------- | ---------------------- | ----------- | --- |
| 001       | João    | Av. 7 de Setembro, 456 | Porto Velho | RO  |
| 002       | Maria   | Av. Rio Madeira, 9812  | Porto Velho | RO  |

**ITEM_PEDIDO:**

| Nº Pedido | Produto | Quantidade | Valor Unit. Prod |
| --------- | ------- | ---------- | ---------------- |
| 001       | Caneta  | 2          | 5,00             |
| 001       | Lápis   | 1          | 1,00             |

## Dependência Funcional

Uma dependência funcional existe quando um atributo (ou conjunto de atributos) determina unicamente o valor de outro atributo.

**Notação:** A → B (A determina B)

**Exemplo:** Em uma tabela ALUNO:

- Matrícula → Nome (cada matrícula tem um único nome)
- Matrícula → Curso (cada matrícula tem um único curso)

### Dependência Funcional Total vs Parcial

Em chaves primárias compostas, analisamos se a dependência é da chave completa ou de parte dela.

**Dependência Total:** O atributo depende de TODOS os campos da chave composta.

**Dependência Parcial:** O atributo depende apenas de PARTE da chave composta.

**Exemplo - Tabela ITEM_VENDA (Nº_Venda + Cod_Produto):**

- Quantidade depende TOTALMENTE de (Nº_Venda + Cod_Produto)
- Nome_Produto depende PARCIALMENTE apenas de Cod_Produto

### Dependência Funcional Transitiva

Ocorre quando um atributo não-chave determina outro atributo não-chave.

**Notação:** A → B → C (C depende transitivamente de A através de B)

**Exemplo:** Em uma tabela FUNCIONARIO:

- CPF → Departamento
- Departamento → Localização

Portanto: CPF → Localização (dependência transitiva)

## Benefícios da Normalização

- **Redução de redundância:** Dados armazenados uma única vez
- **Eliminação de anomalias:** Atualizações consistentes
- **Manutenção da integridade:** Relacionamentos bem definidos
- **Flexibilidade:** Facilita alterações futuras no esquema

A normalização é fundamental para criar bancos de dados robustos e eficientes.

## Segunda Forma Normal (2FN)

A 2FN elimina **dependências funcionais parciais** em chaves primárias compostas. Uma tabela está na 2FN se:

1. Está na 1FN
2. Todos os atributos não-chave dependem **totalmente** da chave primária (não de parte dela)

### Aplicando 2FN - Exemplo Prático

Considere a tabela ITEM_PEDIDO com chave composta (Nº_Pedido, Cod_Produto):

**Tabela original (1FN mas não 2FN):**

| Nº_Pedido | Cod_Produto | Qtd | Descrição | Valor_Unit |
| --------- | ----------- | --- | --------- | ---------- |
| 001       | 1001        | 2   | Caneta    | 1.50       |
| 001       | 1002        | 1   | Lápis     | 1.00       |

**Problema:** Descrição e Valor_Unit dependem apenas de Cod_Produto (dependência parcial).

**Após 2FN - Três tabelas:**
**PEDIDO:**

| Nº_Pedido | Data  | Cliente |
| --------- | ----- | ------- |
| 001       | 15/01 | João    |

**ITEM_PEDIDO:**

| Nº_Pedido | Cod_Produto | Quantidade |
| --------- | ----------- | ---------- |
| 001       | 1001        | 2          |
| 001       | 1002        | 1          |

**PRODUTO:**

| Cod_Produto | Descrição | Valor_Unit |
| ----------- | --------- | ---------- |
| 1001        | Caneta    | 1.50       |
| 1002        | Lápis     | 1.00       |

## Terceira Forma Normal (3FN)

A 3FN elimina **dependências funcionais transitivas**. Uma tabela está na 3FN se:

1. Está na 2FN
2. Nenhum atributo não-chave depende de outro atributo não-chave

### Aplicando 3FN - Exemplo Prático

Considere a tabela PEDIDO com dependência transitiva:

**Tabela original (2FN mas não 3FN):**

| Nº_Pedido | Cliente | Endereço | Cidade    | UF  |
| --------- | ------- | -------- | --------- | --- |
| 001       | João    | Rua A    | São Paulo | SP  |

**Problema:** Endereço, Cidade, UF dependem de Cliente (não da chave).

**Após 3FN - Duas tabelas:**
**PEDIDO:**

| Nº_Pedido | Cliente | Data_Entrega |
| --------- | ------- | ------------ |
| 001       | João    | 20/01        |

**CLIENTE:**

| Cliente | Endereço | Cidade    | UF  |
| ------- | -------- | --------- | --- |
| João    | Rua A    | São Paulo | SP  |

## Forma Normal de Boyce-Codd (FNBC)

A FNBC trata casos especiais onde existem múltiplas chaves candidatas que se sobrepõem. Uma tabela está na FNBC se todo determinante for uma chave candidata.

### Exemplo FNBC

Considere uma tabela TURMA_PROFESSOR com três chaves candidatas sobrepostas:

**Chaves candidatas:**

1. (Cod_Curso, Turma)
2. (Cod_Curso, Matricula_Professor)
3. (Turma, Matricula_Professor)

**Tabela original:**

| Cod_Curso | Turma | Matricula_Professor | Nome_Professor |
| --------- | ----- | ------------------- | -------------- |
| BD001     | A     | P001                | Maria Silva    |

**Problema:** Matricula_Professor determina Nome_Professor, mas não é chave candidata.

**Após FNBC - Duas tabelas:**
**TURMA:**

| Cod_Curso | Turma | Matricula_Professor |
| --------- | ----- | ------------------- |
| BD001     | A     | P001                |

**PROFESSOR:**

| Matricula_Professor | Nome_Professor |
| ------------------- | -------------- |
| P001                | Maria Silva    |

## Quarta Forma Normal (4FN)

A 4FN trata **dependências multivaloradas independentes**. Uma tabela está na 4FN se não existirem duas ou mais dependências multivaloradas independentes.

### Exemplo 4FN

Uma dependência multivalorada ocorre quando um atributo determina múltiplos valores independentes de outro atributo.

**Exemplo:** Um cliente pode ter múltiplos telefones E múltiplos endereços de entrega, independentemente.

## Quinta Forma Normal (5FN)

A 5FN trata **dependências de junção** em relacionamentos complexos (ternários ou superiores). Uma tabela está na 5FN se não puder ser decomposta sem perda de informação.

### Quando Aplicar 5FN

Casos raros envolvendo relacionamentos múltiplos onde a decomposição em tabelas menores resultaria em perda de informações originais.

**Exemplo:** Em um sistema de projetos, onde funcionários trabalham em projetos usando ferramentas específicas, pode haver dependências complexas que exigem análise cuidadosa.

## Benefícios das Formas Normais Avançadas

- **Eliminação completa de anomalias:** 2FN e 3FN resolvem problemas restantes da 1FN
- **Otimização de performance:** Estruturas mais eficientes para consultas
- **Manutenção simplificada:** Mudanças locais não afetam outras partes
- **Flexibilidade:** Adaptação fácil a novos requisitos

## Ordem Recomendada de Aplicação

1. **1FN** - Eliminar grupos repetitivos
2. **2FN** - Remover dependências parciais
3. **3FN** - Eliminar dependências transitivas
4. **FNBC** - Tratar chaves candidatas sobrepostas
5. **4FN** - Resolver dependências multivaloradas
6. **5FN** - Casos especiais de dependências de junção

A normalização avançada garante bancos de dados robustos e eficientes para aplicações complexas.
