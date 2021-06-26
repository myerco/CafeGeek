---
title: Material Instance
description: Teste
tags: [Unreal Engine, Materiais, material instance, material]
---

[CafeGeek](http://CafeGeek.eti.br)  / [Desenvolvimento de jogos utilizando Unreal Engine](http://cafeGeek.eti.br/unreal_engine/index.html)

# Material Instance
Neste capitulo vamos apresentar o objeto *Material Instance* que flexibiliza a implementação de materiais no Unreal Engine.

## Índice
1. [O que é Material Instance?](#1)
    1. [Convertendo nós em parâmetros](#1.1)
    1. [Criando Material Instance](#1.2)
1. [Editor de material Instance](#2)
1. [Atividades](#3)
    1. [Atividade 1](#3.1)

<a name="1"></a>
## 1. O que é Material Instance?
A *Mateial Instance* ou Instanciação de Material é uma maneira de criar um Material pai, que pode então ser usado como base para fazer uma ampla variedade de Materiais filhos de aparência diferente. Para obter essa flexibilidade, o *Material Instancing* usa um conceito chamado herança: as propriedades do pai são fornecidas aos seus filhos. Aqui está um exemplo de herança de material em ação.

<a name="1.1"></a>
### 1.1 Convertendo nós em parâmetros
Convertemos os nós em parâmetros para que possam ser manipulados posteriormente pelo *Material Instance*.    

Para que possamos exemplificar segue abaixo os passos.

1. Criamos uma copia de *M_Base* com o nome *M_Base_parametros*.
1. Convertendo nós em parâmetros.    
  ![ue4_material_no_convert_parameter](imagens/materiais/ue4_material_no_convert_parameter.jpg)     
  *Figura: Material convert to Parameter*
1. Definimos os seguintes atributos nos parâmetros:
  - **Parameter name** - Escolha um nome para o parâmetro que representa o input do material.
  - **Group** - Usado para agrupar os parâmetros por um determinado valor ou tema.
    Sugestão de grupos:
      - Texture Parameter Values.
        - Diffuse,NormalMap, Rough Texture
      - Scalar Parameter Values.
        - Metallic, Roughness
      - Vector Parameter Values.
        - Color (R,G,B,A), UVTiling(R,G,B,A)

<a name="1.2"></a>
### 1.2 Criando Material Instance
Selecione o material *M_Base_parametros* ou outro material e com o botão direito acione o menu de contexto e escolha **Create Material Instance**.     

![ue4_material_create_material_instance](imagens/materiais/ue4_material_create_material_instance.jpg)   
  *Figura: Create material instance*

<a name="2"></a>
## 2. Editor de material Instance
![ue4_material_instance_editor](imagens/materiais/ue4_material_instance_editor.jpg)     
  *Figura: Material instance editor*

- **Details** - Propriedades e acesso aos parâmetros.
- **Basico** - Grupo definido nos parâmetros dentro do material pai.
- **Color, Metallic, Roughness, Specular** - Parâmetros criados dentro do material pai. Podem ser alterados e até salvos.
- **Parent** - Material pai.

<a name="3"></a>
## 3. ATIVIDADES
<a name="3.1"></a>
### 16.1 Atividade 1
#### Regras
1. Regra 1
1. Regra 2
#### Desafio      
1. Desafio 1

***

## Referências
- [Creating and Using Material Instances](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Materials/HowTo/Instancing/index.html)
- [Material Parameter Collections](https://docs.unrealengine.com/en-US/RenderingAndGraphics/Materials/ParameterCollections/index.html)
- [Material Parameter Collections](https://www.unrealengine.com/en-US/blog/material-parameter-collections)
