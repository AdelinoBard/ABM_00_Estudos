# **Formatação**

A formatação de código é subjetiva e não existe uma regra universal que deve ser seguida à risca. No entanto, o princípio fundamental é: **não perca tempo discutindo sobre formatação**. Utilize ferramentas automatizadas para padronizar seu código, como [EditorConfig](https://editorconfig.org/) ou o próprio **Code Cleanup** do Visual Studio. Isso economiza tempo e evita debates desnecessários entre engenheiros.

Para aspectos que não podem ser automatizados, como indentação, uso de espaços versus tabs, aspas simples versus duplas, entre outros, estabeleça um padrão claro e siga-o de forma consistente.

## **Utilize capitalização consistente**

C# é uma linguagem fortemente tipada, mas a consistência na capitalização ainda é essencial para a legibilidade do código. Use convenções como **PascalCase** para classes e métodos, e **camelCase** para variáveis e parâmetros.

**Ruim:**
```csharp
const int DAYS_IN_WEEK = 7;
const int daysInMonth = 30;

var songs = new List<string> { "Back In Black", "Stairway to Heaven", "Hey Jude" };
var Artists = new List<string> { "ACDC", "Led Zeppelin", "The Beatles" };

void EraseDatabase() {}
void restore_database() {}

class animal {}
class Alpaca {}
```

**Bom:**
```csharp
const int DaysInWeek = 7;
const int DaysInMonth = 30;

var songs = new List<string> { "Back In Black", "Stairway to Heaven", "Hey Jude" };
var artists = new List<string> { "ACDC", "Led Zeppelin", "The Beatles" };

void EraseDatabase() {}
void RestoreDatabase() {}

class Animal {}
class Alpaca {}
```

---

## **Mantenha funções e chamadas de funções próximas**

Em C#, o código deve fluir naturalmente. Se uma função chama outra, mantenha ambas próximas no arquivo-fonte, idealmente organizando-as de maneira lógica, com chamadas precedendo definições sempre que possível. Como os desenvolvedores tendem a ler código de cima para baixo, essa abordagem melhora a compreensão.

**Ruim:**
```csharp
class PerformanceReview
{
    private Employee employee;

    public PerformanceReview(Employee employee)
    {
        this.employee = employee;
    }

    public List<Employee> LookupPeers()
    {
        return Database.Lookup(employee, "peers");
    }

    public Employee LookupManager()
    {
        return Database.Lookup(employee, "manager");
    }

    public void GetPeerReviews()
    {
        var peers = LookupPeers();
        // ...
    }

    public void PerformReview()
    {
        GetPeerReviews();
        GetManagerReview();
        GetSelfReview();
    }

    public void GetManagerReview()
    {
        var manager = LookupManager();
    }

    public void GetSelfReview()
    {
        // ...
    }
}

// Uso da classe:
var review = new PerformanceReview(employee);
review.PerformReview();
```

**Bom:**
```csharp
class PerformanceReview
{
    private Employee employee;

    public PerformanceReview(Employee employee)
    {
        this.employee = employee;
    }

    public void PerformReview()
    {
        GetPeerReviews();
        GetManagerReview();
        GetSelfReview();
    }

    public void GetPeerReviews()
    {
        var peers = LookupPeers();
        // ...
    }

    private List<Employee> LookupPeers()
    {
        return Database.Lookup(employee, "peers");
    }

    public void GetManagerReview()
    {
        var manager = LookupManager();
    }

    private Employee LookupManager()
    {
        return Database.Lookup(employee, "manager");
    }

    public void GetSelfReview()
    {
        // ...
    }
}

// Uso da classe:
var review = new PerformanceReview(employee);
review.PerformReview();
```

---