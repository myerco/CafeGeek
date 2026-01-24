---
title: Abstração de Dados
excerpt: "Entenda os níveis de abstração em sistemas de banco de dados: físico, lógico e de visão, essenciais para o design e uso eficiente de dados."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-1"
date: 2026-01-22T08:48:05-04:00
order: 1
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

<div class="mermaid">
graph TD
    subgraph "Arquitetura de três níveis <br>- Independência de Dados"
        A["Nível de Visão<br/>(o que cada usuário vê)<br/>← visões do usuário"] 
        B["Nível Lógico<br/>(tabelas + relações)<br/>← modelo geral dos dados"] 
        C["Nível Físico<br/>(discos, blocos, índices)<br/>← como é guardado na máquina"]
        C -->|Independência Física| B
        B -->|Independência Lógica| A
    end
</div>

## Objetivos

- Compreender o conceito de abstração de dados em SGBD.
- Explorar os três níveis de abstração: físico, lógico e de visão.
- Entender como esses níveis facilitam o uso e gerenciamento de bancos de dados.

## Por que a Abstração é Importante?

Em sistemas de banco de dados, a abstração permite que usuários e desenvolvedores interajam com os dados sem precisar conhecer os detalhes técnicos internos. Isso simplifica o trabalho e aumenta a segurança, pois cada nível oculta complexidades desnecessárias.

Um Sistema Gerenciador de Banco de Dados (SGBD) oferece três níveis de abstração para organizar essa interação:

1. **Nível Físico**: Como os dados são armazenados fisicamente.
2. **Nível Lógico (ou Conceitual)**: Quais dados existem e suas relações.
3. **Nível de Visão**: O que cada usuário vê, personalizado e seguro.

## Nível Físico

Este é o nível mais baixo e técnico. Ele descreve exatamente como os dados são armazenados no hardware — em discos, memória ou outros dispositivos.

**Exemplo**: Imagine um registro de cliente armazenado em um bloco de 512 bytes no disco rígido. Detalhes como endereços de memória, tamanhos de blocos e algoritmos de compressão são tratados aqui. Usuários comuns não precisam se preocupar com isso; é responsabilidade dos administradores de sistema.

## Nível Lógico (Conceitual)

O nível intermediário define quais dados estão no banco e como se relacionam, sem entrar em detalhes físicos.

**Exemplo**: Usando uma analogia com programação, pense em uma classe `Cliente`:

```java
class Cliente {
    String nome;
    float salario;
    String cidade;
}
```

Aqui, descrevemos tabelas, índices, relacionamentos e restrições. É o nível usado por desenvolvedores para modelar o banco de dados.

## Nível de Visão

O nível mais alto oferece uma visão personalizada dos dados para cada usuário ou aplicação. Ele restringe o acesso, mostrando apenas o necessário.

### Exemplo 1: Visão para Funcionários do RH**

Um funcionário de vendas vê apenas dados de clientes e pedidos, enquanto um gerente acessa relatórios financeiros. Isso garante segurança e simplicidade — ninguém vê dados irrelevantes ou confidenciais.

```sql
-- Nível Lógico (tabelas reais)
CREATE TABLE funcionarios (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    salario DECIMAL(10,2),
    departamento VARCHAR(50),
    data_contratacao DATE,
    cpf VARCHAR(14) UNIQUE,
    endereco_privado TEXT
);

-- Nível de Visão: O que um analista do RH vê
CREATE VIEW visao_rh AS
SELECT 
    id,
    nome,
    departamento,
    data_contratacao,
    CASE 
        WHEN salario > 10000 THEN 'Faixa Alta'
        WHEN salario > 5000 THEN 'Faixa Média'
        ELSE 'Faixa Básica'
    END AS faixa_salarial,
    EXTRACT(YEAR FROM AGE(CURRENT_DATE, data_contratacao)) AS anos_empresa
FROM funcionarios
WHERE data_contratacao >= '2020-01-01';

-- O analista do RH usa apenas:
SELECT * FROM visao_rh WHERE departamento = 'TI';
```

```python
# No código do dashboard, o desenvolvedor só precisa:
import psycopg2

conn = psycopg2.connect("dbname=empresa user=gerente")
cur = conn.cursor()
cur.execute("SELECT * FROM visao_rh WHERE anos_empresa >= %s", ('10',))
# Não precisa saber como as 3 tabelas são unidas ou calculadas!
```

## Benefícios da Abstração

- **Simplicidade**: Usuários focam no que precisam, não em detalhes técnicos.
- **Segurança**: Controle de acesso por nível.
- **Flexibilidade**: Mudanças em um nível não afetam os outros diretamente.
- **Manutenibilidade**: Facilita atualizações e otimizações.

Em resumo, a abstração transforma bancos de dados complexos em ferramentas acessíveis e eficientes.
