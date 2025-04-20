# **Funções**

## Argumentos de Funções (Idealmente 2 ou Menos)

Limitar o número de parâmetros em funções é essencial para manter o código testável e compreensível. Com mais de três parâmetros, você enfrenta uma explosão combinatória de casos de teste, onde cada argumento precisa ser validado em diversas combinações.

O ideal é usar **um ou dois argumentos**. Três argumentos devem ser considerados o limite máximo, e qualquer quantidade superior deve ser repensada. Geralmente, muitos parâmetros indicam que a função está tentando fazer coisas demais. Quando isso não for o caso, frequentemente um objeto (classe ou struct) pode encapsular os dados relacionados.

Em C#, você pode usar **classes**, **structs** ou **records** para agrupar parâmetros relacionados, tornando o código mais limpo e expressivo.

### Vantagens de Usar Objetos como Parâmetros:

1. **Clareza na assinatura**: Fica evidente quais propriedades a função utiliza
2. **Manutenção simplificada**: Adicionar ou remover parâmetros não exige mudanças na assinatura do método
3. **Imutabilidade**: Usando `readonly struct` ou `record`, você pode garantir que os dados não serão alterados
4. **Validação centralizada**: O objeto pode validar seu próprio estado

**Ruim** (muitos parâmetros primitivos):
```csharp
public void CreateMenu(string title, string body, string buttonText, bool cancellable)
{
    // ...
}
```

**Bom** (usando um objeto parâmetro):
```csharp
// Usando record (imutável por padrão)
public record MenuOptions(string Title, string Body, string ButtonText, bool Cancellable);

public void CreateMenu(MenuOptions options)
{
    // ...
}

// Chamada mais limpa
CreateMenu(new MenuOptions(
    Title: "Foo",
    Body: "Bar",
    ButtonText: "Baz",
    Cancellable: true
));
```

**Alternativa com classe** (útil para validação complexa):
```csharp
public class MenuOptions
{
    public string Title { get; }
    public string Body { get; }
    public string ButtonText { get; }
    public bool Cancellable { get; }
    
    public MenuOptions(string title, string body, string buttonText, bool cancellable)
    {
        Title = title ?? throw new ArgumentNullException(nameof(title));
        Body = body ?? throw new ArgumentNullException(nameof(body));
        ButtonText = buttonText ?? throw new ArgumentNullException(nameof(buttonText));
        Cancellable = cancellable;
    }
}
```

### Dicas Adicionais para C#:

1. **Parâmetros opcionais**: Use parâmetros nomeados e opcionais para casos simples
   ```csharp
   public void CreateMenu(string title, string body, string buttonText = "OK", bool cancellable = true)
   ```

2. **Pattern matching**: Em C# 7.0+, você pode usar desconstrução para objetos
   ```csharp
   public void ProcessMenu((string title, string body, string buttonText) menu)
   {
       var (title, body, buttonText) = menu;
       // ...
   }
   ```

3. **Métodos de extensão**: Quando apropriado, use métodos de extensão para manter as funções próximas aos dados que manipulam

Lembre-se: **Funções pequenas com poucos parâmetros são mais fáceis de testar, manter e reutilizar**. Quando sentir necessidade de muitos parâmetros, considere refatorar para objetos bem definidos.

---

## Funções Devem Fazer Apenas Uma Coisa

Este é o princípio mais importante da engenharia de software. Quando funções tentam fazer múltiplas coisas, tornam-se difíceis de compor, testar e entender. Funções com responsabilidade única são mais fáceis de refatorar, testar e reutilizar, resultando em código significativamente mais limpo.

Em C#, podemos aplicar esse princípio usando:

1. **Métodos pequenos e focados**
2. **Separação de preocupações**
3. **Composição de funções**
4. **LINQ para operações em coleções**
5. **Métodos estáticos puros quando apropriado**

**Ruim** (múltiplas responsabilidades):
```csharp
public void EmailClients(IEnumerable<Client> clients)
{
    foreach (var client in clients)
    {
        var clientRecord = database.Lookup(client.Id);
        if (clientRecord.IsActive)
        {
            EmailService.Send(client);
        }
    }
}
```

**Bom** (responsabilidades separadas):
```csharp
public void EmailActiveClients(IEnumerable<Client> clients)
{
    var activeClients = clients.Where(IsActiveClient);
    activeClients.ForEach(EmailClient);
}

private bool IsActiveClient(Client client)
{
    var clientRecord = database.Lookup(client.Id);
    return clientRecord.IsActive;
}

private void EmailClient(Client client)
{
    EmailService.Send(client);
}
```

### Melhorias Adicionais para C#:

1. **Usando LINQ para maior clareza**:
```csharp
public void EmailActiveClients(IEnumerable<Client> clients)
{
    clients
        .Where(client => database.Lookup(client.Id).IsActive)
        .ToList()
        .ForEach(EmailClient);
}
```

2. **Métodos de extensão para melhor legibilidade**:
```csharp
public static class ClientExtensions
{
    public static bool IsActive(this Client client, IDatabase database)
    {
        return database.Lookup(client.Id).IsActive;
    }
}

// Uso:
clients.Where(c => c.IsActive(database)).ForEach(EmailClient);
```

3. **Padrão Repository para abstração de dados**:
```csharp
public class ClientService
{
    private readonly IClientRepository _repository;
    private readonly IEmailService _emailService;

    public void EmailActiveClients()
    {
        _repository.GetActiveClients().ForEach(_emailService.Send);
    }
}
```

### Benefícios desta Abordagem em C#:

1. **Testabilidade**: Cada função pode ser testada isoladamente
2. **Reusabilidade**: `IsActiveClient` pode ser usado em outros contextos
3. **Manutenibilidade**: Mudanças em como clientes ativos são determinados afetam apenas uma função
4. **Legibilidade**: O código de alto nível expressa claramente a intenção
5. **Paralelismo**: Fica mais fácil paralelizar operações quando são atômicas

Lembre-se: **Se uma função faz mais do que o que seu nome sugere, ela está violando o princípio da responsabilidade única**. Quebre funções complexas em operações atômicas que possam ser compostas para formar comportamentos mais complexos.

---

## Nomes de Funções Devem Revelar sua Intenção

Em C#, os nomes das funções devem comunicar claramente seu propósito sem exigir que o leitor examine sua implementação. Um bom nome de função:

1. **Explica exatamente o que a função faz**
2. **Evita ambiguidades ou significados ocultos**
3. **Usa verbos fortes que descrevem a ação**
4. **Inclui o contexto quando necessário**
5. **Segue as convenções de nomeação do C# (PascalCase para métodos)**

**Ruim** (nome ambíguo):
```csharp
public void AddToDate(DateTime date, int value)
{
    // ...
}

// Chamada confusa - o que está sendo adicionado?
AddToDate(currentDate, 5);
```

**Bom** (nome explícito):
```csharp
public DateTime AddMonthsToDate(int months, DateTime date)
{
    return date.AddMonths(months);
}

// Chamada clara
var newDate = AddMonthsToDate(5, currentDate);
```

