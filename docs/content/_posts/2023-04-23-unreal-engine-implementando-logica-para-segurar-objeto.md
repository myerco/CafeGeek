---
title: "Implementando a lógica para segurar um objeto com Unreal Engine"
categories:
  - Unreal Engine
tags:
  - lógica
  - blueprint
---

Em alguns jogos o personagem pode realizar uma serie de interações com os objetos na cena, como por exemplo segurar, arremessar, guardar ou simplesmente retornar o objeto para o lugar onde estava.

A seguir vamos apresentar uma lógica para segurar o objeto, manter preso ao personagem e arremessá-lo.

{% include iframe.html
    src="https://blueprintue.com/render/5tm72obo/"
    title="Cafegeek - Segurando um objeto da cena"
    caption="Lógica para segurar e manter preso um objeto do tipo Grab na frente do jogador."
    ref="https://blueprintue.com/render/5tm72obo/"
%}

## Variáveis

**fRadius** - Determina o raio de detecção que o personagem emite;

**fInteractionDistance** - Determina a distância de detecção do personagem em relação ao objeto;

**Holding** - Caso o personagem esteja segurando um objeto está variável será `true`;

## Componentes

LocationToLook -  Arrow Component que é usado como referência as coordenadas do objeto.
