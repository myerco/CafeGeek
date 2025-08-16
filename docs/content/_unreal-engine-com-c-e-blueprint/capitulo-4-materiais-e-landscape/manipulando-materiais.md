---
title: Manipulando materiais
excerpt: Neste capítulo iremos manipular os materiais com lógica de script Blueprint e construir funções para utilizar dentro dos materiais.
categories: 
  - "unreal-engine-com-c-e-blueprint"
  - "capitulo-4-materiais-e-landscape"
permalink: /:categories/:title
date: 2024-06-02T08:48:05-04:00
last_modified_at: 2023-03-28T08:48:05-04:00
order: 402
tags:
  - Materiais
---

## 1. O que é Material Instance?

A **Mateial Instance** ou Instanciação de Material é uma maneira de criar um Material pai, que pode então ser usado como base para fazer uma ampla variedade de Materiais filhos de aparência diferente. Para obter essa flexibilidade, o **Material Instancing** usa um conceito chamado herança: as propriedades do pai são fornecidas aos seus filhos. Aqui está um exemplo de herança de material em ação.

### 1.1. Convertendo nós em parâmetros

Convertemos os nós em parâmetros para que possam ser manipulados posteriormente pelo **Material Instance**. Para que possamos exemplificar segue abaixo os passos.

Vamos criar o material base com o nome `M_Base_Master`.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-base-master.webp"
    alt="Figura: Blueprint Material Instance."
    caption="Lógica do material com cor base e normal."
%}

Agora vamos converter os nós em parâmetros.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-convert-parameter.webp"
    alt="Figura: Material Instance - Convert to Parameter."
    caption="Convertendo valores em parâmetros."
%}

Resultado dos material com parâmetros.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-base-master-with-parameter.webp"
    alt="Figura: Material Instance -  Usando parâmetros."
    caption="Resultado do nó com parâmetros."
%}

Em seguida definimos os seguintes atributos nos parâmetros:

- `Parameter name` - Nome para o parâmetro que representa o input do material.
- `Group` - Usado para agrupar os parâmetros por um determinado valor ou tema.

Sugestão de grupos:

- Texture Parameter Values: Diffuse,NormalMap, Rough Texture;

- Scalar Parameter Values:  Valores escalares;

- Metallic, Roughness: Vector Parameter Values : Color (R,G,B,A), UVTiling(R,G,B,A).

### 1.2. Criando Material Instance

Selecione o material `M_Base_Master` ou outro material e com o botão direito acione o menu de contexto e escolha `Create Material Instance`.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-create-material-instance.webp"
    alt="Figura: Material Instance - Create material instance."
    caption="Usamos um material como base."
%}

***

## 2. Editor de material Instance

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-instance-editor.webp"
    alt="Figura: Material Instance instance editor."
    caption="Material Instance e suas propriedades."
%}

- `Details` - Propriedades e acesso aos parâmetros;

- `Parameter Groups` - Grupo definido nos parâmetros dentro do material pai.
  Os parâmetros estão agrupados por tipo de valor Texture, Scalar e Vector;

- `Parent` - Material pai.

***

## 3. Switch Parameter

`StaticSwitchParameter` recebe duas entradas e gera a primeira, se o valor do parâmetro for verdadeiro, e a segunda, caso contrário. No exemplo abaixo se o parâmetro for verdadeiro a multiplicação com a cor pode ser realizada caso contrário o textura não é multiplicada.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-switch-parameter.webp"
    alt="Figura: Blueprint Material Instance - Switch Parameter."
    caption="Figura: O nó Switch Parameters é visível no Editor de Material Instance e permite alternar entre dois valores, no exemplo acima o parâmetro é chamado de ColorSwitch."
%}

***

## 4. Organizando parâmetros e definindo valor máximo e mínimo

Podemos organizar os parâmetros agrupando com a opção `Group` do nó e com `Sort Priority` ordenamos a visualização.

### 4.1. Group

No exemplo abaixo criamos os grupos:

- Base Parameters;

- Multipliers;

- UV Tiling.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-parameter-group.webp"
    alt="Figura: Material Instance - Parameter Group."
    caption="Criando vários parâmetros agrupados."
