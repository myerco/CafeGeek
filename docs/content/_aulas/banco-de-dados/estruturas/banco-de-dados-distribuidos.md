---
title: Banco de Dados Distribuídos
excerpt: "Banco de dados distribuídos: replicação, fragmentação, vantagens e desafios."
categories:
  - "banco-de-dados"
  - "estruturas"
date: 2026-01-31T08:48:05-04:00
order: 10
tags:
  - banco-de-dados
sidebar:
  nav: introducao-a-banco-de-dados
---

Um sistema distribuído é qualquer sistema de múltiplas localidades conectadas juntas em uma espécie de redes de comunicações, nas quais o usuário (usuário final ou programador de aplicação) de qualquer localidade (site) pode acessar os dados armazenados em outro local. **C.J.Date**
{: .notice}

## Banco de Dados Distribuídos

Consiste em múltiplas localidades conectadas por redes, onde o usuário pode acessar dados de qualquer site.

<div class="mermaid">
architecture-beta
    group porto_velho(cloud)[Porto Velho]
    group brasilia(cloud)[Brasilia]

    %% Componentes em Porto Velho
    service t1(internet)[Terminal 1] in porto_velho
    service t2(internet)[Terminal 2] in porto_velho
    service cpu1(server)[Servidor 1] in porto_velho
    service bd1(database)[Banco de Dados 1] in porto_velho

    %% Componentes em Brasília
    service t3(internet)[Terminal 3] in brasilia
    service t4(internet)[Terminal 4] in brasilia
    service cpu2(server)[Servidor 2] in brasilia
    service bd2(database)[Banco de Dados 2] in brasilia

    %% Conexões Porto Velho
    t2:B --> T:cpu1
    t1:R --> L:cpu1
    cpu1:B <-- T:bd1

    %% Conexões Brasília
    t3:B --> T:cpu2
    t4:L --> R:cpu2
    cpu2:B <-- T:bd2

    %% Interconexão entre CPUs
    cpu1:R <--> L:cpu2
</div>

## Armazenamento

- Replicação - Os sistemas mantém réplicas idênticas (cópias) da relação. Cada réplica é armazenada em diferentes sites, resultando na replicação dos dados. A alternativa para replicação é armazenada somente em cópia da relação r.
- Fragmentação - A relação é particionada em vários fragmentos. Cada fragmento é armazenado em um site diferente.
- Replicação e fragmentação - A relação é particionada em vários segmentos. O sistema mantém diversas réplicas de cada fragmento.

### Replicação

“Se uma relação r é replicada, uma cópia da relação r é armazenada em dois ou mais sites. No caso mais extremo, temos replicação total, na qual cada cópia é armazenada em todos os sites do sistema”.
{: .notice}

<div class="mermaid">
architecture-beta
    group porto_velho(cloud)[Porto Velho]
    group brasilia(cloud)[Brasilia]

    %% Componentes em Porto Velho
    service t1(internet)[Terminal 1] in porto_velho
    service t2(internet)[Terminal 2] in porto_velho
    service cpu1(server)[Servidor 1] in porto_velho
    service bd1(database)[Banco de Dados 1] in porto_velho

    %% Componentes em Brasília
    service t3(internet)[Terminal 3] in brasilia
    service t4(internet)[Terminal 4] in brasilia
    service cpu2(server)[Servidor 2] in brasilia
    service bd2(database)[Banco de Dados 2] in brasilia

    %% Conexões Porto Velho
    t2:B --> T:cpu1
    t1:R --> L:cpu1
    cpu1:B <-- T:bd1

    %% Conexões Brasília
    t3:B --> T:cpu2
    t4:L --> R:cpu2
    cpu2:B <-- T:bd2

    %% Interconexão entre CPUs
    cpu1:R <--> L:cpu2
</div>

#### Vantagens e desvantagens

- Disponibilidade;
- Aumento do paralelismo;
- Aumento do overhead para atualização.

### Fragmentação

Se uma relação r é fragmentada, r é dividida em fragmentos (r1, r2… rn). Esses fragmentos contém informações suficientes para permitir a reconstrução da relação original r.
{: .notice}

