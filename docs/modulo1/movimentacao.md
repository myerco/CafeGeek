[Home](https://myerco.github.io/unreal-engine) / [Unreal](https://myerco.github.io/unreal-engine/unreal.html)
# Movimentação

## Índice
> 1. [Mapeamento de ações](#1)
> 1. [Malhas](#2)
> 1. [Classes)](#3)
> 1. [Posição e coordenadas](#4)
> 1. [Herança](#5)
> 1. [Adicionando atores](#5)
> 1. [Listando atores](#6)
> 1. [Mapeamento de ações](#7)
> 1. [Movimentação de peão **Pawn**](#8)

<a name="1"></a>
## 1. Mapeamentos de ações
- Estrutura
![Game Mode Quick Reference](https://docs.unrealengine.com/Images/Gameplay/Framework/QuickReference/GameFramework.webp)

- **Menu->Project->Input**  
![](../imagens/actor/actor16.png)

- Mapeamento de um evento a um botão
 - Valores 0 e 1
 - Exemplo:
  1. Tecla Espaço = Pulo
  1. Tecla Enter = Disparo
  1. Tecla C  = Agachar
- Mapeamento de Movimentação nos eixos
 - Mapeamento de um evento a um botão ou a um eixo de controle
 - É atualizado constantemente
 - Escala de valores
 - Exemplo:
  1. Tecla W = MoverDireita
  1. Tecla D = MoverEsquerda


## GameMode
 - Definido por *level*
 - Pode ser para definido para o todo o projeto;
 - Menu **Project**  
 ![](../imagens/actor/actor15.png)

1. PlayerController
 - Controlador do jogador definido por *Level*
 ![](#)

## 8. Movimentação de peão *Pawn*
- Componentes  
![](../imagens/actor/actor17.png)
- Habilitando a entrada de comandos   
![](../imagens/actor/actor18.png)
- Implementando movimentação com teclado  
![](../imagens/actor/actor19.png)
- Captura as coordenadas do ator para que possamos utilizar os métodos de movimentação **Virar** e **OlhaCima**  
![](../imagens/actor/actor21.png)
- Movimentação utilizando mouse  
![](../imagens/actor/actor20.png)
- Controle de movimentação do ator (Classe) - Caso as opções *Use controller rotation pitch/Yaw* estiverem ativas (**true**) a cápsula do ator irá sem movimentar no seu próprio eixo.    
![](../imagens/actor/actor22.png)

- Controle de movimentação do braço que sustenta a câmera **SpringArm**  
- Quando verdadeiro *Use Pawn control Rotation* somente o braço com a câmera são movimentados.  
![](../imagens/actor/actor23.png)
- **Enumeration** para registro de poses/estados do personagem.    
![](../imagens/actor/actor24.png)

## Referências
- [PlayerInput](https://docs.unrealengine.com/en-US/Programming/Tutorials/PlayerInput/index.html)
- [Enabled Input](https://docs.unrealengine.com/en-US/Gameplay/HowTo/ActorInput/Blueprints/index.html)  
- [Mapeando de comandos](https://docs.unrealengine.com/en-US/Gameplay/Input/index.html)  
- [CharacterMovement](https://docs.unrealengine.com/en-US/Gameplay/HowTo/CharacterMovement/Blueprints/index.html)  
- [Create a Free camera pawn with custom inputs](https://isaratech.com/ue4-create-a-free-camera-pawn-with-custom-inputs/)
