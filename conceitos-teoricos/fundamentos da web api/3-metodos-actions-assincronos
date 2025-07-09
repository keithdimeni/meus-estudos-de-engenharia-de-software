# Fundamentos Web API

## Métodos Actions Assíncronos
O servidor web de uma aplicação .NET possui um pool de threads que são usadas para servir as requisições que chegam em a método Action.

### Método Action Síncrono
**Como Funciona:**

- Quando uma requisição chega, uma thread desse pool é encarregada de processar essa requisição.
- Se a requisição for processada de forma síncrona, a thread encarregada fica ``bloqueada`` até a requisição finalizar. 

Dessa forma, a execução dos métodos é `contínua`, e se uma thread começar a executar um método, ela ficará ocupada até a execução do método terminar.


``` bash
"Thread" é uma unidade de execução dentro de um processo. No .NET, cada thread pode executar tarefas de forma independente, permitindo que o servidor processe várias requisições ao mesmo tempo.

Pool (ou "pool de threads") é um conjunto gerenciado de threads prontas para serem usadas. Em vez de criar e destruir threads para cada requisição, o servidor mantém um grupo de threads já criadas (o pool) e as reutiliza, melhorando o desempenho e a eficiência do processamento das requisições.
```


### Método Action Assíncrono
**Como Funciona:**

- Quando uma requisição chega, uma `thread` desse `pool` é encarregada de processar essa requisição.
- Se a requisição for processada de forma assíncrona, a thread é devolvida ao pool para servir novas requisições.

Dessa forma, a execução dos métodos não é `contínua`. Quando a operação assíncrona terminar, a thread é avisada e retoma o controle de execução da Action.

Na plataforma .NET usa-se a abordagem simplificada à programação assíncrona, fazendo uso das palavras-chave `async` e `await` para criar métodos assíncronos TAP(Task-based Asynchronous Pattern).

As palavras `async` e `await` e o tipo `Task` são a base da programação assíncrona no .NET.

### Exemplo
```csharp
[HttpGet]
public async Task<ActionResult<IEnumerable<Categoria>>> GetCategoriasAsync()
{
  return await _context.Categorias.ToListAsync();
}
```

### Regras e convenções

- A assinatura do método deve incluir o modificador `async`
- O método deve ter um tipo de retorno da `Task<TResult>`, `Task` ou `void`.
- As declarações devem incluir pelo menos uma expressão `await`. Isso diz ao compilador que o método precisa ser suspenso enquanto a operação aguardada estiver ocupada.
- É uma boa prática o uso do sufixo Async no nome do método.

**Async, Await e Task**

- A instrução `async` faz com que um método possa ser executado de forma assíncrona.
- A palavra reservada `await` é usada para indicar que a execução do método deve `esperar`(de forma não bloqueante) até que uma tarefa assíncrona seja concluída.
- A classe `Task<TResult>` representa uma `única operação` que retorna um valor. Essa `operação` pode ser executada de forma assíncrona.

### Vale a pena?

O assincronismo é útil para melhorar a experiência do usuário quando há alguma operação que demanda muito tempo para ser executada.

- O assincronismo não é grátis.
- Sempre que usar, haverá uma perda de desempenho, especialmente se usar thread.
- O ganho que ele dá é a execução em paralelo, assim você pode atender mais requisições.
- A requisição específica não ficará mais rápida.