---
title: Variáveis
excerpt: Neste capítulo serão descritos os tipos de variáveis e sua manipulação.
permalink: /pages/unreal-engine/variaveis
last_modified_at: 2023-03-28T08:48:05-04:00
sidebar:
    nav: dev_unreal
toc: true  
categories:
  - Unreal Engine
tags:
  - Blueprint
  - Variáveis
  - Controle de fluxo
---

[Intermediário](/collection-archive/){: .btn .btn--warning}

## 1. O que são variáveis?

{% include imagelocal.html
    src="unreal/variaveis/unreal-engine-variables.webp"
    alt="Blueprint Variables"
    caption=""
%}

Variáveis são estruturas que são utilizadas para armazenar um valor de um determinado tipo na memória do computador.

Estrutura de memória.

| Variável |  Tipo   |   Valor   |
| :------- | :-----: | :-------: |
| iSoma    | Integer |     0     |
| fValor   |  Float  |    6.5    |
| tName    | String  | "Gandalf" |
| bRunnig  | Boolean |   false   |
| vLista   | FVector |  (1,2,4)  |

Abaixo um exemplo em C++:

```cpp
// Variável do tipo inteiro
int iSoma = 0;

// Variável do tipo ponto flutuante
float fValor = 6.5;
```

## 2. Variáveis no Unreal Engine

Variáveis no **Unreal Engine** são propriedades que contêm um valor ou fazem referência a um objeto ou ator no mundo. Essas propriedades podem ser acessíveis internamente ao **Blueprint** que as contém, ou podem ser tornadas acessíveis externamente para que seus valores possam ser modificados por designers que trabalham com instâncias do **Blueprint** colocadas em um nível.

### 2.1. Tipos de Variáveis

Para armazenar qualquer informação na memória devemos definir um tipo de dados primitivo ou mesmo uma estrutura de dados, a seguir alguns tipos de dados:

- `Boolean` - Armazena valores falso ou verdadeiro (true e false).

    ```cpp
    bool VariavelBoolean;
    VariavelBoolean = true;
    ```

- `Integer` - Valores inteiros entre −2.147.483.648 e 2.147.483.647

    ```cpp
    int32 VariavelInt;
    VariavelInt = 1;
    ```

    Utilize int32, uint8, uint32 para representar números inteiros.

- `Float` - Valores com casas decimais tal como 0,0553, 101,2887 e -78,322 .

    ```cpp
    float VariavelFloat;
    VariavelFloat = 2.4;
    ```

- `String`- Grupo de caracteres alfanuméricos.

    ```cpp
    FString VariavelString ;
    VariavelString = TEXT("Alo mundo!!");
    ```

### 2.2. Declarando variáveis com Blueprint

Declarando variáveis informamos ao computador que estamos reservando um espaço de memória temporário.  

{% include imagelocal.html
    src="unreal/variaveis/unreal-engine-variable.webp"
    alt="Figura: Blueprint Variables."
    caption="Variáveis no Editor de Blueprint."
%}

{% include imagelocal.html
    src="unreal/variaveis/unreal-engine-variable-details.webp"
    alt="Figura: Details ou propriedades das variáveis."
    caption="As variáveis tem tipos e propriedades que determinam o sua utilização."
%}

Observe que a propriedade `Category` agrupa as variáveis por uma categoria.

### 2.3. Declarando variáveis com C++

```cpp
    int32 Count;
```

**Informação:** As variáveis que serão manipuladas por Blueprints ou pelo Editor Viewport, devem ser expostas para essa finalidade usando a macro UPROPERTY.
{: .notice--danger}

```cpp
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Parâmetros")
    int32 iLife = 10;
```

## 3. Métodos Get e Set

Para acessar o conteúdo das variáveis utilizamos os métodos `Get` e `Set`, onde:

`Get`: Obtém o valor de uma variável.

`Set`: Atualiza o valor da variável.

### 3.1. Métodos Get e Set Blueprint

{% include imagelocal.html
    src="unreal/variaveis/unreal-engine-get-set.webp"
    alt="Figura: Métodos Get e Set."
    caption="Get se Set, obtém e atualiza respectivamente a variável Life."
%}

`BeginPlay` - Ao iniciar o jogo a lista de comandos conectados a estes nó deve ser acionado.

`Print String` - Escreve um texto na cena do jogo.

`Add +` - Variáveis numéricas podem ser manipuladas com operadores matemáticos.

`Converts` - Converte tipos de variáveis, neste caso converte um valor do tipo `integer` em um do tipo `String`.

### 3.2. Métodos Get e Set em C++

Arquivo Header.

```cpp
// MyHero.h
UPROPERTY()
virtual void BeginPlay() override;
```

Arquivo de implementação.

```cpp
// Myhero.cpp
void AMyHeroClass::BeginPlay()
 {
    Super::BeginPlay();
    int32 iLifeLocal = 5;
    float fSpeed = 3.7f;
    FString fsName = TEXT("O nome do personagem é Nostromo");
    iLifeLocal = iLifeLocal + iLife;
    // iLife é uma variável global
    UE_LOG(LogTemp, Warning, TEXT("O resultado é =, %d %f %s"), iLife, fSpeed, *fsName );
 }
 ```

## 4. Tratamento e armazenamento de texto no Unreal Engine

No **Unreal Engine** são definidos alguns tipos de dados para manipulação e armazenamento de caracteres alfanuméricos, entre elas estão os tipos de variáveis a seguir.

