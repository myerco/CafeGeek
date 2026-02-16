---
title: Controle de Transações
excerpt: "Controle de transações e propriedades ACID."
categories:
  - "banco-de-dados"
  - "estruturas"
date: 2026-01-31T08:48:05-04:00
order: 8
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

Uma transação é uma unidade de execução de programa que acessa e, possivelmente, atualiza vários itens de dados. Uma transação, geralmente, é o resultado da execução de um programa de usuário escrito em uma linguagem de manipulação de dados de alto nível ou em uma linguagem de programação (por exemplo: SQL, COBOL, C ou pascal), e é delimitada por declarações (ou chamadas de função) da forma begin transaction e end transaction. A transação consiste em todas as operações alí executadas, entre o começo e o fim da transação. **Abrahan Silberschatz**
{: .notice}

## Controle de Transações

Uma transação é uma unidade de execução que acessa ou atualiza itens de dados.

## Propriedades ACID

- Atomicidade: Ou todas as operações da transação são refletidas corretamente no banco de dados ou nenhuma o será.
- Consistência: A execução de uma transação isolada (ou seja, sem a execução concorrente, de outra transação) preserva a consistência do banco de dados.
- Isolamento: Embora diversas transações possam ser executadas de forma concorrente, o sistema garante que, para todo par de transações Ti e Tj, Ti tenha a sensação de que Tj terminou sua execução antes de Ti terminar. Assim, cada transação não toma conhecimento de outras transações concorrentes no sistema.
- Durabilidade: Depois da transação completar-se com sucesso, as mudanças que ela faz no banco persistem, até mesmo se houver falhas no sistema.

## Operações

- READ(X) - transfere o item de dados X do banco de dados para um buffer local alocado à transação que executou a operação de read.
- WRITE(X) - transfere o item de dados X do buffer local da transação que executou a write de volta ao banco de dados. Esta operação não resulta necessariamente na atualização imediata dos dados no disco.

## Estados

- Ativa
- Efetivação Parcial
- Em Falha
- Abortada (Rolled Back)
- Efetivada (Committed)

<div class="mermaid">
graph LR
    %% Definição de Estilos
    classDef default fill:#808080,stroke:#333,stroke-width:1px,color:#000;
    classDef invisible fill:none,stroke:none,color:#FF4500,font-weight:bold;

    %% Nós
    A(Ativa)
    B(Em efetivação parcial)
    C(Em efetivação)
    D(Em falha)
    E(Abortada)
    
    %% Rótulos de texto em vermelho
    L1[Transação concluída]:::invisible
    L2[Transação abortou]:::invisible

    %% Conexões
    A --- B
    B --- C
    A --- D
    D --- E

    %% Posicionamento dos rótulos (ajuste visual)
    C --- L1
    E --- L2
</div>