### Padrões Recomendados para C#:

1. **Prefira verbos específicos**:
   - `CalculateTotal()` em vez de `ProcessData()`
   - `ValidateCredentials()` em vez de `CheckUser()`

2. **Para métodos booleanos, use prefixos como "Is", "Has", "Can"**:
   ```csharp
   public bool IsActiveUser(User user)
   public bool HasPendingOrders(Customer customer)
   public bool CanUserEditDocument(User user, Document doc)
   ```

3. **Métodos que retornam algo devem descrever o retorno**:
   ```csharp
   public decimal CalculateOrderTotal(Order order)
   public TimeSpan GetRemainingTime(DateTime deadline)
   ```

4. **Para void methods, use verbos de ação forte**:
   ```csharp
   public void SendEmailNotification(EmailMessage message)
   public void LogSecurityEvent(SecurityEvent @event)
   ```

**Exemplo Avançado com C# Moderno**:

```csharp
// Ruim - nome genérico demais
public void Process(Employee emp, DateTime dt) { ... }

// Bom - específico e expressivo
public void UpdateEmployeeHireDate(Employee employee, DateTime newHireDate)
{
    employee.HireDate = newHireDate;
    _repository.Save(employee);
}

// Melhor ainda - usando records e imutabilidade
public record UpdateHireDateCommand(EmployeeId Id, DateTime NewHireDate);

public Employee Handle(UpdateHireDateCommand command)
{
    var employee = _repository.GetById(command.Id);
    return employee with { HireDate = command.NewHireDate };
}
```

### Dicas Específicas para C#:

1. **Considere usar substantivos para métodos de conversão**:
   ```csharp
   public string AsBase64String(byte[] data)
   public Money ToLocalCurrency(Money amount, Currency targetCurrency)
   ```

2. **Para métodos assíncronos, adicione o sufixo "Async"**:
   ```csharp
   public async Task<Report> GenerateSalesReportAsync(DateTimeRange period)
   ```

3. **Evite abreviações** (exceto para termos amplamente conhecidos):
   ```csharp
   // Ruim
   public void CalcTot(Order ord)
   
   // Bom
   public void CalculateOrderTotal(Order order)
   ```

Lembre-se: **O nome da função deve deixar óbvio o que ela faz, o que recebe e o que retorna**. Se você precisar ler o corpo da função para entender seu propósito, o nome precisa ser melhorado.

---

## Funções Devem Manter um Único Nível de Abstração

Em C#, manter cada função em um único nível de abstração é crucial para criar código limpo e sustentável. Quando uma função mistura níveis de abstração (detalhes de implementação com lógica de alto nível), torna-se difícil de entender, testar e manter.

### Problemas do Código com Múltiplos Níveis:
- Difícil de testar unidades específicas
- Baixa reutilização de código
- Violação do Princípio da Responsabilidade Única
- Dificuldade em isolar problemas

**Ruim** (múltiplos níveis de abstração):
```csharp
public void ProcessCode(string code)
{
    // Nível 1: Configuração (alto nível)
    var regexPatterns = new List<string> { /* padrões regex */ };
    
    // Nível 2: Tokenização (médio nível)
    var statements = code.Split(' ');
    var tokens = new List<string>();
    
    foreach (var pattern in regexPatterns)
    {
        var regex = new Regex(pattern);
        foreach (var statement in statements)
        {
            tokens.Add(regex.Match(statement).Value);
        }
    }
    
    // Nível 3: Análise léxica (baixo nível)
    var ast = new List<SyntaxNode>();
    foreach (var token in tokens)
    {
        ast.Add(new Lexer().ParseToken(token));
    }
    
    // Nível 1 novamente: Processamento (alto nível)
    foreach (var node in ast)
    {
        new Compiler().CompileNode(node);
    }
}
```

**Bom** (níveis de abstração separados):
```csharp
// Alto nível: Orquestração
public void ProcessCode(string code)
{
    var tokens = Tokenize(code, GetRegexPatterns());
    var syntaxTree = Lex(tokens);
    Compile(syntaxTree);
}

// Médio nível: Tokenização
private List<string> Tokenize(string code, IEnumerable<string> patterns)
{
    var statements = code.Split(' ');
    var tokens = new List<string>();
    
    foreach (var pattern in patterns)
    {
        tokens.AddRange(MatchPattern(statements, pattern));
    }
    
    return tokens;
}

// Baixo nível: Operação concreta
private IEnumerable<string> MatchPattern(IEnumerable<string> inputs, string pattern)
{
    var regex = new Regex(pattern);
    return inputs.Select(input => regex.Match(input).Value);
}

// Médio nível: Análise léxica
private List<SyntaxNode> Lex(IEnumerable<string> tokens)
{
    return tokens.Select(token => new Lexer().ParseToken(token)).ToList();
}

// Alto nível: Compilação
private void Compile(IEnumerable<SyntaxNode> syntaxTree)
{
    var compiler = new Compiler();
    foreach (var node in syntaxTree)
    {
        compiler.CompileNode(node);
    }
}
```

### Técnicas Específicas para C#:

1. **Métodos de Extensão para Encadeamento**:
```csharp
public static class CodeProcessingExtensions
{
    public static List<string> Tokenize(this string code, IEnumerable<string> patterns)
    {
        // implementação
    }
    
    public static List<SyntaxNode> ToSyntaxTree(this IEnumerable<string> tokens)
    {
        // implementação
    }
}

// Uso fluente:
code.Tokenize(patterns).ToSyntaxTree().ForEach(node => Compiler.Compile(node));
```

2. **LINQ para Abstração de Operações**:
```csharp
private List<string> Tokenize(string code, IEnumerable<string> patterns)
{
    return patterns
        .SelectMany(pattern => 
            code.Split(' ')
                .Select(s => new Regex(pattern).Match(s).Value))
        .ToList();
}
```

3. **Padrão Strategy para Variações**:
```csharp
public interface ITokenizer
{
    IEnumerable<string> Tokenize(string code);
}

public class RegexTokenizer : ITokenizer { /* implementação */ }
public class LexicalTokenizer : ITokenizer { /* implementação */ }

// A função de alto nível não muda mesmo com implementações diferentes
public void ProcessCode(string code, ITokenizer tokenizer)
{
    var tokens = tokenizer.Tokenize(code);
    // ... restante do processamento
}
```

### Benefícios desta Abordagem em C#:

1. **Testabilidade Unitária**: Cada função pode ser testada isoladamente
2. **Reusabilidade**: Componentes como `Tokenize` podem ser usados em outros contextos
3. **Manutenção**: Mudanças em um nível não afetam outros níveis
4. **Legibilidade**: O código de alto nível lê-se como documentação
5. **Extensibilidade**: Novas implementações podem ser adicionadas sem modificar a lógica principal

