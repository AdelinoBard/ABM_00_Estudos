# **Propriedades em C# (Abordagem Moderna)**

As propriedades em C# são uma evolução em relação aos campos tradicionais (`public double saldo;`), pois permitem encapsular o acesso aos dados enquanto adicionam lógica de validação, controle de acesso e outras operações.

## **1. Estrutura Básica**

Uma propriedade pode ser autoimplementada ou ter lógica personalizada:

```csharp
public class ContaBancaria
{
    // Campo privado (backing field)
    private double _saldo;

    // Propriedade com getter e setter controlados
    public double Saldo
    {
        get { return _saldo; }           // Retorna o valor
        private set                      // Set pode ser restrito
        {
            if (value >= 0)              // Validação
                _saldo = value;
            else
                Console.WriteLine("Saldo não pode ser negativo!");
        }
    }
}
```

## **2. Vantagens das Propriedades**

| **Vantagem** | **Exemplo** |
| --- | --- |
| **Sintaxe limpa** | `conta.Saldo` em vez de `conta.GetSaldo()` ou `conta.SetSaldo(valor)` |
| **Validação integrada** | Bloqueia valores negativos no setter. |
| **Controle de acesso diferenciado** | Get público (`public get`), set privado (`private set`). |
| **Flexibilidade** | Pode ser convertida em autoimplementada (`public double Saldo { get; set; }`) sem quebrar o código. |

## **3. Exemplo Prático**

```csharp
public class ContaBancaria
{
    private double _saldo;

    public double Saldo
    {
        get => _saldo;                   // Forma simplificada do get
        private set => _saldo = value >= 0 ? value : _saldo; // Atribui só se válido
    }

    public void Depositar(double valor)
    {
        Saldo += valor;  // Usa o setter para aplicar validação
    }

    public void Sacar(double valor)
    {
        if (valor <= Saldo)
            Saldo -= valor;
        else
            Console.WriteLine("Saldo insuficiente!");
    }
}
```

**Uso:**

```csharp
var conta = new ContaBancaria();
conta.Depositar(500);
conta.Sacar(200);
Console.WriteLine(conta.Saldo); // 300

// conta.Saldo = -100;          // Erro (set é privado)
```

## **4. Propriedades Autoimplementadas**

Se não há lógica adicional, use a forma simplificada:

```csharp
public class Cliente
{
    public string Nome { get; set; }    // Get/set públicos automáticos
    public int Idade { get; private set; } // Set restrito
}
```

#### **5. Quando Usar?**

- **Prefira propriedades** para expor dados de uma classe (melhor encapsulamento).
- **Use campos privados** apenas para variáveis internas sem necessidade de exposição controlada.

---
