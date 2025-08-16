# Paginação, Ordenação e Filtro

## Paginação - Conceito

É usada para dividir grandes conjuntos de dados em partes menores, chamadas `páginas`, para que os clientes da API possam solicitar e receber apenas a quantidade de dados desejada de cada vez.

Objetivo da paginação é `evitar apresentar` em uma única página uma `grande quantidade` de registros otimizados a carga dos dados conforme a demanda do usuário.

Podemos implementar a paginação usando diversas abordagens como: `Query Strings`, `Cabeçalhos HTTP`, `HATEOAS`, `Protocolo OData`, `Bibliotecas e frameworks`.

## Filtro - Conceito

É usada para recuperar um `subconjunto específico de dados` de um conjunto maior com base em critérios ou condições específicas.

### Maneiras de filtrar dados em uma Web API

- `Filtragem por consulta(Query Filtering)`: Usa parâmetros de consulta na URL do request para especificar critérios de filtro.

- `Filtragem por rota (Route Filtering)`: Define rotas específicas no controlador que aceitam parâmetros no próprio URL da solicitação.

- `Filtragem avançada`: Implementa lógica de filtragem mais complexa usando classes de parâmetros personalizados.

- `Usar pacotes de terceiros`: [*Pacote Sieve*](https://github.com/Biarity/Sieve)

### Abordagem usada

1. Criar um único endpoint para filtrar dados com base em mais de uma propriedade permitindo que usuário defina critérios de filtro de forma flexível.

2. Criar endpoints separados para cada propriedade, permitindo que usuários especifiquem o campo e i valor como parâmetros de consulta na URL da solicitação.
>*A segunda abordagem é a mais aderente ao padrão Restful.*