Lembre-se: **Se sua função contém tanto detalhes de implementação quanto lógica de negócios, ela está violando o princípio de abstração única**. Sempre que você vir operações de baixo nível (como manipulação de strings, loops complexos) misturadas com lógica de negócios, é hora de refatorar.

---

## Remova Código Duplicado

Em C#, a eliminação de duplicação é crucial para criar código sustentável. Duplicação aumenta o risco de inconsistências e torna a manutenção mais difícil.

### Exemplo - Eliminando Duplicação em Exibição de Funcionários

**Ruim** (código duplicado):
```csharp
public void ShowDeveloperList(IEnumerable<Developer> developers)
{
    foreach (var developer in developers)
    {
        var data = new DeveloperDisplayData(
            developer.CalculateExpectedSalary(),
            developer.GetExperience(),
            developer.GetGithubLink()
        );
        
        Render(data);
    }
}

public void ShowManagerList(IEnumerable<Manager> managers)
{
    foreach (var manager in managers)
    {
        var data = new ManagerDisplayData(
            manager.CalculateExpectedSalary(),
            manager.GetExperience(),
            manager.GetMBAProjects()
        );
        
        Render(data);
    }
}
```

**Bom** (usando herança ou interfaces):
```csharp
// Abordagem com interface
public interface IEmployee
{
    decimal CalculateExpectedSalary();
    int GetExperience();
    EmployeeDisplayData GetDisplayData();
}

public class Developer : IEmployee { /* implementação */ }
public class Manager : IEmployee { /* implementação */ }

public void ShowEmployeeList(IEnumerable<IEmployee> employees)
{
    foreach (var employee in employees)
    {
        var data = employee.GetDisplayData();
        Render(data);
    }
}
```

**Alternativa com padrão Visitor** (para lógica mais complexa):
```csharp
public interface IEmployeeVisitor<T>
{
    T Visit(Developer developer);
    T Visit(Manager manager);
}

public class DisplayDataVisitor : IEmployeeVisitor<DisplayData>
{
    public DisplayData Visit(Developer developer)
    {
        return new DisplayData(
            developer.CalculateExpectedSalary(),
            developer.GetExperience(),
            githubLink: developer.GetGithubLink());
    }
    
    public DisplayData Visit(Manager manager)
    {
        return new DisplayData(
            manager.CalculateExpectedSalary(),
            manager.GetExperience(),
            portfolio: manager.GetMBAProjects());
    }
}
```

### Definindo Objetos Padrão em C#

**Ruim** (lógica de preenchimento manual):
```csharp
public class MenuConfig
{
    public string Title { get; set; }
    public string Body { get; set; }
    public string ButtonText { get; set; }
    public bool Cancellable { get; set; }
}

public void CreateMenu(MenuConfig config)
{
    config.Title = config.Title ?? "Foo";
    config.Body = config.Body ?? "Bar";
    config.ButtonText = config.ButtonText ?? "Baz";
    config.Cancellable = config.Cancellable != null ? config.Cancellable : true;
}
```

**Bom** (usando inicializadores de objetos):
```csharp
public class MenuConfig
{
    public string Title { get; set; } = "Foo";
    public string Body { get; set; } = "Bar";
    public string ButtonText { get; set; } = "Baz";
    public bool Cancellable { get; set; } = true;
}

// Uso:
var config = new MenuConfig 
{
    Title = "Order",
    ButtonText = "Send"
    // Body e Cancellable manterão os valores padrão
};
```

