---
title: Gatilhos e Funções (Triggers/Functions)
excerpt: "Gatilhos (triggers): definição, requisitos, vantagens e sintaxe."
categories:
  - "banco-de-dados"
  - "estruturas"
date: 2026-01-31T08:48:05-04:00
order: 6
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

Um gatilho é um comando executado automaticamente pelo sistema como consequência de uma modificação (INSERT, UPDATE ou DELETE) no banco de dados.

- **Requisitos:** Deve-se especificar as condições de execução e as ações a serem tomadas.
- **Vantagens:** Prevenção de transações inválidas, auditoria sofisticada, sincronismo de tabelas replicadas e geração de colunas derivadas.
- **Sintaxe:** Define-se o momento (`BEFORE` ou `AFTER`), o comando e se a execução é para cada linha (`FOR EACH ROW`).
- Triggers são silimares a stored procedures,  a Trigger pode incluir comandos SQL.
- São executados implicitamente quando são executados os comandos:
  - INSERT;
  - UPDATE;
  - DELETE.
- Estão associadas a tabelas.
- Tem três partes básicas:
  - Comando;
  - Restrição;
  - Ação.

<div class="mermaid">
graph TD
    A[Aplicação/Usuário] -->|Executa SQL: INSERT, UPDATE, DELETE| B{Evento de Tabela}
    B -->|Trigger disparada| C[Verifica Momento: BEFORE / AFTER / INSTEAD OF]

    subgraph Lógica no Postgres
    C --> D[Chamada da Trigger Function]
    D --> E[[Código PL/pgSQL: Validação, Logs, Cálculos]]
    E --> F{Resultado da Lógica}
    end
    
    F -->|Sucesso| G[Confirma Operação no Disco - Commit]
    F -->|Erro/Raise Exception| H[Aborta Operação - Rollback]
    
    G --> I[Retorno para o Usuário]
    H --> I
</div>

## Vantagens

- Previne transações inválidas:
  - Exemplo: inserir um valor não válido ou não realizar a operação por causa de uma instrução não completada.
- Prove sofisticada auditoria:
  - Exemplo:  pode ser associado um comando de auditoria registrando a operação.
- Mantém sincronismo em tabelas replicadas:
  - Exemplo: pode ser associado um comando para gravar dados da operação em outra tabela.
- Automaticamente gera colunas de valores derivados:
  - Exemplo: podemos computar e armazenar valores por outras tabelas.

## Sintaxe Oracle

```sql
CREATE TRIGGER verifica_salario 
BEFORE delete OR insert OR update
ON atendentes
FOR EACH ROW
BEGIN
    IF(TO_CHAR(SYSDATE, 'DY') = 'SAT' OR TO_CHAR(SYSDATE, 'DY') = 'SUN') THEN  
        raise_application_error( -20501,'Desculpe vai cuidar da sua vida, não trabalhe no fds');
    END IF;
    IF (TO_CHAR(SYSDATE, 'HH24') < 8 OR TO_CHAR(SYSDATE, 'HH24') >=18) THEN 
        raise_application_error(-20502,'Horário não permitido, desculpe e vá dormir');
    END IF;
END;
```

---

## Sintaxe PostgreSQL

No PostgreSQL, triggers são implementados com uma função procedural e a declaração do gatilho.

```sql
CREATE OR REPLACE FUNCTION nome_da_funcao()
RETURNS TRIGGER AS $$
BEGIN
    -- Lógica da trigger aqui
    -- NEW : Contém os novos dados (INSERT/UPDATE)
    -- OLD : Contém os dados antigos (UPDATE/DELETE)
    RETURN NEW; -- ou OLD, dependendo da trigger
END;
$$ LANGUAGE plpgsql;
```

