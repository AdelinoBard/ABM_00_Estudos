# **Encapsulamento: Exemplos Práticos**

## **1. Classe `Pessoa` - Controle de Dados Básicos**

### **Versão sem Encapsulamento (Problema)**

```csharp
public class Pessoa
{
    public string Nome;  // Acesso direto sem proteção
    public int Idade;    // Pode receber valores inválidos (ex: -10)
}
```

**Problema**: Ausência de validação permite dados inconsistentes.

### **Versão com Encapsulamento (Solução)**

```csharp
public class Pessoa
{
    private string _nome;
    private int _idade;

    public string Nome
    {
        get => _nome;
        set => _nome = value; // Pode adicionar validações se necessário
    }

    public int Idade
    {
        get => _idade;
        set => _idade = value >= 0 ? value : throw new ArgumentException("Idade não pode ser negativa!");
    }
}
```

### **Versão Simplificada (Propriedades Automáticas)**

```csharp
public class Pessoa
{
    public string Nome { get; set; }  // Encapsulamento básico
    public int Idade { get; set; }    // Validação pode ser adicionada depois
}
```

**Vantagens**:

- Controle centralizado das regras de validação
- Flexibilidade para evoluir a implementação
- Proteção contra acesso indevido

## **2. Classe `ContaBancaria` - Gerenciamento Seguro de Saldo**

### **Implementação com Encapsulamento**

```csharp
public class ContaBancaria
{
    private double _saldo;

    public double Saldo => _saldo; // Somente leitura

    public ContaBancaria(double saldoInicial) => _saldo = saldoInicial;

    public void Depositar(double valor)
    {
        if (valor <= 0)
            throw new ArgumentException("Valor deve ser positivo");

        _saldo += valor;
        Console.WriteLine($"Depósito de R${valor:F2} realizado.");
    }

    public void Sacar(double valor)
    {
        if (valor <= 0)
            throw new ArgumentException("Valor deve ser positivo");

        if (_saldo < valor)
            throw new InvalidOperationException("Saldo insuficiente");

        _saldo -= valor;
        Console.WriteLine($"Saque de R${valor:F2} realizado.");
    }
}
```

### **Exemplo de Uso**

```csharp
var conta = new ContaBancaria(1000);
conta.Depositar(500);
conta.Sacar(200);
Console.WriteLine($"Saldo atual: R${conta.Saldo:F2}");
```

**Proteções Implementadas**:

- Saldo não pode ser modificado diretamente
- Validação de valores positivos
- Verificação de saldo suficiente para saques

## **3. Classe `Funcionario` - Controle de Salário**

### **Evolução da Implementação**

```csharp
public class Funcionario
{
    private double _salario;

    public double Salario => _salario; // Somente leitura

    public Funcionario(double salarioInicial) => _salario = salarioInicial;

    public void AumentarSalario(double percentual)
    {
        if (percentual <= 0)
            throw new ArgumentException("Percentual deve ser positivo");

        _salario *= (1 + percentual/100);
        Console.WriteLine($"Aumento aplicado. Novo salário: R${_salario:F2}");
    }
}
```

**Melhorias**:

- Controle rígido sobre modificações salariais
- Validação de percentual positivo
- Histórico de alterações pode ser adicionado posteriormente

## **4. Classe `Conta` - Métodos Auxiliares Privados**

### **Implementação com Método Privado**

```csharp
public class Conta
{
    private double _saldo;
    private const double TARIFA = 0.10;

    public Conta(double saldoInicial) => _saldo = saldoInicial;

    public void Depositar(double valor)
    {
        ValidarValor(valor);
        _saldo += valor;
        AplicarTarifa();
        Console.WriteLine($"Depósito realizado. Saldo: R${_saldo:F2}");
    }

    public void Sacar(double valor)
    {
        ValidarValor(valor);
        if (_saldo < valor + TARIFA)
            throw new InvalidOperationException("Saldo insuficiente");

        _saldo -= valor;
        AplicarTarifa();
        Console.WriteLine($"Saque realizado. Saldo: R${_saldo:F2}");
    }

    private void ValidarValor(double valor)
    {
        if (valor <= 0)
            throw new ArgumentException("Valor deve ser positivo");
    }

    private void AplicarTarifa() => _saldo -= TARIFA;
}
```

**Benefícios**:

- Tarifa aplicada automaticamente em cada operação
- Validação centralizada
- Lógica complexa escondida do usuário da classe

## **Padrões Recomendados**

1. **Prefira propriedades** a campos públicos
2. **Métodos auxiliares** devem ser privados
3. **Validações** devem ocorrer nos setters e métodos
4. **Exceções** são melhores que mensagens no console
5. **Constantes** para valores fixos (como tarifas)

Estes exemplos demonstram como o encapsulamento:

- Protege a integridade dos dados
- Facilita manutenção futura
- Esconde detalhes de implementação
- Oferece interfaces claras e seguras para interação

---
