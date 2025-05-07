# Domínio e Aplicação na Programação Orientada a Objetos

Na Programação Orientada a Objetos (POO), um **domínio** representa um conjunto de entidades, informações e processos relacionados a um determinado contexto. A construção de uma aplicação busca refletir esse domínio, automatizando ou tornando mais eficiente a execução de suas tarefas.

## Exemplo de Domínio: Sistema Bancário

Imagine que queremos desenvolver um sistema para um banco. Nesse cenário, podemos identificar alguns elementos essenciais:

- **Entidades do domínio:** Clientes, funcionários, agências e contas bancárias.
- **Informações e processos relacionados:** Cada entidade possui atributos e ações associadas que definem seu comportamento e interação.

A aplicação surge para operacionalizar essas interações, garantindo que o domínio seja bem representado e que as tarefas do banco sejam facilitadas.

## Identificação de Elementos de um Domínio

A identificação dos elementos de um domínio é um processo fundamental no desenvolvimento de software. Isso exige compreender:

1. **Entidades** – Os objetos que fazem parte do domínio.
2. **Informações** – Os dados associados a cada entidade.
3. **Processos** – As interações entre as entidades dentro do contexto.

Entretanto, esse conhecimento geralmente pertence a especialistas do domínio (por exemplo, gerentes e funcionários do banco), que podem não ter experiência técnica para desenvolver uma aplicação. Os desenvolvedores precisam, portanto, criar estratégias para entender e modelar esses elementos da forma mais eficiente possível.

## Aplicação Prática com Programação Orientada a Objetos

A POO facilita a modelagem de domínios reais, permitindo representar entidades, informações e processos por meio de **classes e objetos**. Vamos ilustrar um exemplo simples de um **sistema bancário** em C#:

```csharp
using System;

class ContaBancaria
{
    public string Titular { get; set; }
    public decimal Saldo { get; private set; }

    public ContaBancaria(string titular, decimal saldoInicial)
    {
        Titular = titular;
        Saldo = saldoInicial;
    }

    public void Depositar(decimal valor)
    {
        Saldo += valor;
        Console.WriteLine($"Depósito de {valor:C} realizado. Saldo atual: {Saldo:C}");
    }

    public void Sacar(decimal valor)
    {
        if (valor > Saldo)
        {
            Console.WriteLine("Saldo insuficiente.");
        }
        else
        {
            Saldo -= valor;
            Console.WriteLine($"Saque de {valor:C} realizado. Saldo atual: {Saldo:C}");
        }
    }
}

class Program
{
    static void Main()
    {
        ContaBancaria conta = new ContaBancaria("João", 1000);
        conta.Depositar(500);
        conta.Sacar(300);
    }
}
```

### Explicação:

- A classe `ContaBancaria` representa uma entidade do domínio bancário.
- O atributo `Saldo` define a informação associada à conta.
- Os métodos `Depositar` e `Sacar` representam os processos que ocorrem no domínio.

Esse pequeno exemplo demonstra como modelamos um domínio real na POO, tornando suas interações compreensíveis e sistematizadas.

---
