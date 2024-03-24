---
title: Colisão
excerpt: Neste capitulo será apresentado o efeito de colisão de objetos.
permalink: /unreal-engine-capitulo-1/colisao
last_modified_at: 2023-03-28T08:48:05-04:00
layout: single
order: 10
sidebar:
    nav: dev_unreal_1
toc: true  
categories:
  - Unreal Engine
tags:
  - Blueprint
  - Colisão
---

## 1. Collision Responses

**Collision Responses** e **Trace Responses** formam a base de como o Unreal Engine 4 lida com colisão e transmissão de raios durante o tempo de execução. Cada objeto que pode colidir recebe um tipo de objeto e uma série de respostas que definem como ele interage com todos os outros tipos de objeto. Quando ocorre um evento de colisão ou sobreposição, ambos (ou todos) os objetos envolvidos podem ser configurados para afetar ou serem afetados pelo bloqueio, sobreposição ou ignorando um ao outro. [Collision Overview](https://docs.unrealengine.com/4.27/en-US/InteractiveExperiences/Physics/Collision/Overview/)

**Trace Responses** funcionam basicamente da mesma maneira, exceto que o próprio rastreamento (*ray cast*) pode ser definido como um dos tipos de resposta de rastreamento, permitindo assim que os atores o bloqueiem ou ignorem com base em suas respostas de rastreamento.

## 2. Interações

Existem algumas regras a serem lembradas sobre como as colisões são tratadas:

- O bloqueio ocorrerá naturalmente entre dois (ou mais) Atores definidos como **Block** (Bloquear). No entanto, `Simulation Generates Hit Events` precisa ser habilitado para executar `Event Hit`, que é usado em Blueprints, `Destructible Actors`, `Triggers`, etc...

- Definir Atores para **Overlap** (Sobrepor) muitas vezes parecerá que eles ignoram uns aos outros e, sem Gerar Eventos de Sobreposição, eles são essencialmente os mesmos.

- Para que dois ou mais objetos de simulação bloqueiem um ao outro, ambos precisam ser configurados para bloquear seus respectivos tipos de objeto.

- Para dois ou mais objetos de simulação: se um for configurado para sobrepor um objeto e o segundo objeto for configurado para bloquear o outro, a sobreposição ocorrerá, mas não o bloqueio.

- Eventos de sobreposição, **Overlap**, podem ser gerados mesmo que um objeto Bloqueie outro, especialmente se estiver viajando em alta velocidade.

- Não é recomendado que um objeto tenha eventos de colisão e sobreposição. Embora seja possível, é necessário  manuseio manual.

- Se um objeto for configurado para ignorar e o outro for configurado para sobrepor, nenhum evento de sobreposição será disparado.

## 3. Exemplos comuns de interação de colisão

**Nota:** As interações a seguir pressupõem que todos os objetos tenham `Collision Enabled` definido como `Collision Enabled`, de modo que estejam configurados para colidir totalmente com tudo. Se a colisão estiver desabilitada, é como se ignorar tivesse sido definido para todas as `Collision Responses` .
{: .notice--info}

Para a seção a seguir, abaixo a configuração usada para explicar o que está acontecendo:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_setup.png"
    alt="Figura: Exemplo de colisão."
    caption="A esfera é um PhysicsBody e a caixa é WorldDynamic, e alterando suas configurações de colisão podemos obter uma série de comportamentos."
    ref="https://docs.unrealengine.com/4.27/en-US/InteractiveExperiences/Physics/Collision/Overview/"
%}

### 3.1. Colisão

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent.png"
    alt="Figura: Collision Overview."
    caption="Ao definir ambas as configurações de colisão para bloquear uma à outra, você obtém uma colisão, ótima para que os objetos interajam entre si."
%}

Configuração de colisão de esfera.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Sphere.png"
    alt="Figura: Configuração de colisão de esfera."
    caption="Neste caso, a esfera é um PhysicsBody e está configurada para bloquear WorldDynamic (que é o que é a parede)."
%}

Configuração de colisão de parede.

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Configuração de colisão de parede."
    caption="A parede é uma WorldDynamic e está configurada para bloquear os Atores PhysicsBody (que é o que a esfera é)."
%}

Nesse caso, a esfera e a parede simplesmente colidirão; nenhuma outra notificação da colisão ocorrerá.

### 3.2. Colisão e Simulação Geram Eventos de acerto

