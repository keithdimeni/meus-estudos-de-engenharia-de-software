# Fundamentos Web API

## Log de dados e Logging

`Log de dados` é um arquivo gerado por um software para descrever eventos sobre o seu funcionamento, utilização por usuários ou interação com outros sistemas sendo incrementado com o tempo com informações que permitem detectar problemas de funcionamento. segurança e acessibilidade.

Para obter um `log de dados` realizamos o `registro em log` ou `logging`.

O `registro em log(logging)` é um recurso essencial em aplicativos para detectar ou investigar problemas e analisar comportamento em geral.

### Provedores

Um provedor de Log `exibe` ou `armazena` logs no ASP.NET Core existem vários provedores como:
- Console
- Debug
- EventLog
- AzureApp
- Trace
- Event

Os níveis de log permitem definir os níveis de severidade do registro das informações.
Existem diferentes níveis de Log:

- **Critical**: logs que descrevem uma falha de sistema que requer atenção imediata.
- **Debug**: logs que são usados para investigação interativa durante o desenvolvimento.
- **Error**: logs que destacam quando o fluxo atual de execução é interrompido devido a uma falha.
- **Information**: logs que rastreaia, o fluxo geral do aplicativo.
- **None**: especifica que uma categoria de log não deve gravar nenhuma mensagem.
- **Trace**: logs que contêm as mensagens mais detalhadas. Essas mensagens podem conter dados confidenciais do aplicativo. Essas mensagens estão desativadas por padrão e nunca devem ser ativadas em um ambiente de produção.
- **Warning**: logs que destacam um evento anormal ou inesperado no fluxo do aplicativo, mas não fazem com que a execução do aplicativo pare.

#### Configuração de provedores

A configuração do provedor de log pode ser fornecida por um mais provedores de configuração:

- Formatos de arquivo(INI, JSON e XML).
- Argumentos da linha de comando.
- variáveis de ambiente.
- Objetos .NET na memória.
- O armazenamento não criptografado do Secret Manager.
- Um armazenamento de usuários criptografado, como o Cofre de Chaves do Azure.
- Provedores personalizados(instalados ou criados).

Por padrão o arquivo `app.settings.json` define as configurações do logging.