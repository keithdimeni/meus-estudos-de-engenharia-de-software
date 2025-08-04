# Fundamentos Web API

## Configurações

A configuração de aplicativos no ASP.NET Core se baseia em lista de pares `chave-valor` estabelecidos por `provedores de configuração`.

Os provedores de configuração leem os dados de configuração em pares chave-valor de várias fontes de configuração:

- Arquivos no formato `JSON`, `XML`, `INI`, `Texto`, etc.
- Variáveis de ambiente
- Argumentos da linha de comando
- Uma coleção na memória
- Provedores personalizados
- Arquivos de configuração diversos

`Json` é o formato mais usado.

### Como ler os arquivos de configuração `appsettings.json`

- Usar o serviço disponível pela interface `IConfiguration`
- Através da injeção de dependência para obter o serviço `IConfiguration` configuração por padrão.
