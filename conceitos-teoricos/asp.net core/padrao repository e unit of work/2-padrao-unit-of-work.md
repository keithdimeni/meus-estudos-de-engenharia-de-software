# Padrão Unit Of Work (Unidade de Trabalho)

## Conceito

Mantém uma lista de objetos afetados por uma transação comercial e coordena a gravação de alterações e a resolução de problemas de simultaneidade.

Uma `Unidade de Trabalho(Unit Of Work)` registra tudo o que você faz durante uma transação comercial que pode afetar o banco de dados. Ao terminar, ela descobre tudo o que precisa ser feito para alterar o banco de dados como resultado do seu trabalho.

### Utilidade

- Gerenciar as transações.
- Ordenar o CRUD no banco de dados.
- Impedir a concorrencia (duplicação de atualizações).
- Usar somente uma instância do contexto por requisição.

### Implementação

1. Criar um interface para o `Unit Of Work` que geralmente inclui métodos para iniciar, confirmar(commit) e reverter(rollback) transações.

2. Criar uma classe concreta que implemente a interface do Unit Of Work onde devemos gerenciar uma instância do `DbContext` para permitir a execução de transações sendo que esta classe usa um repositório genérico para armazenar objtos.

3. Configurar a injeção de dependência registrando o serviço do Unit Of Work no contêiner DI ASP.NET Core.

**Na implementação dos `repositórios` não teremos o método SaveChanges que será implementado apenas na Unit Of Work**.

#### Definição de responsabilidades

Os `repositórios` são os responsáveis por realizar operações de leitura e escrita no banco de dados, mas `não devem chamar o SaveChanges`.

Eles simplesmente interagem com o DBContext, modificam objetos e preparam as mudanças para persistência.

A **Unit of Work** é o responsável por gerenciar transações,e mais importante, por chamar o `SaveChanges`.

Ela é quem inicia, confirma ou reverte a transação e garante que todas as operações realizadas nos repositórios sejam incluídas em uma única transação do banco de dados.
