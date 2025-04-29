# Princípio de Substituição de Liskov (LSP) em C#

O Princípio de Substituição de Liskov (LSP) pode parecer complexo à primeira vista, mas sua essência é simples: **"Se S é um subtipo de T, então objetos do tipo T devem poder ser substituídos por objetos do tipo S sem alterar as propriedades corretas do programa."**

Em termos mais acessíveis: quando você tem uma classe base e uma classe derivada, você deve poder usar qualquer uma delas intercambiavelmente sem causar comportamentos inesperados.

## O Problema Clássico: Quadrado e Retângulo

Matematicamente, um quadrado é um retângulo, mas isso não significa que essa relação "é-um" deva ser implementada via herança na programação. Vejamos por quê:

### Implementação Ruim (Violando o LSP)

```csharp
public class Rectangle
{
    public virtual int Width { get; set; }
    public virtual int Height { get; set; }
    
    public int Area => Width * Height;
    
    public void SetSize(int width, int height)
    {
        Width = width;
        Height = height;
    }
}

public class Square : Rectangle
{
    public override int Width
    {
        set { base.Width = base.Height = value; }
    }
    
    public override int Height
    {
        set { base.Width = base.Height = value; }
    }
}

public class AreaCalculator
{
    public static void CalculateAndPrintArea(Rectangle rectangle)
    {
        rectangle.SetSize(4, 5);
        Console.WriteLine($"Área esperada: 20, Área calculada: {rectangle.Area}");
    }
}

// Uso:
var rectangle = new Rectangle();
var square = new Square();

AreaCalculator.CalculateAndPrintArea(rectangle); // Funciona corretamente
AreaCalculator.CalculateAndPrintArea(square);    // Quebra o comportamento esperado (imprime 25)
```

**Problemas:**
- O quadrado altera o comportamento fundamental do retângulo
- Código cliente espera que SetSize(4,5) resulte em área 20
- A substituição viola o contrato da classe base

### Implementação Boa (Respeitando o LSP)

```csharp
public abstract class Shape
{
    public abstract int Area { get; }
}

public class Rectangle : Shape
{
    public int Width { get; set; }
    public int Height { get; set; }
    
    public override int Area => Width * Height;
}

public class Square : Shape
{
    public int SideLength { get; set; }
    
    public override int Area => SideLength * SideLength;
}

public class AreaCalculator
{
    public static void PrintArea(Shape shape)
    {
        Console.WriteLine($"Área calculada: {shape.Area}");
    }
}

// Uso:
var rectangle = new Rectangle { Width = 4, Height = 5 };
var square = new Square { SideLength = 5 };

AreaCalculator.PrintArea(rectangle); // 20
AreaCalculator.PrintArea(square);    // 25
```

**Melhorias:**
- Ambas as classes derivam de Shape, mas não há relação de herança entre si
- Cada classe mantém suas propriedades específicas
- O comportamento é previsível e consistente
- Código cliente não precisa fazer verificações de tipo

## Princípios Aplicados

- **LSP**: Subtipos são verdadeiramente substituíveis por seus tipos base  
- **OCP**: Novas formas geométricas podem ser adicionadas sem modificar código existente  
- **Composição sobre herança**: Evitamos herança inadequada  

## Conclusão

O LSP nos ensina que:
- Herança deve representar relações verdadeiramente "é-um"
- Classes derivadas não devem fortalecer pré-condições ou enfraquecer pós-condições
- O comportamento esperado deve ser mantido em todas as substituições

Em C#, podemos aplicar o LSP usando:
- Interfaces bem definidas
- Classes abstratas quando apropriado
- Composição em vez de herança quando a relação não é perfeita
- Princípios de design por contrato