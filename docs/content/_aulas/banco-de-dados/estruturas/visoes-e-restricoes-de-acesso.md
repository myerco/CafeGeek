---
title: Visões e restrições de acesso
excerpt: "Visões (views) e restrições de acesso em bancos de dados."
categories:
  - "banco-de-dados"
  - "estruturas"
date: 2026-01-31T08:48:05-04:00
order: 4
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

No nível externo da arquitetura ANSI/SPARC, o banco de dados  é percebido como uma “visão externa”, definida por um esquema externo. Diversos usuários podem ter visões externas diversas. **C.J. Date**
{: .notice}

Uma visão é considerada uma **tabela virtual**; ela não existe fisicamente, mas aparece ao usuário como uma tabela real.

<div class="mermaid">
graph TD
    subgraph Tabela_Base [Tabela Base: Funcionários]
        direction TB
        DB[(Banco de Dados)]

        %% Uso de aspas duplas para permitir o caractere pipe |
        T_Cols["ID | Nome | Salário | Departamento | Telefone"]
        T_Rows["Ana | 9.0000 | TI| (69) 96584-5475<br/>João | 9.500 | TI| (69) 8694-4758<br/>Maria |10000| RH| (69) 7845-4756<br/>Humberto | 9000|ADM| (69) 9869-5874"]
        
        DB --- T_Cols
        T_Cols --- T_Rows
    end

    Tabela_Base --> Processo{Definição da VIEW}

    subgraph Restricoes [Mecanismos de Filtro]
        direction LR
        V_Rest["<b>Restrição Vertical</b><br/>(Colunas Selecionadas)"]
        H_Rest["<b>Restrição Horizontal</b><br/>(Cláusula WHERE)"]
    end

    Processo --> V_Rest
    Processo --> H_Rest

    V_Rest --> View_Final
    H_Rest --> View_Final

    subgraph View_Virtual [Objeto: VIEW]
        View_Final[[Virtual: vw_ti_contatos]]
        V_Display["Nome | Departamento<br/>---<br/>Ana | TI<br/>João | TI"]
    end

    %% Estilização
    style Tabela_Base fill:#f9f9f9,stroke:#333,stroke-width:2px
    style View_Virtual fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style V_Rest fill:#fff9c4,stroke:#fbc02d
    style H_Rest fill:#fff9c4,stroke:#fbc02dgraph TD
    
</div>

## Características

- Uma visão pode ser considerada como uma tabela virtual. Isto é, uma tabela que não existe por si, mas que parece ao usuário como se assim fosse;
- A visão é operada como se fosse uma tabela real;
- É uma janela para um subconjunto de dados de uma tabela;
- Toda mudança na tabela é automaticamente e instantaneamente refletida através desta janela;
- Mostra Linhas pertinentes para os usuários.

Funciona como uma janela para um subconjunto de dados, refletindo automaticamente mudanças nas tabelas base.

## Sintaxe SQL

 ```sql
 CREATE VIEW nome_da_view AS subquery
 ```

- Exemplos mostram a criação de visões para filtrar funcionários com salários específicos e a execução de consultas normais sobre essas visões.

## Criando a VIEW bons_empregados

```sql
CREATE VIEW bons_empregados
AS
SELECT nome, sal
FROM empregado
WHERE sal > 10000;
```

## Executando a VIEW

```sql
SELECT * FROM bons_empregados;
SELECT * FROM bons_empregados ORDER BY  sal ;
SELECT nome FROM  bons_empregados WHERE nome = ‘ANA MARIA’;
```
