---
title: Estruturas de programação no Unreal Engine
description: Neste capítulo serão descritas as estruturas de armazenamento, manipulação e fluxo da lógica de programação.
tags: [Unreal Engine,blueprint,programação,estruturas,variáveis,c++]
layout: page
---

***

[O que são variáveis?](estruturas_de_programacao_no_unreal_engine.html#o-que-s-o-variáveis)

[Variáveis no Unreal Engine](estruturas_de_programacao_no_unreal_engine.html#variáveis-no-unreal-engine)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Tipos de Variáveis](estruturas_de_programacao_no_unreal_engine.html#tipos-de-variáveis)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Declarando variáveis](estruturas_de_programacao_no_unreal_engine.html#declarando-variáveis)

[Métodos Get e Set](estruturas_de_programacao_no_unreal_engine.html#m-todos-get-e-set)

[Tratamento e armazenamento de texto no Unreal Engine](estruturas_de_programacao_no_unreal_engine.html#tratamento-e-armazenamento-de-texto-no-unreal-engine)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Concatenando textos usando a função Append](estruturas_de_programacao_no_unreal_engine.html#concatenando-textos-usando-a-fun--o-append)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Procurando texto dentro de uma string](estruturas_de_programacao_no_unreal_engine.html#procurando-texto-dentro-de-uma-string)

[Variáveis do tipo numéricas Integer e Float](estruturas_de_programacao_no_unreal_engine.html#variáveis-do-tipo-num-ricas-integer-e-float)

[Armazenando valores lógicos com Boolean](estruturas_de_programacao_no_unreal_engine.html#armazenando-valores-l-gicos-com-boolean)

[Controle de acesso a variáveis](estruturas_de_programacao_no_unreal_engine.html#controle-de-acesso-a-variáveis)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Variáveis Privadas](estruturas_de_programacao_no_unreal_engine.html#variáveis-privadas)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Variáveis Públicas](estruturas_de_programacao_no_unreal_engine.html#variáveis-p-blicas)

[O que são estruturas de controle ou fluxo?](estruturas_de_programacao_no_unreal_engine.html#o-que-s-o-estruturas-de-controle-ou-fluxo-)

[Estruturas de fluxo condicional](estruturas_de_programacao_no_unreal_engine.html#estruturas-de-fluxo-condicional)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Controle de fluxo com Branch (if)](estruturas_de_programacao_no_unreal_engine.html#controle-de-fluxo-com-branch--if-)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Switch Nodes](estruturas_de_programacao_no_unreal_engine.html#switch-nodes)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Sequenciamento de fluxo com Sequence](estruturas_de_programacao_no_unreal_engine.html#sequenciamento-de-fluxo-com-sequence)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Flip Flop](estruturas_de_programacao_no_unreal_engine.html#flip-flop)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Gate e Multi Gate](estruturas_de_programacao_no_unreal_engine.html#gate-e-multi-gate)

[Estruturas de repetição](estruturas_de_programacao_no_unreal_engine.html#estruturas-de-repeti--o)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[For Loop](estruturas_de_programacao_no_unreal_engine.html#for-loop)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[While Loop](estruturas_de_programacao_no_unreal_engine.html#while-loop)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Do N](estruturas_de_programacao_no_unreal_engine.html#do-n)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Do once](estruturas_de_programacao_no_unreal_engine.html#do-once)

[O que são variáveis do tipo array?](estruturas_de_programacao_no_unreal_engine.html#o-que-s-o-variáveis-do-tipo-array-)

[Declarando arrays e acessando os seus elementos](estruturas_de_programacao_no_unreal_engine.html#declarando-arrays-e-acessando-os-seus-elementos)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Método Get para arrays](estruturas_de_programacao_no_unreal_engine.html#m-todo-get-para-arrays)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Get utilizando uma variável como índice](estruturas_de_programacao_no_unreal_engine.html#get-utilizando-uma-vari-vel-como--ndice)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Último índice e a quantidade de elementos do array](estruturas_de_programacao_no_unreal_engine.html#-ltimo--ndice-e-a-quantidade-de-elementos-do-array)

[Percorrendo arrays](estruturas_de_programacao_no_unreal_engine.html#percorrendo-arrays)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Listando todos os elementos utilizando For](estruturas_de_programacao_no_unreal_engine.html#listando-todos-os-elementos-utilizando-for)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Usando o comando Find](estruturas_de_programacao_no_unreal_engine.html#usando-o-comando-find)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Contando elementos dentro de um array](estruturas_de_programacao_no_unreal_engine.html#contando-elementos-dentro-de-um-array)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Percorrendo e atualizando dados](estruturas_de_programacao_no_unreal_engine.html#percorrendo-e-atualizando-dados)

[Removendo elementos do array](estruturas_de_programacao_no_unreal_engine.html#removendo-elementos-do-array)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Removendo utilizando Remove](estruturas_de_programacao_no_unreal_engine.html#removendo-utilizando-remove)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Removendo passando uma variável como parâmetro](estruturas_de_programacao_no_unreal_engine.html#removendo-passando-uma-vari-vel-como-par-metro)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Removendo utilizando nó Remove Index](estruturas_de_programacao_no_unreal_engine.html#removendo-utilizando-n--remove-index)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Limpando o array com Clear](estruturas_de_programacao_no_unreal_engine.html#limpando-o-array-com-clear)

[O que são Enums?](estruturas_de_programacao_no_unreal_engine.html#o-que-s-o-enums-)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Criando Enums no Unreal Engine](estruturas_de_programacao_no_unreal_engine.html#criando-enums-no-unreal-engine)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Exemplos de uso A lâmpada](estruturas_de_programacao_no_unreal_engine.html#exemplos-de-uso---a-l-mpada)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Exemplos de uso A pedra das emoções](estruturas_de_programacao_no_unreal_engine.html#exemplos-de-uso---a-pedra-das-emo--es)
