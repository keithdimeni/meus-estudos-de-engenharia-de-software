# Fundamentos Web API

## Data Annotations - validação do modelo

Os atributos `Data Annotations` permitem aplicar a validação no modelo de domínio definindo atributos.

Os critérios de validação são definidos em um lugar(**Model**) e são aplicados onde o modelo for usado.

### Como funcionam?
Quando os parâmetros do Model são usados nas Actions, ao popular o objeto do modelo usando os dados da requisição, o framework verifica se o objeto é válido com base nso atributos `Data Annotations` definidos nas propriedades do modelo.

### Principais atributos:

- `Required`: obriga a entrada de um campo especificado.
- `RegularExpression`: Permite usar expressões regulares em validações mais específicas.
- `StringLength`: Determina o comprimento máximo e mínimo permitidos.
- `MinimumLength`: Determina a quantidade mínima de caracteres permitida.
- `MaxLength`: Determina o tamanho máximo do campo na tabela do banco de dados(usando EF Core).
- `Range`: Define um intervalo para uuma propriedade onde a validação será aplicada.
- `CrediCard`: valida a entrada para o formato de um cartão de crédito.
- `URL`: define o formato exigido para uma url.
- `Phone`: valida a entrada para o formato Telefone
- `Compare`: permite comparar duas propriedades


### Vantagens e Desvantagens

`Vantagem`
- Simplicidade e centralização da validação no modelo

`Desvantagens`
- Polui o modelo de domínio com atributos

## Validação personalizada

Existem duas abordagens para validação personalizada:

1. **Criar atributos customizados**
- Foco é validar uma propriedade.
- Pode ser reutilizada em diversos modelos e propriedades.

2. **Implementar `IValidatableObject` no seu modelo**
- Pode acessar todas propriedades do modelo e realizar uma validação mais complexa.
- Não popde ser reutilizado em outros modelos.