Apenas a colisão é útil e, em geral, o mínimo para interações físicas, mas se você quiser que algo relate, ele colidiu para que um **Blueprint** ou seção de código possa ser acionado:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideEvent.png"
    alt="Figura: Colisão de eventos."
    caption="Eventos de colisão."
%}

Configuração de colisão de esfera:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideEvent_Sphere.png"
    alt="Figura: Configuração de Colisão de uma esfera."
    caption="Parâmetros da colisão."
%}

Como no exemplo acima, a esfera é um `PhysicsBody` e está configurada para bloquear `WorldDynamic` (que é o que é a parede). No entanto, a esfera também habilitou `Simulation Generates Hit Event` para que acione um evento para si mesma sempre que colidir com algo.

Configuração de colisão de parede:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Configuração de Colisão da Parede."
    caption="Parâmetros da colisão."
%}

A parede é uma `WorldDynamic` e está configurada para bloquear os Atores `PhysicsBody` (que é o que a esfera é). Como a parede não está configurada para `Simulation Generates Hit Event` , ela não gerará um evento para si mesma.

Com a esfera definida como Simulação gera eventos de acerto, a esfera informará a si mesma que sofreu uma colisão. Ele irá disparar eventos como `ReceiveHit` ou `OnComponentHit` no **Blueprint** da esfera. Agora, se a caixa tivesse um evento de colisão, ela não dispararia porque nunca notificará a si mesma que aconteceu.

Além disso, um objeto que está relatando colisões rígidas relatará todas elas e relatórios de spam quando estiver apenas parado em algo, portanto, é melhor ter cuidado ao filtrar o que está colidindo em seu **Blueprint** ou no código.

## 4. Sobrepor e ignorar

Para todos os efeitos, *Overlap* (Sobrepor) e *Ignore* (Ignorar) funcionam exatamente da mesma forma, supondo que Gerar eventos de sobreposição esteja desativado. Nesse caso, a esfera está configurada para sobrepor ou ignorar a caixa:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_ignore.png"
    alt="Figura: Overlap and Ignore."
    caption="Sobrepor ou ignorar."
%}

Configuração das propriedades de colisão de esfera:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_OverlapNoEvent_Sphere.png"
    alt="Figura: Configuração de Colisão da  esfera."
    caption="Parâmetros da colisão."
%}

Aqui a esfera está configurada para se sobrepor,`Overlap`, aos `WorldDynamic Actors` (como nossa parede), mas não tem a opção Gerar Eventos de Sobreposição habilitado. No que diz respeito à esfera, ela não colidiu ou se sobrepôs a nada, efetivamente ignorou a parede.

Configuração das propriedades colisão de parede:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Configuração de colisão de parede."
    caption="Parâmetros da colisão."
%}

A parede é uma `WorldDynamic` e está configurada para bloquear,`Block`, os Atores `PhysicsBody` (que é o que a esfera é). Como dito acima, ambos os Atores precisam ser configurados para bloquear os respectivos tipos de objetos um do outro. Se não o fizerem, não colidirão.

## 5. Configuração das propriedades da colisão de esfera

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_ignore_sphere.png"
    alt="Figura: Collide ignore Sphere."
    caption="Figura: Collide ignore Sphere."
%}

Aqui a esfera está configurada para ignorar, `Ignore`, os Atores `WorldDynamic` (como nossa parede), e ela passará pela parede.

Configuração das propriedades de colisão de parede:

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideNoEvent_Box.png"
    alt="Figura: Collide No Event."
    caption="Parâmetros da colisão."
%}

A parede é uma `WorldDynamic` e está configurada para bloquear os Atores `PhysicsBody` (que é o que a esfera é). Como dito acima, ambos os Atores precisam ser configurados para bloquear, `Block`, os respectivos tipos de objetos um do outro. Se não o fizerem, não colidirão.

## 6. Sobrepor e gerar eventos de sobreposição

Ao contrário das colisões que podem disparar todos os quadros, os eventos de sobreposição são `ReceiveBeginOverlap` e `ReceiveEndOverlap`, que são disparados apenas nesses casos específicos.

**Informação:** Para que uma sobreposição ocorra, ambos os Atores precisam habilitar Gerar Eventos de Sobreposição. Isso é para desempenho. No caso em que tanto a Esfera quanto a Caixa desejam sobreposições quando movemos a Esfera ou a Caixa, fazemos uma consulta de sobreposição para ver se precisamos disparar algum evento.
{: .notice--info}

