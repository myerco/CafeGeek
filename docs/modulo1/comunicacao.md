# Comunicação entre Blueprint

> 1. [Conceito ](#1)  
> 1. [Preparando o ambiente de testes ](#1)  
> 1. [Comunicação direta ](#1)  
> 1. [Blueprint Interface](#2)  
> 1. [Event Dispacher](#3)  

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

## 2. Preparando o ambiente de testes
1. Crie um **Blueprint Actor** com os seguintes parâmetros para que funcione como controlador de objetos.
  1. Adicione e configure um Static Mesh
  1. Adicione e configure um Box Colision

1. Implemente a função para desligar e ligar a iluminação os objetos **Light Point** passados como parâmetro.  

![](../imagens/comunicacao/comunicacao1.png)    
1. Adicione a variável *Lampada* do tipo **Point Light** e configure **Instance Editable** para *true*.

![](../imagens/comunicacao/comunicacao2.png)      
1. Adicione dois objetos **Light Point**.
1. Em um dos objetos de iluminação adicione a **tag** *lampada*.


## 3. Acesso direto
Usaremos o evento **OnBeginOverLap** para alterar o estado da lâmpada de ligado para desligado acessando diretamente o objeto pois o mesmo é passado como parâmetro.  

![](../imagens/comunicacao/comunicacao3.png)      

## 4. Utilizando CAST
Usaremos o evento **OnEndOverlap** para ler todos os objetos que tem a **tag** *lampada* da cena e carregar em um array de objetos. Para cada objeto será executado o comando **Cast** informando o **type** para ter acesso a todas a funcionalidades do objeto.

![](../imagens/comunicacao/comunicacao4.png)      

## 5. Utilizando Interface

## 6. Dispacher





## Referências
- [Types of Blueprints](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/Types/index.html)
- [Blueprint interface](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/UserGuide/Types/Interface/index.html)
