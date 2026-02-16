---
title: Programação de Banco de Dados
excerpt: "PL/SQL, procedures, functions e vantagens da programação procedural."
categories:
  - "banco-de-dados"
  - "estruturas"
date: 2026-01-31T08:48:05-04:00
order: 5
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

- SGBD’s permitem a manipulação da informação no banco de dados usando um esquema de objetos procedural de unidades de programa. No ORACLE isso é feito através do PL/SQL.
- Procedures e Functions são exemplos do PL/SQL.
- Uma Procedure ou Function é um esquema de objetos que logicamente agrupam um conjunto de comandos SQL e outros comandos PL/SQL.
- São armazenados dentro do banco de dados.

<div class="mermaid">
sequenceDiagram
    participant C as Cliente (Aplicação/User)
    box "Servidor PostgreSQL" #f9f9f9
    participant S as Motor do Banco de Dados
    participant P as Stored Procedure (PL/pgSQL)
    participant D as Tabelas (Dados)
    end

    Note over C, D: Fluxo de Execução Cliente-Servidor

    C->>S: CALL nome_procedure(parametros)
    Note right of C: Envia apenas o comando de chamada

    S->>P: Invoca a lógica armazenada
    
    rect rgb(240, 240, 240)
        Note right of P: Processamento interno no Servidor
        P->>D: Executa Consultas (SELECT/INSERT/UPDATE)
        D-->>P: Retorna resultados intermediários
        P->>P: Aplica lógica de programação (IF, LOOP, etc)
    end

    P-->>S: Finaliza execução/Retorna valores
    S-->>C: Resposta final (Status ou Outliers)
    
    Note over C, S: Menor tráfego de rede: Lógica roda próxima ao dado
</div>

O Oracle utiliza a linguagem procedural **PL/SQL** para agrupar comandos SQL e lógica de programação.

- **Procedures e Functions:** São esquemas de objetos armazenados dentro do banco.
- **Vantagens:** Melhoria na segurança (restrição de operações), performance (redução de tráfego na rede), integridade e compartilhamento de memória.
- **Elementos:** Inclui variáveis, cursores, exceções e estruturas de controle como `IF...THEN`, `LOOP` e `FOR`.

## Vantagens

- Segurança – Podemos restringir operações de banco de dados para cada usuário através de procedures;
- Performance – Reduzem significativamente os custos da informação que trafega pela rede, comparada com um SQL executado individualmente;
- Alocação de memória – Somente uma cópia da procedure encontra-se na memória e esta é compartilhada;
- Integridade – Garantem a integridade e consistência das aplicações.

## PL/SQL ORACLE

- É uma linguagem procedural que provê a capacidade para definir e executar unidades de programa, como por exemplo:
  - Procedures;
  - Functions;
  - Packages.
- Podemos incluir dentro de procedures:
  - Variávies;
  - Cursors;
  - Exceptions.
- Comandos:
  - IF ... THEN;
  - ELSE;
  - END IF;

## Programação Procedural no PostgreSQL (PL/pgSQL)

O PostgreSQL utiliza a linguagem procedural **PL/pgSQL** para criar funções e procedures armazenadas no banco de dados, de forma semelhante ao Oracle.

- **Funções e Procedures:** Permitem lógica de programação, uso de variáveis, controle de fluxo e cursores.
- **Diferenças:**
  - No PostgreSQL, procedures e functions são criadas com sintaxe diferente e o uso de `LANGUAGE plpgsql`.
  - Funções sempre retornam um valor; procedures não retornam valor diretamente.
  - Não há packages como no Oracle.

### Sintaxe PostgreSQL

```sql
-- Função que insere um empregado
CREATE OR REPLACE FUNCTION inserir_empregado(p_nome VARCHAR, p_sal NUMERIC, p_id_dept INTEGER)
RETURNS VOID AS $$
BEGIN
  INSERT INTO empregado (nome, salario, id_dept)
  VALUES (p_nome, p_sal, p_id_dept);
END;
$$ LANGUAGE plpgsql;

-- Chamada da função
SELECT inserir_empregado('Frodo', 3000, 1);

-- Procedure (PostgreSQL 11+)
CREATE OR REPLACE PROCEDURE remover_departamento(p_id_dept INTEGER)
LANGUAGE plpgsql
AS $$
BEGIN
  DELETE FROM departamento WHERE id_dept = p_id_dept;
END;
$$;

-- Chamada da procedure
CALL remover_departamento(2);
```

### Recursos do PL/pgSQL

- Controle de fluxo: IF, CASE, LOOP, FOR, WHILE
- Manipulação de exceções: EXCEPTION
- Cursores para manipulação de conjuntos de dados

## Sintaxe Oracle

```sql
CREATE OR REPLACE PROCEDURE empregado
(pNome VARCHAR,  pSal NUMBER, pId_dept NUMBER)
AS
BEGIN
  INSERT INTO empregado 
  VALUES (semp.nextval, pNome,pSal,pId_dept);
END;
```

```sql
EXECUTE empregado(‘Sauron’,5000,2);
```

```sql
CREATE OR REPLACE FUNCTION (pNome VARCHAR,pSal NUMBER, pId_dept NUMBER) 
RETURN NUMBER 
AS 
vNovoID NUMBER(4);
BEGIN
  SELECT  semp.nextval INTO vNovoID FROM dual;
  INSERT INTO  emp
  VALUES (vNovoID, pNome,pSal,pId_dept);
  RETURN (new_empno);
END;
```

```sql
CREATE OR REPLACE FUNCTION  remove(pid_dept NUMBER) 
RETURN NUMBER
IS
 tot_empno NUMBER(4);
BEGIN
  DELETE FROM departamento  WHERE deptno = vdeptno;
  SELECT count(*) INTO tot_empno
  FROM empregado;   
  RETURN (tot_empno);
END;
```

