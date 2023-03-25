---
title: Implementando Data Tables com Unreal Engine
description: Data Tables são estruturas de dados com vários tipos de variáveis agrupados
tags: [Unreal Engine,data tables]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
sidebar:  
  - title: "ESTRUTURAS DE DADOS"
    nav: "dev_unreal_estruturas"
date: 2022-09-25 
---

***

- [1. O que são Data Tables?](#1-o-que-são-data-tables)
- [2. Criando um objeto do tipo Data Table](#2-criando-um-objeto-do-tipo-data-table)
- [3. Inserindo dados no objeto do tipo Data Table](#3-inserindo-dados-no-objeto-do-tipo-data-table)
- [4. Importando dados de um arquivo csv](#4-importando-dados-de-um-arquivo-csv)
- [5. Exemplo de utilização de Data Table](#5-exemplo-de-utilização-de-data-table)
  - [5.1. Implementando o objeto BP\_Vida](#51-implementando-o-objeto-bp_vida)
  - [5.2. Implementando o objeto BP\_Elementos](#52-implementando-o-objeto-bp_elementos)
  - [5.3. Logica da carga dos dados](#53-logica-da-carga-dos-dados)

***

Neste capitulo vamos explorar os objetos do tipo **Data tables** que são basicamente tabelas de dados disponíveis para os desenvolvedores e são definidas por tipos *Structure*.  

## 1. O que são Data Tables?

***

**Data Tables** são estruturas de dados com vários tipos de variáveis agrupados e podem ser utilizadas para armazenamento de forma estática de informações dos personagens e suas características, recursos do jogo como espadas, escudos, magias, propriedades do jogo como níveis, dificuldades e pontuação.

## 2. Criando um objeto do tipo Data Table

***

Vamos implementar o **SElementos** do tipo *Structure* que servirá como base para o objeto `Data Table`.

{% include imagebase.html
    src="unreal/estruturas/blueprint_structure.webp"
    alt="Figura: Blueprint - Structure SElementos."
    caption="Figura: Blueprint - Structure SElementos."
%}

Definimos as seguintes variáveis.

{% include imagebase.html
    src="unreal/estruturas/blueprint_structure_variable_3.webp"
    alt="Figura: Blueprint - Criando as variáveis dentro da estrutura."
    caption="Figura: Blueprint - Criando as variáveis dentro da estrutura."
%}

Utilizando o menu de contexto escolha `Miscellaneous` > `Data Table`.

{% include imagebase.html
    src="unreal/estruturas/blueprint_datatable_menu.webp"
    alt="Figura: Blueprint - Menu de contexto Miscellaneous > Data Table."
    caption="Figura: Blueprint - Menu de contexto Miscellaneous > Data Table."
%}

Logo em seguida devemos definir a estrutura de dados da tabela utilizando o variável **SElementos** do tipo `Structure`.

{% include imagebase.html
    src="unreal/estruturas/blueprint_datatable_row_structure.webp"
    alt="Figura: Blueprint - Definindo a estrutura da tabela usando Structure e Data Table."
    caption="Figura: Blueprint - Definindo a estrutura da tabela usando Structure e Data Table."
%}

*DTElementos* do tipo `Data Tables`.

{% include imagebase.html
    src="unreal/estruturas/blueprint_datatables.webp"
    alt="Figura: Blueprint - Data Table."
    caption="Figura: Blueprint - Data Table."
%}

## 3. Inserindo dados no objeto do tipo Data Table

***

Ao abrir o objeto de Data Table é apresentado um editor para manipulação de dados, inserindo, removendo e alterando as linhas.  
A coluna **RowName** não pode ser repetida, funcionado como identificador único da linha.

{% include imagebase.html
    src="unreal/estruturas/blueprint_datatables_editor.webp"
    alt="Figura: Blueprint - Exemplo do editor para inserir linhas na tabela."
    caption="Figura: Blueprint - Exemplo do editor para inserir linhas na tabela."
%}

## 4. Importando dados de um arquivo csv

***

É possível importar as linhas de um arquivo texto com elementos separados por vírgulas.

Primeiramente vamos definir um arquivo separado por vírgulas com as informações necessárias para o nosso propósito.

```csv
rowname,Name,type,property,value
1,Mithril,Rock,Life,10
2,The Ring of Barahir,Ring,Strength,50
3,Soul Stone,Gem,Damage,50
4,Mithril Stone Black,Rock,Life,10
```

Agora vamos implementar o objeto SArtifact do tipo *Structure* com a seguinte estrutura para que possamos carregar os dados do arquivo:

{% include imagebase.html
    src="unreal/estruturas/blueprint_datatables_artifact.webp"
    alt="Figura: Blueprint - Definindo Structure para carregar os dados."
    caption="Figura: Blueprint - Definindo Structure para carregar os dados."
%}

Em seguida implemente o objeto TArtifact do tipo `Data Table` e com o botão direito do mouse em cima do objeto e selecione `Reimport`, logo em seguida escolha o arquivo csv:

{% include imagebase.html
    src="unreal/estruturas/blueprint_datatables_import.webp"
    alt="Figura: Blueprint - Data Table Reimport."
    caption="Figura: Blueprint - Data Table Reimport."
%}

Os dados serão importados e na aba `Data Table Details` os parâmetros de importação serão apresentados.

{% include imagebase.html
    src="unreal/estruturas/blueprint_datatables_details.webp"
    alt="Figura: Blueprint - Data Table Details."
    caption="Figura: Blueprint - Data Table Details."
%}

## 5. Exemplo de utilização de Data Table

***

Para este exemplo vamos implementar um objeto para automaticamente adicionar outros objetos (Vida) na cena, a posição dos objetos pode se controlada com um vetor de coordenadas.  

### 5.1. Implementando o objeto BP_Vida

Este objeto deverá estar na cena para interação com o jogador pois pode aumentar o valor da vida do personagem com as seguintes variáveis e componentes.  

{% include imagebase.html
    src="unreal/estruturas/blueprint_component_bp_vida.webp"
    alt="Figura: Blueprint - Exemplo do objeto BP_vida."
    caption="Figura: Blueprint - Exemplo do objeto BP_vida."
%}

### 5.2. Implementando o objeto BP_Elementos

Este objeto serve como referência na cena para posicionamento de objetos *BP_Vida* com as seguintes variáveis e componentes.

{% include imagebase.html
    src="unreal/estruturas/blueprint_component_bp_elementos.webp"
    alt="Figura: Blueprint - Exemplo do objeto de posicionamento dos objetos vida."
    caption="Figura: Blueprint - Exemplo do objeto de posicionamento dos objetos vida."
%}

Observe que a variável **Posicao** é do tipo vector e tem a propriedade `Show 3D Widget` habilitada para facilitar o posicionamento do elemento na cena.  

{% include imagebase.html
    src="unreal/estruturas/blueprint_vetor_widget.webp"
    alt="Figura: Blueprint - Show 3D Widget."
    caption="Figura: Blueprint - Show 3D Widget."
%}

O Vetor **Posicao** na cena.

{% include imagebase.html
    src="unreal/estruturas/blueprint_actor_posicao.webp"
    alt="Figura: Blueprint - Posição do ator na cena."
    caption="Figura: Blueprint - Posição do ator na cena."
%}

Detalhes das coordenadas.

{% include imagebase.html
    src="unreal/estruturas/blueprint_actor_posicao_detalhe.webp"
    alt="Figura: Blueprint - Coordenadas."
    caption="Figura: Blueprint - Coordenadas."
%}

### 5.3. Logica da carga dos dados

Para cada elemento do vetor *Posicao* é implementado um objeto do tipo BP_vida nas coordenadas de vetor.

{% include imagebase.html
    src="unreal/estruturas/blueprint_getdatatable.webp"
    alt="Figura: Blueprint - Carregando dados utilizando GetDataTableRow."
    caption="Figura: Blueprint - Carregando dados utilizando GetDataTableRow."
%}

- `Get data Table Row` - Tenta recuperar uma linha da `DataTable` por meio de texto em **RowName**.  No exemplo a linha recuperada deve coincidir com uma variável passada como parâmetro;

Para cada objeto adicionado na cena são definidas propriedades.

{% include imagebase.html
    src="unreal/estruturas/blueprint_spawn_bp_vida.webp"
    alt="Figura: Blueprint - Criando objetos usando os dados do Data Table."
    caption="Figura: Blueprint - Criando objetos usando os dados do Data Table."
%}
