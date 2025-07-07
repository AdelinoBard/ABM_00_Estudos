# `launchSettings.json`

Ele está localizado na pasta `/Properties` do projeto backend e é usado pelo Visual Studio e pela CLI do .NET para definir como a aplicação será iniciada.

---

## Finalidade do `launchSettings.json`

Esse arquivo define **perfis de inicialização** que controlam:

- Qual servidor será usado (IIS Express ou Kestrel)
- Quais URLs a aplicação escutará
- Se o navegador será aberto automaticamente
- Quais variáveis de ambiente serão aplicadas

---

## Estrutura modelo

```json
{
  "$schema": "http://json.schemastore.org/launchsettings.json",
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iisExpress": {
      "applicationUrl": "http://localhost:40080",
      "sslPort": 40443
    }
  },
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": false,
      "launchUrl": "swagger",
      "applicationUrl": "http://localhost:40080",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development",
        "ASPNETCORE_HOSTINGSTARTUPASSEMBLIES": "Microsoft.AspNetCore.SpaProxy"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": false,
      "launchUrl": "swagger",
      "applicationUrl": "https://localhost:40443;http://localhost:40080",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development",
        "ASPNETCORE_HOSTINGSTARTUPASSEMBLIES": "Microsoft.AspNetCore.SpaProxy"
      }
    },
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": false,
      "launchUrl": "swagger",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development",
        "ASPNETCORE_HOSTINGSTARTUPASSEMBLIES": "Microsoft.AspNetCore.SpaProxy"
      }
    }
  }
}
```

---

### Explicando os principais elementos

- **`commandName`**: Define como o projeto será iniciado. `"Project"` usa o servidor Kestrel; `"IISExpress"` usa o IIS Express.
- **`applicationUrl`**: Define as portas e protocolos que a aplicação escutará. Neste caso, HTTP na porta 40080 e HTTPS na 40443.
- **`launchBrowser`**: Se `true`, o navegador será aberto automaticamente ao iniciar a aplicação.
- **`launchUrl`**: Define a rota inicial, como `"swagger"` para abrir a documentação da API.
- **`environmentVariables`**:
  - `"ASPNETCORE_ENVIRONMENT"`: Define o ambiente (`Development`, `Staging`, `Production`).
  - `"ASPNETCORE_HOSTINGSTARTUPASSEMBLIES"`: Usado para habilitar o proxy SPA, essencial para integração com Angular.

---

## Portas fixas: por que são importantes?

Usar portas fixas como `40080` e `40443` facilita a integração com o frontend Angular, que pode depender de proxies e endpoints estáveis. Isso evita erros como `404 Not Found` quando o Angular tenta se comunicar com o backend.

---

## Perfis múltiplos: como usar?

Você pode alternar entre os perfis (`http`, `https`, `IIS Express`) diretamente no Visual Studio, usando o menu suspenso ao lado do botão de execução. Isso permite testar diferentes cenários sem alterar o código.

---
