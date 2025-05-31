# Métodos: Parâmetros

## **7. Tuplas como Parâmetros**

Podemos usar tuplas para passar múltiplos valores como argumento.

```csharp
void ExibirDados((string nome, int idade) pessoa)
{
    Console.WriteLine($"Nome: {pessoa.nome}, Idade: {pessoa.idade}");
}

var usuario = ("Carlos", 35);
ExibirDados(usuario); // Saída: Nome: Carlos, Idade: 35
```
