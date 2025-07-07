# Controllers

Controllers são **classes responsáveis por lidar com requisições HTTP**. Eles fazem parte do padrão MVC (Model-View-Controller) e são essenciais em projetos ASP.NET Core, especialmente em APIs REST.

## Funções principais

- Receber requisições do cliente (Angular, por exemplo)
- Executar lógica de negócio ou chamar serviços
- Retornar respostas (geralmente em JSON)

---

## Estrutura e localização

- Os controllers ficam na pasta `/Controllers/` do projeto.
- Cada controller é uma classe C# com sufixo `Controller`, como `ProdutoController`.
- Em APIs Web, os controllers geralmente **herdam de `ControllerBase`**, pois não precisam renderizar views.

```csharp
[ApiController]
[Route("[controller]")]
public class ProdutoController : ControllerBase
{
    [HttpGet]
    public IEnumerable<Produto> Get() => _produtoService.ListarTodos();
}
```

---

## Diferença entre `Controller` e `ControllerBase`

| Classe Base      | Uso Principal                   | Renderiza Views? |
| ---------------- | ------------------------------- | ---------------- |
| `Controller`     | Projetos MVC com HTML           | Sim              |
| `ControllerBase` | APIs REST (como no seu projeto) | Não              |

---

## Ciclo de vida de uma requisição

1. O Angular faz uma chamada HTTP para a API.
2. O middleware de roteamento do ASP.NET Core identifica o controller e a action.
3. O método do controller é executado.
4. A resposta (geralmente JSON) é enviada de volta ao Angular.

---

## Exemplo prático: `WeatherForecastController`

Esse controller é gerado automaticamente em projetos ASP.NET Core Web API. Ele:

- Simula dados de previsão do tempo
- Expõe um endpoint `/weatherforecast`
- Retorna uma lista de objetos `WeatherForecast` em JSON

É ideal para testes iniciais e para entender como funciona a comunicação entre backend e frontend.

---

## Configurações comuns em controllers

Controllers permitem aplicar configurações coletivas como:

- Autorização (`[Authorize]`)
- Roteamento (`[Route("api/[controller]")]`)
- Cache (`[ResponseCache(Duration = 60)]`)

Essas configurações podem ser aplicadas por atributos diretamente na classe ou nos métodos.

---

## Integração com Angular

No Angular, você pode usar o `HttpClient` para consumir os endpoints dos controllers:

```typescript
this.http
  .get<WeatherForecast[]>("/weatherforecast")
  .subscribe((data) => (this.previsoes = data));
```

Essa comunicação é fluida graças à estrutura clara dos controllers no ASP.NET Core.

---

## Obs

Em um projeto ASP.NET MVC típico, os controladores são usados ​​principalmente para servir as visualizações ao cliente, que contêm conteúdo HTML estático ou dinâmico. Esse não é o caso em projetos de API Web, cujo principal objetivo é servir saída JSON (APIs REST), respostas baseadas em XML (serviços web SOAP), um recurso estático ou criado dinamicamente (arquivos JPG, JS e CSS) ou mesmo uma resposta HTTP simples (como um redirecionamento HTTP 301) sem o corpo do conteúdo.

---
