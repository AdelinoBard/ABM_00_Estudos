# **Parâmetros e Passagem de Valores em Métodos**

Os parâmetros são fundamentais em programação, pois permitem que métodos recebam dados externos para processamento.

## **Passagem de Parâmetros: Valor vs Referência**

### **1.1 Passagem por Valor (Cópia)**

- **Como funciona:**  
  O método recebe uma **cópia** do valor original. Alterações dentro do método **não afetam** a variável externa.
- **Quando usar:**  
  Ideal quando queremos trabalhar com o valor sem modificar o original.

**Exemplo em C#:**

```csharp
static void Incrementar(int valor)
{
    valor += 10;
    Console.WriteLine($"Dentro do método: {valor}");
}

int numero = 5;
Incrementar(numero);
Console.WriteLine($"Fora do método: {numero}");
```

**Saída:**

```
Dentro do método: 15
Fora do método: 5
```

_(O valor original permanece inalterado.)_

### **Passagem por Referência (`ref` e `out`)**

- **Como funciona:**  
  O método recebe uma **referência** à variável original. Alterações internas **afetam** a variável externa.
- **Diferença entre `ref` e `out`:**
  - `ref`: Exige que a variável seja inicializada antes da chamada.
  - `out`: Não requer inicialização prévia (o método deve atribuir um valor).

**Exemplo com `ref`:**

```csharp
static void Duplicar(ref int numero)
{
    numero *= 2;
}

int valorOriginal = 3;
Duplicar(ref valorOriginal);
Console.WriteLine(valorOriginal); // Saída: 6
```

**Exemplo com `out`:**

```csharp
static bool TentarDividir(int dividendo, int divisor, out int resultado)
{
    if (divisor == 0)
    {
        resultado = 0;
        return false;
    }
    resultado = dividendo / divisor;
    return true;
}

if (TentarDividir(10, 2, out int resultado))
{
    Console.WriteLine($"Resultado: {resultado}"); // Saída: 5
}
```

## **Sobrecarga de Métodos (Overloading)**

Permite definir **múltiplas versões** de um método com o mesmo nome, mas com parâmetros diferentes (tipo, quantidade ou ordem).

### **Regras:**

- Os métodos devem diferir na **assinatura** (lista de parâmetros).
- O tipo de retorno **não** diferencia sobrecargas.

**Exemplo Prático:**

```csharp
// Versão para calcular área do quadrado (1 parâmetro)
static double CalcularArea(double lado)
{
    return lado * lado;
}

// Versão para calcular área do retângulo (2 parâmetros)
static double CalcularArea(double largura, double altura)
{
    return largura * altura;
}

// Versão para calcular área do círculo (usando Math.PI)
static double CalcularArea(double raio, bool isCirculo)
{
    return isCirculo ? Math.PI * raio * raio : 0;
}
```

**Uso:**

```csharp
Console.WriteLine(CalcularArea(5));           // Quadrado: 25
Console.WriteLine(CalcularArea(4, 3));        // Retângulo: 12
Console.WriteLine(CalcularArea(2, true));     // Círculo: ~12.566
```

## **Parâmetros Variáveis (`params`)**

Permite que um método aceite um **número variável** de argumentos do mesmo tipo, simplificando chamadas com múltiplos valores.

### **Regras:**

- Só pode haver **um `params`** por método.
- Deve ser o **último parâmetro** na lista.

**Exemplo:**

```csharp
static int Somar(params int[] numeros)
{
    int total = 0;
    foreach (int num in numeros)
    {
        total += num;
    }
    return total;
}

Console.WriteLine(Somar(1, 2, 3));       // 6
Console.WriteLine(Somar(10, 20, 30, 40)); // 100
```

**Alternativa sem `params` (menos elegante):**

```csharp
Somar(new int[] {1, 2, 3}); // Funciona, mas é verboso
```

## **Dicas e Boas Práticas**

1. **Prefira passagem por valor** para evitar efeitos colaterais, a menos que a modificação externa seja necessária.
2. **Use `out`** para retornar múltiplos valores sem criar estruturas complexas.
3. **Sobrecarregue com cuidado:** Métodos com nomes iguais devem ter propósitos semelhantes para evitar confusão.
4. **`params` é útil**, mas evite abusar em métodos com muitos parâmetros fixos.

---
