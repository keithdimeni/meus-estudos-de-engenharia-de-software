# Fundamentos Web API

## Filtros

Filtros são `atributos` anexados às classes ou métodos dos controladores que injetam lógica extra ao processamento da requisição e permitem a implementação de funcionalidades relacionadas a `autorização`, `exception`, `log`, `cache` de forma simples e elegante.

Eles permitem executar um código personalizado antes ou depois de executar um método `Action`.

Permitem também realizar `tarefas repetitivas` comuns a métodos `Actions` e são chamados em certos estágios do pipeline.

### Tipos de Filtros

- **Authorization**: determina se o usuário está autorizado no request atual. São executados primeiro.

- **Resource**: podem executar código antes e depois do resto do filtro ser executado. Tratam da requisição após a autorização e executam antes do `model binding` ocorrer.

- **Action**: executam o código imediatamente antes e depois do método `Action` do controlador ser chamado.

- **Exception**: são usados para manipular exceções ocorridas antes de qualquer coisa escrita no corpo da resposta.

- **Result**: executamo código antes ou depois da execução do s resultados das actions individuais do controlador.

### Implementação síncrona

Os filtros `síncronos` que executam código antes e depois do estágio do pipeline definem os método `OnActionExecuting` e `OnActionExecuted`.

``` csharp
public clas CustomActionFilter: IActionFilter
{
  public void OnActionExecuting(ActionExecutingContext context)
  {
    //código: antes que a action executa
  }

  public void OnActionExecuted(ActionExecutedContext context)
  {
    //código: depois que a action executa
  }
}
```

### Implementação assíncrona

Os filtros assíncronos herdam de `IAsyncActionFilter` e são definidos com um único método: `OnActionExecutingAsync` que usa um `FilterTypeExecutingContext` e o delegate `FilterTypeExecutionDelegate` para executar o estágio do pipeline do filtro.

``` csharp
public clas CustomAsyncActionFilter: IAsyncActionFilter
{
  public async Task OnActionExecuting(ActionExecutingContext context, ActionExecutionDelegate next)
  {
    //código: antes que a action executa
    await next();
    //código: depois que a action executa
  }
}
```

### Escopo e ordem de execução

Pode ser adicionado ao pipeline em um dos três escopos

1. Pelo método `Action`.
2. Pela classe do `controlador`.
3. `Globalmente` (é aplicado a todos os controladores e actions).

A `ordem padrão` de execução é:

1. Filtro `Global`.
2. Filtro de nível de `classe`(controlador).
3. Filtro de nível de `método` (Action).

### Filtros personalizados

Além dos filtros oferecidos por padrão pelo framework ASP.NET Core podemos criar `filtros personalizados`.

1. Na abordagem síncrona temos que criar uma clase que implementa a interface `IActionFilter`.
2. Na abordagem assíncrona temos que criar uma classe que implementa a interface `IAsyncActionFilter`.