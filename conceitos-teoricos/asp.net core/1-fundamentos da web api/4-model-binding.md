# Fundamentos Web API

## Model Binding(Vinculação de modelos)

É um recurso que permite mapear dados de uma requisão Http para os parâmetros de uma Action de um controlador.

Inclui todos tipos de parâmetros: números, strings, arrays, listas, tipos complexos, listas de objetos, etc.

Toda vez que implementamos `Actions` que recebem `parâmetros` estamos usando `Model Binding`.

### Como funciona

Quando nossa API recebe uma requisição HTTP, ela a roteia para um método `Action` específico de um controlador com base na `rota definida`.

Ela determina qual método Action será executado com base no que está definido na `rota` e, vincula os valores da requisição HTTP aos `parâmetros` desse método `Action`.

``` csharp
[HttpGet("{id}")]
public async Task<ActionResult<Produto>> Get(int id) {...}
-> api/produtos/1
```
O template de rota `id` extrai o valor da URL e passa para o método `Action` com `parâmetro id` do tipo `int`.

### Fonte de dados

1. Valores de formulário: POST e PUT enviados no corpo da requisição.

**Exemplo:**
``` csharp
[HttpPost]
public ActionResult Post([FromBody] Produto produto){...} 
```

``` csharp
[HttpPut("{id}")]
public ActionResult Put(int id, [FromBody] Produto produto){...} 
```

`Model Binding` permite uma configuração usando atributos para indicar a fonte dos dados ou mesmo se desejamos que ele ocorra ou não.

2. Rotas: `[Route("api/[Controller]")]` ou `HttpGet("{id}")`.

3. Query Strings: api/produtos/4`?nome=suco&ativo=true`.

#### Atributos para definir se o Model Binding vai ocorrer ou não

- `BindRequired`: adiciona um erro ao ModelState se a vinculação de dados aos parâmetros não puder ocorrer.
- `BindNever`: Informa ao Model Binding para não vincular a informação ao parâmetro.

#### Atributos que indicam a fonte de dados dos parâmetros

1. `FromForm`: dados recebidos do formulário
2. `FromRoute`: dados oriundos da rota de dados
3. `FromQuery`: dados da cadeia de consulta(query string)
4. `FromHeader`: dados que vêm no cabeçalho da requisição HTTP
5. `FromBody`: dados recebidos do `body` da requisição
6. `FromServices`: vincula o valor especificado à implementação que foi configurado no `container de injeção de depedência`.

**Atributo [FromServices]**

Sobrescreve a fonte de associação injetando os valores via `injeção de dependência` em um nétodo `Action específico`.

Permite injetar as dependências diretamente no método `Action` do controlador que requer a dependência.

Habilita a injeção de um serviço diretamente em um método Action `sem usar a injeção de construtor`.

**A vantagem do `[FromServices]` em relação a `Injeção via Construtor`:**

- Mantém o construtor do controlador mais limpo.
- Injeta dependências apenas onde realmente são necessárias.
- Facilita a leitura e manutenção do código, principalmente em controladores com muitas Actions e dependências variadas.

Modo de uso:

Antes...
- Definir os serviços
- Registrar os serviços
- Aplicar o atributo [FromServices] ao método Action que requer o serviço

Apartir do .NET 7 a dependência é resolvida por inferência, sem a necessidade de usar [FromServices] no método Action.