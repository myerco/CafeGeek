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

# Eventos
->Java,C++, C#

# Funções (**functions**)
- Pedaços de código que retornam algum valor
para o programa que executou a chamada.
- São mini programas com as características de alocação de memória, estruturas internas de código e variáveis locais.
- Podem receber parâmetros externos.  
- Funções não suportam o nó **Delay** ou eventos de temporização.
- Funções podem ter ser replicadas
em jogos multiplayer.

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
- Suportam o nó **Delay**.
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
# Evento


### Referências

[Best Practices](https://docs.unrealengine.com/en-US/Engine/Blueprints/BestPractices/index.html)
