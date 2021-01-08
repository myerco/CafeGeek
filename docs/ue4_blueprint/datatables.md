---
title: Data Tables
tags: [Unreal Engine,data tables]
---

[CafeGeek](https://myerco.github.io/unreal-engine)  / [Desenvolvimento de jogos utilizando Unreal Engine 4](https://myerco.github.io/unreal-engine/unreal.html)

# Data tables

<a name="3"></a>
## Conceito
*Data tables* são basicamente estruturas de tabelas de dados disponíveis para os desenvolvedores.  
Definimos variáveis do tipo *Structure* para definir a estrutura das tabelas.

## Criando data tables
1. Objeto *SElementos* do tipo *Structure*.  ![](../imagens/estruturas/estruturas7.png)
  - Variáveis :
  ![](../imagens/estruturas/estruturas9.png)

1. *DTElementos* do tipo *Data Tables*. ![](../imagens/estruturas/estruturas8.png)
- Menu *Miscellaneous/Data Table*

  ![](../imagens/estruturas/estruturas14.png)
- Devemos definir a estutura de dados da tabela.  
  ![](../imagens/estruturas/estruturas17.png)

- Os dados devem ser inseridos.  
![](../imagens/estruturas/estruturas10.png)

## Implementando o objeto *BP_Vida*
Este objeto deverá estar na cena para interação com o jogador.
  - Variáveis e componentes.  
  ![](../imagens/estruturas/estruturas11.png)

## Implementando o objeto *BP_Elementos*
Este objeto serve como referência na cena para posicionamento de ojetos *BP_Vida*.
  - Variáveis e componentes.

  ![](../imagens/estruturas/estruturas15.png)
  - Observe que a variável *Posicao* é do tipo vector e te a propriedade **Show 3D Widget** esta habilitada para facilitar o posicionamento do elemento na cena.

  ![](../imagens/estruturas/estruturas16.png)

## Implementando a carga dos dados.

  - Para cada elemento do vetor *Posicao* é implementado um objeto do tipo BP_vida nas coordenadas de vetor.

  ![](../imagens/estruturas/estruturas12.png)

  - **Get data Table Row** - Tenta recuperar uma linha da **DataTable** por meio de texto em **RowName**.
  No exemplo a linha recuparada deve coincidir com uma variável passada como parâmetro.

  - Para cada objeto adicionado na cena são definiddas propriedades.

![](../imagens/estruturas/estruturas13.png)



***
## Referências
- [Data Driven Gameplay Elements](https://docs.unrealengine.com/en-US/InteractiveExperiences/DataDriven/index.html)
- [Get Data Table Row](https://docs.unrealengine.com/en-US/BlueprintAPI/Utilities/GetDataTableRow/index.html)
