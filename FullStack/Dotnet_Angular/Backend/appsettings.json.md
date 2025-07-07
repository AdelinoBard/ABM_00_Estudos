# `appsettings.json`

É um arquivo de **configuração baseado em JSON** que substitui o antigo `Web.config` usado em versões anteriores do ASP.NET. A sintaxe XML foi substituída pelo formato JSON, mais legível e consideravelmente menos prolixo.

Ele armazena **pares chave/valor** que definem comportamentos e parâmetros da aplicação, como:

- Strings de conexão com banco de dados
- Níveis de log
- URLs de serviços externos
- Configurações personalizadas

---

## Estrutura típica do arquivo

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=MyDb;Trusted_Connection=True;"
  },
  "AppSettings": {
    "FeatureXEnabled": true,
    "ApiBaseUrl": "https://api.exemplo.com"
  }
}
```

---

## Como ele é usado no código?

Você pode acessar os valores usando **injeção de dependência** com a interface `IConfiguration`. Exemplo:

```csharp
public class MeuController
{
    private readonly string _apiBaseUrl;

    public MeuController(IConfiguration config)
    {
        _apiBaseUrl = config["AppSettings:ApiBaseUrl"];
    }
}
```

Se quiser evitar o uso de literais de string, pode mapear os valores para uma **classe POCO** fortemente tipada.

---

### Arquivos por ambiente

Além do `appsettings.json`, você pode ter arquivos como:

- `appsettings.Development.json`
- `appsettings.Production.json`
- `appsettings.Staging.json`

Esses arquivos **sobrescrevem** valores do principal conforme o ambiente definido pela variável `ASPNETCORE_ENVIRONMENT`.

---

### Segurança e boas práticas

- **Não armazene segredos sensíveis** diretamente no `appsettings.json`. Use o recurso de [User Secrets](https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets) durante o desenvolvimento.
- Em produção, prefira **variáveis de ambiente** ou serviços como Azure Key Vault.

---

### Curiosidade útil

O Visual Studio 2022 organiza automaticamente os arquivos `appsettings.{Environment}.json` como filhos do `appsettings.json` na Solution Explorer, facilitando a navegação e manutenção.

---
