---
title: Estruturas de Gerenciadores de Banco de Dados
excerpt: "Funções, estrutura e processamento dos SGBDs."
categories:
  - "banco-de-dados"
  - "estruturas"
date: 2026-01-31T08:48:05-04:00
order: 2
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

Um SGBD é um conjunto de dados associados a programas que permitem o acesso e a manipulação dessas informações.

## Funções

- Armazenar dados em disco de forma estruturada
- Fornecer mecanismos de criação/alteração de definições
- Manter a localização de cada elemento

## Estrutura e Processamento

<div class="mermaid">
flowchart TD
    subgraph SGBD
        DML["Compilador DML"]
        DDL["Interpretador DDL"]
        ARMAZENAMENTO["Gerenciamento de Armazenamento"]
        DADOS["Dados Físicos"]
    end
    DML -->|"Comandos de Manipulação"| ARMAZENAMENTO
    DDL -->|"Definição de Estruturas"| ARMAZENAMENTO
    ARMAZENAMENTO --> DADOS
    DADOS -->|"Metadados, índices, estatísticas"| ARMAZENAMENTO
</div>

## Arquitetura do Postgresql

{% include image.html
    src="https://docs.netapp.com/pt-br/ontap-apps-dbs/media/postgresql-architecture.png"
    alt="Figura: Arquitetura Postgresql."
    caption="Figura: Arquitetura Postgresql."
    ref="https://docs.netapp.com/pt-br/ontap-apps-dbs/postgres/postgres-architecture.html"
%}

A arquitetura do PostgreSQL é baseada em um modelo **process-per-user** (um processo para cada usuário), utilizando uma área de memória compartilhada para garantir eficiência e consistência.

Abaixo, descrevo os componentes principais divididos pelas categorias da imagem:

### Processos de Conexão e Execução

- **Postmaster (Processo Pai):** É o primeiro processo iniciado. Ele escuta conexões de clientes em uma porta específica (geralmente 5432), autentica o usuário e cria (**forks**) um novo processo backend para cada nova conexão.
- **Backend Process:** É o processo dedicado a um único cliente. Ele recebe as consultas SQL, as planeja, executa e retorna os resultados, interagindo diretamente com a Memória Compartilhada.

### Shared Memory (Memória Compartilhada)

Esta é a RAM utilizada por todos os processos do PostgreSQL para evitar I/O excessivo em disco.

- **Shared Buffers:** O "coração" da performance. Armazena cópias das páginas de dados lidas do disco. Se um dado já está aqui, a leitura é instantânea.
- **WAL Buffers (Write Ahead Log):** Armazena temporariamente as mudanças feitas no banco antes de serem gravadas no arquivo WAL em disco. Isso garante que as transações não sejam perdidas em caso de falha.
- **CLOG Buffers (Commit Log):** Mantém o status das transações (se foram finalizadas com sucesso ou abortadas) para controle de concorrência (MVCC).
- **Temp Buffers:** Usados para tabelas temporárias e operações que não precisam ser visíveis para outros usuários.

### Utility Processes (Processos Utilitários)

Processos de segundo plano que mantêm a saúde e integridade do sistema:

- **Writer (Background Writer):** Move periodicamente as páginas "sujas" (modificadas) dos *Shared Buffers* para os arquivos de dados no disco.
- **WAL Writer:** Grava o conteúdo dos *WAL Buffers* para os arquivos WAL físicos no disco de forma persistente.
- **Checkpointer:** Cria pontos de verificação (checkpoints) para garantir que todos os dados na memória e nos logs de transação foram sincronizados com os arquivos de dados físicos.
- **Archiver Process:** Copia os arquivos WAL cheios para um local de armazenamento externo (backup contínuo).
- **Logging Collector:** Captura as mensagens de erro e logs do sistema e as grava nos arquivos de log.
- **Stats Collector:** Coleta informações sobre a atividade do banco (ex: número de acessos a uma tabela) para o otimizador de consultas.
- **Autovacuum Launcher:** Gerencia processos de limpeza automática para remover dados obsoletos ("mortos") e evitar que o banco cresça desnecessariamente.

### Physical Files (Arquivos Físicos/Disco)

Representa como o dado é armazenado permanentemente:

- **Data Files:** Onde as tabelas e índices realmente residem.
- **WAL Files:** Registros sequenciais de todas as mudanças. Essenciais para recuperação de desastres (*Crash Recovery*).
- **Log Files:** Arquivos de texto contendo erros, avisos e atividades monitoradas.
- **Archive Files:** Cópias de segurança dos WALs para recuperação em um ponto específico do tempo (*Point-in-Time Recovery*).

