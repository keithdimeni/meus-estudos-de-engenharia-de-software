# Programação Assíncrona

## Conceito

Usada para melhorar a escalabilidade da aplicação.

Não há ganho direto de desempenho ela apenas permite lidar com mais requisições simultâneas.

Dá um ganho indireto de desempenho com com melhoria no tempo médio de resposta.

Quando o número de `solicitações simultâneas` para nosso aplicativo é maior do que o número disponível de *threads de trabalhos*, as solicitações vão para o `estado pendente` até que qualquer uma das solicitações ativa seja concluída.
> `Thread - (Linha de execução)` É uma sequência de instruções que podem ser executadas simultaneamente com outras sequências de instruções.

Para melhorar a situação será necessário dimensionar o aplicativo para lidar melhor com as requisições simultâneas evitando que elas vão para o estado pendente.

No `escalonamento horizontal`, incluímos mais servidores para que requisições adicionais possam ser tratadas por diferentes instâncias de aplicativos hospedados em outro servidor.

No `escalonamento vertical`, melhoramos o poder de processamento do servidor disponível adicionando mais memória, CPU, etc., ou melhorando a escalabilidade do aplicativo de modo que seja capaz de utilizar melhor os recursos disponíveis e, por sua vez, possa lidar com mais requisições simultâneas.

As técnicas de programação assíncrona ajudam a `melhorar a escalabilidade` do aplicativo usando `async e await`.

Não melhoramos o desempenho aplicando a programação assíncrona.

Em vez disso, usando `async`, aguardamos a resposta e liberados a `thread`(até obtermos uma resposta) para processamento de outras requisições em uma fila.

## Cenários para aplicar a programação assíncrona

- `Acesso ao banco de dados`: Recuperar ou salvar dados em um banco de dados.
- `Chamadas a serviços web`: Interagir com serviços web, fazer solicitações HTTP.
- `Tarefas de longa duração`: Processamento de imagens, cálculos complexos, relatórios.
- `Operação de Entrada e Saída(E/S)`: Operação de leitura/escrita em disco, comunicação com periféricos.
- `Melhorar a escalabilidade`: Manipular requisições concorrentes sem bloquear as threads.
- `Manter a responsividade`: Manter a aplicação respondendo em operações longas.

> O uso indevido da `programação assíncrona` pode levar a problemas de `concorrência` e complexidade desnecessária.