**Informação:** Se a caixa não quiser sobreposições, quando ela se mover, não faremos uma consulta de sobreposição. Mas agora poderíamos estar sobrepondo com a Esfera, e assim a Esfera precisaria marcar e verificar se há sobreposições em cada quadro caso alguém se movesse para eles.
{: .notice--info}

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_overlapEvent.png"
    alt="Figura: Evento overlap."
    caption="Evento de sobreposição."
%}

## 7. Colisão de esfera

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_OverlapEvent_Sphere.png"
    alt="Figura: Colisão da esfera."
    caption="Parâmetros da colisão."
%}

Aqui, a esfera está configurada para sobrepor, `Overlap`, os Atores `WorldDynamic` (como nossa parede), e ela gerará um evento para si mesma quando se sobrepuser a algo.

## 8. Colisão de parede

{% include image.html
    src="https://docs.unrealengine.com/4.27/Images/InteractiveExperiences/Physics/Collision/Overview/COL_collideOverLapEvent_Box.png"
    alt="Figura: Evento overlap no box."
    caption="Parâmetros da colisão."
%}

A parede é uma WorldDynamic e está configurada para bloquear, `Block`, os Atores `PhysicsBody` (que é o que a esfera é). Como dito acima, ambos os Atores precisam ser configurados para bloquear os respectivos tipos de objetos um do outro. Se não o fizerem, não colidirão. Mas, uma sobreposição ocorre aqui, e os eventos para a esfera e a caixa são disparados.

## 9. Colisão Simples versus Complexa

No **Unreal Engine**, você tem acesso a formas de colisão simples e complexas. Colisão Simples, `Simplex Collision`, são primitivos como cubos, esferas, cápsulas e cascos convexos. Colisão Complexa, `Complex Collsion`, é o `trimesh` de um determinado objeto. Por padrão, o **Unreal Engine** cria formas simples e complexas, então, com base no que o usuário deseja (consulta complexa versus consulta simples), o solucionador de física usará a forma correspondente para consultas de cena e testes de colisão. [Simple versus Complex Collision](https://docs.unrealengine.com/5.1/en-US/simple-versus-complex-collision-in-unreal-engine/)

## 10. Static Mesh e colisões

No painel `Static Mesh Editor > Details`, você pode encontrar as configurações de `Complex Collision` na categoria `Collision`.

{% include image.html
    src="https://docs.unrealengine.com/5.0/Images/making-interactive-experiences/Physics/collision/simple-vs-complex/StaticMeshSettingsCollisionComplexity.webp"
    alt="Figura: Staticmesh Settings Collision Complexity."
    caption="Configurando a colisão da Static Mesh."
%}

- `Project Default` :  Usa as configurações físicas do projeto, isso fará com que solicitações de colisão simples usem colisão simples e solicitações complexas usem colisão complexa; o comportamento "padrão".

- `Simple and Complex`:  Esse sinalizador permite a criação de formas simples e complexas, usando formas simples para consultas de cena regulares e testes de colisão e usando formas complexas (por poli) para consultas de cena complexas.

- `Use Simple Collision As Complex`:  Isso significa que, se uma consulta complexa for solicitada, o mecanismo ainda consultará formas simples; basicamente ignorando o trimesh. Isso ajuda a economizar memória, pois não precisamos preparar o trimesh e pode melhorar o desempenho se a geometria de colisão for mais simples.

- `Use Complex Collision As Simple`:  Isso significa que, se uma consulta simples for solicitada, o mecanismo consultará formas complexas; basicamente ignorando a simples colisão. Isso nos permite usar o trimesh para a colisão de simulação de física. Observe que, se você estiver usando `UseComplexAsSimple`, não poderá simular o objeto, mas poderá usá-lo para colidir com outros objetos simulados (simples).

Por exemplo, na imagem abaixo a cadeira à esquerda tem colisão simples, e quando o peão acima dela cai sobre ela, ele desliza para fora da grande superfície angulada que cobre o assento. No entanto; a cadeira à direita está usando `Use Complex Collision As Simple`, e quando o peão acima dele cair, ele pousará no assento da cadeira e permanecerá lá.

{% include image.html
    src="https://docs.unrealengine.com/5.0/Images/making-interactive-experiences/Physics/collision/simple-vs-complex/exImage.webp"
    alt="Figura: Simple vs Complex."
    caption="Comparando os tipos de colisão."
%}
