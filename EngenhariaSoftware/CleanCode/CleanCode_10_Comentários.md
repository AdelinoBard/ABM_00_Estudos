# **Comentários em C#**

## Comente apenas lógica complexa de negócio

Em C#, como em outras linguagens, código autoexplicativo é preferível a comentários. Use comentários apenas para explicar *porquês* não *o quês*.

**Ruim:**
```csharp
public int HashIt(string data)
{
    // A hash
    int hash = 0;

    // Tamanho da string
    int length = data.Length;

    // Loop em cada caracter da informação
    for (int i = 0; i < length; i++)
    {
        // Pega o código do caracter
        int charCode = data[i];
        // Cria a hash
        hash = ((hash << 5) - hash) + charCode;
        // Converte para um integer 32-bit
        hash &= hash;
    }
    return hash;
}
```

**Bom:**
```csharp
public int HashIt(string data)
{
    int hash = 0;
    int length = data.Length;

    for (int i = 0; i < length; i++)
    {
        int charCode = data[i];
        hash = ((hash << 5) - hash) + charCode;
        
        // Converte para um integer 32-bit
        hash &= hash;
    }
    return hash;
}
```

## Não deixe código comentado

O controle de versão (Git, SVN, etc.) já cuida do histórico - não polua seu código com trechos comentados.

**Ruim:**
```csharp
ProcessData();
// ValidateData();
// TransformData();
// SendNotification();
```

**Bom:**
```csharp
ProcessData();
```

## Não use comentários como registro de alterações

O histórico do seu sistema de versionamento já fornece essas informações.

**Ruim:**
```csharp
/*
 * 2023-01-15: Removida validação complexa (AL)
 * 2022-11-02: Adicionado cache (MP)
 * 2022-08-10: Otimizada consulta (RC)
 */
public decimal CalculateTotal(Order order)
{
    return order.Subtotal + order.Taxes;
}
```

**Bom:**
```csharp
public decimal CalculateTotal(Order order)
{
    return order.Subtotal + order.Taxes;
}
```

## Evite marcadores de posição redundantes
Em C#, namespaces, classes e métodos já fornecem estruturação natural.

**Ruim:**
```csharp
////////////////////////////////////////////////////////////
// Customer Service Implementation
////////////////////////////////////////////////////////////
public class CustomerService
{
    ////////////////////////////////////////////////////////
    // Dependency Injection
    ////////////////////////////////////////////////////////
    private readonly IRepository _repository;
    
    ////////////////////////////////////////////////////////
    // Public Methods
    ////////////////////////////////////////////////////////
    public Customer GetById(int id)
    {
        // ...
    }
}
```

**Bom:**
```csharp
public class CustomerService
{
    private readonly IRepository _repository;
    
    public Customer GetById(int id)
    {
        // ...
    }
}
```

## Comentários XML para documentação pública (quando necessário)

Em C#, comentários XML são úteis para APIs públicas, mas evite excessos em implementações internas.

**Adequado:**
```csharp
/// <summary>
/// Calcula o imposto para um determinado valor
/// </summary>
/// <param name="amount">Valor base para cálculo</param>
/// <returns>Valor do imposto calculado</returns>
public decimal CalculateTax(decimal amount)
{
    // Lógica complexa de cálculo de imposto
    return amount * 0.1m;
}
```

> Lembre-se: em C#, como em outras linguagens, **o melhor comentário é aquele que você não precisa escrever** porque seu código já é claro o suficiente.

---