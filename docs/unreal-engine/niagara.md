---
title: Niagara
description: Niagara.
tags: [Unreal Engine,actor,atores]
layout: page
---

[Niagara Visual Effects](https://docs.unrealengine.com/en-US/Engine/Niagara/index.html)

## Estrutura
1. Módulos
Os módulos funcionam em um paradigma de gráfico - você pode criar módulos com HLSL no Editor de scripts usando um gráfico de nó visual. Módulos são equivalentes aos comportamentos de *Cascade*. Módulos comunicam dados comuns, encapsulam comportamentos e empilham juntos.
1. Emissores  
Os emissores funcionam em um paradigma de pilha - eles servem como contêineres para módulos e podem empilhar juntos para criar vários efeitos. Um emissor tem um único propósito, mas também é reutilizável. Os parâmetros são transferidos até o nível do emissor dos módulos, mas você pode modificar módulos e parâmetros no emissor.

1. Sistemas  
Emissores, sistemas funcionam em um paradigma de pilha e também funcionam com uma linha de tempo do *Sequencer* - que você pode usar para controlar como os emissores no sistema se comportam. Um sistema é um contêiner para emissores. O sistema combina esses emissores em um efeito. Ao editar um sistema no Editor Niagara, você pode modificar e substituir qualquer parâmetro, módulo ou emissor que esteja no sistema.

1. Definir ambiente
- [x] Floresta
- [ ] Cidade  

**Resposta:** Floresta definida pelo produtor

1. Documento
- [x] Introdução
- [ ] Resumo da história
- [ ] Modelo de controle
- [ ] HUD
