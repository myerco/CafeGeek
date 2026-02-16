---
title: gatilhos-triggers
excerpt: "Gatilhos (triggers): definição, requisitos, vantagens e sintaxe."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-2"
date: 2026-01-31T08:48:05-04:00
order: 6
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

## Gatilhos (Triggers)

Um gatilho é um comando executado automaticamente pelo sistema como consequência de uma modificação (INSERT, UPDATE ou DELETE) no banco de dados.

- **Requisitos:** Deve-se especificar as condições de execução e as ações a serem tomadas.
- **Vantagens:** Prevenção de transações inválidas, auditoria sofisticada, sincronismo de tabelas replicadas e geração de colunas derivadas.
- **Sintaxe:** Define-se o momento (`BEFORE` ou `AFTER`), o comando e se a execução é para cada linha (`FOR EACH ROW`).

## Caraterísticas

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
ON empregado
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

No PostgreSQL, triggers são implementados com uma função procedural e a declaração do gatilho:

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

-- Trigger associada à tabela empregado
CREATE TRIGGER verifica_salario
BEFORE INSERT OR UPDATE OR DELETE ON empregado
FOR EACH ROW EXECUTE FUNCTION verifica_salario();
```

```sql
INSERT INTO empregado
VALUES (1, 'Sarah Freitas', 10000, 2);
-- Se o comando é executado em horário não previsto na trigger, exemplo 07h, a inserção não é realizada
```
