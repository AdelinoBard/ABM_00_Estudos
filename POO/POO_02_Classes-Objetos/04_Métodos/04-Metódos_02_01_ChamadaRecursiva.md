# Métodos: Chamada Recursiva

A **recursão** ocorre quando um método chama a si mesmo para resolver um problema. Esse conceito é útil para dividir uma questão complexa em partes menores e mais gerenciáveis.

## **1. Como Funciona?**

A estrutura de um método recursivo possui duas partes essenciais:

1. **Condição de Parada**: Define o momento em que a recursão deve parar, evitando loops infinitos.
2. **Chamada Recursiva**: O método se chama novamente, reduzindo o problema até alcançar a condição de parada.

## **2. Exemplo Simples: Contagem Regressiva**

Aqui está um exemplo básico para ilustrar a recursão:

```csharp
void ContagemRegressiva(int n)
{
    if (n <= 0) // Condição de parada
    {
        Console.WriteLine("Fim!");
        return;
    }

    Console.WriteLine(n);
    ContagemRegressiva(n - 1); // Chamada recursiva com um valor menor
}

ContagemRegressiva(3);
/* Saída:
   3
   2
   1
   Fim!
*/
```

## **3. Exemplo Didático: Cálculo de Fatorial**

O fatorial de `n` (representado por `n!`) é o produto de todos os números de `1` até `n`. Exemplo:

- `5! = 5 × 4 × 3 × 2 × 1 = 120`

Implementação recursiva simplificada em C#:

```csharp
int Fatorial(int n)
{
    if (n <= 1) return 1; // Condição de parada
    return n * Fatorial(n - 1); // Chamada recursiva
}

Console.WriteLine(Fatorial(5)); // Saída: 120
```

## **4. Exemplo: Soma de Números até N**

Aqui, somamos todos os números de `1` até `n` usando recursão:

```csharp
int SomaAteN(int n)
{
    if (n <= 1) return n; // Condição de parada
    return n + SomaAteN(n - 1); // Chamada recursiva
}

Console.WriteLine(SomaAteN(3)); // Saída: 6 (1 + 2 + 3)
```

## **5. Cuidados ao Usar Recursão**

Antes de usar recursão, considere os seguintes pontos:

- Sempre inclua uma **condição de parada** para evitar _loops infinitos_.
- Métodos recursivos podem consumir muita **memória** em casos de chamadas muito profundas.
- Nem sempre a recursão é a melhor opção; **loops** (`for` ou `while`) podem ser mais eficientes em alguns problemas.

## **6. Exercício Proposto**

Implemente um método recursivo que calcula o `n`-ésimo termo da sequência de Fibonacci, onde:

- `Fibonacci(0) = 0`
- `Fibonacci(1) = 1`
- `Fibonacci(n) = Fibonacci(n-1) + Fibonacci(n-2)`

```csharp
int Fibonacci(int n)
{
    if (n <= 1) return n; // Condição de parada
    return Fibonacci(n - 1) + Fibonacci(n - 2); // Chamada recursiva
}

Console.WriteLine(Fibonacci(6)); // Saída esperada: 8
```

---
