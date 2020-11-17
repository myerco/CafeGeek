# Convertendo Blueprints para C++

1. Blueprints vs C++
  - Blueprints são mais fáceis de ser lidos e entendidos pelos membros da equipe,
  - C++ evitam sobrecarga de chamadas de função economizando ciclos de CPU.
  - C++ Conseguem acesso a Library math.
  - Sistema de versionamento do C++ utiliza ferramentas como o GIT ou SVN, Blueprints necessita de
  ferramenta específica.
  - Para projeto em plataformas mobile o recomendado é c++.

1. O que é ideal?
    - Depende do problema.
    - Equipes pequenas e projetos pequenos = Blueprints
    - Equipes pequenas com cultura de desenvolvimento e necessidade de processamento = c++

## 1. Herança

1.  Modelo
- Classe C++ -> Blueprints = Certo
- Blueprints -> Classe C++  = Errado

1. Blueprintable
Expõe esta classe como uma classe base aceitável para a criação de Blueprints. O padrão é NotBlueprintable, a menos que herdado de outra forma. Isso é herdado por subclasses.

1. Uma breve história sobre Herança.
  - classe Pessoa  c++
    int Vida;  
    Movimentacao();  
  - classe Hugo Blueprint
      Vida ->Herdada   
      Movimentacao() - Herdada  
      AddActiveTrigger()  
      float SpeedPlataforma  
      int Vida #Error  

1. Tipos de variáveis
| Blueprint | C++ |
|:-:|-|
| integer | int  |
| Vector | FVector |
|  |  |


1. Migrando a plataforma
- Verificando a classe pai do Blueprint **BP_Plataforma** = *static_mesh_actor*.
1. Criar a classe c++ **Plataforma** do tipo
*AStaticMeshActor*
1. Alterara classe pai do **BP_Plataforma** para **Plataforma**

## Referências

[Exposing Gameplay Elements to Blueprints](https://docs.unrealengine.com/en-US/Engine/Blueprints/TechnicalGuide/ExtendingBlueprints/index.html)
