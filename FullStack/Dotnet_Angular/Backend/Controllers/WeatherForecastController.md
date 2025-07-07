# `WeatherForecastController`

O `WeatherForecastController` é um dos primeiros controladores gerados automaticamente em um projeto ASP.NET Core Web API. Ele serve como um exemplo funcional para demonstrar como criar e expor endpoints RESTful.

Esse controlador é excelente para aprendizado, mas em projetos reais você criará controladores específicos para suas entidades (como `ProdutoController`, `UsuarioController`, etc.). O `WeatherForecastController` é como um “laboratório” para entender os fundamentos.

---

## Finalidade do `WeatherForecastController`

Esse controlador simula uma API de previsão do tempo. Ele é útil para:

- Testar a estrutura básica de uma Web API
- Demonstrar como retornar dados em formato JSON
- Validar o funcionamento do pipeline HTTP no .NET

---

## Estrutura do controlador

```csharp
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
    private static readonly string[] Summaries = new[]
    {
        "Freezing", "Bracing", "Chilly", "Cool", "Mild",
        "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
    };

    private readonly ILogger<WeatherForecastController> _logger;

    public WeatherForecastController(ILogger<WeatherForecastController> logger)
    {
        _logger = logger;
    }

    [HttpGet]
    public IEnumerable<WeatherForecast> Get()
    {
        var rng = new Random();
        return Enumerable.Range(1, 5).Select(index => new WeatherForecast
        {
            Date = DateTime.Now.AddDays(index),
            TemperatureC = rng.Next(-20, 55),
            Summary = Summaries[rng.Next(Summaries.Length)]
        })
        .ToArray();
    }
}
```

---

### Explicando os principais elementos

- `[ApiController]`: Indica que essa classe é um controlador de API, habilitando validações automáticas e binding inteligente.
- `[Route("[controller]")]`: Define a rota como `/weatherforecast`, baseada no nome da classe.
- `ILogger`: Injetado via construtor para registrar logs (útil para depuração).
- `Summaries`: Array estático com descrições de clima.
- `Get()`: Método HTTP GET que retorna uma lista de objetos `WeatherForecast` com dados aleatórios.

---

## Como acessar no navegador

Ao iniciar o projeto com F5 no Visual Studio, você pode acessar: <https://localhost:40443/weatherforecast>

Esse endpoint retorna uma matriz JSON com 5 previsões de tempo simuladas. O número da porta pode variar conforme a configuração do projeto.

---

## Integração com o Frontend Angular

O Angular pode consumir esse endpoint via HTTP usando `HttpClient`. Isso permite:

- Obter dados simulados para exibir em componentes
- Testar chamadas assíncronas e tratamento de respostas
- Validar integração entre frontend e backend

---
