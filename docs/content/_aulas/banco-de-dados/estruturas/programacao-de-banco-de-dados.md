---
title: Procedimentos e Funções (stored Procedures/Functions)
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

- SGBD’s permitem a manipulação da informação no banco de dados usando um esquema de objetos procedural de unidades de programa. No ORACLE isso é feito através do PL/SQL
- Procedures e Functions são exemplos do PL/SQL
- Uma Procedure ou Function é um esquema de objetos que logicamente agrupam um conjunto de comandos SQL e outros comandos PL/SQL
- São armazenados dentro do banco de dados

<div class="mermaid">
sequenceDiagram
    participant C as Cliente (Aplicação/Usuário)
    box Servidor PostgreSQL #f9f9f9
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
        P-->>D: Executa Consultas (SELECT/INSERT/UPDATE)
        D-->>P: Retorna resultados intermediários
        P-->>P: Aplica lógica de programação (IF, LOOP, etc)
    end

    P-->>S: Finaliza execução/Retorna valores
    S-->>C: Resposta final (Status ou Outliers)
    
    Note over C, S: Menor tráfego de rede: Lógica roda próxima ao dado
</div>

## Características

- **Procedures e Functions:** São esquemas de objetos armazenados dentro do banco.
- **Elementos:** Inclui variáveis, cursores, exceções e estruturas de controle como `IF...THEN`, `LOOP` e `FOR`.

## Vantagens

- Segurança – Podemos restringir operações de banco de dados para cada usuário através de procedures;
- Performance – Reduzem significativamente os custos da informação que trafega pela rede, comparada com um SQL executado individualmente;
- Alocação de memória – Somente uma cópia da procedure encontra-se na memória e esta é compartilhada;
- Integridade – Garantem a integridade e consistência das aplicações.

## PL/SQL no ORACLE

O Oracle utiliza a Linguagem Procedural **PL/SQL** para agrupar comandos SQL e lógica de programação.

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

## PL/pgSQL no PostgreSQL

O PostgreSQL utiliza a linguagem procedural **PL/pgSQL** para criar funções e procedures armazenadas no banco de dados, de forma semelhante ao Oracle.

- **Funções e Procedures:** Permitem lógica de programação, uso de variáveis, controle de fluxo e cursores.
- **Diferenças:**
  - No PostgreSQL, procedures e functions são criadas com sintaxe diferente e o uso de `LANGUAGE plpgsql`.
  - Funções sempre retornam um valor; procedures não retornam valor diretamente.
  - Não há packages como no Oracle.

