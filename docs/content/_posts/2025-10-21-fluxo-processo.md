
```mermaid
flowchart TD
   

    %% Fluxo principal
    A[🟡 Nova Demanda<br/>Backlog] --> B{🟠 Análise de Viabilidade}
    
    B -->|Não Viável| C[🟣 Rejeitado]
    B -->|Viável| D[🔴 Priorizado]
    
    C --> Z[⚫ Arquivado]
    
    D --> E[🟡 Sprint Backlog<br/>Aguardando Alocação]
    E --> F[🟠 Levantamento de Requisitos]
    F --> G[🟠 Em Implementação]
    G --> H[🟢 Testes Técnicos]
    
    H --> I{🟡 Testes Negociais}
    I -->|Aprovado| J[🟢 Aprovado]
    I -->|Reprovado| K[🔴 Reprovado]
    
    J --> L[🔵 Homologado]
    L --> M[🔵 Entregue]
    M --> N[⚫ Arquivado]
    
    K --> G

    %% Aplicação de estilos
    class A,B,E triagem
    class D priorizacao
    class F,G desenvolvimento
    class H,I,J,K validacao
    class L,M conclusao
    class C,N,Z arquivado
```


```mermaid
flowchart TD
    %% Domínios COBIT 2019
    subgraph Governanca [GOVERNANÇA - DOMÍNIO EDM]
        A[EDM01<br/>Garantir Framework Governança] --> B[EDM02<br/>Garantir Criação de Valor]
        B --> C[EDM03<br/>Garantir Avaliação de Riscos]
        C --> D[EDM04<br/>Garantir Recursos]
        D --> E[EDM05<br/>Garantir Engajamento Stakeholders]
    end
    
    %% Processos de Gestão
    subgraph Gestao [GERENCIAMENTO - DOMÍNIOS APO, BAI, DSS]
        F[APO01<br/>Gerenciar Programa TI] --> G[BAI01<br/>Gerenciar Programas e Projetos]
        G --> H[BAI06<br/>Mudanças Controladas]
        H --> I[DSS01<br/>Operações]
        I --> J[DSS02<br/>Solicitações de Serviço]
    end
    
    %% Conexão Governança-Gestão
    E --> F
    
    %% Fluxo Operacional
    subgraph Operacional [PROCESSOS OPERACIONAIS]
        K[Desenvolvimento] --> L[Liberação]
        L --> M[Implantação]
        M --> N[Sustentação]
        N --> O[Monitoramento]
    end
    
    %% Feedback
    O --> C
```

```mermaid
flowchart TD
    A[Pacote Desenvolvido<br/>APRO13: Aceite de Solução] --> B[Preparar Documentação Liberação]
    
    B --> C[APO12: Avaliar Riscos de Segurança]
    C --> D[BAI06.01: Classificar Mudança]
    
    D --> E[Tipo de Mudança]
    E -->|Padrão| F[Aprovação Automática]
    E -->|Normal| G[CAB: Análise Detalhada]
    E -->|Emergencial| H[CAB Emergencial]
    
    F --> I[BAI06.04: Agendar Liberação]
    G --> I
    H --> I
    
    I --> J[BAI06.05: Preparar Rollback]
    J --> K[BAI06.06: Comunicar Stakeholders]
    K --> L[BAI07.01: Planejar Transição]
```

## Fase 1: Demanda e Análise de Viabilidade (Governança Inicial)

Estágio (Scrum + COBIT)	Atividades Chave (COBIT BAI)	Artefatos Principais	Status no Fluxo
- 📋 Triagem e Análise Estratégica	BAI02 - Gerenciar de Requisitos: Captura e registro inicial da demanda.
    - BAI01 - Gerenciar Programas e Projetos: Inicia o processo como um "projeto" ou "demanda".
    - BAI03 - Análise de Soluções: Identifica opções (desenvolver, comprar, customizar).
    - BAI04 - Manter a disponibilidade de tecnologia: Avalia impacto na infraestrutura.	Termo de Abertura de Demanda, Registro de Requisitos Iniciais,
    - Análise de Viabilidade (Técnica, Econômica, Legal).
    -Backlog de Demanda → Em Análise
- 🎯 Priorização e Tomada de Decisão
    - BAI01 - Gerenciar Programas e Projetos: Apresenta a análise para o comitê de governança (ex: Portfolio Board).
    - APO05 - Gerenciar o Portfolio: A priorização é feita com base no alinhamento estratégico, valor, risco e recursos.
    - Business Case,
    - Análise de Viabilidade aprovada,
    - Decisão do Comitê.	Aprovado / Rejeitado / Priorizado