<div class="mermaid">
flowchart LR
    subgraph "Estrutura das Tabelas"
        direction LR
        subgraph T1[Tabela 1]
            direction TB
            A1[A]
            B1[B]
            C1[C]
        end

        subgraph T2[Tabela 2]
            direction TB
            A2[A]
        end

        subgraph T3[Tabela 3]
            direction TB
            B3[B]
        end
        subgraph T4[Tabela 4]
            direction TB
            C3[C]
        end        
    end

    T1 --> T2
    T1 --> T3
    T1 --> T4
    
    style A1 fill:#e3f2fd
    style B1 fill:#f3e5f5
    style C1 fill:#e8f5e8
    style A2 fill:#e3f2fd
    style B3 fill:#f3e5f5
    style C3 fill:#e8f5e8
</div>

- Fragmentação Horizontal - A relação r é particionada em número de subconjuntos (r1, r2...rn). Cada  tupla da relação r deve pertencer a pelo menos um fragmento, de modo que a relação original possa ser reconstruída, se necessário.
- Fragmentação Vertical - Em sua forma mais simples, a fragmentação vertical é o mesmo que uma decomposição. Implica na definição de vários subconjuntos de atributos (R1, R2...Rn) do esquema R. Para garantir que a relação possa ser reconstruída é necessário incluir os atributos da chave primária de R em cada um dos R.

### Fragmentação Horizontal

#### ALUNOS - FR00

| CD  | NOME       | UF  |
| --- | ---------- | --- |
| 01  | JOÃO SILVA | RO  |
| 02  | ANA GOMES  | RO  |

#### FR01

| CD  | NOME       | UF  |
| --- | ---------- | --- |
| 01  | JOÃO SILVA | RO  |
| 02  | ANA GOMES  | RO  |

#### FR02

| CD  | NOME          | UF  |
| --- | ------------- | --- |
| 03  | ANDRÉ NUNES   | RJ  |
| 04  | SARAH FREITAS | SP  |
| 06  | MARIA CLARA   | RJ  |

#### FR03

| CD  | NOME           | UF  |
| --- | -------------- | --- |
| 04  | SARAH FREITAS  | SP  |
| 07  | AUGUSTO CAMPOS | SP  |

- FR00 - É a tabela principal;
- FR01 - É um fragmento da tabela FR00;
- O atributo UF é o principal particionador;
- Considere uma chave primária composta:
  - UFNNN - RO001

### Fragmentação Vertical

### ALUNOS - FR00R

| CD  | NOME           | UF  | FOTO |
| --- | -------------- | --- | ---- |
| 01  | JOÃO SILVA     | RO  | 🎥    |
| 02  | ANA GOMES      | RO  | 🎥    |
| 03  | ANDRÉ NUNES    | RJ  | 🎥    |
| 04  | SARAH FREITAS  | SP  | 🎥    |
| 06  | MARIA CLARA    | RJ  | 🎥    |
| 07  | AUGUSTO CAMPOS | SP  | 🎥    |

### FR01R

| CD  | FOTO |
| --- | ---- |
| 01  | 🎥    |
| 02  | 🎥    |
| 03  | 🎥    |
| 06  | 🎥    |

### Fragmentação e replicação

### ALUNOS - FR00FR

| CD  | NOME           | UF  | FOTO |
| --- | -------------- | --- | ---- |
| 01  | JOÃO SILVA     | RO  | 🔑    |
| 02  | ANA GOMES      | RO  | 🔑    |
| 03  | ANDRÉ NUNES    | RJ  | 🔑    |
| 04  | SARAH FREITAS  | SP  | 🔑    |
| 06  | MARIA CLARA    | RJ  | 🔑    |
| 07  | AUGUSTO CAMPOS | SP  | 🔑    |

### FR01FR

| CD  | FOTO |
| --- | ---- |
| 01  | 🔑    |
| 02  | 🔑    |
| 03  | 🔑    |
| 06  | 🔑    |

### FR02FR

---

| CD     | FOTO  |
| ------ | ----- |
| 01     | 🔑     |
| 02     | 🔑     |
| 03     | 🔑     |
| **06** | **🔑** |

## Fragmentação vantagens

- Autonomia local;
- Capacidade e crescimento incremental;
- Confiança e disponibilidade;
- Eficiência e flexibilidade.

## Fragmentação desvantagens

- Processamento de consultas;
- Propagação de atualização;
- Concorrência;
- Recuperação;
- Gerenciamento de catálogo.

## Obseração

- Oferece autonomia local e eficiência, mas dificulta o processamento de consultas, o controle de concorrência e a recuperação.
