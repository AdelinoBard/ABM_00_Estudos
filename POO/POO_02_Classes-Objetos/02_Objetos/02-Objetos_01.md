# Objetos

Objetos são estruturas que representam entidades do mundo real ou conceitos abstratos em programação orientada a objetos (POO). Eles combinam dados (atributos) e comportamentos (métodos) em uma única unidade lógica.

- **Nas aplicações orientadas a objetos, as entidades são representadas por objetos.**
- **Uma aplicação orientada a objetos é composta por objetos.**
- **Em geral, um objeto representa uma entidade do domínio.**

**Exemplo:**  
Os objetos não representam apenas coisas concretas como os clientes do banco. Eles também devem ser utilizados para representar coisas abstratas como uma conta de um cliente ou um serviço que o banco ofereça. Em um sistema bancário, um cliente chamado "João" pode ser representado por um objeto com atributos como `Nome`, `DataDeNascimento` e métodos como `RealizarSaque()`.

## Objeto em C#

Na linguagem C#, todas as classes são derivadas, direta ou indiretamente, da classe base `Object`. Isso significa que todos os membros definidos na classe `Object` estão disponíveis em todas as instâncias de classes. Além disso, referências a qualquer tipo de objeto podem ser armazenadas em variáveis do tipo `Object`, permitindo um alto grau de flexibilidade.

Esse comportamento permite a aplicação do conceito de polimorfismo para criar métodos genéricos, que podem operar em objetos de diferentes classes. Em C#, a palavra-chave `object` é um alias para a classe `Object`, podendo ser usada de maneira intercambiável.

**Exemplo Simples:**

```csharp
object numero = 10; // Boxing implícito
Console.WriteLine(numero); // Saída: 10
```

## Atributos e Métodos

### Atributos (Attributes)

São variáveis que armazenam os dados de um objeto.

São as características de um objeto, como nome, cor e tamanho.

**Exemplo:**

```csharp
public class Pessoa
{
    public string Nome { get; set; } // Atributo
    public int Idade { get; set; }   // Atributo
}
```

### Métodos (Methods)

São funções que definem as ações que um objeto pode realizar.

São os comportamentos ou ações que um objeto pode realizar, como calcular, mover e comunicar.

**Exemplo:**

```csharp
public class Calculadora
{
    public int Somar(int a, int b) // Método
    {
        return a + b;
    }
}
```

## Exemplo Prático: Cliente e Conta Bancária

Abaixo está um exemplo completo de uma aplicação simples que representa um banco com clientes e contas, ilustrando a interação entre objetos.

### **Objetos**:

Os objetos criados no código são:

- `cliente`: Instância da classe `Cliente`, criada com as propriedades `Nome`, `DataDeNascimento` e `Sexo` inicializadas.
- `conta`: Instância da classe `Conta`, criada com as propriedades `Numero` e `Titular` inicializadas.

### **Atributos**:

**Classe `Cliente`:**

- `Nome`: do tipo `string`, usado para armazenar o nome do cliente.
- `DataDeNascimento`: do tipo `DateTime`, usado para armazenar a data de nascimento do cliente.
- `Sexo`: do tipo `string`, usado para armazenar o sexo do cliente.

**Classe `Conta`:**

- `Numero`: do tipo `int`, identifica a conta.
- `Saldo`: do tipo `decimal`, armazena o saldo da conta. Este atributo tem o modificador `private set`, indicando que ele só pode ser modificado dentro da própria classe.
- `Titular`: do tipo `Cliente`, representa o cliente associado à conta.

### **Métodos**:

**Classe `Conta`:**

- `Depositar(decimal valor)`: Adiciona o valor passado como parâmetro ao saldo da conta e exibe uma mensagem informativa.
- `Sacar(decimal valor)`: Subtrai o valor do saldo, se for suficiente, e exibe uma mensagem. Caso contrário, lança uma exceção `InvalidOperationException`.

### c#

```csharp
using System;

public class Cliente
{
    public string Nome { get; set; }
    public DateTime DataDeNascimento { get; set; }
    public string Sexo { get; set; }
}

public class Conta
{
    public int Numero { get; set; }
    public decimal Saldo { get; private set; }
    public Cliente Titular { get; set; }

    public void Depositar(decimal valor)
    {
        Saldo += valor;
        Console.WriteLine($"Depósito de {valor:C} realizado na conta {Numero}. Saldo atual: {Saldo:C}");
    }

    public void Sacar(decimal valor)
    {
        if (valor <= Saldo)
        {
            Saldo -= valor;
            Console.WriteLine($"Saque de {valor:C} realizado na conta {Numero}. Saldo atual: {Saldo:C}");
        }
        else
        {
            throw new InvalidOperationException("Saldo insuficiente.");
        }
    }
}

public class Program
{
    public static void Main()
    {
        Cliente cliente = new Cliente
        {
            Nome = "João",
            DataDeNascimento = new DateTime(1985, 5, 23),
            Sexo = "Masculino"
        };

        Conta conta = new Conta
        {
            Numero = 12345,
            Titular = cliente
        };

        conta.Depositar(1000);
        conta.Sacar(250);

        Console.WriteLine($"Cliente: {conta.Titular.Nome}, Saldo: {conta.Saldo:C}");
    }
}
```

## Conceitos Correlatos (para estudo adicional)

1. **Herança:** Como classes podem herdar atributos e métodos de outras classes.

2. **Polimorfismo:** Capacidade de objetos de diferentes classes responderem ao mesmo método de formas distintas.

3. **Encapsulamento:** Proteção dos dados internos de um objeto.

4. **Classes Abstratas e Interfaces:** Modelagem de comportamentos compartilhados.

5. **Coleções de Objetos:** Listas, dicionários e arrays para gerenciar múltiplos objetos.
