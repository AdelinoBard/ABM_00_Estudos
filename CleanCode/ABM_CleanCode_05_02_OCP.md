# Princípio do Aberto/Fechado (OCP - Open/Closed Principle)  

Como definido por Bertrand Meyer, **"Entidades de software (classes, módulos, métodos) devem estar abertas para extensão, mas fechadas para modificação."** Isso significa que você deve poder **adicionar novas funcionalidades sem alterar código existente**, reduzindo riscos de regressão e melhorando a manutenibilidade.

## **Ruim (Violando o OCP):**
```csharp
public class AjaxAdapter : Adapter  
{
    public string Name => "ajaxAdapter";
}

public class NodeAdapter : Adapter  
{
    public string Name => "nodeAdapter";
}

public class HttpRequester  
{
    private readonly Adapter _adapter;

    public HttpRequester(Adapter adapter)  
    {
        _adapter = adapter;
    }

    public async Task<string> Fetch(string url)  
    {
        if (_adapter.Name == "ajaxAdapter")  
        {
            return await MakeAjaxCall(url);  
        }
        else if (_adapter.Name == "nodeAdapter")  
        {
            return await MakeHttpCall(url);  
        }
        throw new NotSupportedException("Adapter não suportado.");
    }

    private async Task<string> MakeAjaxCall(string url) { /* ... */ }  
    private async Task<string> MakeHttpCall(string url) { /* ... */ }  
}
```
**Problemas:**  
- `HttpRequester` **precisa ser modificado** sempre que um novo `Adapter` é adicionado.  
- Alto acoplamento: Lógica de requisição depende de verificações condicionais (`if-else`).  
- Viola OCP, pois novas implementações exigem mudanças na classe existente.  

## **Bom (Respeitando o OCP):**  
```csharp
public interface IAdapter  
{
    Task<string> Request(string url);  
}

public class AjaxAdapter : IAdapter  
{
    public async Task<string> Request(string url)  
    {
        // Implementação específica para AJAX...
    }
}

public class NodeAdapter : IAdapter  
{
    public async Task<string> Request(string url)  
    {
        // Implementação específica para HTTP (Node)...
    }
}

public class HttpRequester  
{
    private readonly IAdapter _adapter;

    public HttpRequester(IAdapter adapter)  
    {
        _adapter = adapter;
    }

    public async Task<string> Fetch(string url)  
    {
        var response = await _adapter.Request(url);  
        // Transformação comum da resposta (se necessário)...
        return response;  
    }
}
```
**Melhorias:**  
- **Extensível sem modificação**: Novos adapters (ex: `GraphQLAdapter`) só precisam implementar `IAdapter`.  
- **Fechado para mudanças**: `HttpRequester` não precisa ser alterado para novos adapters.  
- **Baixo acoplamento**: Depende de uma abstração (`IAdapter`), não de implementações concretas.  

## Princípios Aplicados:  
- **OCP**: Estende comportamentos sem modificar código existente.  
- **Inversão de Dependência (DIP)**: Depende de abstrações (`IAdapter`), não de classes concretas.  
- **Polimorfismo**: Cada adapter implementa sua lógica específica de forma isolada.  

## Exemplo de Uso:  
```csharp
var ajaxAdapter = new AjaxAdapter();  
var requester = new HttpRequester(ajaxAdapter);  
var result = await requester.Fetch("https://api.example.com");  
```

**Benefícios:**  
- Código mais **testável** (facilita mocking de `IAdapter`).  
- **Menos propenso a bugs**, pois mudanças são localizadas.  
- Alinhado com *Código Limpo*: **Claro, conciso e sustentável**.  