| Variável | Tamanho  | Considerações                                                                                                                                      |
| :------: | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
|  `Text`  | 40 Bytes | Podemos adicionar opções avançadas como exemplo `String Table`, ideal para textos longos que podem variar conforme a lingua definida pelo jogador. |
| `String` | 16 Bytes | Armazenamento e consumo de memória mediano                                                                                                         |
|  `Name`  | 8 Bytes  | Cadeias de caracteres  curtas que ocupam pouca memória.                                                                                            |

Podemos realizar as seguintes operações em `strings`:

- Atribuir o valor de uma `string` para outra;

- Acessar caracteres individualmente;

- Adicionar uma `string` no final de outra;

- Concatenar `strings`;

- Procurar uma determinada letra ou Substring dentro da `string`.

### 4.1. Strings em Blueprint

{% include imagelocal.html
    src="unreal/variaveis/unreal-engine-string-functions.webp"
    alt="Figura: String functions."
    caption="Append - Concatena tuas ou mais strings, Contains- Retorna falso ou verdadeiro se encontra um string dentro de outra."
%}

### 4.2. String em C++

Arquivo header.

```cpp
// myHero.h
UPROPERTY()
virtual void BeginPlay() override;

UPROPERTY()
FString NomeCharacter;

UPROPERTY()
FString ClassCharacter;

```

Arquivo de implementação.

```cpp
// myHero.cpp
void AMyHeroClass::BeginPlay()
 {
    Super::BeginPlay();

    FString fsMessage = TEXT("Procurando a classe do personagem");
    FString fsResultado;

    fsResultado.append("O nome é ",*NomeCharacter)

    // ou
    fsResultado =TEXT("O nome é ");
    fsResultado += *NomeCharacter;

    UE_LOG(LogTemp, Warning, TEXT("O resultado é =,  %s"), *fsResultado );

    // Procurando uma Substring
    if (fsMessage.Contains("class"))
    {
      UE_LOG(LogTemp, Warning, TEXT("Encontrei!!"));
    }
    else
        UE_LOG(LogTemp, Warning, TEXT("Não encontrei"));
 }

```

#### 4.2.1. Concatenando textos usando a função Append

A função `Append` concatena duas ou mais `strings`, passamos como parâmetros os textos que gostaríamos de concatenar e tendo como resultado um novo texto contendo os dois textos.

```cpp

FString sTexto = TEXT("Alo mundo...");
sTexto.append("Cruel");

// Resultado: Alo mundo...Cruel
```

#### 4.2.2. Procurando texto dentro de uma string em Blueprint

A função `Contains` procura uma sequencia de caracteres dentro de uma `string`, passamos os seguintes parâmetros para a função.

- `Search In` - Texto passado como parâmetro.
- `Substring` - Texto que deve ser localizado.
- `Use Case` - Diferencia maiúsculas e minúsculas.
 `Search from end` - Inicia a busca pelo fim do texto.

#### 4.2.3. Procurando texto com C++

```cpp

FString sTexto = TEXT("Procurando o texto escondido.");

if (sTexto.Contains(TEXT("texto")))
{
  return true;
}
else
  return false;

// Resultado: Alo mundo...Cruel
```

## 5. Variáveis do tipo numéricas Integer e Float

Valores numéricos utilizam operadores matemáticos para a sua manutenção, como veremos a seguir.  

### 5.1. Inteiro em Blueprint

{% include imagelocal.html
    src="unreal/variaveis/unreal-engine-variable-division.webp"
    alt="Figura: Utilizando Divisão com inteiros."
    caption="A exemplo acima divide um inteiro por 2 e trunca o resultado."
%}

{% include imagelocal.html
    src="unreal/variaveis/unreal-engine-variable-multiplication.webp"
    alt="Figura: Multiplicação valores."
    caption="Neste exemplo multiplicamos o valor por 100."
%}

### 5.2. Inteiro em C++

```cpp
void AMyCharacterClass::BeginPlay()
{
    Super::BeginPlay();
    Float fStrength = 10;
    int32 iLife = 0;

    iLife = int(fStrength / 2);
}
```

- (+) - soma;

- (*) - Multiplicação;

- (/) - Divisão.

***

## 6. Armazenando valores lógicos com Boolean

Variáveis Boolean armazenam dois valores : falso `false` ou verdadeiro `true`.

{% include imagelocal.html
    src="unreal/variaveis/unreal-engine-variable-boolean.webp"
    alt="Figura: Variável Boolean."
    caption="No exemplo acima se o valor de life for maior que 50 então o valor é atualizado para true."
%}

## 7. Controle de acesso a variáveis

Como especificar quais variáveis de um objeto um usuário pode acessar e quais estão fora dos limites? Usando os especificadores de controle de acesso público e privado.

### 7.1. Variáveis Privadas

Variáveis privadas só podem ser acessadas por membros da mesma classe.

Variavel private usando Blueprint.

{% include imagelocal.html
    src="unreal/variaveis/unreal-engine-variable-private-details.webp"
    alt="Figura: Private details."
    caption="Com a opção Privada marcada em uma variável, isso evita que a variável seja modificada por módulos externos."
%}

Variáveis Privadas em C++.

```cpp
private:
   bool Running = false;
```

### 7.2. Variáveis Públicas

Para permitir que uma variável seja modificada de fora de seu módulos, torne-a pública.  

Variavel públicas em Blueprint.

{% include imagelocal.html
    src="unreal/variaveis/unreal-engine-variable-public.webp"
    alt="Figura: Public."
    caption="Expondo a variável."
%}

{% include imagelocal.html
    src="unreal/variaveis/unreal-engine-variable-public-details.webp"
    alt="Figura: Public details."
    caption="Expõe a variável no Editor ViewPort."
%}

Variáveis Públicas com C++

```cpp
public:

  float Damage;

  UPROPERTY(BlueprintCallable, Category="Player")
  bool IsRunning;

```
