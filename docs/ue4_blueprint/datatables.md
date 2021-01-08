---
title: Data tables - Tabelas de dados
tags: [Unreal Engine,data tables]
---

[CafeGeek](https://myerco.github.io/unreal-engine)  / [Desenvolvimento de jogos utilizando Unreal Engine 4](https://myerco.github.io/unreal-engine/ue4_blueprint/index.html)

# Data tables - Tabelas de dados
**Data tables** são basicamente estruturas de tabelas de dados disponíveis para os desenvolvedores e são definidas por tipos *Structure* para estruturas os dados.  

## Índice
1. [Conceito](#1)
1. [Criando Data Table](#2)
1. [Inserindo dados em Data Table](#3)
1. [Exemplo de utilização](#4)
    1. [Implementando o objeto BP_Vida](#41)
    1. [Implementando o objeto BP_Elementos](#42)
    1. [Lógica da carga dos dados](#43)

<a name="1"></a>
## 1. Conceituando
Sendo estruturas de dados com vários tipos de variáveis agrupados podem ser utilizadas para armazenamento de informações dos personagens e suas características, recursos do jogo como espadas, escudos, magias e propriedades do jogo como níveis, dificuldades e pontuação.

<a name="2"></a>
## 2. Criando Data Table
1. Primeiramente devemos implementar o **SElementos** do tipo *Structure* que servirá como base para o objeto **Data Table**.     
![](../imagens/estruturas/blueprint_structure.png)  
1. Vamos definir as seguintes variáveis.   
![](../imagens/estruturas/blueprint_structure_variable_3.png)   
1. Utilizando o menu de contexto escolha *Miscellaneous/Data Table*.    
![](../imagens/estruturas/blueprint_datatable_menu.png)
1. Devemos definir a estrutura de dados da tabela utlizando o variável **SElementos** do tipo **Structure**.   
![](../imagens/estruturas/blueprint_datatable_row_structure.png)   
1. *DTElementos* do tipo *Data Tables*.   
 ![](../imagens/estruturas/blueprint_datatables.png)

<a name="3"></a>
## 3.Inserindo dados em Data Table
Ao abrir o objeto de Data Table é apresentado um editor para manipulação de dados, inserindo, removendo e alterando as linhas.  
A coluna **RowName** não pode ser repetida, funcionado como identificador único da linha.
![](../imagens/estruturas/blueprint_datatables_editor.png)

<a name="4"></a>
## 4. Exemplo de utilização
Para este exemplo vamos implementar um objeto para automaticamente adicionar outros objetos (Vida) na cena, a posição dos objetos pode se controlada com um vetor de coordenadas.  

<a name="41"></a>
### 4.1 Implementando o objeto *BP_Vida*
Este objeto deverá estar na cena para interação com o jogador pois pode aumentar o valor da vida do personagem.
1. Variáveis e componentes.  
![](../imagens/estruturas/blueprint_component_bp_vida.png)

<a name="22"></a>
## 4.2 Implementando o objeto *BP_Elementos*
Este objeto serve como referência na cena para posicionamento de ojetos *BP_Vida*.
1. Variáveis e componentes.   
![](../imagens/estruturas/blueprint_component_bp_elementos.png)
- Observe que a variável **Posicao** é do tipo vector e te a propriedade **Show 3D Widget** esta habilitada para facilitar o posicionamento do elemento na cena.  
![](../imagens/estruturas/blueprint_vetor_widget.png)

<a name="43"></a>
## 4.3 Logíca da carga dos dados.
Para cada elemento do vetor *Posicao* é implementado um objeto do tipo BP_vida nas coordenadas de vetor.   
![](../imagens/estruturas/blueprint_getdatatable.png)

- **Get data Table Row** - Tenta recuperar uma linha da **DataTable** por meio de texto em **RowName**.  
No exemplo a linha recuparada deve coincidir com uma variável passada como parâmetro.

- Para cada objeto adicionado na cena são definidas propriedades.    
![](../imagens/estruturas/blueprint_spawn_bp_vida.png)

***
## Referências
- [Data Driven Gameplay Elements](https://docs.unrealengine.com/en-US/InteractiveExperiences/DataDriven/index.html)
- [Get Data Table Row](https://docs.unrealengine.com/en-US/BlueprintAPI/Utilities/GetDataTableRow/index.html)

***
## Tags
[Blueprint](https://myerco.github.io/unreal-engine/ue4_blueprint/blueprint.html), [Unreal Engine](https://myerco.github.io/unreal-engine/ue4_blueprint/index.html), [CafeGeek](https://myerco.github.io/unreal-engine/)
