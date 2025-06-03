## **3. Como Implementar Encapsulamento em C#**

O encapsulamento é um dos pilares fundamentais da Programação Orientada a Objetos (POO). Em C#, ele é implementado principalmente através de modificadores de acesso e propriedades, permitindo controlar rigorosamente como os dados de uma classe são acessados e modificados.

### **3.1 Implementação Básica**

#### **a) Atributos Privados + Métodos Públicos (Abordagem Tradicional)**

```csharp
public class ContaBancaria
{
    // Atributo privado - só acessível dentro da classe
    private double _saldo;

    // Método público para operação de depósito
    public void Depositar(double valor)
    {
        if (valor > 0)
            _saldo += valor;
        else
            Console.WriteLine("Valor de depósito inválido!");
    }

    // Método público para consulta segura
    public double ObterSaldo()
    {
        return _saldo;
    }
}
```

**Vantagens:**

- Controle total sobre as operações
- Possibilidade de adicionar validações complexas
- Clareza na intenção (métodos como ações)

**Uso:**

```csharp
var conta = new ContaBancaria();
conta.Depositar(500);
Console.WriteLine($"Saldo: {conta.ObterSaldo()}");
```

#### **b) Propriedades (Abordagem Moderna)**

```csharp
public class ContaBancaria
{
    private double _saldo;

    // Propriedade com lógica de validação
    public double Saldo
    {
        get => _saldo;
        private set  // Set pode ser restrito
        {
            if (value >= 0)
                _saldo = value;
            else
                Console.WriteLine("Saldo não pode ser negativo!");
        }
    }

    // Método que utiliza a propriedade internamente
    public void AplicarJuros(double taxa)
    {
        Saldo *= (1 + taxa/100); // Usa o setter da propriedade
    }
}
```

**Vantagens:**

- Sintaxe mais limpa e intuitiva
- Combina acesso direto com lógica de validação
- Pode ter níveis de acesso diferentes para get/set

**Uso:**

```csharp
var conta = new ContaBancaria();
// conta.Saldo = -100; // Erro - set é privado
Console.WriteLine(conta.Saldo); // Get público
```

### **3.2 Padrões Avançados de Encapsulamento**

#### **a) Propriedades Auto-Implementadas**

Para casos simples sem lógica adicional:

```csharp
public class Cliente
{
    public string Nome { get; set; } // Getter e setter padrão
    public int Id { get; } // Somente leitura (set apenas no construtor)

    public Cliente(int id)
    {
        Id = id; // Pode ser setado apenas no construtor
    }
}
```

#### **b) Encapsulamento com Expressões Corporadas (C# 7+)**

```csharp
public class Retangulo
{
    private double _largura;
    private double _altura;

    public double Area => _largura * _altura; // Propriedade somente-leitura

    public Retangulo(double largura, double altura)
    {
        _largura = largura > 0 ? largura : throw new ArgumentException();
        _altura = altura > 0 ? altura : throw new ArgumentException();
    }
}
```

#### **c) Padrão de Backing Field**

```csharp
public class Temperatura
{
    private double _celsius;

    public double Celsius
    {
        get => _celsius;
        set => _celsius = value >= -273.15 ? value : _celsius;
    }

    public double Fahrenheit
    {
        get => (_celsius * 9/5) + 32;
        set => _celsius = (value - 32) * 5/9;
    }
}
```

### **3.3 Encapsulamento em Hierarquias de Herança**

#### **Modificador `protected`**

```csharp
public class Veiculo
{
    protected string _chassi; // Acessível por classes derivadas

    public void Ligar() => Console.WriteLine("Veículo ligado");
}

public class Carro : Veiculo
{
    public void ExibirChassi() => Console.WriteLine(_chassi);
}
```

#### **Classes e Membros `sealed`**

```csharp
public sealed class ContaPoupanca : ContaBancaria
{
    public void AplicarRendimento() { /* ... */ }
}

// Erro: Não pode herdar de classe sealed
// public class ContaPremium : ContaPoupanca { }
```

### **3.4 Boas Práticas de Encapsulamento**

1. **Princípio do Menor Privilégio**

   - Comece com `private` e aumente a visibilidade apenas quando necessário

2. **Imutabilidade para Thread Safety**

   ```csharp
   public class Configuracao
   {
       public string Servidor { get; }
       public int Porta { get; }

       public Configuracao(string servidor, int porta)
       {
           Servidor = servidor;
           Porta = porta;
       }
   }
   ```

3. **Validação Centralizada**

   ```csharp
   public class Pedido
   {
       private DateTime _data;

       public DateTime Data
       {
           get => _data;
           set => _data = value <= DateTime.Now ? value
               : throw new ArgumentException("Data futura inválida");
       }
   }
   ```

4. **Encapsulamento de Coleções**

   ```csharp
   public class Biblioteca
   {
       private readonly List<Livro> _livros = new List<Livro>();

       // Expõe coleção como somente-leitura
       public IReadOnlyCollection<Livro> Livros => _livros.AsReadOnly();

       public void AdicionarLivro(Livro livro) => _livros.Add(livro);
   }
   ```

### **3.5 Exemplo Completo: Sistema de Usuários**

```csharp
public class Usuario
{
    private string _email;
    private string _senha;
    private DateTime _dataCadastro;

    public string Nome { get; set; }

    public string Email
    {
        get => _email;
        set => _email = ValidarEmail(value) ? value
            : throw new FormatException("Email inválido");
    }

    public int Idade { get; private set; }

    public string Senha
    {
        private get => _senha;
        set => _senha = CriptografarSenha(value);
    }

    public TimeSpan TempoCadastro => DateTime.Now - _dataCadastro;

    public Usuario(string nome, string email, int idade)
    {
        Nome = nome;
        Email = email;
        DefinirIdade(idade);
        _dataCadastro = DateTime.Now;
    }

    public bool VerificarSenha(string senha)
    {
        return CriptografarSenha(senha) == _senha;
    }

    public void DefinirIdade(int idade)
    {
        if (idade >= 0 && idade <= 120)
            Idade = idade;
    }

    private bool ValidarEmail(string email) => email.Contains("@");
    private string CriptografarSenha(string senha) => /* lógica */;
}
```

### **3.6 Perguntas Frequentes**

**Q: Quando usar métodos vs propriedades?**

- Use métodos para:
  - Ações que modificam estado significativamente (`TransferirFundos()`)
  - Operações com parâmetros complexos
  - Quando o nome do verbo é importante (`CalcularImposto()`)
- Use propriedades para:
  - Características do objeto (`Cor`, `Tamanho`)
  - Valores simples com get/set básico
  - Quando a sintaxe de campo faz sentido (`obj.Valor = 10`)

**Q: Como proteger classes de alterações indevidas?**

- Use `readonly` para campos que não devem mudar após construção
- Considere `init` (C# 9+) para propriedades imutáveis pós-construção
- Para coleções, exponha interfaces (`IReadOnlyList`) em vez da coleção real

**Q: Propriedades auto-implementadas vs campos completos?**

- Auto-implementadas quando não precisa de lógica adicional
- Campos completos quando precisa:
  - Validação
  - Notificações (ex: INotifyPropertyChanged)
  - Lógica complexa no get/set