- **BEFORE**: Executa antes de inserir/alterar o dado (bom para validar ou modificar dados antes de salvar).
- **AFTER**: Executa após a ação (bom para auditoria).
- **FOR EACH ROW**: A trigger roda para cada linha afetada pelo SQL.
- **FOR EACH STATEMENT**: A trigger roda uma vez por comando SQL, independente de quantas linhas foram afetadas.
- **NEW / OLD**: São variáveis especiais que permitem acessar os dados que estão sendo inseridos/atualizados (NEW) ou os dados anteriores (OLD).
- **TG_OP**: Variável que contém o nome da operação que disparou a trigger (INSERT, UPDATE, DELETE).

## Exemplos

**Observação:** Utilize a estrutura de tabelas da aula [Restrições de Integridade](https://cafegeek.eti.br/curso/banco-de-dados/modelo-de-dados/restricoes-de-integridade/)
{: .notice}

### Segurança

```sql
-- Função que será chamada pelo trigger
CREATE OR REPLACE FUNCTION verifica_salario() RETURNS trigger AS $$
BEGIN
  IF (EXTRACT(ISODOW FROM CURRENT_DATE) = 6 OR EXTRACT(ISODOW FROM CURRENT_DATE) = 7) THEN
    RAISE EXCEPTION 'Desculpe vai cuidar da sua vida, não trabalhe no fds';
  END IF;
  IF (EXTRACT(HOUR FROM CURRENT_TIME) < 8 OR EXTRACT(HOUR FROM CURRENT_TIME) >= 18) THEN
    RAISE EXCEPTION 'Horário não permitido, desculpe e vá dormir';
  END IF;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Trigger associada à tabela atendendes
CREATE TRIGGER verifica_salario
BEFORE INSERT OR UPDATE OR DELETE ON atendentes
FOR EACH ROW EXECUTE FUNCTION verifica_salario();
```

```sql
-- Inserindo um novo atendente da tabela pessoa
INSERT INTO atendentes
VALUES (1, 1, 10000);
-- Se o comando é executado em horário não previsto na trigger, exemplo 07h, a inserção não é realizada
```

Para implementando uma restrição por usuário vamos realizar o seguinte:

- Adicionando o atributo login na tabela de pessoas do tipo booleano
- O campo deve sinalizar quais pessoas podem ou não acessar o sistema
- O valor verdadeiro permite acesso

```sql
ALTER TABLE public.pessoas 
ADD COLUMN login BOOLEAN DEFAULT FALSE;
```

- **CURRENT_USER**: Função para determinar qual usuário conectou no banco de dados.

```sql
CREATE OR REPLACE FUNCTION check_permissao_atendente()
RETURNS TRIGGER AS $$
BEGIN
    -- Verifica se a pessoa existe, tem login ativo e se o e-mail bate com o usuário atual
    IF NOT EXISTS (
        SELECT 1 
        FROM public.pessoas 
        WHERE 
          login = TRUE 
          AND email = CURRENT_USER
    ) THEN
        RAISE EXCEPTION 'Ação bloqueada: O usuário atual não possui permissão de login ou não corresponde ao registro de pessoa informado.';
    END IF;

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER tg_valida_atendente_login
BEFORE INSERT ON public.atendentes
FOR EACH ROW
EXECUTE FUNCTION check_permissao_atendente();

```

### Auditoria

Criando a tabela de log de sistema


```sql
CREATE TABLE IF NOT EXISTS log_sistema (
    id_log SERIAL PRIMARY KEY,
    tabela_afetada VARCHAR(50) DEFAULT 'PESSOAS',
    operacao VARCHAR(20) DEFAULT 'INSERT',
    id_registro BIGINT,
    usuario_db VARCHAR(50) DEFAULT CURRENT_USER,
    data_log DATE DEFAULT CURRENT_DATE, -- Alterado de Timestamp para Date como solicitado
    detalhes TEXT
);
```

```sql
-- Função que será chamada pelo trigger
CREATE OR REPLACE FUNCTION FN_AUDITORIA_ATENDENTES() RETURNS TRIGGER AS $$
BEGIN
    IF (TG_OP = 'INSERT') THEN
        INSERT INTO LOG_SISTEMA (TABELA_AFETADA, OPERACAO, ID_REGISTRO, DETALHES)
        VALUES ('ATENDENTES', 'INSERT', NEW.ID, 
                'Novo atendente inserido. Salário inicial: ' || NEW.SALARIO);
        RETURN NEW;

    ELSIF (TG_OP = 'UPDATE') THEN
        INSERT INTO LOG_SISTEMA (TABELA_AFETADA, OPERACAO, ID_REGISTRO, DETALHES)
        VALUES ('ATENDENTES', 'UPDATE', NEW.ID, 
                'Salário alterado de ' || OLD.SALARIO || ' para ' || NEW.SALARIO);
        RETURN NEW;

    ELSIF (TG_OP = 'DELETE') THEN
        INSERT INTO LOG_SISTEMA (TABELA_AFETADA, OPERACAO, ID_REGISTRO, DETALHES)
        VALUES ('ATENDENTES', 'DELETE', OLD.ID, 
                'Atendente removido. Último salário: ' || OLD.SALARIO);
        RETURN OLD;
    END IF;
    
    RETURN NULL;
END;
$$ LANGUAGE PLPGSQL;

-- Trigger associada à tabela atendendes
CREATE TRIGGER TRG_AUDITORIA_ATENDENTES
AFTER INSERT OR UPDATE OR DELETE ON ATENDENTES
FOR EACH ROW
EXECUTE FUNCTION FN_AUDITORIA_ATENDENTES();

-- Teste 1: Inserção
INSERT INTO ATENDENTES (ID, ID_PESSOA, SALARIO) VALUES (1, 10, 3000);

-- Teste 2: Atualização
UPDATE ATENDENTES SET SALARIO = 5000 WHERE ID = 1;

-- Teste 3: Deleção
DELETE FROM ATENDENTES WHERE ID = 1;

-- Verificar logs
SELECT * FROM LOG_SISTEMA WHERE TABELA_AFETADA = 'ATENDENTES';
```

Versão da trigger de auditoria salvando todos os dados da tabela

```sql
CREATE OR REPLACE FUNCTION FN_AUDITORIA_ATENDENTES_JSON()
RETURNS TRIGGER AS $$
BEGIN
    IF (TG_OP = 'INSERT') THEN
        INSERT INTO LOG_SISTEMA (TABELA_AFETADA, OPERACAO, ID_REGISTRO, DETALHES)
        VALUES ('ATENDENTES', 'INSERT', NEW.ID, 
                jsonb_build_object('novo_registro', to_jsonb(NEW))::TEXT);
        RETURN NEW;

    ELSIF (TG_OP = 'UPDATE') THEN
        INSERT INTO LOG_SISTEMA (TABELA_AFETADA, OPERACAO, ID_REGISTRO, DETALHES)
        VALUES ('ATENDENTES', 'UPDATE', NEW.ID, 
                jsonb_build_object(
                    'antes', to_jsonb(OLD), 
                    'depois', to_jsonb(NEW)
                )::TEXT);
        RETURN NEW;

    ELSIF (TG_OP = 'DELETE') THEN
        INSERT INTO LOG_SISTEMA (TABELA_AFETADA, OPERACAO, ID_REGISTRO, DETALHES)
        VALUES ('ATENDENTES', 'DELETE', OLD.ID, 
                jsonb_build_object('registro_removido', to_jsonb(OLD))::TEXT);
        RETURN OLD;
    END IF;
    
    RETURN NULL;
END;
$$ LANGUAGE PLPGSQL;

-- Atualizando a associação da trigger

DROP TRIGGER IF EXISTS TRG_AUDITORIA_ATENDENTES ON ATENDENTES;

CREATE TRIGGER TRG_AUDITORIA_ATENDENTES
AFTER INSERT OR UPDATE OR DELETE ON ATENDENTES
FOR EACH ROW
EXECUTE FUNCTION FN_AUDITORIA_ATENDENTES_JSON();
```

### Replicação de dados

Considerando a aula de [Visões e Restrições de Acesso](https://cafegeek.eti.br/curso/banco-de-dados/estruturas/visoes-e-restricoes-de-acesso/), podemos implementar a tabela `atendentes_replicados` em um esquema separado para aumentar a segurança.

```sql
CREATE OR REPLACE TABLE CONSULTA.ATENDENTES_REPLICADOS AS
SELECT * FROM ATENDENTES;

CREATE OR REPLACE FUNCTION FN_REPLICA_ATENDENTES()
RETURNS TRIGGER AS $$
BEGIN
    IF (TG_OP = 'INSERT') THEN    
      INSERT INTO ATENDENTES_REPLICADOS (ID, ID_PESSOA, SALARIO)
      VALUES (NEW.ID, NEW.ID_PESSOA, NEW.SALARIO);
      RETURN NEW;

    ELSIF (TG_OP = 'UPDATE') THEN
      UPDATE ATENDENTES_REPLICADOS SET SALARIO = NEW.SAL   
      SET SALARIO = NEW.SALARIO,
          ID_PESSOA = NEW.ID_PESSOA
      WHERE ID = NEW.ID;
    RETURN NEW;

    ELSIF (TG_OP = 'DELETE') THEN
      DELETE FROM ATENDENTES_REPLICADOS WHERE ID = OLD.ID;
      RETURN OLD;
    END IF;
    
    RETURN NULL;
END;
$$ LANGUAGE PLPGSQL

CREATE TRIGGER TRG_AUDITORIA_ATENDENTES
AFTER INSERT OR UPDATE OR DELETE ON ATENDENTES
FOR EACH ROW
EXECUTE FUNCTION FN_REPLICA_ATENDENTES();
```

## Usando Cursores

Imagine que você faz uma consulta (SELECT) que retorna 10.000 linhas. Se você usar um comando SQL comum, o banco tentará processar ou te entregar todas essas linhas de uma vez só na memória.

O Cursor é um objeto de banco de dados que nos permite "apontar" para o resultado de uma consulta e percorrer linha por linha, de forma controlada.
Para que servem?

- Economia de Memória: Você não carrega o resultado inteiro de uma vez.

- Processamento Individual: Quando você precisa aplicar uma lógica complexa (um IF, um cálculo externo) em cada linha individualmente, o que seria impossível em um SELECT puro.

- Navegação: Permite avançar, retroceder ou pular registros dentro de um conjunto de dados.

### Exemplo Simples

```sql
DO $$
DECLARE
    -- 1. Declaração do cursor
    cur_emails CURSOR FOR SELECT email FROM public.pessoas WHERE login = TRUE;
    v_email text;
BEGIN
    -- 2. Abertura
    OPEN cur_emails;
    
    LOOP
        -- 3. Busca a linha atual e move para a próxima
        FETCH cur_emails INTO v_email;
        EXIT WHEN NOT FOUND; -- Sai do loop se não houver mais linhas
        
        RAISE NOTICE 'E-mail autorizado: %', v_email;
    END LOOP;
    
    -- 4. Fechamento
    CLOSE cur_emails;
END $$;
```

```sql
CREATE OR REPLACE FUNCTION check_atendente_com_for()
RETURNS TRIGGER AS $$
DECLARE
    -- Declaramos o cursor com parâmetros
    cur_validacao CURSOR  FOR 
        SELECT login, email 
        FROM public.pessoas;
        
    v_autorizado boolean := FALSE;

BEGIN
    -- O comando FOR gerencia o cursor automaticamente
    FOR reg IN cur_validacao LOOP
        -- Se entrar aqui, o registro existe. Agora validamos as regras:
        IF reg.login = TRUE AND reg.email = CURRENT_USER THEN
            v_autorizado := TRUE;
        END IF;
    END LOOP;

    -- Se após o loop a flag continuar falsa, barramos a inserção
    IF NOT v_autorizado THEN
        RAISE EXCEPTION 'Ação Não Permitida: Regras de login ou usuário inválidas.';
    END IF;

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
``` 