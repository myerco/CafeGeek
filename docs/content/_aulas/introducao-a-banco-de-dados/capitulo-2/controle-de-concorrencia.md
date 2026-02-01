---
title: controle-de-concorrencia
excerpt: "Controle de concorrência, bloqueios e deadlock."
categories:
  - "introducao-a-banco-de-dados"
  - "capitulo-2"
date: 2026-01-31T08:48:05-04:00
order: 9
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

Vimos que uma propriedade fundamental da transação é o isolamento. Quando diversas transações são executadas de modo concorrente em um banco da dados, a propriedade do isolamento pode não ser preservada. É necessário que o sistema controle a interação entre as transações concorrentes. Este controle é alcançado por meio de uma larga fama de mecanismos chamados de controle de concorrência. **Abrahan Silberschatz**
{: .notice}

## Controle de Concorrência

Necessário para gerenciar a interação entre transações simultâneas e preservar o isolamento.

### Serialização

- Supomos que todas as transações são individualmente corretas;
- Dado qualquer conjunto de transações, qualquer execução serial dessas transações (isto é, qualquer execução dessas transações, uma de cada vez em qualquer ordem) preserva a integridade do banco de dados.

### Bloqueios

Um meio de garantir a serialização é obrigar que o acesso aos itens de dados seja feito de maneira mutuamente exclusiva. Isto é, enquanto uma transação acessa um item de dados nenhuma outra transação pode modificá-lo. O método mais usado para sua implementação é permitir acesso a um item de dados somente se ele estiver bloqueado.”Um meio de garantir a serialização é obrigar que o acesso aos itens de dados seja feito de maneira mutuamente exclusiva. Isto é, enquanto uma transação acessa um item de dados nenhuma outra transação pode modificá-lo. O método mais usado para sua implementação é permitir acesso a um item de dados somente se ele estiver bloqueado.”

## Mecanismos

- Bloqueios (Locks): podem ser Compartilhados (S), permitindo apenas leitura, ou Exclusivos (X), permitindo leitura e escrita.
- Deadlock: situação de espera mútua onde transações aguardam a liberação de bloqueios umas das outras.
- Protocolo de Bloqueio em Duas Fases: consiste na Fase de Expansão (obtenção de bloqueios) e Fase de Encolhimento (liberação de bloqueios).

## Matriz compatibilidade

|     | S          | X     |
| --- | ---------- | ----- |
| S   | VERDADEIRO | FALSO |
| X   | FALSO      | FALSO |

## Exempplo 1

Considere que A e B sejam 100 e 200

| T1          | T2             |
| ----------- | -------------- |
| Lock-x(b)   | Lock-s(a)      |
| Read(b)     | Read(a)        |
| b := b - 50 | Unlock(a)      |
| Write(b)    | Lock-s(b)      |
| Unlock(b)   | Read(b)        |
| Lock-x(a)   | Unlock(b)      |
| Read(a)     | Display(a + b) |
| a := a + 50 |                |
| Write(a)    |                |
| Unlock(a)   |                |

---

### Exemplo de bloqueios em PostgreSQL

```sql
-- Bloqueio exclusivo (X) para escrita
BEGIN;
SELECT * FROM contas WHERE id = 2 FOR UPDATE; -- T1 bloqueia linha para escrita
UPDATE contas SET saldo = saldo - 50 WHERE id = 2;
COMMIT;

-- Bloqueio compartilhado (S) para leitura
BEGIN;
SELECT * FROM contas WHERE id = 1 FOR SHARE; -- T2 bloqueia linha para leitura
SELECT saldo FROM contas WHERE id = 1;
COMMIT;
```

| Tempo | T1           | T2            | GERENCIADOR    |
| ----- | ------------ | ------------- | -------------- |
| 1     | Lock-x(b);   |               |                |
| 2     |              |               | Grant-X(b, T1) |
| 3     | Read(b);     |               |                |
| 4     | b := b - 50; |               |                |
| 5     | Write(b);    |               |                |
| 6     | Unlock(b);   |               |                |
| 7     |              | Lock-s(a);    |                |
| 8     |              |               | Grant-S(a, T2) |
| 9     |              | Read(a);      |                |
| 10    |              | Unlock(a);    |                |
| 11    |              | Lock-s(b);    |                |
| 12    |              |               | Grant-S(b, T2) |
| 13    |              | Read(b);      |                |
| 14    |              | Unlock(b);    |                |
| 15    |              | Display(a+b); |                |
| 16    | Lock-x(a);   |               |                |
| 17    |              |               | Grant-X(a, T1) |
| 18    | Read(a);     |               |                |
| 19    | a := a + 50; |               |                |
| 20    | Write(a);    |               |                |
| 21    | Unlock(a);   |               |                |

