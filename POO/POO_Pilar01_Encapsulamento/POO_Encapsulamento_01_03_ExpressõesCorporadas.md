# **Encapsulamento com Expressões Corporadas (C# 7+)**

O encapsulamento é um dos pilares da programação orientada a objetos, permitindo ocultar detalhes internos de uma classe e expor apenas o que é necessário. No C# 7 e versões posteriores, as **expressões corporadas** (_expression-bodied members_) simplificam a sintaxe para definir propriedades, métodos e outros membros de forma mais concisa, mantendo a segurança e a clareza do código.

## **1. Propriedades Somente-Leitura com Expressões Corporadas**

No exemplo abaixo, a propriedade `Area` é definida como somente-leitura usando uma expressão corporal (`=>`), eliminando a necessidade de um bloco `get` tradicional:

```csharp
public class Retangulo
{
    private double _largura;
    private double _altura;

    // Propriedade calculada usando expressão corporal
    public double Area => _largura * _altura;

    public Retangulo(double largura, double altura)
    {
        _largura = largura > 0 ? largura : throw new ArgumentException("Largura deve ser maior que zero.");
        _altura = altura > 0 ? altura : throw new ArgumentException("Altura deve ser maior que zero.");
    }
}
```

### **Funcionamento:**

- `Area` é uma **propriedade somente-leitura** que retorna o produto de `_largura` e `_altura`.
- A expressão `=> _largura * _altura` substitui o bloco `get { return _largura * _altura; }`.

## **2. Validação no Construtor com Operador Ternário**

O construtor valida os valores de `largura` e `altura` usando um **operador ternário** combinado com `throw` para garantir que sejam positivos:

```csharp
public Retangulo(double largura, double altura)
{
    _largura = largura > 0 ? largura : throw new ArgumentException("Largura inválida.");
    _altura = altura > 0 ? altura : throw new ArgumentException("Altura inválida.");
}
```

### **Vantagens:**

- Código mais compacto sem perder legibilidade.
- Lança uma exceção imediatamente se os valores forem inválidos.

## **3. Exemplo Prático: Usando a Classe `Retangulo`**

```csharp
class Program
{
    static void Main()
    {
        // Cria um retângulo válido
        var retangulo = new Retangulo(5, 3);
        Console.WriteLine($"Área: {retangulo.Area}"); // Saída: 15

        // Tentativa com valores inválidos (lança exceção)
        try
        {
            var retanguloInvalido = new Retangulo(-2, 4);
        }
        catch (ArgumentException ex)
        {
            Console.WriteLine($"Erro: {ex.Message}"); // Saída: Largura inválida.
        }
    }
}
```

### **Saída:**

```
Área: 15
Erro: Largura inválida.
```

## **4. Quando Usar Expressões Corporadas?**

- **Propriedades calculadas simples** (ex: `Area`, `Perimetro`).
- **Métodos que retornam um valor diretamente** (ex: `ToString()`).
- **Construtores com validações curtas** (como no exemplo acima).

### **Cuidados:**

- Evite expressões muito complexas, pois podem prejudicar a legibilidade.
- Use apenas quando a lógica for direta e autoexplicativa.

## **5. Comparação com Sintaxe Tradicional**

| **Versão com Expressão Corporada** | **Versão Tradicional** |
| --- | --- |
| `public double Area => _largura * _altura;` | `public double Area { get { return _largura * _altura; } }` |

A versão moderna é mais enxuta e mantém a mesma funcionalidade.

---
