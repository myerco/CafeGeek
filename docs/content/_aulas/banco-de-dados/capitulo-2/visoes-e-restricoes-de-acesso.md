---
title: visoes-e-restricoes-de-acesso
excerpt: "Visões (views) e restrições de acesso em bancos de dados."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-2"
date: 2026-01-31T08:48:05-04:00
order: 4
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

No nível externo da arquitetura ANSI/SPARC, o banco de dados  é percebido como uma “visão externa”, definida por um esquema externo. Diversos usuários podem ter visões externas diversas. **C.J. Date**
{: .notice}

## Visões (Views) e Restrições de Acesso

Uma visão é considerada uma **tabela virtual**; ela não existe fisicamente, mas aparece ao usuário como uma tabela real.

### Características

- Uma visão pode ser considerada como uma tabela virtual. Isto é, uma tabela que não existe por si, mas que parece ao usuário como se assim fosse;
- A visão é operada como se fosse uma tabela real;
- É uma janela para um subconjunto de dados de uma tabela;
- Toda mudança na tabela é automaticamente e instantaneamente refletida através desta janela;
- Mostra Linhas pertinentes para os usuários.

Funciona como uma janela para um subconjunto de dados, refletindo automaticamente mudanças nas tabelas base.

### Sintaxe SQL

 ```sql
 CREATE VIEW nome_da_view AS subquery
 ```

- Exemplos mostram a criação de visões para filtrar funcionários com salários específicos e a execução de consultas normais sobre essas visões.

### Criando a VIEW bons_empregados

```sql
CREATE VIEW bons_empregados
AS
SELECT nome, sal
FROM empregado
WHERE sal > 10000;
```

### Executando a VIEW

```sql
SELECT * FROM bons_empregados;
SELECT * FROM bons_empregados ORDER BY  sal ;
SELECT nome FROM  bons_empregados WHERE nome = ‘ANA MARIA’;
```