%}

### 4.2. Valor Mínimo e Máximo

Podemos limitar os valores mínimo e máximo que podem ser passados como parâmetro utilizando a opção `Slider`.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-slider-min-max.webp"
    alt="Figura: Material Instance - Slider Min e Slider Max."
    caption="Limitando os valores dos parâmetros utilizando Slider Min en Max."
%}

***

## 5. Implementando Material Instance com Blueprint

Podemos manipular os objetos do tipo material com scripts Blueprint possibilitando implementar objetos com materiais mais interativos, como por exemplo, um objeto que muda de cor ao click do mouse.

Para exemplificar utilizaremos o Level Blueprint interagindo com um objeto na cena.

Selecione um ator no `View Port` e adicione uma referência no `Open Level Blueprint` com a opção `Create a Reference to`, em seguida vamos utilizar o nó `Create Dynamic Material Instance` para criar uma associação de um material com a nossa lógica.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-bp-create-material-instance-set.webp"
    alt="Figura: Material - Create material instance set."
    caption="Acima a lógica para criar o material instance e alterar a textura."
%}

- `Create Dynamic Material Instance` - Cria um Material Instance dinâmico que pode ser modificado durante a *gameplay*. O material referenciado em `Source Material` deve conter parâmetros;

- `Set Texture Parameter Value` - Atualiza o valor do parâmetro informado em `Parameter Name`, é do tipo textura;

- `Set Scalar Parameter Value` - Atualiza o valor escalar do parâmetro informado em `Parameter Name` com o valor `value`;

- `Set Vector Parameter Value` - Atualiza o vetor do parâmetro informado em `Parameter Name` com o valor `value`.

{% include iframe.html
    src="https://blueprintue.com/render/eckgsjqu/"
    title="Cafegeek - Material and Blueprint #2 Create Dynanmic Material Instance and Set"
    caption="Acima a lógica para criar o material instance e alterar a textura."
    ref="https://blueprintue.com/blueprint/eckgsjqu/"
%}

{% include iframe.html
    src="https://blueprintue.com/render/3oeee-_g/"
    title="Cafegeek - Material and Material #1 Click Objects and Change Color"
    ref="https://blueprintue.com/blueprint/3oeee-_g/"
%}

O script habilita o click do mouse e quando selecionado um objeto o evento customizado Change Color e acionado.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-bp-level-blueprint-call-event.webp"
    alt="Figura: Blueprint Material - Open Level blueprint call event."
    caption="Figura: No Level Blueprint implemente a lógica para chamar o Evento ChangeColor."
%}

***

## 6. Parameter Global

Podemos definir parâmetros globais, que afetem todo o jogo, para que os materiais possam referenciar parâmetros escalares e vetoriais.

**Informação:** É uma ferramenta poderosa que os artistas podem usar para obter dados globais em muitos materiais de uma só vez. Ele também pode ser usado para gerar efeitos por nível, como quantidade de neve, quantidade de destruição, umidade, etc., que, de outra forma, exigiria a configuração de valores de parâmetros individuais em muitas instâncias de materiais diferentes em seu nível.
{: .notice--info}

Criando parâmetros globais utilizamos a opção do menu de contexto `Materials & Textures > Material Parameter Gobal`.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-menu-parameter-collection.webp"
    alt="Figura: Material - Parameter Collections."
    caption="Menu de contexto > Materials & Textures > Material Parameter Collection"
%}

Depois de criado o objeto podemos adicionar e editar valores do tipo `Scalar` e `Vector` no objeto `Parameter Collection`. Exemplo de nome `MPC_Base`.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-edit-parameter-collection.webp"
    alt="Figura: Material - Editor de Parameter Collection."
    caption="Parâmetros do material."
%}

No Editor de Materiais usamos o menu de contexto (RMB) e escolhemos a opção `Material Parameter Collection` selecionando o objeto criado com os parâmetros em `Collection`, `MPC_Base`.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-collectionparameter.webp"
    alt="Figura: Material - Collection Parameter."
    caption="Chamando no editor de materiais um Collection Parameter."
%}

***

## 7. Material Function

