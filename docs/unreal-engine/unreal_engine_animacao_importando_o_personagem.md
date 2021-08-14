---
title: Animação - Importando o personagem
description: Neste capitulo vamos importar o personagem e suas animações para dentro do Unreal Engine.
tags: [Unreal Engine, Animação]
layout: page
---

Neste capitulo vamos importar o personagem baixado anteriormente e suas animações para dentro do Unreal Engine.

## Índice
1. [Importando o personagem](#1-importando-o-personagem)

## 1 Importando Mesh e Skeletal
1. Crie a pasta `/Projeto/Characteres/Mutant/Mesh`;
1. Copie o arquivo `mutant.fbx` para a pasta criada no passo anterior;
1. Importe o arquivo com a opção `Import All`:

   ![Figura: FBX import options](imagens/animacao/unreal_engine_fbx_import_options.jpg)

   *Figura: FBX import options*

## 2. Importando animações
1. Crie a pasta `/Projeto/Characteres/Mutant/animations`;
1. Copie os arquivos para pasta criada no passo anterior:
 - Mutant_Run.fbx;
 - Mutant_Idle.fbx;
 - Mutant_Walking.fbx.
1. Desmarque a opção `Import Mesh` para que a malha não seja importada novamente;
1. Escolha o esqueleto do personagem com `SKeleton`.

## 3. Vídeo aula
[![Importando personagem](http://img.youtube.com/vi/6ZLatHfD7P8/0.jpg)](https://youtu.be/6ZLatHfD7P8 "Aula 03")

*Vídeo: Aula 03 - Importando personagem*


#### Referências
- [FBX Import Options Reference](https://docs.unrealengine.com/en-US/Engine/Content/Importing/FBX/ImportOptions/index.html)   
- [Animations Tools](https://docs.unrealengine.com/en-US/Engine/Animation/Persona/Modes/index.html)  
- [AnimGraph](https://docs.unrealengine.com/en-US/Engine/Animation/AnimBlueprints/AnimGraph/index.html)
