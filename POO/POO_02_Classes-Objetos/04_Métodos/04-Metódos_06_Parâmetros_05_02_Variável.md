# Métodos: Parâmetros

## **5.2. Parâmetros Variáveis (`params`)**

Em muitos casos, precisamos criar métodos que aceitem uma quantidade variável de argumentos, sem definir explicitamente quantos serão passados. Para isso, C# oferece o modificador **`params`**, permitindo que um método receba um número indefinido de parâmetros do mesmo tipo.

## **Como funciona o `params`?**

O modificador `params` transforma os argumentos passados em um **array**, permitindo que o método processe cada um de forma iterativa.

### **Exemplo básico**

Aqui está um método que soma valores passados como argumentos:

```csharp
static int Somar(params int[] numeros)
{
    int soma = 0;
    foreach (int num in numeros)
    {
        soma += num;
    }
    return soma;
}

// Uso:
Console.WriteLine(Somar(1, 2, 3));  // Saída: 6
Console.WriteLine(Somar(10, 20));   // Saída: 30
Console.WriteLine(Somar());         // Saída: 0 (nenhum número passado)
```

Observações:

- Podemos chamar `Somar` com **qualquer quantidade** de números.
- Se não passarmos nenhum número, a soma será **zero**.

## **Alternativa sem `params`**

Se não utilizarmos `params`, precisaríamos passar um **array explicitamente**, tornando a chamada mais verbosa:

```csharp
Console.WriteLine(Somar(new int[] {1, 2, 3}));  // Funciona, mas é menos elegante
```

Com `params`, evitamos a necessidade de instanciar um array manualmente.

## **Regras importantes**

Ao usar `params`, é essencial seguir algumas regras:

- Só pode haver **um** `params` por método.
- O parâmetro `params` **deve ser o último** da lista de parâmetros.

**Exemplo correto:**

```csharp
static void ExibirMensagem(string titulo, params string[] mensagens)
{
    Console.WriteLine($"Título: {titulo}");
    foreach (string mensagem in mensagens)
    {
        Console.WriteLine($"- {mensagem}");
    }
}
```

Uso:

```csharp
ExibirMensagem("Notas", "Olá", "Bem-vindo", "Até mais!");
```

**Exemplo incorreto (erro):**

```csharp
static void ExibirMensagem(params string[] mensagens, string titulo) { }  // `params` não é o último
```

## **`params` com pelo menos um argumento obrigatório**

Às vezes, queremos garantir que pelo menos **um** argumento seja passado. Para isso, podemos definir um primeiro parâmetro fixo antes do `params`:

```csharp
static double CalcularMedia(double primeiroValor, params double[] outrosValores)
{
    double soma = primeiroValor;
    foreach (double valor in outrosValores)
    {
        soma += valor;
    }
    return soma / (1 + outrosValores.Length);
}
```

Uso:

```csharp
Console.WriteLine(CalcularMedia(5.0));             // 5.0 (apenas um número)
Console.WriteLine(CalcularMedia(5.0, 10.0, 15.0)); // 10.0 (média de 5, 10 e 15)
```

---
