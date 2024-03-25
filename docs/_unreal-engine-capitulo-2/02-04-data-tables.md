---
title: Data Tables
excerpt: Neste capitulo vamos explorar o objeto Data Tables.  
permalink: /unreal-engine-capitulo-2/data-tables
last_modified_at: 2023-03-28T08:48:05-04:00
layout: single
order: 204
sidebar:
    nav: dev_unreal_2
toc: true  
categories:
  - Unreal Engine
tags:
  - variáveis estruturadas
  - Structure
  - Data tables
  - Importando dados
  - .csv
---

## 1. O que são Data Tables?

**Data Tables** são estruturas de dados com vários tipos de variáveis agrupados e podem ser utilizadas para armazenamento de forma estática de informações dos personagens e suas características, recursos do jogo como espadas, escudos, magias, propriedades do jogo como níveis, dificuldades e pontuação.

Vamos explorar os objetos do tipo **Data tables** que são basicamente tabelas de dados disponíveis para os desenvolvedores e são definidas por tipos *Structure*.  

## 2. Criando um objeto do tipo Data Table

![image-left](/assets/images/unreal/estruturas/unreal-engine-datatable-example.webp){: .align-left}
Vamos implementar o **SElementos** do tipo *Structure* que servirá como base para o objeto `Data Table`.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-structure-variable-3.webp"
    alt="Figura: Criando as variáveis dentro da estrutura."
    caption="Definimos as seguintes variáveis."
%}

Utilizando o menu de contexto escolha `Miscellaneous` > `Data Table`.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-datatable-menu.webp"
    alt="Figura: Menu de contexto Miscellaneous > Data Table."
   caption=""
%}

Logo em seguida devemos definir a estrutura de dados da tabela utilizando o variável **SElementos** do tipo `Structure`.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-datatable-row-structure.webp"
    alt="Figura: Definindo a estrutura da tabela usando Structure e Data Table."
   caption=""
%}

## 3. Inserindo dados no objeto do tipo Data Table

Ao abrir o objeto de Data Table é apresentado um editor para manipulação de dados, inserindo, removendo e alterando as linhas.  
A coluna **RowName** não pode ser repetida, funcionado como identificador único da linha.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-datatables-editor.webp"
    alt="Figura: Exemplo do editor para inserir linhas na tabela."
   caption=""
%}

## 4. Importando dados de um arquivo csv

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

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-datatables-artifact.webp"
    alt="Figura: Definindo Structure para carregar os dados."
   caption=""
%}

Em seguida implemente o objeto TArtifact do tipo `Data Table` e com o botão direito do mouse em cima do objeto e selecione `Reimport`, logo em seguida escolha o arquivo csv:

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-datatables-import.webp"
    alt="Figura: Data Table Reimport."
   caption=""
%}

Os dados serão importados e na aba `Data Table Details` os parâmetros de importação serão apresentados.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-datatables-details.webp"
    alt="Figura: Data Table Details."
   caption=""
%}

## 5. Exemplo de utilização de Data Table

Para este exemplo vamos implementar um objeto para automaticamente adicionar outros objetos (Vida) na cena, a posição dos objetos pode se controlada com um vetor de coordenadas.  

### 5.1. Implementando o objeto BP-Vida

Este objeto deverá estar na cena para interação com o jogador pois pode aumentar o valor da vida do personagem com as seguintes variáveis e componentes.  

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-component-bp-vida.webp"
    alt="Figura: Exemplo do objeto BP_vida."
   caption=""
%}

### 5.2. Implementando o objeto BP_Elementos

Este objeto serve como referência na cena para posicionamento de objetos *BP_Vida* com as seguintes variáveis e componentes.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-component-bp-elementos.webp"
    alt="Figura: Exemplo do objeto de posicionamento dos objetos vida."
   caption=""
%}

Observe que a variável **Posicao** é do tipo vector e tem a propriedade `Show 3D Widget` habilitada para facilitar o posicionamento do elemento na cena.  

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-vetor-widget.webp"
    alt="Figura: Show 3D Widget."
   caption=""
%}

O Vetor **Posicao** na cena.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-actor-posicao.webp"
    alt="Figura: Posição do ator na cena."
   caption=""
%}

Detalhes das coordenadas.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-actor-posicao-detalhe.webp"
    alt="Figura: Coordenadas."
   caption=""
%}

### 5.3. Logica da carga dos dados

Para cada elemento do vetor *Posicao* é implementado um objeto do tipo BP_vida nas coordenadas de vetor.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-getdatatable.webp"
    alt="Figura: Carregando dados utilizando GetDataTableRow."
   caption=""
%}

- `Get data Table Row` - Tenta recuperar uma linha da `DataTable` por meio de texto em **RowName**.  No exemplo a linha recuperada deve coincidir com uma variável passada como parâmetro;

Para cada objeto adicionado na cena são definidas propriedades.

{% include imagelocal.html
    src="unreal/estruturas/unreal-engine-spawn-bp-vida.webp"
    alt="Figura: Criando objetos usando os dados do Data Table."
   caption=""
%}
