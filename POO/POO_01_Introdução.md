# Programação Orientada a Objetos (POO)

## 1. Introdução à POO

### O que é Programação Orientada a Objetos?

A Programação Orientada a Objetos (POO) é um paradigma de programação que organiza o código em "objetos", que representam entidades do mundo real ou conceitos abstratos. Esses objetos contêm dados (**atributos**) e comportamentos (**métodos**).

### Benefícios da POO

A POO oferece uma maneira eficiente de organizar código complexo através de conceitos como classes, objetos, encapsulamento, herança e polimorfismo.

- **Organização:** Estrutura clara para código complexo
- **Reutilização:** Classes podem ser usadas em vários projetos
- **Manutenção:** Mais fácil de entender e modificar
- **Segurança:** Encapsulamento protege os dados internos

## 2. Classes e Objetos

### O que é uma Classe?

Uma classe é um modelo ou "projeto" para criação de objetos. Ela define os atributos e comportamentos que os objetos terão.

```csharp
// Exemplo simples de classe
public class Animal
{
    // Atributo
    public string Nome;

    // Método
    public void Comer()
    {
        Console.WriteLine($"{Nome} está comendo.");
    }
}
```

### O que é um Objeto?

Um objeto é uma instância concreta criada a partir de uma classe.

```csharp
// Criando objetos
Animal meuCachorro = new Animal();
meuCachorro.Nome = "Rex";
meuCachorro.Comer();  // Saída: Rex está comendo.
```

## 3. Atributos e Métodos

### Atributos

São variáveis que armazenam o estado do objeto.

```csharp
public class Pessoa
{
    public string Nome;
    public int Idade;
}
```

### Métodos

São funções que definem o comportamento do objeto.

```csharp
public class Calculadora
{
    public int Somar(int a, int b)
    {
        return a + b;
    }
}
```

## 4. Encapsulamento

Protege os dados internos de um objeto, expondo apenas o necessário.

```csharp
public class ContaBancaria
{
    private double saldo;  // Privado = acesso restrito

    public void Depositar(double valor)
    {
        if (valor > 0)
            saldo += valor;
    }

    public double VerSaldo()
    {
        return saldo;
    }
}
```

## 5. Herança

Permite criar novas classes baseadas em classes existentes.

```csharp
// Classe base
public class Veiculo
{
    public void LigarMotor()
    {
        Console.WriteLine("Motor ligado.");
    }
}

// Classe derivada
public class Carro : Veiculo
{
    public void Dirigir()
    {
        Console.WriteLine("Carro em movimento.");
    }
}

// Uso
Carro meuCarro = new Carro();
meuCarro.LigarMotor();  // Herdado de Veiculo
meuCarro.Dirigir();     // Específico de Carro
```

## 6. Polimorfismo

Objetos diferentes podem responder ao mesmo comando de maneiras distintas.

```csharp
public class Forma
{
    public virtual void Desenhar()
    {
        Console.WriteLine("Desenhando forma genérica");
    }
}

public class Circulo : Forma
{
    public override void Desenhar()
    {
        Console.WriteLine("Desenhando um círculo");
    }
}

// Uso
Forma forma1 = new Circulo();
forma1.Desenhar();  // Saída: Desenhando um círculo
```

## 7. Abstração

Foca no essencial, ignorando detalhes irrelevantes.

```csharp
public abstract class InstrumentoMusical
{
    public abstract void Tocar();
}

public class Piano : InstrumentoMusical
{
    public override void Tocar()
    {
        Console.WriteLine("Tocando piano...");
    }
}
```

## 8. Mensagens e Chamadas de Método

Objetos interagem chamando métodos de outros objetos.

```csharp
public class Mensagem
{
    public void Enviar(string texto)
    {
        Console.WriteLine($"Mensagem enviada: {texto}");
    }
}

// Uso
Mensagem msg = new Mensagem();
msg.Enviar("Olá, mundo!");
```

## 9. Reuso de Classes

Classes podem ser reutilizadas em diferentes contextos.

```csharp
public class Data
{
    public string Formatar(DateTime data)
    {
        return data.ToString("dd/MM/yyyy");
    }
}

// Uso em diferentes partes do programa
Data formatador = new Data();
Console.WriteLine(formatador.Formatar(DateTime.Now));
```

## Exercícios Práticos

1. Crie uma classe `Retangulo` com atributos `Largura` e `Altura` e um método `CalcularArea()`

```c#
using System;

class Retangulo
{
    public double Largura { get; set; }
    public double Altura { get; set; }

    public double CalcularArea()
    {
        return Largura * Altura;
    }
}

class Program
{
    static void Main()
    {
        Retangulo retangulo = new Retangulo();
        retangulo.Largura = 5;
        retangulo.Altura = 10;

        Console.WriteLine($"A área do retângulo é: {retangulo.CalcularArea()}");
    }
}
```

2. Implemente uma classe `Pessoa` com encapsulamento para o atributo `Idade` (não pode ser negativo)

```c#
using System;

class Pessoa
{
    private int idade;

    public int Idade
    {
        get { return idade; }
        set
        {
            if (value >= 0)
                idade = value;
            else
                throw new ArgumentException("A idade não pode ser negativa.");
        }
    }
}

class Program
{
    static void Main()
    {
        try
        {
            Pessoa pessoa = new Pessoa();
            pessoa.Idade = 25;
            Console.WriteLine($"A idade da pessoa é: {pessoa.Idade}");

            pessoa.Idade = -5; // Isso vai gerar uma exceção
        }
        catch (ArgumentException e)
        {
            Console.WriteLine($"Erro: {e.Message}");
        }
    }
}
```

3. Crie uma hierarquia de classes: `Animal` -> `Cachorro` e `Animal` -> `Gato`, cada um com seu método de emitir som

```c#
using System;

class Animal
{
    public virtual void EmitirSom()
    {
        Console.WriteLine("O animal faz um som.");
    }
}

class Cachorro : Animal
{
    public override void EmitirSom()
    {
        Console.WriteLine("O cachorro late: Au Au!");
    }
}

class Gato : Animal
{
    public override void EmitirSom()
    {
        Console.WriteLine("O gato mia: Miau!");
    }
}

class Program
{
    static void Main()
    {
        Animal meuCachorro = new Cachorro();
        Animal meuGato = new Gato();

        meuCachorro.EmitirSom();
        meuGato.EmitirSom();
    }
}
```

---
