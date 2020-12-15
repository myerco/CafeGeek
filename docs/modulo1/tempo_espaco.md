# Temo e espaço

> [1. Causando dano com *Set Timer By Event*](#1)
> [1. *Time Line*](#1)
> [1. FPS e *Delta Time*](#1)
> [1. Configurando o *Frame Rate*](#1)
> [1. Vetores](#1)
> [1. Distância, Direção e movimentação](#1)
> [1. Ajustando o *Delta Time*](#1)   

## Delta Time
É o tempo entre cada frame.  
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


Timeline
1.Curves
2.Custon Curves
->Miscelanios->Curve
->Time->External->Curve
->BP->Timeline->SetVectorCurve
3.Loop
->BP->TimeLine->SetLooping
4.Length
->BP->Timeline->SetTimeLength
->BP->Timeline->GetTimeLength
5.Playback Position
->BP->Timeline->GetPlaybackPosition
6.Auto play
7.Ignore time dilation
8.Set timer by event e clear timer
->BP->SetTimerbyEvent
->BP-ClearAndInvalidateTimerByHandle
9.Set timer by function e Clear timer
->BP->SetTimerbyFunction
10. Delta time
->Conceito
->10 FPS = 1s/9fr =0.1 (100ms)
->Delta seconds = intervalo entre os quadros
->Habilitando console = Editor preferences->Open console command box (ao lado do P ´)
->Project settings->Use fixed frame rate
->Comando->stat fps
->Comando->t.MaxFPS 100 (Valor)
->Comando->stat unit
->Comando->stat game
11. FPS
->BP->Event Tick->PrintString(delta seconds)
->BP ->Get World Delta Seconds
12. Tick - movimento
13. Tick - velocidade constante

## Referências
- [Delta timing](https://en.wikipedia.org/wiki/Delta_timing)
- [How to use delta time](https://answers.unrealengine.com/questions/38798/how-to-use-delta-time.html)
- [Tutorial enentendo o que é o deltatime](https://www.fabricadejogos.net/posts/tutorial-entendo-o-que-o-deltatime/)
- [fps vs capacidade humana](http://teclab.net.br/fps-vs-capacidade-humana/)
