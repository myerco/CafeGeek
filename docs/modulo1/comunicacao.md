# Comunicação entre Blueprint

> [1. Conceito ](#1)  
> [2. Comunicação direta ](#1)  
> [3. Blueprint Interface](#2)  
> [4. Event Dispacher](#3)  

## 1. Conceito
- Um meio para objetos individuais separados interagirem uns com os outros
  - Imagine um Light Blueprint e um LightSwitch Blueprint
    Como você faria um trabalhar com o outro?

- Útil para fazer coisas como:
  - Transmitindo um evento para vários ouvintes
  - Dizendo a um objeto específico para fazer algo
  - Consultando outro objeto por
    Status
    Estado
    Valores de propriedade
    Valores variáveis
    Resultados
- UE4 não tem como apenas “enviar um sinal amplo para todos”
    Curiosidades: fizemos isso há muito tempo na UE2, mas não é muito eficiente
- A comunicação sempre envolverá o seguinte:
  - Um projeto de envio
  - Pelo menos um Receiving Blueprint
- A comunicação sempre exigirá uma referência em algum ponto
  - Em outras palavras, uma das partes - o remetente ou o receptor - deve tomar conhecimento da outra
  - Isso ocorre porque, como afirmado acima, não existe um sistema de comunicação de amplo espectro
- Toda a comunicação do Blueprint é unilateral
  - Blueprints podem enviar dados para frente e para trás, mas requer que ambos os Blueprints configurem seus próprios caminhos individuais de comunicação
  - As consultas são possíveis, mas são iniciadas pelo remetente (ainda unidirecional)    

## 1. Acesso direto


## Referências
- [Types of Blueprints](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/Types/index.html)
- [Blueprint interface](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/Types/Interface/index.html)
