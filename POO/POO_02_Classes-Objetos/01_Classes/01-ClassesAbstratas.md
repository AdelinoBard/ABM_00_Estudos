# Classes Abstratas em C#

## O que são classes abstratas?

Em programação orientada a objetos, uma **classe abstrata** é uma classe que **não pode ser instanciada diretamente**. Em vez disso, ela serve como uma **base** para outras classes derivadas. Seu propósito é definir uma **estrutura comum**, garantindo que todas as classes que a herdam tenham uma implementação mínima esperada.

Em C#, usamos o modificador `abstract` para definir uma classe como abstrata.

### Exemplo básico

```csharp
abstract class Animal
{
    public abstract void EmitirSom();
}
```

Nesta estrutura:

- `Animal` é uma classe abstrata.
- Ela define um método `EmitirSom`, mas **não o implementa**.
- Classes que herdarem `Animal` precisarão **fornecer** uma implementação para `EmitirSom`.

## Implementação em classes derivadas

Uma classe derivada de uma classe abstrata **deve implementar os métodos abstratos**.

```csharp
class Cachorro : Animal
{
    public override void EmitirSom()
    {
        Console.WriteLine("Au Au!");
    }
}

class Gato : Animal
{
    public override void EmitirSom()
    {
        Console.WriteLine("Miau!");
    }
}
```

Aqui:

- `Cachorro` e `Gato` **herdam** `Animal`.
- Ambas implementam `EmitirSom` de forma específica.

Agora, podemos instanciar `Cachorro` e `Gato`, mas **não** podemos instanciar diretamente `Animal`:

```csharp
Animal meuCachorro = new Cachorro();
meuCachorro.EmitirSom(); // Saída: "Au Au!"

Animal meuGato = new Gato();
meuGato.EmitirSom(); // Saída: "Miau!"
```

## Por que usar classes abstratas?

Usamos classes abstratas quando queremos **garantir um comportamento mínimo** para todas as classes que herdam dela. Algumas vantagens são:

- **Organização do código** – define uma estrutura comum.
- **Reutilização** – evita duplicação de código.
- **Segurança** – força a implementação de métodos essenciais.

Se tivermos um sistema que lida com diversos **tipos de contas bancárias**, por exemplo, poderíamos criar uma estrutura comum usando uma classe abstrata:

```csharp
abstract class ContaBancaria
{
    public abstract void Sacar(decimal valor);
}
```

Dessa forma, todas as contas bancárias precisam ter um método `Sacar`, mas cada uma pode **implementá-lo de maneira diferente**.