**Material Functions** ou Funções de material são pequenos fragmentos de códigos gráficos de material que podem ser salvos em pacotes e reutilizados em vários materiais, em outras palavras são funções de programação. Seu objetivo é agilizar o processo de criação de material, dando acesso instantâneo a redes comumente usadas de nós materiais.
São compostas basicamente por entradas de parâmetros e saída de dados.

Utilizamos o menu de Contexto `Material & Textures` > `Material Function` para criar as funções;

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-function-output.webp"
    alt="Figura: Blueprint Material Function - Output."
    caption="Figura: O editor da lógica da função criada utilizando os nós Texture Sample e um Vector 3 e redirecionando para a saída Output Result."
%}

- Perceba que a função apresenta um nó de resultado;

- Podemos adicionar parâmetros para a função.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-function-call.webp"
    alt="Figura: Blueprint Material Function Call."
    caption="Figura: Chamamos a função dentro do editor de materiais usando a função MaterialFunctionCall."
%}

### 7.1. MakeMaterialAttribute

O nó `Make Material Attributes` une vários atributos. Isso é útil ao criar suas próprias funções de camada de material, pois você terá acesso a todos os atributos padrão para sua saída. Isso também pode ser usado para configurações de material complexas nas quais você deseja definir mais de um tipo de material e combiná-los, tudo dentro de um material.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-function-makematerialattributes.webp"
    alt="Figura: Material - MakeMaterialAttribute."
    caption="Podemos juntar vários atributos utilizando MakeMaterialAttribute possibilitando construir camadas ou Layers e utilizar no retorno da função."
%}

Ao usar a nó é necessário configurar o nó resultado do material principal com `Use Material Attribute` para `True`.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-use-material-attributes.webp"
    alt="Figura: Blueprint Material - Nó resultado com Use Material Attribute true."
    caption=" Devemos configurar o nó resultado do material com Use Material Attribute true."
%}

### 7.2. BreakMaterialAttribute

É o inverso de `MakeMaterialAttribute` possibilitando a separação dos atributos recebidos por uma função.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-breakmaterialattributes.webp"
    alt="Figura: Material - BreakMaterialAttribute."
    caption="Expandindo os atributos do material."
%}

### 7.3. Parâmetros dentro das funções

Podemos adicionar parâmetros utilizamos o nó  `Input <Type>`.

Criamos o nó e ajustamos as propriedades do parâmetro:

- `Input Name` - Nome do parâmetro;

- `Input Type` - Lista de tipos (VectorX, Scalar, Texture);

- `Preview value` - Valores que podem ser usados como padrão;

- `Use Preview value as Default` - Usa os valores configurados como padrão.

Chamamos a função dentro de um material expression utilizando:

- F + LMB;

- LMB e digitando `Function/MaterialFunctionCall`.

Logo em seguida configuramos a propriedade `Material Function`.

### 7.4. Adicionando Propriedades em uma material Function

Usamos `SetMaterialAttributes` para adicionar outros atributos no resultado de uma função que retorna um conjunto de atributos.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-setmaterialattributes.webp"
    alt="Figura: Material - SetMaterialAttributes."
    caption="A função MF_Base retorna um conjunto de atributos e com o nó SetMaterialAttributes podemos adicionar ou alterar os atributos vindos da função."
%}

### 7.5. BlendMaterialAttribute

Usamos `BlendMaterialAttribute` para misturar duas funções, implementaremos duas funções, MF_Base e MF_Rust_Base, para exemplificar [Make Material Attributes](https://docs.unrealengine.com/5.0/en-US/material-attributes-expressions-in-unreal-engine/).

Função com a cor da base.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-function-base.webp"
    alt="Figura: Função MF_Base."
    caption="A função MF_Base implementa detalhes básicos de um material."
%}

Função para utilizar na mistura.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-function-rust.webp"
    alt="Figura: MF_Rust_Base."
    caption="Nova função com a mesma lógica trocando as texturas."
%}

Fazendo a mistura das duas funções.

{% include imagelocal.html
    src="unreal/materiais/unreal-engine-material-function-blend-attributes.webp"
    alt="Figura: Material Function BlendMaterialAttribute."
    caption="O parâmetro Alpha controla como os valores são misturados."
%}
