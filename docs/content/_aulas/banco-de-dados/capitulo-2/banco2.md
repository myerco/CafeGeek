Abaixo apresento o conteúdo consolidado das apresentações de **Banco de Dados II** em formato Markdown, estruturado conforme as fontes fornecidas.

---

# Conteúdo Programático: Banco de Dados II

## 1. Apresentação da Disciplina
A disciplina é ministrada pelo professor **Marco Yerco Mendizabel Cabrera**, Analista de Sistemas e Especialista em Banco de Dados. 

*   **Objetivos Principais:**
    *   Implementar regras de negócios via restrições de integridade, procedimentos e funções.
    *   Implementar visualizações e programas armazenados.
    *   Apresentar aspectos de controle de concorrência, otimização de consultas e modelos de banco de dados distribuídos.
*   **Projetos e Ferramentas:** Serão desenvolvidos projetos de gerenciamento de alunos, vendas e projetos utilizando o **Oracle XE 11 (SGBD)** e o **SQL Developer** como cliente de acesso.

## 2. Sistemas Gerenciadores de Banco de Dados (SGBD)
Um SGBD é um conjunto de dados associados a programas que permitem o acesso e a manipulação dessas informações.
*   **Funções:** É responsável por armazenar dados em disco de forma estruturada, fornecer mecanismos de criação/alteração de definições e manter a localização de cada elemento.
*   **Estrutura e Processamento:**
    *   **Processamento de Consultas:** Envolve compiladores DML (traduzem comandos para baixo nível) e interpretadores DDL (registram metadados).
    *   **Gerenciamento de Armazenamento:** Controla autorizações, integridade, transações (garantindo persistência pós-falhas), administração de arquivos em disco e administração de buffer (intermediação entre disco e memória).
*   **Dados Físicos:** O sistema armazena o próprio banco, dicionários de metadados, índices para acesso rápido e estatísticas para otimização.

## 3. Restrições de Integridade
As regras de integridade garantem que mudanças feitas por usuários autorizados não resultem em perda de consistência, protegendo o banco de danos acidentais.
*   **Integridade de Domínio:** Define valores válidos para atributos, comparável a variáveis tipadas em linguagens de programação. Exemplos no Oracle incluem o uso de `CHECK`, `NOT NULL` e `CREATE DOMAIN`.
*   **Integridade Referencial:** Define que tabelas relacionadas devem manter a consistência entre chaves primárias (PK) e estrangeiras (FK).
    *   **Termos:** Tabela Pai (referenciada pela PK) e Tabela Filho (dependente, contém a FK).
    *   **Opção CASCADE:** Permite que a exclusão de uma linha na tabela pai remova automaticamente as linhas correspondentes na tabela filha. Alternativamente, pode-se usar `SET NULL` para anular as referências na tabela filha.

## 4. Visões (Views) e Restrições de Acesso
Uma visão é considerada uma **tabela virtual**; ela não existe fisicamente, mas aparece ao usuário como uma tabela real.
*   **Características:** Funciona como uma janela para um subconjunto de dados, refletindo automaticamente mudanças nas tabelas base.
*   **Sintaxe SQL:** `CREATE VIEW nome_da_view AS subquery`. Exemplos mostram a criação de visões para filtrar funcionários com salários específicos e a execução de consultas normais sobre essas visões.

## 5. Programação de Banco de Dados (PL/SQL)
O Oracle utiliza a linguagem procedural **PL/SQL** para agrupar comandos SQL e lógica de programação.
*   **Procedures e Functions:** São esquemas de objetos armazenados dentro do banco.
*   **Vantagens:** Melhoria na segurança (restrição de operações), performance (redução de tráfego na rede), integridade e compartilhamento de memória.
*   **Elementos:** Inclui variáveis, cursores, exceções e estruturas de controle como `IF...THEN`, `LOOP` e `FOR`.

## 6. Gatilhos (Triggers)
Um gatilho é um comando executado automaticamente pelo sistema como consequência de uma modificação (INSERT, UPDATE ou DELETE) no banco de dados.
*   **Requisitos:** Deve-se especificar as condições de execução e as ações a serem tomadas.
*   **Vantagens:** Prevenção de transações inválidas, auditoria sofisticada, sincronismo de tabelas replicadas e geração de colunas derivadas.
*   **Sintaxe:** Define-se o momento (`BEFORE` ou `AFTER`), o comando e se a execução é para cada linha (`FOR EACH ROW`).

## 7. Processamento e Otimização de Consultas
Envolve as atividades de extrair dados e traduzir consultas de alto nível para expressões físicas eficientes.
*   **Etapas:**
    1.  **Análise Sintática:** Traduz o SQL para uma expressão de álgebra relacional.
    2.  **Otimização:** Seleciona o plano de execução mais eficiente baseando-se em algoritmos, índices e estatísticas de custo.
    3.  **Avaliação:** Estima custos via tempo de CPU, acesso a disco (IO) e uso de RAM.
*   **Execução de Joins:** O otimizador decide o caminho de acesso (varredura total ou índice), o método de união (Nested loop, Sort merge ou Hash joins) e a ordem de execução.
*   **Fases no Oracle:** Parse (verificação e busca no dicionário), Execute (aplicação física) e Fetch (retorno dos dados).

## 8. Controle de Transações
Uma transação é uma unidade de execução que acessa ou atualiza itens de dados.
*   **Propriedades ACID:**
    *   **Atomicidade:** Ou todas as operações são refletidas ou nenhuma será.
    *   **Consistência:** A execução isolada preserva a integridade do banco.
    *   **Isolamento:** Transações concorrentes não interferem umas nas outras.
    *   **Durabilidade:** Mudanças persistem após o sucesso, mesmo em falhas de sistema.
*   **Estados:** Uma transação pode estar Ativa, em Efetivação Parcial, em Falha, Abortada (Rolled Back) ou Efetivada (Committed).

## 9. Controle de Concorrência
Necessário para gerenciar a interação entre transações simultâneas e preservar o isolamento.
*   **Mecanismos:**
    *   **Bloqueios (Locks):** Podem ser Compartilhados (S), permitindo apenas leitura, ou Exclusivos (X), permitindo leitura e escrita.
    *   **Deadlock:** Situação de espera mútua onde transações aguardam a liberação de bloqueios umas das outras.
*   **Protocolo de Bloqueio em Duas Fases:** Consiste na Fase de Expansão (obtenção de bloqueios) e Fase de Encolhimento (liberação de bloqueios).

## 10. Banco de Dados Distribuídos
Consiste em múltiplas localidades conectadas por redes, onde o usuário pode acessar dados de qualquer site.
*   **Armazenamento:**
    *   **Replicação:** O sistema mantém cópias idênticas da relação em diferentes sites, aumentando a disponibilidade e o paralelismo.
    *   **Fragmentação:** A relação é particionada em fragmentos horizontais (subconjuntos de tuplas) ou verticais (subconjuntos de atributos).
*   **Vantagens e Desafios:** Oferece autonomia local e eficiência, mas dificulta o processamento de consultas, o controle de concorrência e a recuperação.