---
title: Implementando Material Instance com Unreal Engine
description: Neste capitulo vamos apresentar o objeto Material Instance que flexibiliza a implementação de materiais no Unreal Engine.
tags: [unreal engine, material instance, material]
categories: Unreal Engine
author: 
- Cafegeek
layout: post
sidebar:  
  - title: "UNREAL ENGINE COM C++ E BLUEPRINT"
    image: /imagens/unreal/logos/unreal_engine.webp
    nav: "dev_unreal"
date: 2022-09-21 
---

***

- [1. O que é Material Instance?](#1-o-que-é-material-instance)
  - [1.1. Convertendo nós em parâmetros](#11-convertendo-nós-em-parâmetros)
  - [1.2. Criando Material Instance](#12-criando-material-instance)
- [2. Editor de material Instance](#2-editor-de-material-instance)
- [3. Switch Parameter](#3-switch-parameter)
- [4. Organizando parâmetros e definindo valor máximo e mínimo](#4-organizando-parâmetros-e-definindo-valor-máximo-e-mínimo)
  - [4.1. Group](#41-group)
  - [4.2. Valor Mínimo e Máximo](#42-valor-mínimo-e-máximo)

***

## 1. O que é Material Instance?

***

A **Mateial Instance** ou Instanciação de Material é uma maneira de criar um Material pai, que pode então ser usado como base para fazer uma ampla variedade de Materiais filhos de aparência diferente. Para obter essa flexibilidade, o **Material Instancing** usa um conceito chamado herança: as propriedades do pai são fornecidas aos seus filhos. Aqui está um exemplo de herança de material em ação.

### 1.1. Convertendo nós em parâmetros

Convertemos os nós em parâmetros para que possam ser manipulados posteriormente pelo **Material Instance**. Para que possamos exemplificar segue abaixo os passos.

Vamos criar o material base com o nome `M_Base_Master`.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_base_master.webp"
    alt="Figura: Blueprint Material Instance - Base Master."
    caption="Figura: Lógica do material com cor base e normal."
%}

Agora vamos converter os nós em parâmetros.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_convert_parameter.webp"
    alt="Figura: Blueprint Material Instance - Convert to Parameter."
    caption="Figura: Convertendo valores em parâmetros."
%}

Resultado dos material com parâmetros.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_base_master_with_parameter.webp"
    alt="Figura: Blueprint Material Instance -  Resultado do material com parâmetros."
    caption="Figura: Resultado do nó com parâmetros."
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

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_create_material_instance.webp"
    alt="Figura: Blueprint Material Instance - Create material instance."
    caption="Figura: Criando um objeto Material Instance."
%}

## 2. Editor de material Instance

***

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_instance_editor.webp"
    alt="Figura: Blueprint Material Instance instance editor."
    caption="Figura: Editor de Material Instance e suas propriedades."
%}

- `Details` - Propriedades e acesso aos parâmetros;

- `Parameter Groups` - Grupo definido nos parâmetros dentro do material pai.
  Os parâmetros estão agrupados por tipo de valor Texture, Scalar e Vector;

- `Parent` - Material pai.

## 3. Switch Parameter

***

`StaticSwitchParameter` recebe duas entradas e gera a primeira, se o valor do parâmetro for verdadeiro, e a segunda, caso contrário. No exemplo abaixo se o parâmetro for verdadeiro a multiplicação com a cor pode ser realizada caso contrário o textura não é multiplicada.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_switch_parameter.webp"
    alt="Figura: Blueprint Material Instance - Switch Parameter."
    caption="Figura: O nó Switch Parameters é visível no Editor de Material Instance e permite alternar entre dois valores, no exemplo acima o parâmetro é chamado de ColorSwitch."
%}

## 4. Organizando parâmetros e definindo valor máximo e mínimo

***

Podemos organizar os parâmetros agrupando com a opção `Group` do nó e com `Sort Priority` ordenamos a visualização.

### 4.1. Group

No exemplo abaixo criamos os grupos:

- Base Parameters;

- Multipliers;

- UV Tiling.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_parameter_group.webp"
    alt="Figura: Blueprint Material Instance - Parameter Group."
    caption="Figura: Criando vários parâmetros agrupados."
%}

### 4.2. Valor Mínimo e Máximo

Podemos limitar os valores mínimo e máximo que podem ser passados como parâmetro utilizando a opção `Slider`.

{% include imagebase.html
    src="unreal/materiais/unreal_engine_material_slider_min_max.webp"
    alt="Figura: Blueprint Material Instance - Slider Min e Slider Max."
    caption="Figura: Limitando os valores dos parâmetros utilizando Slider Min en Max."
%}
