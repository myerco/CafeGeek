---
title: Estruturas de programação no Unreal Engine
description: Neste capítulo serão descritas as estruturas de armazenamento, manipulação e fluxo da lógica de programação.
tags: [Unreal Engine,blueprint,programação,estruturas,variáveis,c++]
layout: page
---

***

[O que são variáveis?](#o-que-s-o-vari-veis-)

[Variáveis no Unreal Engine](#vari-veis-no-unreal-engine)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Tipos de Variáveis](#tipos-de-vari-veis)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Declarando variáveis](#declarando-vari-veis)

[Métodos Get e Set](#m-todos-get-e-set)

[Tratamento e armazenamento de texto no Unreal Engine](#tratamento-e-armazenamento-de-texto-no-unreal-engine)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Concatenando textos usando a função Append](#concatenando-textos-usando-a-fun--o-append)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Procurando texto dentro de uma string](#procurando-texto-dentro-de-uma-string)

[Variáveis do tipo numéricas Integer e Float](#vari-veis-do-tipo-num-ricas-integer-e-float)

[Armazenando valores lógicos com Boolean](#armazenando-valores-l-gicos-com-boolean)

[Controle de acesso a variáveis](#controle-de-acesso-a-vari-veis)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Variáveis Privadas](#vari-veis-privadas)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Variáveis Públicas](#vari-veis-p-blicas)

[O que são estruturas de controle ou fluxo?](#o-que-s-o-estruturas-de-controle-ou-fluxo-)

[Estruturas de fluxo condicional](#estruturas-de-fluxo-condicional)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Controle de fluxo com Branch (if)](#controle-de-fluxo-com-branch--if-)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Switch Nodes](#switch-nodes)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Sequenciamento de fluxo com Sequence](#sequenciamento-de-fluxo-com-sequence)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Flip Flop](#flip-flop)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Gate e Multi Gate](#gate-e-multi-gate)

[Estruturas de repetição](#estruturas-de-repeti--o)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[For Loop](#for-loop)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[While Loop](#while-loop)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Do N](#do-n)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Do once](#do-once)

[O que são variáveis do tipo array?](#o-que-s-o-vari-veis-do-tipo-array-)

[Declarando arrays e acessando os seus elementos](#declarando-arrays-e-acessando-os-seus-elementos)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Método Get para arrays](#m-todo-get-para-arrays)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Get utilizando uma variável como índice](#get-utilizando-uma-vari-vel-como--ndice)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Último índice e a quantidade de elementos do array](#-ltimo--ndice-e-a-quantidade-de-elementos-do-array)

[Percorrendo arrays](#percorrendo-arrays)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Listando todos os elementos utilizando For](#listando-todos-os-elementos-utilizando-for)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Usando o comando Find](#usando-o-comando-find)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Contando elementos dentro de um array](#contando-elementos-dentro-de-um-array)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Percorrendo e atualizando dados](#percorrendo-e-atualizando-dados)

[Removendo elementos do array](#removendo-elementos-do-array)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Removendo utilizando Remove](#removendo-utilizando-remove)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Removendo passando uma variável como parâmetro](#removendo-passando-uma-vari-vel-como-par-metro)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Removendo utilizando nó Remove Index](#removendo-utilizando-n--remove-index)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Limpando o array com Clear](#limpando-o-array-com-clear)

[O que são Enums?](#o-que-s-o-enums-)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Criando Enums no Unreal Engine](#criando-enums-no-unreal-engine)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Exemplos de uso A lâmpada](#exemplos-de-uso---a-l-mpada)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Exemplos de uso A pedra das emoções](#exemplos-de-uso---a-pedra-das-emo--es)