Considere as transações T3 e T4

| T3                   | T4                   |
|----------------------|----------------------|
| Lock-x(b);           | Lock-s(a);           |
| Read(b);             | Read(a);             |
| b := b - 50;         | Lock-s(b);           |
| Write(b);            | Read(b);             |
| Lock-x(a);           | Display(a + b);      |
| Read(a);             | Unlock(a);           |
| a := a + 50;         | Unlock(b);           |
| Write(a);            |                      |
| Unlock(b);           |                      |
| Unlock(a);           |                      |

## Deadlock

É uma situação em que duas transações ou mais transações estão em um estado simultâneo de espera, cada qual aguardando que uma das demais libere um bloqueio antes que ela possa prosseguir.É uma situação em que duas transações ou mais transações estão em um estado simultâneo de espera, cada qual aguardando que uma das demais libere um bloqueio antes que ela possa prosseguir.

---

### Exemplo de deadlock em PostgreSQL

```sql
-- T3
BEGIN;
SELECT * FROM contas WHERE id = 2 FOR UPDATE; -- bloqueia conta 2
-- T4
BEGIN;
SELECT * FROM contas WHERE id = 1 FOR UPDATE; -- bloqueia conta 1
-- T3 tenta bloquear conta 1
SELECT * FROM contas WHERE id = 1 FOR UPDATE; -- espera T4 liberar
-- T4 tenta bloquear conta 2
SELECT * FROM contas WHERE id = 2 FOR UPDATE; -- espera T3 liberar
-- Deadlock detectado pelo PostgreSQL, uma transação será abortada
```

| T3                | T4             | GERENCIADOR          |
|-------------------|----------------|----------------------|
| Lock-x(b);        |                | Grant-X(b, T3)       |
| Read(b);          |                |                      |
| b := b - 50;      |                |                      |
| Write(b);         |                |                      |
|                   | Lock-s(a);     | Grant-s(a, T4)       |
|                   | Read(a);       |                      |
|                   | Lock-s(b);     | Grant-s(b, T4)       |
| Lock-x(a);        |                | Deadlock             |

## Prevenção

- Bloqueio de todos os itens de dados antes da execução;
- Rollback e Timestamping.

## Bloqueio em duas fases

Um dos protocolos que garantem a serialização é o bloqueio em duas fases. Este protocolo exige que cada transação emita suas solicitações de bloqueio e desbloqueio em duas fases:

---

### Exemplo de bloqueio em duas fases no PostgreSQL

```sql
-- Fase de expansão: obtém todos os bloqueios
BEGIN;
SELECT * FROM contas WHERE id = 2 FOR UPDATE;
SELECT * FROM contas WHERE id = 1 FOR UPDATE;
-- Fase de encolhimento: libera todos os bloqueios ao final
UPDATE contas SET saldo = saldo - 50 WHERE id = 2;
UPDATE contas SET saldo = saldo + 50 WHERE id = 1;
COMMIT;
```

- Fase de expansão - Uma transação pode obter bloqueios, mas não pode liberar nenhum;
- Fase de encolhimento - Uma transação pode liberar bloqueios, mas não consegue obter nenhum bloqueio novo.

| T3                | T4                | GERENCIADOR    |
|-------------------|-------------------|----------------|
| Lock-x(b);        | Lock-s(a);        | Grant-X(b, T3) |
| Lock-x(a);        | Lock-x(b);        |                |
| Read(b);          |                   |                |
| b := b - 50;      |                   |                |
| Write(b);         |                   |                |
|                   |                   | Grant-s(a, T4) |
|                   |                   | Espera...      |
| Read(b);          | Read(a);          |                |
| Read(a);          | Read(b);          |                |
| b := b + a;       | Write(b);         |                |
| Write(b);         | Unlock(a);        |                |
| Unlock(b);        | Unlock(b);        |                |
|                   | Read(b);          |                |
|                   | b := a * b / 10;  |                |
|                   | Write(b);         |                |
|                   | Unlock(a);        |                |
|                   | Unlock(b);        |                |
