# **Propriedades em C#: Encapsulamento Simplificado**

Em C#, **propriedades** são uma maneira prática de controlar o acesso a atributos privados de uma classe. Elas substituem os métodos tradicionais `get` e `set`, tornando o código mais limpo e intuitivo.

### **Problema com Métodos Get/Set Tradicionais**

Antes do uso de propriedades, para acessar e modificar um atributo de uma classe, era necessário utilizar métodos separados:

```csharp
class Pessoa
{
    private string nome;

    public string GetNome() => nome;
    public void SetNome(string novoNome)
    {
        if (!string.IsNullOrEmpty(novoNome))
            nome = novoNome;
    }
}
```

Uso:

```csharp
Pessoa p = new Pessoa();
p.SetNome("Ana");
Console.WriteLine(p.GetNome());
```

Esse estilo tornava o código mais longo e menos intuitivo.

### **Solução: Uso de Propriedades**

As propriedades permitem um acesso mais direto e seguro, sem a necessidade de métodos `get` e `set` separados:

```csharp
class Pessoa
{
    private string nome;

    public string Nome
    {
        get => nome;
        set
        {
            if (!string.IsNullOrEmpty(value))
                nome = value;
        }
    }
}
```

Agora, podemos acessar e modificar `Nome` como se fosse um campo público:

```csharp
Pessoa p = new Pessoa();
p.Nome = "Ana";          // Usa o 'set'
Console.WriteLine(p.Nome); // Usa o 'get'
```

## **2. Tipos de Propriedades**

### **a) Propriedades Completas (Full Properties)**

Quando precisamos de lógica específica para acessar e modificar valores:

```csharp
class Produto
{
    private double preco;

    public double Preco
    {
        get => preco;
        set => preco = value > 0 ? value : 0; // Garante que o preço seja positivo
    }
}
```

### **b) Propriedades Automáticas (Auto-Properties)**

Quando **não há necessidade de lógica adicional**, o C# simplifica:

```csharp
class Cliente
{
    public string Nome { get; set; } // O próprio C# cria um campo privado internamente
}
```

Uso:

```csharp
Cliente c = new Cliente();
c.Nome = "Carlos";
Console.WriteLine(c.Nome);
```

### **c) Propriedades Somente Leitura (Getter-Only)**

A partir do **C# 6**, podemos criar propriedades que só podem ser lidas, garantindo imutabilidade:

```csharp
class Configuracao
{
    public string Tipo { get; } = "Padrão"; // Inicialização direta
}
```

Uso:

```csharp
Configuracao config = new Configuracao();
Console.WriteLine(config.Tipo); // "Padrão"
```

## **3. Exemplo Completo: Classe `Produto`**

Agora, vejamos uma implementação completa com propriedades diferentes:

```csharp
class Produto
{
    public string Nome { get; set; } // Propriedade automática
    public double Preco { get; set; } = 0; // Inicialização padrão

    public string Descricao => $"{Nome} - R${Preco:F2}"; // Propriedade somente leitura
}
```

Uso:

```csharp
Produto p = new Produto();
p.Nome = "Notebook";
p.Preco = 2500.50;
Console.WriteLine(p.Descricao); // "Notebook - R$2500,50"
```

## **4. Boas Práticas ao Usar Propriedades**

1. **Use PascalCase** para nomear propriedades (`Nome`, `Preco`).
2. **Utilize propriedades automáticas** sempre que possível.
3. **Evite lógica complexa** dentro de propriedades; prefira métodos para isso.
4. **Inicialize valores padrão** quando aplicável (`public int Quantidade { get; set; } = 10;`).
5. **Documente suas propriedades** para melhor entendimento:

```csharp
/// <summary>
/// Nome do produto.
/// </summary>
public string Nome { get; set; }
```

---
