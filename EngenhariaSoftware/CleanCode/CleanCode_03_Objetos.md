# **Objetos**

## Use Propriedades (Properties) em C#

Em C#, a forma idiomática e recomendada de acessar e modificar dados em objetos é através de **propriedades**. As propriedades combinam a flexibilidade dos métodos `get` e `set` com a sintaxe concisa de um acesso direto a um campo. Isso oferece vários benefícios, e de uma maneira mais integrada à linguagem C#:

  * **Abstração:** Se a lógica interna de como o valor é obtido ou definido mudar, apenas a implementação da propriedade precisa ser alterada, sem que o código que a utiliza precise ser modificado.

  * **Validação:** Você pode adicionar lógica de validação dentro do acessador `set` da propriedade para garantir que os dados estejam sempre em um estado válido.

  * **Encapsulamento:** As propriedades permitem controlar o acesso aos campos internos da classe, expondo apenas o que é necessário.

  * **Log e Tratamento de Erros:** É fácil adicionar logging, tratamento de exceções ou outras operações dentro dos acessadores `get` e `set`.

  * **Lazy Loading:** Você pode implementar o carregamento tardio de dados dentro do acessador `get` de uma propriedade.

**Ruim (abordagem menos idiomática em C#):**

```csharp
public class BankAccount
{
    public decimal Balance; // Campo público - acesso direto

    // ... outros membros
}

public class Example
{
    public static void Main(string[] args)
    {
        BankAccount account = new BankAccount();
        account.Balance = 100; // Acesso direto ao campo
        Console.WriteLine($"Saldo: {account.Balance}");
    }
}
```

**Bom (usando propriedades em C#):**

```csharp
public class BankAccount
{
    private decimal _balance; // Campo privado

    // Propriedade pública para acessar e modificar o saldo
    public decimal Balance
    {
        get { return _balance; }
        set
        {
            // Adicione validação aqui, se necessário
            if (value >= 0)
            {
                _balance = value;
            }
            else
            {
                Console.WriteLine("O saldo não pode ser negativo.");
                // Ou lance uma exceção: throw new ArgumentException("O saldo não pode ser negativo.");
            }
        }
    }

    // ... outros membros
}

public class Example
{
    public static void Main(string[] args)
    {
        BankAccount account = new BankAccount();
        account.Balance = 100; // Usando a propriedade
        Console.WriteLine($"Saldo: {account.Balance}");

        account.Balance = -50; // A validação na propriedade será executada
        Console.WriteLine($"Saldo após tentativa inválida: {account.Balance}");
    }
}
```

## Faça Objetos Terem Membros Privados (Usando Modificadores de Acesso em C#)

Em C#, o conceito de tornar membros de objetos privados é fundamental para o encapsulamento e é feito através dos **modificadores de acesso**. Os mais comuns são `private`, `public`, `protected`, `internal` e `protected internal`. Para garantir que os dados internos de um objeto não sejam modificados diretamente de fora da classe, você deve declarar os campos como `private` (ou `internal protected` em cenários específicos) e fornecer acesso controlado através de propriedades ou métodos públicos.

**Ruim (campo público):**

```csharp
public class Employee
{
    public string Name;

    public string GetName()
    {
        return Name;
    }

    public Employee(string name)
    {
        Name = name;
    }
}

public class Example
{
    public static void Main(string[] args)
    {
        Employee employee = new Employee("John Doe");
        Console.WriteLine($"Nome do empregado: {employee.GetName()}"); // Nome do empregado: John Doe

        employee.Name = null; // Modificação direta do campo público
        Console.WriteLine($"Nome do empregado após modificação direta: {employee.GetName()}"); // Nome do empregado após modificação direta:
    }
}
```

**Bom (campo privado com propriedade pública):**

```csharp
public class Employee
{
    private string _name;

    public string Name
    {
        get { return _name; }
        // O setter pode ser omitido se você não quiser permitir modificação externa
        // set { _name = value; }
    }

    public Employee(string name)
    {
        _name = name;
    }

    public string GetName()
    {
        return _name;
    }
}

public class Example
{
    public static void Main(string[] args)
    {
        Employee employee = new Employee("John Doe");
        Console.WriteLine($"Nome do empregado: {employee.GetName()}"); // Nome do empregado: John Doe

        // employee._name = null; // Isso geraria um erro de compilação, pois _name é privado
        // employee.Name = null; // Se o setter da propriedade Name for omitido, isso também gerará um erro

        Console.WriteLine($"Nome do empregado após tentativa de modificação: {employee.GetName()}"); // Nome do empregado após tentativa de modificação: John Doe
    }
}
```

Em C#, as propriedades são a maneira padrão e mais limpa de implementar o acesso controlado aos dados de um objeto, seguindo os princípios de encapsulamento do Código Limpo. Elas oferecem uma sintaxe elegante e são amplamente utilizadas em todo o ecossistema .NET.

---