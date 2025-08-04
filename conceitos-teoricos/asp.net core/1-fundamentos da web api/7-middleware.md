# Fundamentos Web API

## Middleware

 **Middleware** é um componente de software que faz parte do `pipeline` de processamento de requisições em uma aplicação web, como no ASP.NET. Ele `intercepta`, `processa` ou `modifica` as requisições e respostas HTTP enquanto elas passam pelo pipeline.

No ASP.NET, os middlewares são executados em sequência, formando uma cadeia. Cada middleware pode:

- Executar alguma lógica antes de passar a requisição para o próximo middleware.
- Modificar a requisição ou a resposta.
- Encerrar o processamento e retornar uma resposta imediatamente.

`Pipeline` é o fluxo sequencial pelo qual uma requisição HTTP passa dentro da apl1icação. Esse fluxo é composto por vários middlewares, que são executados um após o outro, formando uma cadeia de processamento.

### Tratamento de erros globais usando um middleware

Podemos usar o middleware `UseExceptionHandler` para realizar o tratamento de exceções.

Ele poder ser usado para manipular `exceções globalmente` e obter todos detalhes do objeto `Exception` (rastreamento de pilha, exceção interna, mensagens, etc.)

#### Roteiro para usar o middleware: `UseExceptionHandler`

1. Criar uma entidade chamada `ErrorDetails` que é uma classe usada para representar os detalhes dos erros.
2. Criar um método de extensão `ConfigureExceptionHandler` para `IApplicationBuilder`.
3. Usar o middleware `UseExceptionHandler` e configurar o tratamento de erros
4. Habilitar o uso do método de extensão `ConfigureExceptionHandler` na classe `Program` (**app.ConfigureExceptionHandler()**)
5. Testar a implementação no Swagger e no Postam