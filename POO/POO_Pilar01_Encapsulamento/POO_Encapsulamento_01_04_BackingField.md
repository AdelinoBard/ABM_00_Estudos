# **Padrão Backing Field em C#**

O **backing field** (campo de apoio) é uma técnica fundamental em programação orientada a objetos que consiste em usar um **campo privado** para armazenar o estado real de uma propriedade, enquanto a propriedade pública atua como uma interface controlada para acessar e modificar esse valor.

## **Por que Usar um Backing Field?**

1. **Controle de Acesso**: Permite adicionar lógica de validação ou processamento ao definir ou recuperar um valor.
2. **Encapsulamento**: Mantém o estado interno protegido, expondo apenas o necessário.
3. **Flexibilidade**: Permite alterar a implementação interna sem afetar os consumidores da classe.

## **Exemplo Didático: Classe `Temperatura`**

Vamos analisar e aprimorar o exemplo fornecido, explicando cada parte:

### **1. Backing Field Básico**

```csharp
private double _celsius; // Backing field
```

- `_celsius` é o campo privado que armazena o valor real em graus Celsius.
- Por convenção, campos privados em C# são prefixados com `_`.

### **2. Propriedade `Celsius` com Validação**

```csharp
public double Celsius
{
    get => _celsius; // Retorna o valor armazenado
    set => _celsius = value >= -273.15 ? value : _celsius; // Valida antes de atribuir
}
```

- **`get`**: Simplesmente retorna o valor do backing field.
- **`set`**:
  - Verifica se o valor é válido (temperatura não pode ser menor que -273.15°C, o **zero absoluto**).
  - Se for válido (`value >= -273.15`), atribui ao backing field; caso contrário, mantém o valor atual.

### **3. Propriedade `Fahrenheit` com Conversão Automática**

```csharp
public double Fahrenheit
{
    get => (_celsius * 9/5) + 32; // Converte Celsius para Fahrenheit
    set => _celsius = (value - 32) * 5/9; // Converte Fahrenheit para Celsius
}
```

- **`get`**: Calcula e retorna o valor em Fahrenheit com base em `_celsius`.
- **`set`**: Converte o valor de Fahrenheit para Celsius e armazena em `_celsius`.

## **Exemplo de Uso**

```csharp
var temp = new Temperatura();
temp.Celsius = 25; // Atribui 25°C (válido)
Console.WriteLine(temp.Celsius);    // Saída: 25
Console.WriteLine(temp.Fahrenheit); // Saída: 77

temp.Celsius = -300; // Tentativa inválida (mantém 25°C)
Console.WriteLine(temp.Celsius);    // Saída: 25 (valor anterior preservado)

temp.Fahrenheit = 32; // Define 0°C (equivalente a 32°F)
Console.WriteLine(temp.Celsius);    // Saída: 0
```

## **Vantagens do Padrão**

1. **Validação Centralizada**: Garante que `_celsius` nunca seja inválido.
2. **Conversão Automática**: As propriedades gerenciam as transformações entre unidades.
3. **Manutenção Simplificada**: Se a lógica de conversão mudar, basta ajustar a propriedade.

## **Alternativa Simplificada (Auto-Properties)**

Se não há lógica adicional, você pode usar **auto-properties**:

```csharp
public double Celsius { get; set; } // Sem backing field explícito
```

- O compilador gera automaticamente um campo oculto (`<Celsius>k__BackingField`).

---
