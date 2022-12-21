---
title: Manipulando materiais com Blueprint
description: Neste capítulo iremos manipular os materiais com lógica de script Blueprint e construir funções para utilizar dentro dos materiais.
tags: [Unreal Engine,Materiais, material Function, material, blueprint]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
date: 2022-09-21 
---

***

- [Implementando Material Instance com Blueprint](#implementando-material-instance-com-blueprint)
- [Parameter Global](#parameter-global)
- [Material Function](#material-function)
  - [MakeMaterialAttribute](#makematerialattribute)
  - [BreakMaterialAttribute](#breakmaterialattribute)
  - [Parâmetros dentro das funções](#parâmetros-dentro-das-funções)
  - [Adicionando Propriedades em uma material Function](#adicionando-propriedades-em-uma-material-function)
  - [BlendMaterialAttribute](#blendmaterialattribute)

***

## Implementando Material Instance com Blueprint

***

Podemos manipular os objetos do tipo material com scripts Blueprint possibilitando implementar objetos com materiais mais interativos, como por exemplo, um objeto que muda de cor ao click do mouse.

Para exemplificar utilizaremos o Level Blueprint interagindo com um objeto na cena.

Selecione um ator no `View Port` e adicione uma referência no `Open Level Blueprint` com a opção `Create a Reference to`, em seguida vamos utilizar o nó `Create Dynamic Material Instance` para criar uma associação de um material com a nossa lógica.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_bp_create_material_instance_set.webp"
    alt="Figura: Blueprint Material - Create material instance set."
    caption="Figura: Acima a lógica para criar o material instance e alterar a textura."
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
    ref="Link: <https://blueprintue.com/blueprint/3oeee-_g/>"
%}

O script habilita o click do mouse e quando selecionado um objeto o evento customizado Change Color e acionado.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_bp_level_blueprint_call_event.webp"
    alt="Figura: Blueprint Material - Open Level blueprint call event."
    caption="Figura: No Level Blueprint implemente a lógica para chamar o Evento ChangeColor."
%}

## Parameter Global

***

Podemos definir parâmetros globais, que afetem todo o jogo, para que os materiais possam referenciar parâmetros escalares e vetoriais.

> É uma ferramenta poderosa que os artistas podem usar para obter dados globais em muitos materiais de uma só vez. Ele também pode ser usado para gerar efeitos por nível, como quantidade de neve, quantidade de destruição, umidade, etc., que, de outra forma, exigiria a configuração de valores de parâmetros individuais em muitas instâncias de materiais diferentes em seu nível.

Criando parâmetros globais utilizamos a opção do menu de contexto `Materials & Textures > Material Parameter Gobal`.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_menu_parameter_collection.webp"
    alt="Figura: Blueprint Material - Parameter Collections."
    caption="Figura: Menu de contexto > Materials & Textures > Material Parameter Collection"
%}

Depois de criado o objeto podemos adicionar e editar valores do tipo `Scalar` e `Vector` no objeto `Parameter Collection`. Exemplo de nome `MPC_Base`.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_edit_parameter_collection.webp"
    alt="Figura: Blueprint Material - Editor de Parameter Collection."
    caption="Figura: Blueprint Material - Editor de Parameter Collection."
%}

No Editor de Materiais usamos o menu de contexto (RMB) e escolhemos a opção `Material Parameter Collection` selecionando o objeto criado com os parâmetros em `Collection`, `MPC_Base`.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_collectionparameter.webp"
    alt="Figura: Blueprint Material - Collection Parameter."
    caption="Figura: Blueprint Material - Chamando no editor de materiais um Collection Parameter."
%}

## Material Function

***

**Material Functions** ou Funções de material são pequenos fragmentos de códigos gráficos de material que podem ser salvos em pacotes e reutilizados em vários materiais, em outras palavras são funções de programação. Seu objetivo é agilizar o processo de criação de material, dando acesso instantâneo a redes comumente usadas de nós materiais.
São compostas basicamente por entradas de parâmetros e saída de dados.

Utilizamos o menu de Contexto `Material & Textures` > `Material Function` para criar as funções;

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_function_output.webp"
    alt="Figura: Blueprint Material Function - Output."
    caption="Figura: O editor da lógica da função criada utilizando os nós Texture Sample e um Vector 3 e redirecionando para a saída Output Result."
%}

- Perceba que a função apresenta um nó de resultado;

- Podemos adicionar parâmetros para a função.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_function_call.webp"
    alt="Figura: Blueprint Material Function Call."
    caption="Figura: Chamamos a função dentro do editor de materiais usando a função MaterialFunctionCall."
%}

### MakeMaterialAttribute

O nó `Make Material Attributes` une vários atributos. Isso é útil ao criar suas próprias funções de camada de material, pois você terá acesso a todos os atributos padrão para sua saída. Isso também pode ser usado para configurações de material complexas nas quais você deseja definir mais de um tipo de material e combiná-los, tudo dentro de um material.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_function_makematerialattributes.webp"
    alt="Figura: Blueprint Material - MakeMaterialAttribute."
    caption="Figura: Podemos juntar vários atributos utilizando MakeMaterialAttribute possibilitando construir camadas ou Layers e utilizar no retorno da função."
%}

Ao usar a nó é necessário configurar o nó resultado do material principal com `Use Material Attribute` para `True`.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_use_material_attributes.webp"
    alt="Figura: Blueprint Material - Nó resultado com Use Material Attribute true."
    caption="Figura: Devemos configurar o nó resultado do material com Use Material Attribute true."
%}

### BreakMaterialAttribute

É o inverso de `MakeMaterialAttribute` possibilitando a separação dos atributos recebidos por uma função.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_breakmaterialattributes.webp"
    alt="Figura: Blueprint Material - BreakMaterialAttribute."
    caption="Figura: Blueprint Material - BreakMaterialAttribute."
%}

### Parâmetros dentro das funções

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

### Adicionando Propriedades em uma material Function

Usamos `SetMaterialAttributes` para adicionar outros atributos no resultado de uma função que retorna um conjunto de atributos.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_setmaterialattributes.webp"
    alt="Figura: Blueprint Material - SetMaterialAttributes."
    caption="Figura: Blueprint Material - A função MF_Base retorna um conjunto de atributos e com o nó SetMaterialAttributes podemos adicionar ou alterar os atributos vindos da função."
%}

### BlendMaterialAttribute

Usamos `BlendMaterialAttribute` para misturar duas funções, implementaremos duas funções, MF_Base e MF_Mistura, para exemplificar [Make Material Attributes](https://docs.unrealengine.com/5.0/en-US/material-attributes-expressions-in-unreal-engine/).

Função com a cor da base.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_function_base.webp"
    alt="Figura: Material Function base."
    caption="Figura: Blueprint Material - A função MF_Base implementa detalhes básicos de um material."
%}

Função para utilizar na mistura.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_function_rust.webp"
    alt="Figura: Material Function Rust base."
    caption="Figura: Blueprint Material - Função rust."
%}

Fazendo a mistura das duas funções.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_function_blend_attributes.webp"
    alt="Figura: Material Function BlendMaterialAttribute."
    caption="Figura: Material Function BlendMaterialAttribute - O parâmetro Alpha controla como os valores são misturados."
%}