**Observação:** Utilize a estrutura de tabelas da aula [Restrições de Integridade](https://cafegeek.eti.br/curso/banco-de-dados/modelo-de-dados/restricoes-de-integridade/)
{: .notice}

### Sintaxe PostgreSQL

```sql
-- Função que insere uma pessoa 
CREATE OR REPLACE FUNCTION INSERIR_PESSOA (
  PID BIGINT,
  PNOME VARCHAR,
  PDATA_NASCIMENTO DATE,
  PID_SEXO INT,
  PEMAIL VARCHAR
) RETURNS VOID AS $$
BEGIN
  INSERT INTO PESSOAS (ID, NOME, DATA_NASCIMENTO, ID_SEXO, EMAIL) VALUES 
    (pid, pnome, pdata_nascimento, pid_sexo,pemail);

END;
$$ LANGUAGE PLPGSQL;

-- Chamada da função para inserir uma pessoa
SELECT
  INSERIR_PESSOA (
    12,
    'Frodo',
    '1987-03-01',
    1,
    'frodo.rei@gondor.com'
  );

-- Removendo pessoas
CREATE OR REPLACE PROCEDURE REMOVER_PESSOA (PID BIGINT) LANGUAGE PLPGSQL AS $$
BEGIN
  DELETE FROM pessoas WHERE id = pid;
END;
$$;

-- Chamada da procedure para remover uma pessoa
CALL REMOVER_PESSOA (12);
```

### Usando funções para controle de segurança e auditoria

```sql
CREATE OR REPLACE FUNCTION INSERIR_PESSOA (
    PID BIGINT, 
    PNOME VARCHAR, 
    PDATA_NASCIMENTO DATE, 
    PID_SEXO INT, 
    PEMAIL VARCHAR
) RETURNS VOID AS $$
DECLARE
    V_USUARIO_ATUAL VARCHAR := SESSION_USER; -- Captura o usuário logado
BEGIN
    -- 1. Validação de Segurança (Somente yerco@mail)
    IF V_USUARIO_ATUAL != 'yerco@mail' THEN
        RAISE EXCEPTION 'Acesso Negado: O usuário % não tem permissão para inserir registros.', V_USUARIO_ATUAL;
    END IF;

    -- 2. Inserção Principal
    INSERT INTO PESSOAS (ID, NOME, DATA_NASCIMENTO, ID_SEXO, EMAIL) 
    VALUES (PID, PNOME, PDATA_NASCIMENTO, PID_SEXO, PEMAIL);

    -- 3. Registro na Log de Auditoria
    INSERT INTO LOG_SISTEMA (ID_REGISTRO, DETALHES)
    VALUES (PID, 'Inserção realizada com sucesso por ' || V_USUARIO_ATUAL);

EXCEPTION
    WHEN OTHERS THEN
        -- Captura erros de PK duplicada ou outros problemas de banco
        RAISE EXCEPTION 'Falha na operação: %', SQLERRM;
END;
$$ LANGUAGE PLPGSQL;
```

### Usando procedures para dados estatísticos

```sql
-- Criação da tabela de estatísticas para armazenamento de dados agrupados
CREATE TABLE ESTATISTICAS_SISTEMA (
    ID_ESTATISTICA SERIAL PRIMARY KEY,
    DATA_COLETA TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- Quando o dado foi gerado
    
    -- Decomposição do Evento
    ANO INT NOT NULL,
    MES INT NOT NULL,
    DIA INT NOT NULL,
    TRIMESTRE INT NOT NULL,
    SEMESTRE INT NOT NULL,
    
    TIPO_EVENTO VARCHAR(100) NOT NULL, 
    -- Exemplos: 'Atendentes por ano e salário', 'Quantidade de Pessoas por idade'
    
    VALOR_EVENTO JSONB NOT NULL 
    -- Armazena o agrupamento (ex: {"salario_medio": 5000, "total": 10})
);

-- Procedure para calculdo dos dados estatísticos
CREATE OR REPLACE PROCEDURE GERAR_ESTATISTICAS_ATENDENTES()
LANGUAGE PLPGSQL AS $$
DECLARE
    V_DATA TIMESTAMP := CURRENT_TIMESTAMP;
    V_ANO INT := EXTRACT(YEAR FROM CURRENT_DATE);
    V_MES INT := EXTRACT(MONTH FROM CURRENT_DATE);
    V_DIA INT := EXTRACT(DAY FROM CURRENT_DATE);
    V_TRIMESTRE INT := EXTRACT(QUARTER FROM CURRENT_DATE);
    V_SEMESTRE INT := CASE WHEN EXTRACT(MONTH FROM CURRENT_DATE) <= 6 THEN 1 ELSE 2 END;
BEGIN
    -- 1. Estatística: Atendentes por Salário Médio
    INSERT INTO ESTATISTICAS_SISTEMA (DATA_COLETA, ANO, MES, DIA, TRIMESTRE, SEMESTRE, TIPO_EVENTO, VALOR_EVENTO)
    SELECT 
        V_DATA, V_ANO, V_MES, V_DIA, V_TRIMESTRE, V_SEMESTRE,
        'Atendentes por ano e salário',
        jsonb_build_object(
            'total_atendentes', COUNT(*),
            'media_salarial', ROUND(AVG(SALARIO), 2),
            'maior_salario', MAX(SALARIO)
        )
    FROM ATENDENTES;

    -- 2. Estatística: Quantidade de Pessoas por faixa etária
    INSERT INTO ESTATISTICAS_SISTEMA (DATA_COLETA, ANO, MES, DIA, TRIMESTRE, SEMESTRE, TIPO_EVENTO, VALOR_EVENTO)
    SELECT 
        V_DATA, V_ANO, V_MES, V_DIA, V_TRIMESTRE, V_SEMESTRE,
        'Quantidade de Pessoas por idade',
        jsonb_object_agg(faixa_etaria, total)
    FROM (
        SELECT 
            CASE 
                WHEN EXTRACT(YEAR FROM AGE(DATA_NASCIMENTO)) < 18 THEN 'Menor de 18'
                WHEN EXTRACT(YEAR FROM AGE(DATA_NASCIMENTO)) BETWEEN 18 AND 60 THEN 'Adulto'
                ELSE 'Idoso'
            END as faixa_etaria,
            COUNT(*) as total
        FROM PESSOAS
        GROUP BY 1
    ) subquery;

    COMMIT;
END;
$$;

-- Chamada da procedure para gerar estatísticas
CALL GERAR_ESTATISTICAS_ATENDENTES();

-- Implementando um visão para facilitar a visualização das estatísticas
CREATE OR REPLACE VIEW VW_ESTATISTICAS_DASHBOARD AS
SELECT 
    ID_ESTATISTICA,
    DATA_COLETA,
    -- Colunas de Tempo
    ANO,
    MES,
    DIA,
    TRIMESTRE,
    SEMESTRE,
    TIPO_EVENTO,
    
    -- Extração Dinâmica do JSON (Campos de Salário)
    (VALOR_EVENTO->>'total_atendentes')::INT AS QTD_ATENDENTES,
    (VALOR_EVENTO->>'media_salarial')::NUMERIC(10,2) AS MEDIA_SALARIAL,
    (VALOR_EVENTO->>'maior_salario')::NUMERIC(10,2) AS TETO_SALARIAL,
    
    -- Extração das Faixas Etárias (Campos de Pessoas)
    (VALOR_EVENTO->>'Menor de 18')::INT AS QTD_MENORES,
    (VALOR_EVENTO->>'Adulto')::INT AS QTD_ADULTOS,
    (VALOR_EVENTO->>'Idoso')::INT AS QTD_IDOSOS

FROM ESTATISTICAS_SISTEMA;

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
