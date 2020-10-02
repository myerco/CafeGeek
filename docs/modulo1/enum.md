[Home](https://myerco.github.io/unreal-engine) / [Estrutura](https://myerco.github.io/unreal-engine/1-estrutura.html)
# Enums - Enumerarions
### Dificuldade :

|  |   |   |    |   |
|---|---|---|---|---|
| 1 | **2**  | 3  | 4   | 5  |

Neste capitulo serão apresentados Enumerações (*Enumeration*)
Os tópicos apresentados :
1. Conceito e implementação;
1. Declaração
1. Método Get para arrays;
1. Get utilizando uma variável como índice;
1. Último índice e a quantidade de elementos do array;
1. Removendo elementos;
1. Listando todos os elementos utilizando for;
1. Usando o comando *find*;
1. Comando remove *index*
1. Limpando o *clear*;
1. Atualiza o *array* nome clássicos com dados do *array* de nome;
1. Contando elementos dentro de um *array*;

***
## 1. Conceito e implementação
- Uma enumeração é um tipo definido pelo usuário que consiste em um conjunto de constantes integrais nomeadas que são conhecidas como enumeradores.

Exemplo:  
enum cores = { vermelho,amarelo, azul, verde = 20, preto}  

## 2. Criando
1. No cabeçalho do arquivo adicione UENUM() para especificar, ou crie o arquivo EnumName.h.
2. Utilize o código abaixo:
```c+
#include "Status.generated.h"

UENUM()
enum class Status
{
  Stopped     UMETA(DisplayName = "Stopped"),
  Moving      UMETA(DisplayName = "Moving"),
  Attacking   UMETA(DisplayName = "Attacking"),
};
```
1. Use o UENUM() na UCLASS()
```c+
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = Status)
TEnumAsByte<Status> status;
```
