# HUD - Interface com o jogador

>1. [Implementando menu](#1)
>1. [Componentes do menu](#1)
>1. [HUD do jogador](#1)
>1. [Quit game](#1)
>1. [Salvando o jogo](#1)

## Delta Time
É o tempo entre cada frame

Frame: Um quadro ou imagem apresentada, uma animação é composta por vários frames.

Exemplos 1:
Frames 	1 	2 	3 	4 	5 	6 	7 	8 	9 	10
Delta 	1 	2 	3 	4 	5 	6 	7 	8 	9

10 Fps = 10 frames a cada segundo.
1 segundo / 9 = 0,1 segundo ou 100ms.

100 FPS = 100 frames a cada segundo
1 segundo /99 = 0,01 segundo ou 10ms

30 FPS = 1/29 , 0.034 34ms
60 FPS = 1/59 , 0.017 17ms

Exemplos 2:
Centímetros 	1 	2 	3 	4 	5 	6 	7 	8 	9 	10
Segundos 	1 	2 	3 	4 	5 	6 	7 	8 	9 	10

1 cm/s = Total: 10s
Centímetros 	1 	2 	3 	4 	5 	6 	7 	8 	9 	10
Frame 	1 	2 	3 	4 	5 	6 	7 	8 	9 	10

1 cm/frame = total: ?

100FPS = 1 cm/10ms = total:0,1s
10FPS = 1 cm/100ms = total:1s



## Referências
- [](https://en.wikipedia.org/wiki/Delta_timing)
- [](https://answers.unrealengine.com/questions/38798/how-to-use-delta-time.html)
- [](https://www.fabricadejogos.net/posts/tutorial-entendo-o-que-o-deltatime/)
- [](http://teclab.net.br/fps-vs-capacidade-humana/)
