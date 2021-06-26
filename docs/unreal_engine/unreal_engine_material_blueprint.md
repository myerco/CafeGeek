---
title: Materiais e Blueprint
description: Podemos manipular os objetos do tipo material com blueprint.
tags: [Unreal Engine,Materiais, material Function,material, blueprint]
---

[CafeGeek](http://CafeGeek.eti.br)  / [Desenvolvimento de jogos utilizando Unreal Engine](http://cafeGeek.eti.br/unreal_engine/index.html)

# Materiais e Blueprint
Neste capítulo iremos manipular os materiais com lógica de script Blueprint.

## Índice
1. [Materiais e Blueprint](#12)
1. [Parameter Global](#13)
1. [Material Function](#14)

<a name="1"></a>
## 1. Blueprint
Podemos manipular os objetos do tipo material com scripts Blueprint.

Utilizaremos o *Level Blueprint* para exemplificar.

1. Lógica para criar o material e a textura: Create material instance->Set Texture Parameter Value
![ue4_material_bp_create_material_instance_set](imagens/materiais/ue4_material_bp_create_material_instance_set.jpg)   

  *Figura: Blueprint create material instance set*

1. No Level Blueprint implemente a lógica para chamar o Evento **MudaCorEvento**.
![ue4_material_bp_level_blueprint_call_event](imagens/materiais/ue4_material_bp_level_blueprint_call_event.jpg)   
  *Figura: Material Open Level blueprint call event*

<a name="2"></a>
## 2. Parameter Global
Podemos definir parâmetros globais para que os materiais possam referenciar parâmetros escalares e vetoriais.
> É uma ferramenta poderosa que os artistas podem usar para obter dados globais em muitos materiais de uma só vez. Ele também pode ser usado para gerar efeitos por nível, como quantidade de neve, quantidade de destruição, umidade, etc., que, de outra forma, exigiria a configuração de valores de parâmetros individuais em muitas instâncias de materiais diferentes em seu nível.

- Material Parameter->GetCollectionParameter.       
  ![MatPC](https://cdn2.unrealengine.com/blog/MaterialsTexturesScreen1-421x613-1142134069.png)

  *Figura: Parameter Collections - Unreal Engine*

<a name="3"></a>
## 3. Material Function
**Mateial Functions** ou Funções de material são pequenos fragmentos de códigos gráficos de material que podem ser salvos em pacotes e reutilizados em vários materiais, em outras palavras são funções de programação. Seu objetivo é agilizar o processo de criação de material, dando acesso instantâneo a redes comumente usadas de nós materiais.    
São compostas basicamente por entradas de parâmetros e saída de dados.

Input Parameter -> Output Result

<a name="16"></a>
## 16 ATIVIDADES
<a name="16.1"></a>
### 16.1 -
#### Regras
1. -
1. -

#### Desafio      
1. -

***

## Referências
- [Material Parameter Collections](https://www.unrealengine.com/en-US/blog/material-parameter-collections)
