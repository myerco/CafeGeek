# Eventos, funções e macros
1. *Collapse Nodes*;
1. Eventos;
1. Eventos customizados;
1. Entrada de eventos;
1. Funções;
1. Funções com parâmetros e saída;
1. Macros;

#  Módulos

### Eventos, funções e macros

## Conceito de Módulos

# Eventos (**Events**)
Os eventos são nós chamados a partir do código do jogo para iniciar a execução de uma rede individual dentro do /*EventGraph*. Eles permitem que os *Blueprints* executem uma série de ações em resposta a certos eventos que ocorrem dentro do jogo, como quando o jogo começa, quando um nível é reiniciado ou quando um jogador sofre dano.

Os eventos podem ser acessados dentro do *Blueprints* para implementar novas funcionalidades ou para substituir ou aumentar a funcionalidade padrão. Qualquer número de eventos pode ser usado em um único *EventGraph*; embora apenas um de cada tipo possa ser usado.

- Evento de dano  
![](../imagens/modulos/modulo5.png)

- Chamando o evento
![](../imagens/modulos/modulo6.png)

###Evento são MÉTODOS!!!
Os métodos são procedimentos ou funções que realizam as ações próprias do objeto. Assim, os métodos são as ações que o objeto pode realizar. Tudo o que o objeto faz é através de seus métodos, pois é através dos seus métodos que um objeto se manifesta, através deles que o objeto interage com os outros objetos.

class Actor {
  void BeginPlay()
  void Tick()
  void BeginOverlap()
  void Identificar delegate
}

class ExemploEventos : public Actor {

}

```c++

void AProjeto::BeginPlay() {
  Super::BeginPlay();
}

void AProjeto::DestruaMundoNerd(World* mundo ) {
   destroy();
}

// Called every frame
void AProjeto::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

}

```
->Java,C++, C#

# Funções (**functions**)
- Pedaços de código que retornam algum valor
para o programa que executou a chamada.
- São mini programas com as características de alocação de memória, estruturas internas de código e variáveis locais.
- Podem receber parâmetros externos.  
- Funções não suportam o nó **Delay** ou eventos de temporização.
- Funções podem ter ser replicadas
em jogos multiplayer.
- Não aceitam eventos customizados.

Exemplo:  
**C++**   
```c
// Função com parâmetros
void CalculoIMC(float pPeso, float pAltura) {
  // Variável local
  float resultado;
  resultado =  (pAltura * pAltura) / pPeso;
  return = resultado
}  
```
**Blueprint**   
![Function](../imagens/modulos/modulo1.png)

## Macros
- São essencialmente código colapsado.
- São basicamente um modelo *Template* de código ou nós.
- Não suportam o nó **Delay**.
- Não aceitam eventos customizados.
- Não podem ser replicados em jogos multiplayer.

Exemplo:  
**C++**
```c++
  #define MIN(a,b) (((a)<(b)) ? a : b)

  std::cout << "The minimum is " << MIN(42, 8) << endl;
```

**Blueprint**

![Function](../imagens/modulos/modulo2.png)

## Colapse Nodes
- Organização de código, escondendo nós da estrutura principal.
- Aceitam parâmetros de entrada e saída.  

![Function](../imagens/modulos/modulo4.png)


## Executando a função e a macros  
![Function](../imagens/modulos/modulo3.png)



### Referências

- [Best Practices](https://docs.unrealengine.com/en-US/Engine/Blueprints/BestPractices/index.html)
- [Managing complexity in Blueprints](https://www.unrealengine.com/en-US/blog/managing-complexity-in-blueprints?sessionInvalidated=true)
- [Events](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Events/index.html)
