# Fundamentos Web API

## Tipos de retorno

ASP.NET oferece 3 tipos de retorno:

- **Tipo Específico**
- **IActionResult**
- **ActionResult<T>**

### Tipo Específico

Retorna um tipo de dados `complexo` ou `primitivo`(string, int, etc.).


**Exemplo:**
``` bash
[HttpGet]
public string Get()
{
  return "retornando uma string";
}
```

``` bash
[HttpGet]
public Produto Get()
{
  var produto = _context.Produtos.FirstOrDefault();
  return produto;
}
```

### Tipo IActionResult

Apropriado quando vários tipos de retorno ActionResult são possíveis em método Action.

Não retorna diretamente o tipo de dados(string, int, etc.).
``` bash
[HttpGet]
public IActionResult Get()
{
  var produto = _context.Produtos.FirstOrDefault();
  if (produto == null)
    return NotFound();

  return Ok(produto);
}
```

### Tipo ActionResult<T>

Permite retorno de um tipo derivado de ActionResult`(ActionResult implementa a interface IActionResult)` ou o retorno de um tipo específico(T)

``` bash
[HttpGet]
public ActionResult<Produto> Get()
{
  var produto = _context.Produtos.FirstOrDefault();
  if (produto == null)
    return NotFound();

  return produto;
}
```