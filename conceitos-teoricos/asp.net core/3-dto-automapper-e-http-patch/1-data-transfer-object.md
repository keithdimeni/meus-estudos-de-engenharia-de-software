# Data Transfer Object

## Conceito

### A motivação
Quando usamos modelos para receber e enviar dados, expomos todo domínio da aplicação, por isso é importante entender que:

- Ao usar o model, expomos todas informações das entidades do nosso modelo de domínio.
- Não é uma boa prática acessar diretamente e expor as informações das entidades do domínio.
- Evitar retonar entidades de domínio a partir dos endpoints de uma API
- A recomendação é construir as entidades do domínio de uma forma que eles não dependam de nenhuma lógica externa e que sejam isoladas das camadas externas.
- A abordagem mais correta e segura é exibir e expor somente as informações necessárias, restritas a um conjunto de dados.

**Como restringimos o acesso e a exposição das informações das nossas entidades de domínio?**

### Data Transfer Object(DTO)
Um `DTO` é um contêiner de dados usado para transportar dados entre diferentes partes ou camadas de uma aplicação que define como os dados serão enviados pela rede.

Usamos `DTOs` para representar os dados que desejamos expor.

É importante entender que `DTO`e `ViewModel`embora parecidos servem de maneiras diferentes.
>*`ViewModel` é usada na camada de apresentação para estruturar dados que serão exibidos em uma página ou View(mais usadas em aplicações MVC)*

#### DTO - Benefícios

- Permite ocultar propriedades específicas do modelo de entidades por questão de segurança ou para reduzir o tamanho da carga para melhorar o desempenho.

- Permite personalizar as informações que serçao transmitidas e exibidas.

- Permite proteger as entidades contra injeção de dados restringindo as informações que serão expostas na camada de apresentação.

- Desacopla o modelo de entidades da camada de apresentação, permitindo que as entidades e os DTOs evoluam de forma independente sem afetar os clientes da API.


#### DTO - Implementação

1. Criar uma `classe/record` para o `DTO` que contenha os membros que representam os dados que você deseja transferir entre diferentes partes de sua aplicação.

2. A `nomenclatura` usada para os DTOs geralmente usa o `sufixo` *DTO* no final do nome da entidade para qual estamos criando o DTO.

Ex: 
- `Categoria` -> `CategoriaDTO`
- `Produto` -> `ProdutoDTO`

Caso haja separação entre os dados de entrada e saida pode ser feito da seguinte forma:
- CategoriaRequest e Categoria Response
- ProdutoRequest e ProdutoResponse

Podemos incluir métodos para realizar operações específicas nos membros do DTO`(mas a principal função do DTO é armazenar e transferir dados e não contém lógica de negócio)`.

Podemos aplicar `validações`, `formatações` ou outras anotações aos membros de um DTO(Ex: Data Annotations)

##### DTOs na Entrada e Saída de dados

1. DTOs na Entrada(Input DTOs)

São usados para receber dados nos requests HTTP `POST`, `PUT`, `Patch`, etc.

```csharp
[HttpPost]
public IActionResult Create(ProdutoDTO produtoDto)
{
  // validação e processamento dos dados
}
```

2. DTOs no Retorno(Output DTOs)

São usados para modelar os dados que os controladores retornam aos clientes
``` csharp
[HttpGet]
public ActionResult<CategoriaDTO> Get(int id)
{
  var categoria = _unitOfWork.categoriaRepository.Get(c => c.CategoriaId == id);
  var categoriaDto = _mapper.Map<CategoriaDTO>(categoria);
  return Ok(categoriaDto);
}
```

O `mapeamento` entre DTO e entidades pode ser feito de duas formas

1. Fazer o mapeamento manual

2. Usar uma biblioteca, a mais usada é o `AutoMapper`. Realiza o mapeamento de forma automática.