## Fase 2: Planejamento e Desenvolvimento (Execução Controlada)

Estágio (Scrum + COBIT)	Atividades Chave (COBIT BAI)	Artefatos Principais	Status no Fluxo
- 📝 Planejamento Detalhado & Especificação
    - BAI02 - Gerenciar Requisitos: Detalha os requisitos funcionais e não funcionais.
    - BAI05 - Gerenciar Aquisição: Se for adquirir, inicia processo licitatório.
    - BAI06 - Gerenciar Mudanças: Estabelece o controle formal de mudanças.	Especificação de Requisitos Detalhados,
    - Plano de Projeto/Release,
    - Plano de Testes (Técnicos e de Aceitação).	Sprint Backlog
- ⚡ Implementação & Controle
    - BAI07 - Desenvolvimento e Aquisição de Soluções: Desenvolvimento propriamente dito (Scrum: Lev. Requisitos → Em Implementação).
    - BAI06 - Gerenciar Mudanças: Todas as mudanças de escopo são formalmente avaliadas e aprovadas.
    - BAI08 - Gerenciar Conhecimento: Documentação técnica é atualizada.	Incremento da Solução,
    - Registros de Mudança (se houver),
    - Documentação Técnica.	Em Implementação

## Fase 3: Validação e Transição (Qualidade e Entrega)
Estágio (Scrum + COBIT)	Atividades Chave (COBIT BAI)	Artefatos Principais	Status no Fluxo
- 👀 Validação Técnica e de Qualidade	
    - BAI09 - Gerenciar Ativos de Configuração: Versão do software é registrada no ambiente de testes.
    - BAI10 - Gerenciar Testes: Execução de testes unitários, integração, performance e segurança.	Plano de Testes Executado,
    - Relatório de Defeitos,
    - Registro de Configuração.	Em Testes Técnicos
- ⏳ Validação Negocial e Aceitação
    -BAI10 - Gerenciar Testes: Execução de testes de aceitação (UAT) pelos usuários-chave do negócio.
    - BAI02 - Gerenciar Requisitos: Confirma se a solução atende aos requisitos acordados.	Termo de Aceitação do Usuário (UAT),
Relatório Final de Testes.	Em Testes Negociais → Aprovado / Reprovado
- 🚀 Liberação e Implantação
    - BAI11 - Gerenciar Mudanças Organizacionais: Comunicação, treinamento e preparação dos usuários finais.
    - DSS02 - Gerenciar Serviços de Solicitação e Incidentes: Prepara a equipe de suporte.
    - BAI06 - Gerenciar Mudanças: A mudança para produção é formalmente aprovada.
    - Plano de Implantação,
    - Materiais de Treinamento,
    - Ordem de Mudança para Produção.
    - Homologado

## Fase 4: Conclusão e Pós-Implementação (Entrega e Valor)
Estágio (Scrum + COBIT)	Atividades Chave (COBIT BAI)	Artefatos Principais	Status no Fluxo
- ✅ Entrega e Encerramento
    - BAI01 - Gerenciar Programas e Projetos: Encerramento formal do projeto. Lições aprendidas são documentadas.
    - BAI12 - Gerenciar Conhecimento: Documentação final é arquivada e disponibilizada.
    - DSS01 - Operar os Serviços: A solução é formalmente entregue para a equipe de operações/suporte.	Relatório de Encerramento,
Lições Aprendidas,
    - Documentação Final da Solução.	Entregue
- 🔄 Monitoramento do Valor	
    - APO12 - Gerenciar Riscos & EDM03 - Assegurar a Otimização de Riscos: Monitora se os benefícios esperados no Business Case estão sendo realizados e os riscos residuais.	Relatório de Realização de Benefícios.	Em Operação (Novo Status)

