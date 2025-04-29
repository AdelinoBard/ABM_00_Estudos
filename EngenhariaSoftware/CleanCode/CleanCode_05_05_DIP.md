# Princípio da Inversão de Dependência (DIP) em C#

## Os Fundamentos do DIP

O Princípio da Inversão de Dependência estabelece dois conceitos essenciais:

1. **Módulos de alto nível não devem depender de módulos de baixo nível**. Ambos devem depender de abstrações.
2. **Abstrações não devem depender de detalhes**. Detalhes devem depender de abstrações.

Em C#, esse princípio é frequentemente implementado através de:
- Uso de interfaces e classes abstratas
- Injeção de Dependência (DI)
- Padrão de design Strategy

## Benefícios do DIP em C#

- **Redução de acoplamento**: Componentes ficam menos conectados entre si
- **Maior testabilidade**: Facilita o uso de mocks em testes unitários
- **Flexibilidade**: Permite trocar implementações sem modificar código cliente
- **Manutenibilidade**: Isola mudanças em partes específicas do sistema

## Exemplo Prático em C#

### Implementação Ruim (Violando o DIP)

```csharp
public class SqlProductRepository
{
    public Product GetById(int id)
    {
        // Acesso direto ao banco de dados SQL
    }
}

public class ProductService
{
    private readonly SqlProductRepository _repository;
    
    public ProductService()
    {
        _repository = new SqlProductRepository(); // Dependência concreta
    }
    
    public Product GetProduct(int id)
    {
        return _repository.GetById(id);
    }
}
```

**Problemas:**
- `ProductService` está fortemente acoplado a `SqlProductRepository`
- Difícil de testar isoladamente
- Impossível trocar a implementação do repositório sem modificar `ProductService`

### Implementação Boa (Respeitando o DIP)

```csharp
public interface IProductRepository
{
    Product GetById(int id);
}

public class SqlProductRepository : IProductRepository
{
    public Product GetById(int id)
    {
        // Implementação SQL
    }
}

public class MongoProductRepository : IProductRepository
{
    public Product GetById(int id)
    {
        // Implementação MongoDB
    }
}

public class ProductService
{
    private readonly IProductRepository _repository;
    
    public ProductService(IProductRepository repository) // Injeção de dependência
    {
        _repository = repository;
    }
    
    public Product GetProduct(int id)
    {
        return _repository.GetById(id);
    }
}

// Uso:
var sqlRepo = new SqlProductRepository();
var serviceWithSql = new ProductService(sqlRepo);

var mongoRepo = new MongoProductRepository();
var serviceWithMongo = new ProductService(mongoRepo);
```

**Melhorias:**
- `ProductService` depende apenas da abstração `IProductRepository`
- Fácil substituição de implementações
- Testabilidade melhorada (pode-se injetar um mock)
- Aberto para extensão, fechado para modificação (OCP)

## Padrões de Injeção de Dependência em C#

### 1. Injeção por Construtor (Recomendado)

```csharp
public class OrderProcessor
{
    private readonly IPaymentService _paymentService;
    private readonly IShippingService _shippingService;
    
    public OrderProcessor(IPaymentService paymentService, 
                        IShippingService shippingService)
    {
        _paymentService = paymentService;
        _shippingService = shippingService;
    }
}
```

### 2. Injeção por Propriedade

```csharp
public class ReportGenerator
{
    public IDataProvider DataProvider { get; set; }
}
```

### 3. Injeção por Método

```csharp
public class EmailSender
{
    public void Send(IMailService mailService, string message)
    {
        mailService.Send(message);
    }
}
```

## Integração com Containers DI

C# possui suporte nativo para Injeção de Dependência através do `IServiceCollection`:

```csharp
// Configuração no Startup.cs
public void ConfigureServices(IServiceCollection services)
{
    services.AddScoped<IProductRepository, SqlProductRepository>();
    services.AddTransient<IEmailService, SmtpEmailService>();
    services.AddSingleton<ILogger, FileLogger>();
}

// Uso em controllers ou serviços
public class ProductsController : Controller
{
    private readonly IProductRepository _repository;
    
    public ProductsController(IProductRepository repository)
    {
        _repository = repository;
    }
}
```

## Quando Aplicar o DIP

1. **Quando você precisa testar unidades isoladamente**
2. **Em componentes que podem ter múltiplas implementações**
3. **Em sistemas que precisam evoluir com o tempo**
4. **Quando trabalha com recursos externos (banco de dados, APIs, serviços)**

## Conclusão

Aplicar o Princípio da Inversão de Dependência em C#:

- **Desacopla** componentes do sistema  
- **Facilita** testes automatizados  
- **Torna** o código mais flexível e adaptável  
- **Prepara** o sistema para futuras mudanças  

---