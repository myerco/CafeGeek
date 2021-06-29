

# Passo 1

**main.cpp**

```cpp

#include <iostream>
void Log(const char* message)
{
  std::cout << message std::endl;
}

void main() {
  Log("Hello World")
  std::cout << "Meu primeiro..." std::endl;
  std::cin.get();
}
```

## Passo 2
**main.cpp**

```cpp
void Log(const char* message);

int main() {
  Log("Hello World")
  std::cin.get();
}
```

**log.cpp**

```cpp
#include <iostream>
void Log(const char* message)
{
  std::cout << message std::endl;
}
```

## Passo 3
**Math.cpp**

```cpp
#include <iostream>

#define INTEGER int

int Multuply(int i, int j)
{
  INTEGER result = i * j;
  return result;
}
```

**Math.cpp**

```cpp
#include <iostream>

#if 1
int Multuply(int i, int j)
{
  int result = i * j;
  return result;
}
#endif
```

## Passo 4
**Math.cpp**

```cpp
#include <iostream>

const char* Log(const char* message)
{
    return message;
}

int Multuply(int i, int j)
{
  int result = i * j;
  Log("teste");
  return result;
}
```

## Passo 5

**log.cpp**

```cpp
#include <iostream>
int main()
{
  int variable = 8;
  char texto = 'T';  
  float valor = 3.4;
  float valor2 = 3f;

  bool teste = true;

  std::cout << variable std::endl;
  std::cout << sizeof(int) std::endl;
  std::cout << sizeof(variable) std::endl;
  std::cin.get();
}
```

## Passo 6

**log.h**

```cpp
#pragma once

#ifndef _LOG_H

void InitLog();

void Log(const char* message);

#endif

```

**log.cpp**

```cpp
#include "Log.h"
#include <iostream>

// "..log" caminho relativo
// <log.h> caminho do diretórios

void InitLog()
{
  Log("Inicializando log...");
}

void Log(const char* message)
{
    std::cout << message << std::endl;
};

```

**main.cpp**
```cpp
#include "Log.h"

void main();
{
  InitLog();
  Log("Teste...");
}

```
