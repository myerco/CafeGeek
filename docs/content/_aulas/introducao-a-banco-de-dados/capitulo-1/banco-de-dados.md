---
title: BANCO DE DADOS
excerpt: "**BANCO DE DADOS I** Marco Yerco Mendizabel Cabrera Analista de Sistemas"
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2024-03-01T08:48:05-04:00
order: 7
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

{% include imagelocal.html
    src="introducao-a-banco-de-dados/banco-de-dados.png"
    alt="Figura: Mapa mental do Banco de dados."
    caption="Figura: Mapa mental do Banco de dados."
%}

## Objetivos

- Entender o conceito de banco de dados e seus usos.
- Diferenciar bancos de dados de coleções de arquivos.
- Conhecer operações básicas (CRUD) e seu mapeamento em SQL.
- Identificar limitações do armazenamento em arquivos e vantagens dos SGBD.

## O que é um banco de dados?

Um banco de dados é uma coleção organizada de informações que pode ser armazenada, consultada e manipulada de forma eficiente. Ao contrário de arquivos soltos (planilhas ou documentos), um banco de dados oferece estruturas e regras que facilitam a recuperação, a integridade e o compartilhamento dos dados.

## Operações básicas (CRUD)

As operações mais comuns sobre dados formam o acrônimo CRUD:

- Create (Criar): adicionar novos registros.
- Read (Ler): recuperar informações por meio de consultas.
- Update (Atualizar): modificar registros existentes.
- Delete (Excluir): remover registros.

Exemplo em SQL — recuperar nomes e e‑mails de usuários ativos:

```sql
SELECT nome, email
FROM usuarios
WHERE ativo = TRUE;
```

## Tabelas, registros e campos

No modelo relacional, os dados são organizados em tabelas. Cada tabela representa uma entidade (por exemplo, `clientes`) e é formada por linhas (registros ou tuplas) e colunas (campos ou atributos).

Exemplo simplificado de uma tabela `clientes`:

| id | nome              | cpf           | idade |
|----|-------------------|---------------|-------|
| 1  | João Saldanha     | 055.467.956-98| 34    |
| 2  | Ana da Silva      | 123.456.789-00| 22    |

## Por que não usar apenas arquivos?

Antes dos SGBD, informações eram armazenadas em arquivos separados (planilhas, textos, DBFs). Esse modelo apresenta várias limitações:

- Inconsistência e redundância: dados iguais podem existir em vários locais, levando a divergências.
- Dificuldade de integração: relacionar informações entre arquivos exige código ad hoc.
- Isolamento de dados: formatos diferentes dificultam a criação de novas aplicações.
- Problemas de integridade: falta de regras que garantam a validade dos dados.

## O que os SGBD resolvem

Sistemas Gerenciadores de Banco de Dados (SGBD) fornecem mecanismos para:

- Garantir integridade (por meio de restrições e chaves).
- Controlar concorrência e isolamento entre usuários.
- Assegurar atomicidade e recuperação em caso de falhas (transações).
- Aplicar políticas de segurança e permissões de acesso.

Esses recursos tornam os bancos de dados adequados para aplicações críticas e ambientes multiusuário.

## Tipos de Bancos de Dados

Os bancos de dados podem ser classificados de acordo com sua estrutura e finalidade. Os principais tipos são:

| Tipo           | Estrutura Principal         | Exemplos de Uso                |
|----------------|----------------------------|--------------------------------|
| Textual        | Arquivos de texto, documentos| Armazenamento simples, logs    |
| Grafos         | Nós e arestas (relacionamentos)| Redes sociais, mapas, recomendação|
| Relacional     | Tabelas, linhas e colunas   | Sistemas empresariais, ERP     |
| NoSQL          | Documentos, chave-valor, colunas, grafos| Big Data, aplicações web escaláveis |

### Estrutura de Cada Tipo

**Textual:**
Armazena dados em arquivos de texto ou documentos, sem estrutura rígida. Exemplo: arquivos CSV, TXT.

**Grafos:**
Organiza dados em nós (entidades) e arestas (relações). Ideal para dados altamente conectados.

**Relacional:**
Utiliza tabelas com linhas (registros) e colunas (atributos). Permite relacionamentos entre tabelas por meio de chaves.

**NoSQL:**
Inclui diversos modelos: documentos (JSON, BSON), chave-valor, colunar e grafos. Flexível para dados não estruturados ou semi-estruturados.

### Qual tipo é mais usado?

O modelo **relacional** é o mais utilizado em ambientes corporativos devido à sua robustez, padronização (SQL) e facilidade de integração. No entanto, bancos NoSQL têm ganhado espaço em aplicações que exigem alta escalabilidade e flexibilidade.

## Exemplos de Produtos de Banco de Dados

| Produto         | Tipo         | Características Principais         |
|-----------------|-------------|-----------------------------------|
| Oracle          | Relacional   | Alta performance, segurança, escalabilidade|
| MySQL           | Relacional   | Open source, amplamente utilizado |
| PostgreSQL      | Relacional   | Extensível, suporte avançado a dados|
| Microsoft SQL Server | Relacional | Integração com ambiente Windows   |
| MongoDB         | NoSQL (Documentos) | Flexível, escalável, JSON nativo |
| Cassandra       | NoSQL (Colunar)   | Alta disponibilidade, Big Data   |
| Neo4j           | Grafos       | Otimizado para relacionamentos complexos|
| Elasticsearch   | NoSQL (Documentos) | Busca textual, análise de dados  |
| Redis           | NoSQL (Chave-valor) | Rápido, usado para cache         |

Essas opções atendem diferentes necessidades, desde sistemas transacionais até análise de grandes volumes de dados.
