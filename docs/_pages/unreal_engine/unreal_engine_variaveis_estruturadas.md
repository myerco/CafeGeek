---
title: Variáveis estruturadas
excerpt: Structure, é um tipo de dados definido pelo usuário disponível no Unreal Engine em C++ e Blueprint, neste capitulo vamos explorar estes objetos.  
permalink: /pages/unreal_engine/variaveis_estruturadas
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true  
---

## 1. O que são variáveis do tipo Structure?

**Structure**, são estruturas de dados também conhecidas como **registros**, permitem que um usuário combine itens de dados de (possivelmente) diferentes tipos de dados sob um único nome. Em outras palavras, é uma variável que contém outros variáveis de diferentes tipos.  

Podem ser utilizadas para definir propriedades de um elemento do jogo como por exemplo os personagens.

***

## 2. Structure e Class

Em **C++**, uma estrutura é realmente a mesma coisa que uma **Class**, exceto por algumas diferenças sintáticas.  

Por exemplo, **Structs** em **C++** padronizam suas variáveis de membro como públicas por padrão, enquanto as classes têm variáveis privadas por padrão.

### 2.1. C++ Struct

```cpp
struct Character {
    int velocidade;
    int forca;
    bool correndo;
};
```

### 2.2. C++ Class

```cpp
class Character {
    int Velocidade;
    int Forca;
    bool Correndo;
};
```

#### 2.2.1. C++ Struct Unreal

```cpp
USTRUCT([Specifier, Specifier, ...])
struct FStructName
{
    GENERATED_BODY()

    int32 Velocidade;
    int32 Forca;

    UPROPERTY()
    bool Correndo;
};
```

#### 2.2.2. C++ Class Unreal

```cpp
UCLASS()
class YOURMODULE_API APlayerCharacter: public ACharacter
{
  GENERATED_BODY()
public:
  UFUNCTION(BlueprintCallable, Category="Player")
  bool EstaCorrendo();

private:
        bool Correndo = false;
        int32 Velocidade=100;
        int32 Forca = 100;
};
```

***

## 3. Criando variáveis do tipo Structure com Blueprint

Neste passo vamos criar o objeto *SJogador* do tipo `Structure` para exemplificar o uso das variáveis utilizando o menu de contexto `Blueprints` > `Structure`.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_menu_structure.webp"
    alt="Figura: Menu de contexto Blueprints > Structure."
    caption="Cria o objeto do tipo Structure."
%}

### 3.1. Definindo variáveis dentro da estrutura

A seguir vamos adicionar variáveis dentro do da estrutura criada.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_variable.webp"
    alt="Figura: Editor de Structure."
    caption="Podemos adicionar e salvar novos tipos de dados."
%}

1. Nome do tipo `Name` - Armazena o nome do jogador;

1. Vida do tipo `Float` - Total de vida do jogador.;

1. Forca do tipo `Float` - Total de força do jogador;

1. Nível do tipo `Integer` - O Nível que o jogador se encontra;

1. Imagem do tipo `Texture2D/References` - Armazena imagem 2d que representa o jogador;

1. Personagem do tipo `Character/Class` - Armazena a classe de objeto do personagem do jogador.

### 3.2. Acessando as variáveis

Para acessar as variáveis que estão dentro da objeto do tipo `Structure` vamos utilizar `Break Structure`.  

{% include imagelocal.html
    src="unreal/estruturas/blueprint_break_structure.webp"
    alt="Figura: Exemplo de Break Structure."
    caption="Usamos esse nó para acessar as variáveis dentro da estrutura."
%}

### 3.3. Exemplo do uso de variáveis Structure

Para exemplificar a utilização de variáveis `Structure` vamos implementar um level onde os elementos serão construídos dinamicamente, para tal vamos utilizar uma *Array* de objetos do tipo `Point Light Component` para que possam ser adicionados na cena no momento de construção do objeto.

#### 3.3.1. Criando o objeto SControleLuzes

