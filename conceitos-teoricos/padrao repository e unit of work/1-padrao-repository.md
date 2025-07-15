# Padrão Repositório

## Conceito

O padrão `Repository` faz mediação entre o domínio e as camadas de mapeamento de dados, agindo como uma coleção de `objetos de domínio em memória`.

### Benefícios do uso do padrão Repositório

- Minimiza a lógica de consultas na aplicação, evitando consultas esparramadas pelo coódigo(`encapsula a lógica das consultas no repositório`).

- Desacopla a aplicação dos frameworks de persistência como EF Core(`podemos substituir o framework usado facilmente`).

- Facilita a realização de testes unitários no projeto(`usando um repositório Fake`).

### Implementação do padrão Repository

Cria-se uma interface onde definimos o contrato que representa os métodos que deverão ser implementados por uma `classe concreta`.

Registrar no `container de injeção de dependência(DI)` as classes concretas que implementam as interfaces como serviços disponíveis
```csharp
builder.Services.AddScoped<Interface, ClasseConcreta>();
```

**Existem `duas` abordagens para implementação do padrão `Repository`:**

1. `Repositório Específico`.

Cria uma interface para uma `entidade específica` contendo o contrato que define os métodos que a `classe concreta` deverá implementar.

```csharp
public interface ICategoryRepository
{
  IEnumerable<Categoria> ListCategorys();
  Categoria FindCategory(int id);
  void CreateCategory(Categoria categoria);
  void UpdateCategory(int id, Categoria categoria);
  void DeleteCategory(int id);
}
```

```csharp
public class CategoryRepository : ICategoryRepository
{
  private readonly AppDbContext _context;
  
  public CategoryRepository(AppDbContext context)
  {
    _context = context;
  }
  ...
  // Implementação do contrato da interface(métodos)
}
```

1. `Repositório Genérico`.

Cria uma `interface genérica` contendo o contrato que define métodos genéricos que a `classe concreta` deverá implementar.

```csharp
public interface IRepository<T>
{
  IEnumerable<Categoria> List();
  Categoria Find(int id);
  void Create(Categoria categoria);
  void Update(int id, Categoria categoria);
  void Delete (int id);
}
```

```csharp
public class Repository<T> : IRepository<T> where T : class
{
  private readonly AppDbContext _context;
  
  public Repository(AppDbContext context)
  {
    _context = context;
  }
  ...
  // Implementação da interface(métodos)
}
```
