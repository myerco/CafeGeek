# Convertendo Blueprints para C++

## 1. Herança

1.  Modelo
- Classe C++ -> Blueprints = Certo
- Blueprints -> Classe C++  = Errado

1. Blueprintable
Expõe esta classe como uma classe base aceitável para a criação de Blueprints. O padrão é NotBlueprintable, a menos que herdado de outra forma. Isso é herdado por subclasses.

## Referências

[Exposing Gameplay Elements to Blueprints](https://docs.unrealengine.com/en-US/Engine/Blueprints/TechnicalGuide/ExtendingBlueprints/index.html)