{% include imagelocal.html
    src="unreal/estruturas/blueprint_variable_2.webp"
    alt="Figura: Blueprint - Exemplo do objeto SControleLuzes."
    caption="Figura: Blueprint - Exemplo do objeto SControleLuzes."
%}

#### 3.3.2. Lógica para construir os elementos na cena

1. Crie um `level` utilizando o modelo `default`;

1. Implemente um `Blueprint Actor` com o nome `BP_ControleLuzes`;

1. Adicionar as variáveis :

    - **Luzes** - *Array* de tipo `Point Light Component`;

    - **ControLuzes** - *Array* de tipo `SControleLuzes`;

    - **Total_luzes** : Integer.

1. Na construção do objeto (*Construction Script*) adicionamos elementos `Point light component` na cena e logo em seguida no array *Luzes*.  

{% include imagelocal.html
    src="unreal/estruturas/blueprint_loop_array_structures.webp"
    alt="Figura: Blueprint - Lógica que adiciona os elementos em um array do mesmo tipo (PointLightComponent)."
    caption="Figura: Blueprint - Lógica que adiciona os elementos em um array do mesmo tipo (PointLightComponent)."
%}

1. Ao terminar o primeiro `loop` reconstruímos o *array* de controle *ControLuzes* e o percorremos em conjunto com o array *luzes* para configurar as propriedades dos elementos.  

{% include imagelocal.html
    src="unreal/estruturas/blueprint_loop_set_struct.webp"
    alt="Figura: Blueprint - Lógica que altara as propriedades dos objetos do array."
    caption="Figura: Blueprint - Lógica que altara as propriedades dos objetos do array."
%}

1. Adicione o elemento **BP_ControleLuzes** na cena para visualizar as luzes sendo construídas.

Neste capitulo vamos explorar os objetos do tipo **Data tables** que são basicamente tabelas de dados disponíveis para os desenvolvedores e são definidas por tipos *Structure*.  

***

## 4. O que são Data Tables?

**Data Tables** são estruturas de dados com vários tipos de variáveis agrupados e podem ser utilizadas para armazenamento de forma estática de informações dos personagens e suas características, recursos do jogo como espadas, escudos, magias, propriedades do jogo como níveis, dificuldades e pontuação.

***

## 5. Criando um objeto do tipo Data Table

Vamos implementar o **SElementos** do tipo *Structure* que servirá como base para o objeto `Data Table`.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_structure.webp"
    alt="Figura: Blueprint - Structure SElementos."
    caption="Figura: Blueprint - Structure SElementos."
%}

Definimos as seguintes variáveis.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_structure_variable_3.webp"
    alt="Figura: Blueprint - Criando as variáveis dentro da estrutura."
    caption="Figura: Blueprint - Criando as variáveis dentro da estrutura."
%}

Utilizando o menu de contexto escolha `Miscellaneous` > `Data Table`.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_datatable_menu.webp"
    alt="Figura: Blueprint - Menu de contexto Miscellaneous > Data Table."
    caption="Figura: Blueprint - Menu de contexto Miscellaneous > Data Table."
%}

Logo em seguida devemos definir a estrutura de dados da tabela utilizando o variável **SElementos** do tipo `Structure`.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_datatable_row_structure.webp"
    alt="Figura: Blueprint - Definindo a estrutura da tabela usando Structure e Data Table."
    caption="Figura: Blueprint - Definindo a estrutura da tabela usando Structure e Data Table."
%}

*DTElementos* do tipo `Data Tables`.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_datatables.webp"
    alt="Figura: Blueprint - Data Table."
    caption="Figura: Blueprint - Data Table."
%}

***

## 6. Inserindo dados no objeto do tipo Data Table

Ao abrir o objeto de Data Table é apresentado um editor para manipulação de dados, inserindo, removendo e alterando as linhas.  
A coluna **RowName** não pode ser repetida, funcionado como identificador único da linha.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_datatables_editor.webp"
    alt="Figura: Blueprint - Exemplo do editor para inserir linhas na tabela."
    caption="Figura: Blueprint - Exemplo do editor para inserir linhas na tabela."