### Considerações quanto a performance

#### O Mecanismo de WAL (Write-Ahead Logging)

O conceito fundamental aqui é: **nenhuma mudança em um arquivo de dados pode ser gravada antes que o log dessa mudança seja gravado no disco.**

- **Por que isso existe?** Gravar dados em tabelas (Data Files) é uma operação lenta e aleatória no disco. Gravar no WAL é uma operação sequencial e muito rápida.
- **Como funciona:** Quando você faz um `UPDATE`, o PostgreSQL altera a página na memória (**Shared Buffers**) e grava a alteração no **WAL Buffer**. O **WAL Writer** então "despeja" isso no arquivo físico de WAL.
- **Segurança:** Se a energia cair, o PostgreSQL lê os arquivos de WAL ao reiniciar e "refaz" as alterações que estavam na memória mas ainda não tinham chegado aos arquivos de dados finais.

#### Autovacuum: A "Faxina" Necessária

O PostgreSQL utiliza um sistema chamado **MVCC** (Multi-Version Concurrency Control). Isso significa que, quando você deleta ou atualiza uma linha, o banco não apaga o dado antigo imediatamente; ele apenas o marca como "invisível".

- **O Problema (Bloat):** Sem limpeza, o banco de dados ficaria cheio de "lixo" (tuplas mortas), ocupando espaço desnecessário e ficando lento.
- **A Solução:** O **Autovacuum Launcher** aciona processos que percorrem as tabelas, identificam essas linhas mortas e liberam o espaço para que novas inserções possam usar aquele "buraco" no arquivo, sem precisar aumentar o tamanho do arquivo no disco.
- **Impacto:** Se o Autovacuum estiver mal configurado, tabelas que sofrem muitos updates podem "inchar" (bloat), prejudicando drasticamente a performance de leitura.

#### Resumo de Fluxo de Dados

Para visualizar a interação entre os componentes que vimos no gráfico anterior:

| Ação                         | Componente Envolvido              | Localização        |
| ---------------------------- | --------------------------------- | ------------------ |
| **Escrita de Dados**         | Backend Process -> Shared Buffers | RAM                |
| **Garantia de Persistência** | WAL Writer -> WAL Files           | Disco (Sequencial) |
| **Sincronização Final**      | Checkpointer -> Data Files        | Disco (Aleatório)  |
| **Limpeza de Espaço**        | Autovacuum -> Data Files          | Disco              |

### Exemplo de Estrutura Técnica: PostgreSQL

```sql
-- Criação de um banco de dados
CREATE DATABASE escola;

-- Criação de uma tabela
CREATE TABLE alunos (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100),
  matricula VARCHAR(20) UNIQUE,
  data_nascimento DATE
);

-- Criação de um índice
CREATE INDEX idx_nome_aluno ON alunos(nome);

-- Exemplo de view
CREATE VIEW alunos_maiores AS
  SELECT nome, matricula FROM alunos WHERE data_nascimento < '2008-01-01';
```

## Arquitetura do Oracle

{% include image.html
    src="https://learnomate.org/wp-content/uploads/2024/01/1705393115139.png"
    alt="Figura: Arquitetura Oracle."
    caption="Figura: Arquitetura Oracle."
    ref="https://learnomate.org/oracle-dba-architecture/https://learnomate.org/oracle-dba-architecture/"
%}

## Exemplo de Estrutura Técnica: Oracle

```sql
-- Criação de tablespace (Oracle)
CREATE TABLESPACE escola_ts DATAFILE 'escola01.dbf' SIZE 10M;

-- Criação de usuário e concessão de privilégios
CREATE USER escola IDENTIFIED BY senha DEFAULT TABLESPACE escola_ts;
GRANT CONNECT, RESOURCE TO escola;

-- Criação de tabela
CREATE TABLE escola.alunos (
  id NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
  nome VARCHAR2(100),
  matricula VARCHAR2(20) UNIQUE,
  data_nascimento DATE
);

-- Criação de índice
CREATE INDEX idx_nome_aluno ON escola.alunos(nome);

-- Exemplo de view
CREATE OR REPLACE VIEW escola.alunos_maiores AS
  SELECT nome, matricula FROM escola.alunos WHERE data_nascimento < TO_DATE('2008-01-01','YYYY-MM-DD');
```
