# Estrutura inicial do projeto ASP.NET Core Web API

Ao criar um projeto de API Web com ASP.NET Core, o Visual Studio gera uma estrutura com os seguintes componentes principais:

## Pasta `Dependencies`

- Substitui a antiga pasta `References`.
- Contém todas as **dependências internas, externas e de terceiros**.
- Inclui pacotes NuGet como `Swashbuckle.AspNetCore` (Swagger), `Microsoft.EntityFrameworkCore`, entre outros.
- Permite gerenciar bibliotecas essenciais para compilar e executar o projeto.

## Pasta `/Controllers/`

- Armazena os **controladores da API**, como `WeatherForecastController.cs`.
- Cada controller expõe endpoints HTTP (GET, POST, PUT, DELETE).
- Utiliza atributos como `[ApiController]` e `[Route]` para definir rotas e comportamentos.

## Arquivos de nível raiz

| Arquivo | Função |
| --- | --- |
| `Program.cs` | Ponto de entrada da aplicação. Configura serviços, middleware e rotas. |
| `appsettings.json` | Arquivo de configuração. Define strings de conexão, variáveis, etc. |

---

## Conceitos fundamentais do back-end ASP.NET

### Middleware

- Componentes que processam requisições HTTP.
- Ex: autenticação, logging, CORS, roteamento.

### APIs RESTful

- ASP.NET Core é ideal para criar APIs que retornam dados em **JSON**.
- Os endpoints são consumidos facilmente pelo Angular via `HttpClient`.

### Injeção de Dependência

- ASP.NET Core possui suporte nativo.
- Permite registrar serviços e utilizá-los nos controllers de forma desacoplada.

---

## Por que não há `/Pages/` ou `/Views/`?

Esse modelo é uma **API Web**, não um projeto MVC tradicional. Portanto:

- Não há Razor Pages ou Views.
- O foco é **exclusivamente em fornecer dados** para o frontend Angular.
- Toda a renderização da interface é feita no Angular, enquanto o ASP.NET cuida da lógica e persistência.

---

## Comunicação com o Angular

O Angular consome os endpoints da API via HTTP. Exemplo:

```typescript
this.http
  .get<WeatherForecast[]>("/weatherforecast")
  .subscribe((data) => (this.previsoes = data));
```

Essa integração é fluida e permite que o frontend seja totalmente desacoplado do backend.

---