%}

***

## 7. Importando dados de um arquivo csv

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
    src="unreal/estruturas/blueprint_datatables_artifact.webp"
    alt="Figura: Blueprint - Definindo Structure para carregar os dados."
    caption="Figura: Blueprint - Definindo Structure para carregar os dados."
%}

Em seguida implemente o objeto TArtifact do tipo `Data Table` e com o botão direito do mouse em cima do objeto e selecione `Reimport`, logo em seguida escolha o arquivo csv:

{% include imagelocal.html
    src="unreal/estruturas/blueprint_datatables_import.webp"
    alt="Figura: Blueprint - Data Table Reimport."
    caption="Figura: Blueprint - Data Table Reimport."
%}

Os dados serão importados e na aba `Data Table Details` os parâmetros de importação serão apresentados.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_datatables_details.webp"
    alt="Figura: Blueprint - Data Table Details."
    caption="Figura: Blueprint - Data Table Details."
%}

***

## 8. Exemplo de utilização de Data Table

Para este exemplo vamos implementar um objeto para automaticamente adicionar outros objetos (Vida) na cena, a posição dos objetos pode se controlada com um vetor de coordenadas.  

### 8.1. Implementando o objeto BP_Vida

Este objeto deverá estar na cena para interação com o jogador pois pode aumentar o valor da vida do personagem com as seguintes variáveis e componentes.  

{% include imagelocal.html
    src="unreal/estruturas/blueprint_component_bp_vida.webp"
    alt="Figura: Blueprint - Exemplo do objeto BP_vida."
    caption="Figura: Blueprint - Exemplo do objeto BP_vida."
%}

### 8.2. Implementando o objeto BP_Elementos

Este objeto serve como referência na cena para posicionamento de objetos *BP_Vida* com as seguintes variáveis e componentes.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_component_bp_elementos.webp"
    alt="Figura: Blueprint - Exemplo do objeto de posicionamento dos objetos vida."
    caption="Figura: Blueprint - Exemplo do objeto de posicionamento dos objetos vida."
%}

Observe que a variável **Posicao** é do tipo vector e tem a propriedade `Show 3D Widget` habilitada para facilitar o posicionamento do elemento na cena.  

{% include imagelocal.html
    src="unreal/estruturas/blueprint_vetor_widget.webp"
    alt="Figura: Blueprint - Show 3D Widget."
    caption="Figura: Blueprint - Show 3D Widget."
%}

O Vetor **Posicao** na cena.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_actor_posicao.webp"
    alt="Figura: Blueprint - Posição do ator na cena."
    caption="Figura: Blueprint - Posição do ator na cena."
%}

Detalhes das coordenadas.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_actor_posicao_detalhe.webp"
    alt="Figura: Blueprint - Coordenadas."
    caption="Figura: Blueprint - Coordenadas."
%}

### 8.3. Logica da carga dos dados

Para cada elemento do vetor *Posicao* é implementado um objeto do tipo BP_vida nas coordenadas de vetor.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_getdatatable.webp"
    alt="Figura: Blueprint - Carregando dados utilizando GetDataTableRow."
    caption="Figura: Blueprint - Carregando dados utilizando GetDataTableRow."
%}

- `Get data Table Row` - Tenta recuperar uma linha da `DataTable` por meio de texto em **RowName**.  No exemplo a linha recuperada deve coincidir com uma variável passada como parâmetro;

Para cada objeto adicionado na cena são definidas propriedades.

{% include imagelocal.html
    src="unreal/estruturas/blueprint_spawn_bp_vida.webp"
    alt="Figura: Blueprint - Criando objetos usando os dados do Data Table."
    caption="Figura: Blueprint - Criando objetos usando os dados do Data Table."
%}
