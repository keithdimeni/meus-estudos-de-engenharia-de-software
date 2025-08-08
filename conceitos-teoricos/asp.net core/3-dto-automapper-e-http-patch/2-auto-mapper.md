# Data Transfer Object

## AutoMapper

A biblioteca `AutoMapper` realiza o mapeamento entre os objetos que representam nossas entidades e os objetos que representam os nossos `DTOs` filtrando as propriedades que desejamos expor.

Para usar precisamos:

1. `AutoMapper`

```bash
install-package AutoMapper -Version 1x.x.x
dotnet add package AutoMapper --version 1x.x.x
```

2. `AutoMapper.Extensions.Microsoft.DependencyInjection`

```bash
install-package AutoMapper.Extensions.Microsoft.DependencyInjection -Version 1x.x.x
dotnet add package AutoMapper.Extensions.Microsoft.DependencyInjection --version 1x.x.x
```

3. Criar os `perfis de mapeamento` e definir como o `AutoMapper` deve mapear as entidades para os DTOs e vice-versa.(Criar classes de perfil)
