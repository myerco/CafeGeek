---
title: Materiais e Blueprint
description: Podemos manipular os objetos do tipo material com blueprint.
tags: [Unreal Engine,Materiais, material Function, material, blueprint]
layout: page
---

<a name="8"></a>
## CAPÍTULO 9 - Materiais e Landscape

Neste capítulo iremos manipular os materiais com lógica de script Blueprint e construir funções para utilizar dentro dos materiais.


&nbsp;&nbsp;[9.4 Materiais Blueprint](#9.4)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9.4.1 Parameter Global](#9.4.1)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9.4.2 Material Function](#9.4.2)

***

<a name="9.4"></a>
## 9.4 Materiais e Blueprint
Podemos manipular os objetos do tipo material com scripts Blueprint.

1. Utilizaremos o `Level Blueprint` para exemplificar;

2. Adicione uma referência do ator selecionado no `View Port` no `Open Level Blueprint` com a opção `Create a Reference to `;

3. Lógica para criar o material e a textura: `Create material instance > Set Texture Parameter Value`.

    ![Figura: Blueprint Material - Create material instance set.](imagens/materiais/ue4_material_bp_create_material_instance_set.webp "Figura: Blueprint Material - Create material instance set.")   

    > Figura: Blueprint Material - Create material instance set.

    - `Create Dynamic Material Instance` - Cria um Material Instance dinâmico que pode ser modificado durante a *gameplay*;

    - `Set Texture Parameter Value` - Atualiza o valor do parâmetro informado em `Parameter Name`, é do tipo textura;

    - `Set Scalar Parameter Value` - Atualiza o valor escalar do parâmetro informado em `Parameter Name` com o valor `value`;

    - `Set Vector Parameter Value` - Atualiza o vetor do parâmetro informado em `Parameter Name` com o valor `value`.

4. No Level Blueprint implemente a lógica para chamar o Evento **MudaCorEvento**.

    ![Figura: Blueprint Material - Open Level blueprint call event.](imagens/materiais/ue4_material_bp_level_blueprint_call_event.webp "Figura: Blueprint Material - Open Level blueprint call event.")   

    > Figura: Blueprint Material - Open Level blueprint call event.

<a name="9.4.1"></a>
### 9.4.1 Parameter Global
Podemos definir parâmetros globais para que os materiais possam referenciar parâmetros escalares e vetoriais.

""É uma ferramenta poderosa que os artistas podem usar para obter dados globais em muitos materiais de uma só vez. Ele também pode ser usado para gerar efeitos por nível, como quantidade de neve, quantidade de destruição, umidade, etc., que, de outra forma, exigiria a configuração de valores de parâmetros individuais em muitas instâncias de materiais diferentes em seu nível."

1. Criando parâmetros globais utilizamos a opção do menu de contexto `Materials & Textures > Material Parameter Gobal`.

    ![Figura: Blueprint Material - Parameter Collections.](imagens/materiais/unreal_engine_material_menu_parameter_collection.webp "Figura: Blueprint Material - Parameter Collections.")

    > Figura: Blueprint Material - Parameter Collections.

2. Podemos adicionar e editar valores do tipo `Scalar` e `Vector` no objeto `Parameter Collection`.

    ![Figura: Blueprint Material - Editor de Parameter Collection.](imagens/materiais/unreal_engine_material_edit_parameter_collection.webp "Figura: Blueprint Material - Editor de Parameter Collection.")

    > Figura: Blueprint Material - Editor de Parameter Collection.

3. No Editor de Materiais usamos a opção `Material Parameter Collection` e selecionamos o objeto criado com os parâmetros em `Collection`.

    ![Figura: Blueprint Material - Collection Parameter.](imagens/materiais/unreal_engine_material_collectionparameter.webp "Figura: Blueprint Material - Collection Parameter.")

    > Figura: Blueprint Material - Collection Parameter.

<a name="9.4.2"></a>
### 9.4 2Material Function

**Mateial Functions** ou Funções de material são pequenos fragmentos de códigos gráficos de material que podem ser salvos em pacotes e reutilizados em vários materiais, em outras palavras são funções de programação. Seu objetivo é agilizar o processo de criação de material, dando acesso instantâneo a redes comumente usadas de nós materiais.    
São compostas basicamente por entradas de parâmetros e saída de dados.

1. Utilizamos o menu de Context `Material & Textures` > `Material Function`;

2. Abaixo o editor da lógica da função criada utilziando um nó  `Texture Sample` e um `Vector 3`.

    ![Figura: Blueprint Material Function - Output.](imagens/materiais/unreal_engine_material_function_output.webp "Figura: Blueprint Material Function - Output.")

    > Figura: Blueprint Material Function - Output.

    - Perceba que a função apresenta um nó de resultado;

    - Podemos adicionar parâmetros para a função.

4. Chamamos a função dentro do editor de materiais usando a função `MaterialFunctionCall`.

    ![Figura: Bluepritn Material Function Call.](imagens/materiais/unreal_engine_material_function_call.webp "Figura: Bluepritn Material Function Call.")

    > Figura: Bluepritn Material Function Call.

5. Podemos juntar vários atributos utilizando `MakeMaterialAttribute` possibilitando construir camadas ou `Layers` e utilizar no retorno da função.

    ![Figura: Blueprint Material - MakeMaterialAttribute.](imagens/materiais/unreal_engine_material_function_makematerialattributes.webp "Figura: Blueprint Material - MakeMaterialAttribute.")

    > Figura: Blueprint Material - MakeMaterialAttribute.

6. Ao usar a nó é necessário configurar o nó resultado do material principal com `Use Material Attribute` para `True`.

    ![Figura: Blueprint Material - Nó resultado com Use Material Attribute true.](imagens/materiais/unreal_engine_material_use_material_attributes.webp "Figura: Blueprint Material - Nó resultado com Use Material Attribute true.")

    > Figura: Blueprint Material - Nó resultado com Use Material Attribute true.

7. `BreakMaterialAttribute` é o inverso de `MakeMaterialAttribute` possibilitando a separação dos atributos recebidos por uma função.

    ![Figura: Blueprint Material - BreakMaterialAttribute.](imagens/materiais/unreal_engine_material_breakmaterialattributes.webp "Figura: Blueprint Material - BreakMaterialAttribute.")

    > Figura: Blueprint Material - BreakMaterialAttribute.
