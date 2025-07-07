# `WeatherForecast.cs`

O arquivo `WeatherForecast.cs` é um dos primeiros modelos gerados automaticamente quando você cria um projeto ASP.NET Core Web API no Visual Studio. Ele serve como um exemplo funcional para demonstrar como uma API pode retornar dados tipados em formato JSON.

Embora útil para aprendizado, o `WeatherForecast.cs` geralmente é substituído por modelos reais conforme o projeto evolui. Mas ele continua sendo uma ótima referência para entender os fundamentos da arquitetura Web API no .NET.

---

## O que é o `WeatherForecast.cs`?

É uma **classe modelo** que representa uma previsão do tempo. Ela é usada pelo controlador `WeatherForecastController` para retornar dados simulados via requisições HTTP GET.

## Estrutura típica da classe

```csharp
public class WeatherForecast
{
    public DateTime Date { get; set; }
    public int TemperatureC { get; set; }
    public string? Summary { get; set; }

    public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
}
```

---

### Explicando cada propriedade

- `Date`: Representa a data da previsão.
- `TemperatureC`: Temperatura em graus Celsius.
- `Summary`: Texto descritivo do clima (ex: "Chilly", "Hot").
- `TemperatureF`: Temperatura em Fahrenheit, calculada dinamicamente com base em `TemperatureC`.

Essa estrutura é simples, mas poderosa para mostrar como o ASP.NET Core serializa objetos em JSON automaticamente.

---

## Relação com o `WeatherForecastController`

O controlador usa essa classe para retornar uma lista de previsões:

```csharp
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
```

Esse método simula cinco dias de previsão com dados aleatórios. É uma forma prática de testar o funcionamento da API sem depender de banco de dados.

---

## Utilidade no desenvolvimento

- Permite testar rapidamente o funcionamento da API.
- Serve como base para criar modelos mais complexos.
- Ajuda a entender como o ASP.NET Core lida com serialização JSON.
- Facilita testes com ferramentas como Swagger UI ou Postman.

---