```mermaid
flowchart TD
    A[📥 Demanda de Negócio] --> B[📋 Triagem & Análise Estratégica<br>BAI02 - Gerenciar Requisitos]
    B --> C[📊 Backlog de Demanda]
    C --> D{Análise de Viabilidade<br>BAI03, BAI04}
    D -- Viável --> E[🔄 Em Análise]
    D -- Inválida --> F[❌ Rejeitado]
    
    E --> G{🎯 Priorização & Tomada de Decisão<br>APO05, BAI01}
    G -- Aprovada --> H[✅ Priorizado]
    G -- Rejeitada --> F
    
    H --> I[📝 Sprint Backlog<br>Detalhamento de Requisitos BAI02]
    I --> J[⚡ Em Implementação<br>BAI07 - Desenvolvimento]
    
    J --> K{🔄 Mudança de Escopo?<br>BAI06 - Gerenciar Mudanças}
    K -- Sim --> I
    K -- Não --> L[👀 Em Testes Técnicos<br>BAI09, BAI10]
    
    L --> M[⏳ Em Testes Negociais UAT<br>BAI10 - Gerenciar Testes]
    M --> N{Aprovado?}
    N -- Sim --> O[🟢 Aprovado]
    N -- Não --> P[🔴 Reprovado]
    P --> I
    
    O --> Q[🏷️ Homologado]
    Q --> R[🚀 Preparação para Implantação<br>BAI11, DSS02]
    R --> S{Aprovação de Mudança<br>BAI06}
    S -- Aprovada --> T[✅ Entregue / Encerramento<br>BAI01]
    S -- Rejeitada --> R
    
    T --> U[🔄 Em Operação]
    U --> V[📈 Monitoramento de Benefícios<br>APO12 - Gerenciar Riscos]
```

# Processo de liberação

```mermaid
flowchart TD
    A[📥 Demanda de Negócio] --> B[📋 Triagem & Análise Estratégica]
    B --> C[📊 Backlog de Demanda]
    C --> D{Análise de Viabilidade}
    D -- Viável --> E[🔄 Em Análise]
    D -- Inválida --> F[❌ Rejeitado]
    
    E --> G{🎯 Priorização}
    G -- Aprovada --> H[✅ Priorizado]
    G -- Rejeitada --> F
    
    H --> I[📝 Sprint Backlog]
    I --> J[⚡ Em Implementação]
    
    J --> K{🔄 Mudança de Escopo?}
    K -- Sim --> I
    K -- Não --> L[👀 Em Testes Técnicos]
    
    L --> M[⏳ Em Testes Negociais UAT]
    M --> N{Aprovado?}
    N -- Sim --> O[🟢 Aprovado]
    N -- Não --> P[🔴 Reprovado]
    P --> I
    
    O --> Q[🏷️ Homologado]
    Q --> R[🎯 Planejamento da Liberação]
    
    subgraph NovaFase [🔄 Ciclo de Liberação e Adoção]
        R --> S[📢 Campanha de Publicidade]
        S --> T[👥 Treinamento dos Usuários]
        T --> U[🛠️ Implantação Gradual]
        U --> V[📊 Monitoramento de Adoção]
    end
    
    V --> W{✅ Adoção Consolidada?}
    W -- Sim --> X[🚀 Entrega Concluída]
    W -- Não --> Y[🔧 Ajustes de Adoção]
    Y --> S
    
    X --> Z[📈 Retrospectiva e Lições Aprendidas]
```

Fase: Ciclo de Liberação e Adoção

# **Fase: Ciclo de Liberação e Adoção**

| Etapa | Processos COBIT | Atividades Principais | Artefatos Gerados | Responsáveis | Critério de Êxito |
|-------|-----------------|------------------------|-------------------|-------------|-------------------|
| **🎯 Planejamento da Liberação** | **BAI11 - Gerenciar Mudanças Organizacionais**<br>**BAI06 - Gerenciar Mudanças** | - Definir estratégia de rollout<br>- Identificar públicos-alvo e stakeholders<br>- Elaborar plano de comunicação<br>- Estabelecer métricas de adoção<br>- Definir plano de rollback | Plano de Liberação<br>Matriz de Riscos de Adoção<br>Cronograma de Implementação | Gerente de Projeto<br>Líderes de Negócio<br>Comunicação Organizacional | Plano aprovado pelos stakeholders<br>Recursos alocados<br>Riscos identificados e mitigados |
| **📢 Campanha de Publicidade** | **APO07 - Gerenciar Comunicações**<br>**BAI11 - Gerenciar Mudanças Organizacionais** | - Desenvolver material de divulgação<br>- Realizar comunicação multicanal<br>- Organizar webinars de apresentação<br>- Envolver gestores como embaixadores<br>- Estabelecer portal de informações | Newsletters<br>Comunicados Oficiais<br>Materiais de Marketing<br>Portal da Solução<br>Gravações de Webinars | Equipe de Comunicação<br>Marketing Interno<br>Gestores da Área | >80% do público-alvo conscientizado<br>Feedback positivo nas pesquisas<br>Alta participação nos eventos |
| **👥 Treinamento do Sistema** | **BAI12 - Gerenciar Conhecimento**<br>**BAI11 - Gerenciar Mudanças Organizacionais** | - Desenvolver material de treinamento<br>- Conduzir sessões de capacitação<br>- Treinar superusuários<br>- Disponibilizar ambiente sandbox<br>- Oferecer suporte durante aprendizado | Manuais do Usuário<br>Vídeos Tutoriais<br>FAQs<br>Ambiente de Treinamento<br>Certificações de Conclusão | CSCOR (Treinadores)<br>RH<br>Superusuários | >90% dos usuários treinados<br>Avaliação positiva do treinamento<br>Redução de chamados básicos |
| **🛠️ Implantação Gradual** | **BAI06 - Gerenciar Mudanças**<br>**DSS02 - Gerenciar Serviços** | - Implementar para grupo piloto<br>- Coletar feedback inicial<br>- Expandir para demais áreas<br>- Monitorar performance<br>- Ajustar conforme necessário | Checklist de Implantação<br>Plano de Rollback<br>Relatório de Incidentes<br>Feedback do Grupo Piloto | CSCOR<br>Operações de TI<br>Gestores de Departamento | Implantação sem impactos críticos<br>Tempo de resposta dentro do SLA<br>Feedback positivo do piloto |
| **📊 Monitoramento de Adoção** | **APO12 - Gerenciar Riscos**<br>**DSS04 - Gerenciar Continuidade** | - Coletar métricas de uso<br>- Monitorar indicadores de performance<br>- Realizar pesquisas de satisfação<br>- Identificar barreiras à adoção<br>- Propor melhorias contínuas | Dashboard de Adoção<br>Relatórios de Utilização<br>Pesquisas de Satisfação<br>Plano de Melhorias | CSCOR<br>Gestores de Negócio<br>Quality Assurance | >70% de adoção na primeira semana<br>Taxa de satisfação >4.0/5.0<br>Problemas identificados e tratados |

