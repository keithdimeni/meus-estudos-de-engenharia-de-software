# Fundamentos Web API

## O que roteamento?

`mapeamento` de requisições feita via URI
`despacha` as requisições para `endpoints`
Pode `extrair` valores da URL da requisição
Pode `gerar` URLs que mapeiam para endpoints

## Em ASP.NET Core o roteamento pode ser configurado usando:

`Controllers`

`Razor Pages`

`SignalR`

`Middlewares` habilitado para o endpoint(Minimal API)

`Delegates e lambdas` registrados no roteamento (Minimal API)

O Roteamento em Web APIs é baseado nos `ATRIBUTOS` definidos nos controladores
e métodos Acion.

Os `Atributos` mapeam para `Actions` e `Controladores`

Os atributos para definir rotas são: `HttpGet` `HttpPost` `HttpPut` `HttpDelete` `HttpPatch`

## Padrões de roteamento

```
A palavra chave 'controller' é usado para definir o nome do controlador como o nome da rota.
[Route("[controller]")] -> /produtos
```

```
É uma outra forma comum de definir o nome do controlador junto a palavra api
[Route("api/[controller]")] -> /api/produtos
```

```
Combinar o template da rota com a rota definida no atributo Route
[HttpGet("primeiro")] -> /produtos/primeiro | /api/produtos/primeiro
```

```
Combinar o parâmetro com a rota definida no atributo Route
[HttpGet("{id}")] -> /produtos/{id} | /api/produtos/{id}
```

```
Ignorar a rota definida no atributo Route
[HttpGet("/primeiro")] -> /primeiro
```

```
Definir um segundo parâmetro obrigatório
[HttpGet("{id}/{param2}")] -> /produtos/{id}/{param2}
```

```
Atribuir um valor ao segundo parâmetro
[HttpGet("{id}/{param2=Teste}")] -> /produtos/{id}/{param2}
```

```
Permitir que um método Action atenda a dois ou mais endpoints diferentes
[HttpGet("/primeiro")]
[HttpGet("primeiro")]
[HttpGet("teste/outroteste")]

...
```

## Restrições de `Rotas`

Restrições de rota ajudam a `filtrar` ou `impedir` que valores indesejados atinjam os métodos `Action` do controlador.

É feito verificando a restrição com relação ao valor do `parâmetro` da URL.

Usado para  `distinguir` entre duas rotas parecidos e não para `validar` entradas de dados

```
[HttpGet("{id:int:min(1)}")] -> Restrição com tamanho mínimo
```

```
[HttpGet("{valor:alpha}")] -> Restrição com valor alfanumérico
```

```
[HttpGet("{valor:alpha:length(5)}")] -> Restrição com valor alfanumérico de tamanho fixo
```

```
[HttpGet("{valor:alpha:maxlength(5)}")] -> Restrição com valor alfanumérico com tamanho máximo
```

```
[HttpGet("{id:range(5,10)}")] -> Restrição com valor entre 5  e 10
```