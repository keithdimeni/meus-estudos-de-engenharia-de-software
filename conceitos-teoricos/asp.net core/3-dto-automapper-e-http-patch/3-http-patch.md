# Data Transfer Object

## HttpPatch

### Conceito

`HttpPatch`: é um atributo na ASP.NET Core usado para marcar um método Action em um controlador como um manipulador de solicitações `PATCH HTTP`.

`HttpPatch` é semelhante ao `HttpPut`, mas em vez de atualizar um recurso completo, ele permite atualizar somente partes específicas do recurso.

### Como funciona

O Cliente da API deve enviar, no `body da requisição http`, informações que indicarão as alterações que ele deseja fazer no recurso.

### Como a informação será enviada?

- Usar o padrão `RFC 6902 - 'Json Patch'`

`Json Patch` é um formato para descrever alterações em um documento JSON e pode ser usado para evitar o envio de um documento inteiro quando apenas uma parte foi alterada.
>*[Documentação oficial do `JSON Patch`](https://jsonpatch.com/)*

- Este padrão define a estrutura do corpo da requisição HTTP para indicar as alterações que desejamos fazer no recurso, definindo um conjunto de operações que pode ser: `add`, `remove`, `replace`, `move`, `copy` e `test`.

### Operações e Estrutura

A operação possui 3 propriedades:

- `op`: Define o tipo de operação a ser realizada. Ex: `add`, `remove`, etc.
- `patch`: define o caminho da propriedade do objeto que você quer atingir. Ex: `\nome`.
- `value`: define o valor a ser usado na operação.

``` json
[
  {
    "op": "replace",
    "path": "/estoque",
    "value": 10,
  }
]
```

### Método Action

Em controlador um método Action JSON Patch é formado assim:

- É anotado com o atributo `HttpPatch`.
- Aceita um parâmetro do tipo `JSONPatchDocument<T>` com **[FromBody]**.
- Chama o método `ApplyTo(Object)` no documento patch para aplicar as alterações.

``` csharp
[HttpPatch]
public IActionResult PatchTeste(JsonPatchDocument<Tipo> patchDoc)
{
  //...
  patchDoc.ApplyTo(Tipo, ModelState);
  //...
}
```

### Pacotes Nuget

`Microsoft.AspNetCore.JsonPatch`
- Permite implementar operações de patch parcial em recursos RESTful por meio do método `HTTP PATCH`

- Oferece suporte à aplicação de atualizações parciais em objetos complexos, como modelos de domínio ou entidades de banco de dados.

`Microsoft.AspNetCore.Mvc.NewtonsoftJson`

- Habilita o suporte ao `JSON Patch` na ASP.NET Core Web API.
- Fornece um parser e um serializador para o formato JSON Patch.