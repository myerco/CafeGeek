### Dificuldade : **Nível 5**   

## 1. Conceito e implementação
- É um conjunto de variáveis do mesmo tipo agrupadas  
Exemplo:  
Números inteiros
a = ( 5,2,7,3,9)  
Números *float*  
a = ( 5.1,2.9,7.0,3.121,9.43)  
Números *String*  
s = ( 'Ana','José','Hugo','Hulda')

- Podemos representar os arrays da seguinte forma:

|valor|Ana   |José |Hugo   |Hulda|
|índice|  0 | 1  | 2  | 3  |

## 2. Declaração
- Em C++  

```c++
FString  pessoas[4] = { 'Ana','José','Hugo','Hulda'};
int  pessoas[3] = { 4,3,7};
```
- Blueprints

![Declarando array](../imagens/bp_array_1.png)

## 3. Método *Get* para *arrays*
Para acessar qualquer elemento dentro *array* é necessários utilizar o índice.  

- Em c++  

```C++
FString s = pessoa[0];
UE_LOG(LogTemp, Warning, TEXT("O nome é %s",*s);
```  

- Blueprints

![Declarando array](../imagens/bp_array_2.png)


## 4. Get utilizando uma variável como índice
![Declarando array](../imagens/bp_array_3.png)

## 4. Último índice e a quantidade de elementos do *array*
![Declarando array](../imagens/bp_array_4.png)

## 5. Removendo elementos
![Declarando array](../imagens/bp_array_5.png)

## 6. Listando todos os elementos utilizando *for*
![Declarando array](../imagens/bp_array_6.png)

## 7. Usando o comando *find*
![Declarando array](../imagens/bp_array_7.png)
## 8. Comando *remove index*
![Declarando array](../imagens/bp_array_8.png)
## 9. Comando *remove*
![Declarando array](../imagens/bp_array_9.png)
## 10. Limpando o *clear*
![Declarando array](../imagens/bp_array_10.png)
## 11. Atualiza o *array* **nome clássicos** com dados do *array* de **nome**

![Declarando array](../imagens/bp_array_11.png)

## 12. Contando elementos dentro de um *array*
![Declarando array](../imagens/bp_array_12.png)

### Referências

[Unreal Engine Blueprints Array](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Arrays/index.html)

[Unreal Engine Array Nodes](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Arrays/ArrayNodes/index.html)

[C++](https://www.codegrepper.com/code-examples/cpp/ue4+c%2B%2B+array)