---

## **Métricas de Sucesso da Fase**

| Métrica | Alvo | Periodicidade | Responsável |
|---------|------|---------------|-------------|
| **Taxa de Adoção Inicial** | >70% nos primeiros 7 dias | Semanal | CSCOR |
| **Satisfação do Usuário** | >4.0/5.0 | Pós-implantação | Gestores |
| **Redução de Chamados** | -30% em 30 dias | Mensal | Service Desk |
| **Tempo de Resolução** | Dentro do SLA estabelecido | Contínuo | Operações |
| **Utilização de Funcionalidades** | >80% das features principais | Mensal | Business Intelligence |

---

## **Fluxo de Decisão da Fase**

| Ponto de Decisão | Critério | Ação se Positivo | Ação se Negativo |
|------------------|----------|------------------|------------------|
| **Início da Campanha** | Plano de comunicação aprovado | Liberar materiais e comunicados | Revisar e ajustar plano |
| **Liberação para Treinamento** | Ambiente sandbox estável | Iniciar ciclo de treinamentos | Corrigir problemas críticos |
| **Implantação em Produção** | >85% dos usuários treinados | Prosseguir com rollout | Estender período de treinamento |
| **Expansão para Novas Áreas** | Sucesso no grupo piloto | Expandir gradualmente | Investigar e corrigir problemas |
| **Encerramento da Fase** | Adoção consolidada (>80%) | Encerrar fase de liberação | Implementar ações corretivas |


1. 🎯 Planejamento da Liberação (BAI11)

Antecede a Homologação

    Identificar públicos-alvo (usuários finais, gestores, administradores)

    Definir estratégia de comunicação multicanal

    Elaborar plano de treinamento segmentado

    Estabelecer métricas de adoção e sucesso

2. 📢 Campanha de Publicidade (APO07)

Inicia durante os Testes Negociais

    Desenvolver material de divulgação (benefícios, timeline)

    Comunicar via e-mail corporativo, intranet, murais

    Realizar webinars de apresentação da solução

    Envolver gestores como "embaixadores" da mudança

3. 👥 Treinamento do Sistema (BAI12)

Paralelo à Homologação

    Desenvolver material de treinamento (manuais, vídeos, FAQs)

    Agendar sessões de treinamento por perfil de usuário

    Treinar superusuários e gestores primeiro

    Disponibilizar ambiente de treinamento/sandbox

4. 🛠️ Implantação Gradual (BAI06)

Pós-Homologação

    Implantar para grupo piloto (canary release)

    Coletar feedback e ajustar conforme necessário

    Expandir para demais departamentos de forma controlada

    Manter suporte intensivo durante transição

5. 📊 Monitoramento de Adoção (APO12)

Contínuo pós-implantação

    Monitorar métricas de uso e performance

    Coletar feedback contínuo dos usuários

    Identificar resistências e barreiras à adoção

    Realizar ajustes no treinamento e comunicação

