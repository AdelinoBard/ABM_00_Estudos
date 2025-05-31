# **Encapsulamento em Hierarquias de Herança**

O encapsulamento é um dos pilares da programação orientada a objetos (POO) e permite controlar o acesso aos membros de uma classe. Em hierarquias de herança, esse controle se torna ainda mais importante, pois precisamos definir quais membros são acessíveis às classes derivadas.

1. O modificador **`protected`**, permite acesso apenas a classes derivadas.
2. A palavra-chave **`sealed`**, restringe a herança de classes ou a sobrescrita de métodos.

## **1. Modificador `protected`**

O modificador **`protected`** define que um membro (campo, propriedade ou método) só pode ser acessado:

- **Dentro da própria classe.**
- **Por classes derivadas (herdeiras).**

Isso é útil quando queremos permitir que subclasses utilizem certos membros, mas sem expô-los publicamente.

### **Exemplo Prático**

```csharp
public class Veiculo
{
    protected string _chassi; // Acessível apenas por classes derivadas

    public void Ligar() => Console.WriteLine("Veículo ligado.");
}

public class Carro : Veiculo
{
    public void ExibirChassi()
    {
        // Acesso permitido porque Carro herda de Veiculo
        Console.WriteLine($"Chassi: {_chassi}");
    }
}
```

### **Quando Usar `protected`?**

- Quando um atributo ou método **deve ser compartilhado apenas com subclasses**.
- Para evitar expor detalhes internos a outras partes do código.

### **Comparação com Outros Modificadores**

| Modificador | Acesso na própria classe | Acesso em classes derivadas | Acesso em outras classes |
| --- | --- | --- | --- |
| `private` | ✔️ | ❌ | ❌ |
| `protected` | ✔️ | ✔️ | ❌ |
| `public` | ✔️ | ✔️ | ✔️ |

## **2. Classes e Membros `sealed`**

A palavra-chave **`sealed`** tem dois usos principais:

1. **Impedir que uma classe seja herdada.**
2. **Impedir que um método `virtual` ou `override` seja sobrescrito em classes derivadas.**

### **2.1. Classe `sealed`**

Quando uma classe é marcada como `sealed`, nenhuma outra classe pode herdar dela.

#### **Exemplo**

```csharp
public class ContaBancaria
{
    public decimal Saldo { get; protected set; }
}

public sealed class ContaPoupanca : ContaBancaria
{
    public void AplicarRendimento(decimal taxa)
    {
        Saldo += Saldo * taxa;
    }
}

// ERRO: Não é possível herdar de uma classe sealed
// public class ContaPremium : ContaPoupanca { }
```

#### **Por que Usar `sealed`?**

- **Segurança:** Evita extensões não intencionais de classes críticas.
- **Otimização:** O compilador pode aplicar otimizações adicionais.

### **2.2. Método `sealed`**

Um método marcado como `sealed` em uma classe derivada impede que outras classes filhas sobrescrevam esse método.

#### **Exemplo**

```csharp
public class Animal
{
    public virtual void EmitirSom() => Console.WriteLine("Som genérico");
}

public class Cachorro : Animal
{
    public sealed override void EmitirSom() => Console.WriteLine("Au au!");
}

public class PastorAlemao : Cachorro
{
    // ERRO: Não é possível sobrescrever um método sealed
    // public override void EmitirSom() => Console.WriteLine("AU AU FORTE!");
}
```

---