**Melhor ainda** (usando records no C# 9+):
```csharp
public record MenuConfig(
    string Title = "Foo",
    string Body = "Bar",
    string ButtonText = "Baz",
    bool Cancellable = true);

// Uso imutável:
var defaultConfig = new MenuConfig();
var customConfig = defaultConfig with 
{
    Title = "Order",
    ButtonText = "Send"
};
```

### Técnicas Avançadas para Eliminar Duplicação em C#:

1. **Métodos de Extensão** para comportamentos comuns:
```csharp
public static class EmployeeExtensions
{
    public static decimal CalculateBonus(this IEmployee employee)
    {
        return employee.CalculateExpectedSalary() * 0.1m;
    }
}
```

2. **Generics** para algoritmos reutilizáveis:
```csharp
public T Process<T>(T input) where T : IProcessable
{
    // Lógica genérica de processamento
    input.Validate();
    input.Transform();
    return input;
}
```

3. **Template Method Pattern** para esqueletos de algoritmos:
```csharp
public abstract class ReportGenerator
{
    public void GenerateReport()
    {
        var data = GetData();
        var processed = ProcessData(data);
        Render(processed);
    }
    
    protected abstract IEnumerable<Data> GetData();
    protected abstract Report ProcessData(IEnumerable<Data> data);
}
```

### Benefícios desta Abordagem:

1. **Manutenção Simplificada**: Mudanças em apenas um lugar
2. **Consistência**: Comportamento uniforme em toda a aplicação
3. **Testabilidade**: Lógica centralizada é mais fácil de testar
4. **Legibilidade**: Menos código repetitivo = código mais limpo
5. **Extensibilidade**: Novos tipos podem aderir às interfaces existentes

Lembre-se: **"Não se repita" (DRY) é um dos princípios mais importantes do desenvolvimento de software**. Em C#, utilize interfaces, herança, métodos de extensão e generics para criar abstrações eficientes que eliminem duplicação sem comprometer a clareza do código.

---

## Não Use Flags Booleanas como Parâmetros

Em C#, parâmetros booleanos que alteram significativamente o comportamento de uma função indicam uma violação do **Princípio da Responsabilidade Única**. Isso torna o código:

- Menos legível (a intenção não é clara na chamada)
- Mais difícil de manter (complexidade ciclomática aumentada)
- Menos testável (mais caminhos de execução para testar)

**Ruim** (função faz duas coisas):
```csharp
public void CreateFile(string name, bool isTemporary)
{
    if (isTemporary)
    {
        File.Create(Path.Combine("./temp", name));
    }
    else
    {
        File.Create(name);
    }
}

// Chamada ambígua - o que "true" significa?
CreateFile("data.txt", true);
```

**Bom** (funções especializadas):
```csharp
public void CreateFile(string path)
{
    File.Create(path);
}

public void CreateTemporaryFile(string fileName)
{
    CreateFile(Path.Combine("./temp", fileName));
}

// Chamada auto-documentada
CreateTemporaryFile("data.txt");
```

## Soluções Avançadas para C#

### 1. Usando Enums (quando há múltiplas opções)
```csharp
public enum FileLocation
{
    Persistent,
    Temporary,
    Cache
}

public void CreateFile(string name, FileLocation location)
{
    var path = location switch
    {
        FileLocation.Temporary => Path.Combine("./temp", name),
        FileLocation.Cache => Path.Combine("./cache", name),
        _ => name
    };
    
    File.Create(path);
}
```

### 2. Padrão Factory Method
```csharp
public interface IFileCreator
{
    void Create(string name);
}

public class TempFileCreator : IFileCreator { /* implementação */ }
public class PersistentFileCreator : IFileCreator { /* implementação */ }

// Uso:
var creator = new TempFileCreator();
creator.Create("data.txt");
```

### 3. Métodos de Extensão (para APIs fluentes)
```csharp
public static class FileExtensions
{
    public static void CreateTemporary(this FileService fileService, string name)
    {
        fileService.Create(Path.Combine("./temp", name));
    }
}

// Uso:
fileService.CreateTemporary("data.txt");
```

### 4. Parâmetros Opcionais (apenas para casos simples)
```csharp
// Ainda não ideal, mas melhor que flag booleana
public void CreateFile(string name, string directory = null)
{
    var path = directory != null ? Path.Combine(directory, name) : name;
    File.Create(path);
}
```

## Quando é Aceitável Usar Booleanos como Parâmetros?

Apenas quando o parâmetro:
1. **Não altera o fluxo principal** da função
2. **Controla um comportamento secundário** opcional
3. **Tem um nome extremamente descritivo**

**Exemplo aceitável**:
```csharp
public void SendEmail(EmailMessage message, bool shouldRetryOnFailure)
{
    try {
        _emailService.Send(message);
    }
    catch when (shouldRetryOnFailure) {
        // Lógica de retry
    }
}
```

## Benefícios desta Abordagem em C#

1. **Clareza**: As chamadas de método se auto-documentam
2. **Coesão**: Cada função faz exatamente uma coisa
3. **Extensibilidade**: Fácil adicionar novos comportamentos sem modificar funções existentes
4. **Testabilidade**: Cada caminho pode ser testado isoladamente
5. **Manutenção**: Menos propenso a erros quando o comportamento precisa mudar

Lembre-se: **Se você precisar escrever um comentário para explicar o que um parâmetro booleano faz, sua função está tentando fazer coisas demais.** Prefira sempre dividir em funções especializadas.

---

## Evite Efeitos Colaterais (Parte 1)

Em C#, funções sem efeitos colaterais (puras) são mais seguras, previsíveis e fáceis de testar.

**Ruim** (modifica estado externo):
```csharp
public static string Name = "Ryan McDermott";

public static void SplitIntoFirstAndLastName()
{
    Name = Name.Split(' ')[0]; // Efeito colateral: modifica variável estática
}

// Uso:
SplitIntoFirstAndLastName();
Console.WriteLine(Name); // Modificado
```

**Bom** (função pura):
```csharp
public static (string FirstName, string LastName) SplitIntoFirstAndLastName(string fullName)
{
    var parts = fullName.Split(' ');
    return (parts[0], parts.Length > 1 ? parts[1] : "");
}

// Uso:
var name = "Ryan McDermott";
var (firstName, lastName) = SplitIntoFirstAndLastName(name);
Console.WriteLine(name); // Original intacto
```

### Padrões C# para Minimizar Efeitos Colaterais:

1. **Métodos estáticos puros**:
```csharp
public static class StringExtensions
{
    public static string Capitalize(this string input) 
        => string.IsNullOrEmpty(input) ? input : char.ToUpper(input[0]) + input[1..];
}
```

2. **Records para imutabilidade** (C# 9+):
```csharp
public record User(string FirstName, string LastName)
{
    public User CapitalizeNames() 
        => this with 
        {
            FirstName = FirstName.Capitalize(),
            LastName = LastName.Capitalize()
        };
}
```

## Evite Efeitos Colaterais (Parte 2) - Trabalhando com Objetos

Em C#, objetos são passados por referência, exigindo cuidado especial:

**Ruim** (modifica parâmetro):
```csharp
public void AddItemToCart(List<CartItem> cart, Item item)
{
    cart.Add(new CartItem(item, DateTime.Now)); // Efeito colateral
}
```

**Bom** (abordagem imutável):
```csharp
// Usando record imutável
public record CartItem(Item Item, DateTime AddedDate);

public List<CartItem> AddItemToCart(List<CartItem> cart, Item item)
{
    return new List<CartItem>(cart) 
    { 
        new CartItem(item, DateTime.Now) 
    };
}

// Alternativa com LINQ (cria nova lista)
public List<CartItem> AddItemToCart(IEnumerable<CartItem> cart, Item item) 
    => cart.Append(new CartItem(item, DateTime.Now)).ToList();
```

### Técnicas Avançadas em C#:

1. **Padrão Builder para objetos complexos**:
```csharp
public class CartBuilder
{
    private readonly List<CartItem> _items = new();
    
    public CartBuilder AddItem(Item item) 
        => new CartBuilder(_items.Append(new CartItem(item, DateTime.Now)));
    
    public ImmutableList<CartItem> Build() => _items.ToImmutableList();
}
```

2. **Collections imutáveis**:
```csharp
using System.Collections.Immutable;

public ImmutableList<CartItem> AddItemToCart(ImmutableList<CartItem> cart, Item item)
    => cart.Add(new CartItem(item, DateTime.Now));
```

3. **Cópia profunda para objetos complexos**:
```csharp
public static T DeepCopy<T>(this T original) where T : notnull
{
    using var stream = new MemoryStream();
    JsonSerializer.Serialize(stream, original);
    stream.Position = 0;
    return JsonSerializer.Deserialize<T>(stream)!;
}
```

## Quando Efeitos Colaterais são Necessários

Para operações que precisam modificar estado (banco de dados, arquivos, etc):

1. **Padrão Repository**:
```csharp
public class ShoppingCartService
{
    private readonly ICartRepository _repository;
    
    public async Task<Cart> AddItemAsync(CartId cartId, Item item)
    {
        var cart = await _repository.GetAsync(cartId);
        var updatedCart = cart.AddItem(item);
        await _repository.SaveAsync(updatedCart);
        return updatedCart;
    }
}
```

2. **Command Pattern**:
```csharp
public interface ICommand<T>
{
    T Execute();
    bool CanUndo { get; }
    T Undo();
}

public class AddCartItemCommand : ICommand<Cart>
{
    // Implementação com undo support
}
```

## Benefícios desta Abordagem em C#

1. **Thread-safety**: Código imutável é naturalmente thread-safe
2. **Testabilidade**: Funções puras são extremamente fáceis de testar
3. **Previsibilidade**: Sem surpresas com estados compartilhados
4. **Manutenção**: Mudanças têm escopo limitado
5. **Debugging**: Menos estados para rastrear

Lembre-se: **Em C#, utilize `readonly`, `record`, `ImmutableCollections` e retornos de métodos para criar código mais seguro e limpo**. Reserve efeitos colaterais para camadas específicas (como repositórios ou serviços) e mantenha sua lógica de negócios pura.

---

## Evite Modificar Classes Base do Sistema

Em C#, modificar tipos globais ou base (como `object`, `string`, `List<T>`) pode causar problemas:

- **Colisões** com outras bibliotecas ou partes do sistema
- **Comportamento inesperado** quando outros desenvolvedores não esperam suas extensões
- **Dificuldade de manutenção** quando o comportamento padrão muda em atualizações

### Abordagem Ruim (Modificação Direta)
```csharp
// RUIM: Estendendo List<T> diretamente (não recomendado)
public static class ListExtensions
{
    public static List<T> Diff<T>(this List<T> source, List<T> comparison)
    {
        var hash = new HashSet<T>(comparison);
        return source.Where(elem => !hash.Contains(elem)).ToList();
    }
}

// Uso:
var list = new List<int> {1, 2, 3};
var diff = list.Diff(new List<int> {2}); // Funciona, mas polui todos os List<T>
```

### Abordagem Recomendada (Herança ou Composição)
```csharp
// Opção 1: Usando herança (similar ao exemplo JavaScript bom)
public class EnhancedList<T> : List<T>
{
    public EnhancedList() : base() {}
    public EnhancedList(IEnumerable<T> collection) : base(collection) {}
    
    public EnhancedList<T> Diff(IEnumerable<T> comparison)
    {
        var hash = new HashSet<T>(comparison);
        return new EnhancedList<T>(this.Where(elem => !hash.Contains(elem)));
    }
}

// Opção 2: Usando composição (padrão mais seguro)
public class DiffList<T>
{
    private readonly List<T> _items = new();
    
    public IReadOnlyList<T> Items => _items.AsReadOnly();
    
    public void Add(T item) => _items.Add(item);
    public void AddRange(IEnumerable<T> items) => _items.AddRange(items);
    
    public DiffList<T> Diff(IEnumerable<T> comparison)
    {
        var hash = new HashSet<T>(comparison);
        var result = new DiffList<T>();
        result.AddRange(_items.Where(elem => !hash.Contains(elem)));
        return result;
    }
}
```

### Alternativa Recomendada para C#: Métodos de Extensão Controlados

C# permite métodos de extensão de forma mais segura que a modificação de protótipos em JavaScript, por exemplo, mas ainda requer cuidado:

```csharp
// BOM: Método de extensão em namespace específico
namespace MyApp.Collections.Extensions
{
    public static class MyListExtensions
    {
        public static List<T> CalculateDifference<T>(this List<T> source, 
                                                   IEnumerable<T> comparison)
        {
            var hash = new HashSet<T>(comparison);
            return source.Where(elem => !hash.Contains(elem)).ToList();
        }
    }
}

// Uso (requer using explícito):
using MyApp.Collections.Extensions;

var list = new List<int> {1, 2, 3};
var diff = list.CalculateDifference(new[] {2}); // Mais explícito e seguro
```

## Boas Práticas para C#

1. **Prefira composição à herança** para estender funcionalidades
2. **Use namespaces** para organizar e controlar extensões
3. **Seja explícito** em nomes de métodos de extensão
4. **Documente cuidadosamente** qualquer extensão de tipo base
5. **Considere classes utilitárias** em vez de extensões globais

```csharp
// Alternativa com classe utilitária
public static class CollectionUtilities
{
    public static List<T> FindDifference<T>(List<T> source, List<T> comparison)
    {
        var hash = new HashSet<T>(comparison);
        return source.Where(elem => !hash.Contains(elem)).ToList();
    }
}

// Uso mais seguro e explícito:
var diff = CollectionUtilities.FindDifference(list1, list2);
```

## Quando Considerar Métodos de Extensão

São aceitáveis quando:
1. A funcionalidade é **genérica** e **amplamente útil**
2. O nome é **auto-descritivo** e **não ambíguo**
3. Estão **organizados em namespaces** específicos
4. Não **entram em conflito** com funcionalidades existentes

```csharp
// Extensão bem projetada para C#
public static class EnumerableExtensions
{
    public static IEnumerable<T> Except<T>(this IEnumerable<T> source,
                                          IEnumerable<T> comparison,
                                          IEqualityComparer<T> comparer = null)
    {
        var hash = new HashSet<T>(comparison, comparer ?? EqualityComparer<T>.Default);
        return source.Where(elem => !hash.Contains(elem));
    }
}
```

Lembre-se: **Em C#, a clareza e segurança do código devem sempre vir antes da conveniência**. Evite poluir namespaces globais com extensões não essenciais.

---

## Favoreça Programação Funcional quando Apropriado

Em C#, embora seja uma linguagem principalmente orientada a objetos, temos ótimos suportes para programação funcional através de:

- **LINQ (Language Integrated Query)**
- **Expressões lambda**
- **Métodos de extensão funcionais**
- **Imutabilidade (records, readonly structs)**
- **Delegates e Func/Action**

### Exemplo Ruim (Estilo Imperativo)
```csharp
var programmerOutput = new[]
{
    new { Name = "Uncle Bobby", LinesOfCode = 500 },
    new { Name = "Suzie Q", LinesOfCode = 1500 },
    new { Name = "Jimmy Gosling", LinesOfCode = 150 },
    new { Name = "Gracie Hopper", LinesOfCode = 1000 }
};

int totalOutput = 0;

for (int i = 0; i < programmerOutput.Length; i++)
{
    totalOutput += programmerOutput[i].LinesOfCode;
}
```

### Exemplo Bom (Estilo Funcional com LINQ)
```csharp
var programmerOutput = new[]
{
    new { Name = "Uncle Bobby", LinesOfCode = 500 },
    new { Name = "Suzie Q", LinesOfCode = 1500 },
    new { Name = "Jimmy Gosling", LinesOfCode = 150 },
    new { Name = "Gracie Hopper", LinesOfCode = 1000 }
};

const int initialValue = 0;

// Abordagem 1: LINQ puro
var totalOutput = programmerOutput
    .Sum(p => p.LinesOfCode);

// Abordagem 2: Mais explícito (similar ao JavaScript)
var totalOutput2 = programmerOutput
    .Select(p => p.LinesOfCode)
    .Aggregate((acc, lines) => acc + lines);
```

## Benefícios da Abordagem Funcional em C#

1. **Código mais declarativo**: Diz "o que" fazer em vez de "como" fazer
2. **Menos propenso a erros**: Elimina variáveis temporárias e estados mutáveis
3. **Mais fácil de paralelizar**: Operações como `AsParallel()` podem ser adicionadas facilmente
4. **Mais conciso**: Reduz a quantidade de código boilerplate
5. **Melhor testabilidade**: Funções puras são mais fáceis de testar isoladamente

## Técnicas Funcionais Avançadas em C#

### 1. Imutabilidade com Records
```csharp
public record ProgrammerOutput(string Name, int LinesOfCode);

var data = new[]
{
    new ProgrammerOutput("Uncle Bobby", 500),
    new ProgrammerOutput("Suzie Q", 1500)
};

// Transformação funcional
var lines = data.Select(p => p with { LinesOfCode = p.LinesOfCode * 2 });
```

### 2. Pipeline de Operações
```csharp
var result = programmerOutput
    .Where(p => p.LinesOfCode > 100)
    .OrderBy(p => p.Name)
    .GroupBy(p => p.LinesOfCode > 1000)
    .ToDictionary(g => g.Key ? "Senior" : "Junior", g => g.ToList());
```

### 3. Composição de Funções
```csharp
public static class FunctionalExtensions
{
    public static Func<T, TResult> Compose<T, TIntermediate, TResult>(
        this Func<T, TIntermediate> func1, 
        Func<TIntermediate, TResult> func2) => 
        x => func2(func1(x));
}

// Uso:
Func<int, int> double = x => x * 2;
Func<int, string> toString = x => x.ToString();
var doubleAndString = double.Compose(toString);
var result = doubleAndString(5); // "10"
```

## Quando Usar Programação Imperativa em C#

Embora a abordagem funcional seja poderosa, há casos onde o estilo imperativo é mais adequado:

1. **Performance crítica**: Loops podem ser mais rápidos que LINQ
2. **Fluxo complexo**: Quando há muita lógica condicional aninhada
3. **Mutabilidade necessária**: Ao trabalhar com APIs legadas ou otimizações

```csharp
// Híbrido: Imperativo quando necessário, mas encapsulado
public static int CalculateTotalLines(IEnumerable<ProgrammerOutput> programmers)
{
    var total = 0;
    foreach (var p in programmers)
    {
        if (p.LinesOfCode > 0)
            total += p.LinesOfCode;
    }
    return total;
}
```

## Boas Práticas para C# Funcional

1. **Prefira `IEnumerable`** para representar sequências
2. **Use métodos de extensão** para criar pipelines legíveis
3. **Aproveite os delegates** (`Func`, `Action`) para flexibilidade
4. **Mantenha funções puras** quando possível (sem side-effects)
5. **Combine com OOP** - use classes para estado e funções para transformações

```csharp
// Exemplo completo com imutabilidade e LINQ
public record Programmer(string Name, int LinesOfCode);

public static class ProgrammerAnalysis
{
    public static int TotalLinesOfCode(IEnumerable<Programmer> programmers) =>
        programmers.Sum(p => p.LinesOfCode);
    
    public static IEnumerable<string> BusyProgrammers(IEnumerable<Programmer> programmers) =>
        programmers
            .Where(p => p.LinesOfCode > 1000)
            .OrderByDescending(p => p.LinesOfCode)
            .Select(p => p.Name);
}
```

Lembre-se: **Em C#, a programação funcional complementa a OOP, não a substitui**. Use o melhor de cada paradigma conforme a situação exigir.

---

## Encapsule Condicionais

Em C#, podemos encapsular condicionais complexos em métodos ou propriedades bem nomeados para melhorar a legibilidade.

**Ruim:**
```csharp
if (fsm.State == "fetching" && !listNode.Any())
{
    // ...
}
```

**Bom:**
```csharp
private bool ShouldShowSpinner(StateMachine fsm, IEnumerable<Node> listNode)
{
    return fsm.State == "fetching" && !listNode.Any();
}

// Uso:
if (ShouldShowSpinner(fsmInstance, listNodeInstance))
{
    // ...
}
```

**Melhor ainda** (usando propriedade):
```csharp
public class SpinnerControl
{
    private readonly StateMachine _fsm;
    private readonly IEnumerable<Node> _nodes;
    
    public bool ShouldShow => _fsm.State == "fetching" && !_nodes.Any();
    
    // Uso:
    if (spinnerControl.ShouldShow) { ... }
}
```

## Evite Negações em Condicionais

Negações em nomes de métodos ou condições podem tornar o código confuso.

**Ruim:**
```csharp
if (!IsNodeNotPresent(node)) 
{
    // ...
}
```

**Bom:**
```csharp
if (IsNodePresent(node)) 
{
    // ...
}
```

**Dica**: Em C#, considere usar `enums` para estados complexos:
```csharp
public enum NodeState { Present, Absent, Loading }

if (node.State == NodeState.Present) { ... }
```

## Evite Condicionais com Polimorfismo

Em C#, podemos usar herança e interfaces para eliminar condicionais complexos.

**Ruim:**
```csharp
public class Airplane
{
    public AirplaneType Type { get; set; }
    
    public int GetCruisingAltitude()
    {
        switch (Type)
        {
            case AirplaneType.Boeing777:
                return MaxAltitude - PassengerCount;
            case AirplaneType.AirForceOne:
                return MaxAltitude;
            case AirplaneType.Cessna:
                return MaxAltitude - FuelExpenditure;
            default:
                throw new InvalidOperationException();
        }
    }
}
```

**Bom** (usando herança):
```csharp
public abstract class Airplane
{
    public abstract int GetCruisingAltitude();
    protected int MaxAltitude { get; set; }
}

public class Boeing777 : Airplane
{
    public int PassengerCount { get; set; }
    
    public override int GetCruisingAltitude() 
        => MaxAltitude - PassengerCount;
}

public class AirForceOne : Airplane
{
    public override int GetCruisingAltitude() 
        => MaxAltitude;
}

public class Cessna : Airplane
{
    public int FuelExpenditure { get; set; }
    
    public override int GetCruisingAltitude() 
        => MaxAltitude - FuelExpenditure;
}
```

**Melhor ainda** (usando padrão strategy):
```csharp
public interface ICruisingAltitudeCalculator
{
    int Calculate(Airplane plane);
}

public class Boeing777Calculator : ICruisingAltitudeCalculator { ... }
public class AirForceOneCalculator : ICruisingAltitudeCalculator { ... }

public class Airplane
{
    private readonly ICruisingAltitudeCalculator _calculator;
    
    public Airplane(ICruisingAltitudeCalculator calculator)
    {
        _calculator = calculator;
    }
    
    public int GetCruisingAltitude() => _calculator.Calculate(this);
}
```

## Técnicas Avançadas para C#

### 1. Pattern Matching (C# 7+)
```csharp
public int GetCruisingAltitude() => this switch
{
    Boeing777 b => b.MaxAltitude - b.PassengerCount,
    AirForceOne a => a.MaxAltitude,
    Cessna c => c.MaxAltitude - c.FuelExpenditure,
    _ => throw new InvalidOperationException()
};
```

### 2. Dicionário de Funções
```csharp
private static readonly Dictionary<AirplaneType, Func<Airplane, int>> AltitudeCalculators = 
    new()
    {
        [AirplaneType.Boeing777] = a => a.MaxAltitude - ((Boeing777)a).PassengerCount,
        [AirplaneType.AirForceOne] = a => a.MaxAltitude,
        [AirplaneType.Cessna] = a => a.MaxAltitude - ((Cessna)a).FuelExpenditure
    };

public int GetCruisingAltitude() => AltitudeCalculators[Type](this);
```

### 3. Delegates e Expressões Lambda
```csharp
public class Airplane
{
    private readonly Func<int> _cruisingAltitudeCalculator;
    
    public Airplane(Func<int> cruisingAltitudeCalculator)
    {
        _cruisingAltitudeCalculator = cruisingAltitudeCalculator;
    }
    
    public int GetCruisingAltitude() => _cruisingAltitudeCalculator();
}

// Uso:
var boeing = new Airplane(() => maxAlt - passengerCount);
```

## Benefícios desta Abordagem em C#

1. **Menos acoplamento**: Cada classe/função tem uma única responsabilidade
2. **Mais fácil de testar**: Lógica isolada em pequenas unidades
3. **Mais extensível**: Novos tipos não exigem modificação de switches existentes
4. **Mais legível**: Nomes expressivos revelam a intenção
5. **Menos propenso a erros**: Elimina casos default em switches

Lembre-se: **Em C#, o polimorfismo (herança, interfaces, delegates) geralmente é uma solução melhor que condicionais complexos**. Reserve condicionais simples para fluxos de controle básicos e encapsule a complexidade em estruturas bem definidas.

---

## Parte 1: Utilize Polimorfismo em vez de Checagem de Tipos

Em C#, embora a linguagem seja fortemente tipada, ainda podemos cair na tentação de fazer checagem de tipos desnecessária.

**Ruim** (checagem de tipo com `is` ou `GetType()`):
```csharp
public void TravelToTexas(Vehicle vehicle)
{
    if (vehicle is Bicycle bicycle)
    {
        bicycle.Pedal(this.CurrentLocation, new Location("Texas"));
    }
    else if (vehicle is Car car)
    {
        car.Drive(this.CurrentLocation, new Location("Texas"));
    }
}
```

**Bom** (usando polimorfismo):
```csharp
public abstract class Vehicle
{
    public abstract void Move(Location from, Location to);
}

public class Bicycle : Vehicle
{
    public override void Move(Location from, Location to)
    {
        // Implementação específica para bicicleta
        Pedal(from, to);
    }
    
    private void Pedal(Location from, Location to) { ... }
}

public class Car : Vehicle
{
    public override void Move(Location from, Location to)
    {
        // Implementação específica para carro
        Drive(from, to);
    }
    
    private void Drive(Location from, Location to) { ... }
}

// Uso:
public void TravelToTexas(Vehicle vehicle)
{
    vehicle.Move(this.CurrentLocation, new Location("Texas"));
}
```

**Melhor ainda** (usando interface):
```csharp
public interface IMovable
{
    void Move(Location from, Location to);
}

public class Bicycle : IMovable { ... }
public class Car : IMovable { ... }

public void TravelToTexas(IMovable vehicle)
{
    vehicle.Move(this.CurrentLocation, new Location("Texas"));
}
```

## Parte 2: Aproveite o Sistema de Tipos Forte do C#

Em C#, o compilador já faz a checagem de tipos para nós, então não precisamos fazer verificações manuais como em JavaScript, por exemplo.

**Ruim** (verificação desnecessária):
```csharp
public object Combine(object val1, object val2)
{
    if ((val1 is int && val2 is int) || 
        (val1 is string && val2 is string))
    {
        return (dynamic)val1 + (dynamic)val2;
    }
    throw new ArgumentException("Must be of type int or string");
}
```

**Bom** (sobrecarga de métodos):
```csharp
public int Combine(int val1, int val2) => val1 + val2;
public string Combine(string val1, string val2) => val1 + val2;

// Ou usando generics com restrições
public T Combine<T>(T val1, T val2) where T : IAddable<T>
{
    return val1.Add(val2);
}
```

## Técnicas Avançadas para Evitar Checagem de Tipos em C#

### 1. Padrão Visitor para Operações Tipo-Dependentes
```csharp
public interface IVehicleVisitor
{
    void Visit(Bicycle bicycle);
    void Visit(Car car);
}

public abstract class Vehicle
{
    public abstract void Accept(IVehicleVisitor visitor);
}

public class TravelVisitor : IVehicleVisitor
{
    private readonly Location _from;
    private readonly Location _to;
    
    public TravelVisitor(Location from, Location to)
    {
        _from = from;
        _to = to;
    }
    
    public void Visit(Bicycle bicycle) => bicycle.Pedal(_from, _to);
    public void Visit(Car car) => car.Drive(_from, _to);
}
```

### 2. Pattern Matching Moderno (C# 7+)
```csharp
public void ProcessVehicle(Vehicle vehicle)
{
    switch (vehicle)
    {
        case Bicycle b when b.IsElectric:
            b.Charge();
            b.Ride();
            break;
        case Bicycle b:
            b.Ride();
            break;
        case Car c:
            c.Drive();
            break;
        default:
            throw new UnknownVehicleException();
    }
}
```

### 3. Generics com Restrições
```csharp
public interface IAddable<T>
{
    T Add(T other);
}

public class Calculator<T> where T : IAddable<T>
{
    public T Add(T a, T b) => a.Add(b);
}
```

## Quando a Checagem de Tipo é Aceitável em C#

1. **Conversão segura** (operador `as` com null check)
   ```csharp
   if (vehicle is Car car)
   {
       car.ChangeOil();
   }
   ```

2. **Tratamento de exceções específicas**
   ```csharp
   try {
       // operação
   }
   catch (SpecificException ex) {
       // tratamento específico
   }
   ```

3. **Plugins ou sistemas dinâmicos** (uso moderado de `dynamic`)

## Benefícios desta Abordagem em C#

1. **Segurança em tempo de compilação**: Erros são pegos antes da execução
2. **Código mais limpo**: Elimina verificações redundantes
3. **Extensibilidade**: Novos tipos podem ser adicionados sem modificar a lógica existente
4. **Melhor desempenho**: Evita verificações em tempo de execução
5. **Manutenção mais fácil**: O compilador ajuda a identificar problemas

Lembre-se: **Em C#, o sistema de tipos é seu aliado**. Projete suas classes e hierarquias para que o compilador possa verificar o máximo possível, evitando verificações manuais de tipo. Use polimorfismo, interfaces e generics para criar código mais seguro e limpo.

---

## Escreva Código Claro Primeiro, Otimize Depois

Em C# o compilador JIT (Just-In-Time) e o runtime fazem otimizações avançadas automaticamente. Muitas micro-otimizações que eram relevantes no passado hoje são desnecessárias ou até contraproducentes.

### Exemplo Ruim (Otimização Prematura)
```csharp
// Código "otimizado" mas menos legível
for (int i = 0, len = list.Count; i < len; i++) 
{
    // Processamento que não beneficia desta otimização
    ProcessItem(list[i]);
}
```

### Exemplo Bom (Código Limpo e Legível)
```csharp
// Forma mais clara e simples
foreach (var item in list)
{
    ProcessItem(item);
}

// Ou usando LINQ para maior expressividade
list.ForEach(ProcessItem);
```

## Quando Considerar Otimizações em C#

1. **Hot paths identificados** (após profiling)
2. **Algoritmos de alta complexidade**
3. **Processamento de grandes volumes de dados**
4. **Aplicações em tempo real crítico**

### Técnicas de Otimização Relevantes para C#

1. **Uso de `Span<T>` e `Memory<T>`** para evitar alocações:
```csharp
public void ProcessSpan(Span<int> data)
{
    for (int i = 0; i < data.Length; i++)
    {
        data[i] *= 2;
    }
}
```

2. **Structs para evitar alocação no heap**:
```csharp
public readonly struct Point3D
{
    public readonly double X, Y, Z;
    
    public Point3D(double x, double y, double z) => (X, Y, Z) = (x, y, z);
}
```

3. **Pooling de objetos** para tipos frequentemente alocados/desalocados:
```csharp
var pool = ArrayPool<int>.Shared;
var buffer = pool.Rent(1024);
try 
{
    // Usar buffer
}
finally 
{
    pool.Return(buffer);
}
```

## Boas Práticas para Performance em C#

1. **Sempre meça antes de otimizar** (use o BenchmarkDotNet)
2. **Prefira clareza sobre micro-otimizações**
3. **Aproveite as otimizações do compilador**:
   - O JIT faz inline de métodos pequenos
   - Remove código morto
   - Otimiza loops

4. **Use recursos modernos do C#**:
```csharp
// Exemplo: Pattern matching com performance
public double ComputeArea(object shape) => shape switch
{
    Square s => s.Side * s.Side,
    Circle c => c.Radius * c.Radius * Math.PI,
    _ => throw new ArgumentException()
};
```

## Casos Onde Otimizações São Justificáveis

1. **Processamento batch de alta performance**:
```csharp
// Paralelismo bem aplicado
Parallel.ForEach(largeCollection, item => 
{
    ProcessCPUIntensive(item);
});
```

2. **Operações com strings de alta frequência**:
```csharp
// Usando StringBuilder para muitas concatenações
var sb = new StringBuilder();
for (int i = 0; i < 1000; i++)
{
    sb.Append(i);
}
```

3. **Acesso a banco de dados**:
```csharp
// Otimização justificada para queries
var results = await connection.QueryAsync<Customer>(
    "SELECT * FROM Customers WHERE Region = @region",
    new { region });
```

## Ferramentas para Análise de Performance em C#

1. **Profiler do Visual Studio**
2. **BenchmarkDotNet** para micro-benchmarks
3. **PerfView** para análise detalhada
4. **Diagnostic Tools** no Visual Studio

```csharp
// Exemplo de benchmark com BenchmarkDotNet
[MemoryDiagnoser]
public class LoopBenchmark
{
    private List<int> data = Enumerable.Range(0, 1000).ToList();
    
    [Benchmark]
    public int ForLoop()
    {
        int sum = 0;
        for (int i = 0; i < data.Count; i++)
        {
            sum += data[i];
        }
        return sum;
    }
    
    [Benchmark]
    public int ForEachLoop()
    {
        int sum = 0;
        foreach (var item in data)
        {
            sum += item;
        }
        return sum;
    }
}
```

Lembre-se: **Em C#, escreva primeiro o código mais limpo e legível possível**. Só otimize após identificar gargalos reais através de medições precisas. O runtime do .NET é altamente otimizado e muitas micro-otimizações manuais podem:
- Reduzir a legibilidade
- Introduzir bugs sutis
- Dificultar a manutenção
- Ter pouco ou nenhum impacto na performance real

**Regra de ouro**: "Primeiro faça funcionar corretamente, depois meça, e só então otimize - se necessário."

---

## Mantenha Seu Código Base Limpo e Livre de Código Inútil

Em C#, código morto (não utilizado) é tão prejudicial quanto em outras linguagens. Ele:

- Aumenta a complexidade desnecessariamente
- Pode causar confusão durante a manutenção
- Pode levar a falsos positivos em análises estáticas
- Aumenta o tamanho do assembly desnecessariamente

### Exemplo Ruim (Código Morto)
```csharp
// Método antigo não utilizado
public static string OldRequestModule(string url)
{
    // Implementação desatualizada
    return LegacyHttpClient.Get(url);
}

// Novo método que substituiu o anterior
public static async Task<string> NewRequestModule(string url)
{
    return await HttpClient.GetStringAsync(url);
}

// Uso atual (só usa o novo método)
var response = await NewRequestModule("https://api.example.com/data");
```

### Exemplo Bom (Código Limpo)
```csharp
// Apenas o método atualizado permanece
public static async Task<string> RequestModule(string url)
{
    return await HttpClient.GetStringAsync(url);
}

// Uso
var response = await RequestModule("https://api.example.com/data");
```

## Como Identificar e Remover Código Morto em C#

### 1. Ferramentas Estáticas
- **Analisador de Código do Visual Studio** (Mostra métodos não usados)
- **ReSharper/Rider** (Identifica código inacessível)
- **Roslyn Analyzers** (Pode ser configurado para detectar código não utilizado)

### 2. Técnicas Manuais
- **Busca por referências** (Ctrl+F12 no Visual Studio)
- **Coverage de testes** (Revela código não exercitado)
- **Deprecação progressiva**:
```csharp
[Obsolete("Este método será removido na versão 2.0. Use o método RequestModule.")]
public static string OldRequestModule(string url) { ... }
```

### 3. Boas Práticas para C#
- **Remova imediatamente** quando identificar código não utilizado
- **Use #if DEBUG** apenas para código de debug temporário
```csharp
#if DEBUG
public void TemporaryDebugMethod() { ... }
#endif
```
- **Documente decisões** de remoção no histórico de commits

## Casos Especiais em C#

### 1. Métodos Públicos em Bibliotecas
Se você desenvolve uma biblioteca pública, alguns métodos podem parecer não utilizados mas são necessários para a API:
```csharp
public class MyLibrary
{
    // Pode parecer não usado, mas é parte da API pública
    public void Initialize() { ... }
}
```

### 2. Código Chamado por Reflexão
```csharp
// Pode parecer não utilizado, mas é chamado via reflection
[HttpPost]
public IActionResult HiddenEndpoint([FromBody] DataModel data) { ... }
```

### 3. Handlers de Eventos
Alguns métodos podem ser registrados dinamicamente:
```csharp
// Registrado em outro lugar via +=
public void OnDataReceived(object sender, EventArgs e) { ... }
```

## Benefícios de Remover Código Morto em C#

1. **Melhora a manutenibilidade** - Menos código para analisar
2. **Reduz o tamanho do assembly** - Compilações mais rápidas
3. **Facilita refatorações** - Menos dependências ocultas
4. **Melhora a segurança** - Remove potenciais vetores de ataque não monitorados
5. **Documentação mais precisa** - O código existente reflete melhor a realidade

## Ferramentas Recomendadas para C#

1. **NDepend** - Análise avançada de dependências
2. **SonarQube** - Detecção de código morto
3. **Coverlet** - Análise de cobertura de testes
4. **Roslyn Code Cleanup** - Limpeza automática

Lembre-se: **Seu controle de versão (Git, SVN, etc) já mantém o histórico**. Não há necessidade de manter código não utilizado "só por precaução". Remova com confiança e mantenha sua base de código limpa e eficiente.

---