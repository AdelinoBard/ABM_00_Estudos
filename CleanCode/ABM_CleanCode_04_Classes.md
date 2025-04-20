# **Classes**

Em **C#**, siga os princípios do **Código Limpo** ao preferir **classes** em vez de **structs** quando precisar de herança e objetos mais complexos, utilizando encapsulamento e propriedades para maior segurança. **Encadeamento de métodos** melhora a legibilidade ao permitir chamadas fluentes, retornando `this` em métodos modificadores. Além disso, **composição** é frequentemente preferível à herança, pois torna o código mais flexível e modular, evitando hierarquias rígidas. Sempre que possível, pense em **"tem-um" ao invés de "é-um"**, garantindo que a modelagem do seu software seja mais adaptável e sustentável.

---

## **Prefira classes ao invés de estruturas simples**

Em **C#**, as classes são mais flexíveis do que **structs**, especialmente quando se trata de herança. Se você precisar de herança (e esteja ciente de que talvez não precise), prefira classes. Entretanto, prefira **structs** ou **record types** para representar objetos pequenos e imutáveis.

**Ruim:** (Implementação sem classes modernas e com padrões antigos)
```csharp
public class Animal
{
    public int Age;

    public Animal(int age)
    {
        Age = age;
    }

    public void Move() { }
}

public class Mammal : Animal
{
    public string FurColor;

    public Mammal(int age, string furColor) : base(age)
    {
        FurColor = furColor;
    }

    public void LiveBirth() { }
}

public class Human : Mammal
{
    public string LanguageSpoken;

    public Human(int age, string furColor, string languageSpoken) : base(age, furColor)
    {
        LanguageSpoken = languageSpoken;
    }

    public void Speak() { }
}
```

**Bom:** (Usando encapsulamento e propriedades)
```csharp
public class Animal
{
    public int Age { get; private set; }

    public Animal(int age) => Age = age;

    public virtual void Move() { }
}

public class Mammal : Animal
{
    public string FurColor { get; private set; }

    public Mammal(int age, string furColor) : base(age) => FurColor = furColor;

    public virtual void LiveBirth() { }
}

public class Human : Mammal
{
    public string LanguageSpoken { get; private set; }

    public Human(int age, string furColor, string languageSpoken) 
        : base(age, furColor) => LanguageSpoken = languageSpoken;

    public void Speak() { }
}
```

---

## **Use encadeamento de métodos**

Encadeamento de métodos torna seu código mais fluido e legível em **C#**. Para isso, basta retornar `this` nas funções mutáveis.

**Ruim:** (Sem encadeamento de métodos)
```csharp
public class Car
{
    public string Make { get; private set; }
    public string Model { get; private set; }
    public string Color { get; private set; }

    public Car(string make, string model, string color)
    {
        Make = make;
        Model = model;
        Color = color;
    }

    public void SetMake(string make) => Make = make;
    public void SetModel(string model) => Model = model;
    public void SetColor(string color) => Color = color;

    public void Save() => Console.WriteLine($"{Make} {Model} {Color}");
}

var car = new Car("Ford", "F-150", "Red");
car.SetColor("Pink");
car.Save();
```

**Bom:** (Encadeamento de métodos)
```csharp
public class Car
{
    public string Make { get; private set; }
    public string Model { get; private set; }
    public string Color { get; private set; }

    public Car(string make, string model, string color)
    {
        Make = make;
        Model = model;
        Color = color;
    }

    public Car SetMake(string make) { Make = make; return this; }
    public Car SetModel(string model) { Model = model; return this; }
    public Car SetColor(string color) { Color = color; return this; }
    public Car Save() { Console.WriteLine($"{Make} {Model} {Color}"); return this; }
}

var car = new Car("Ford", "F-150", "Red")
    .SetColor("Pink")
    .Save();
```

---

## **Prefira composição ao invés de herança**

Prefira composição ao invés de herança sempre que possível. O princípio **"tem-um" é melhor que "é-um"** ajuda a evitar hierarquias excessivamente rígidas.

**Ruim:** (Abuso de herança)
```csharp
public class Employee
{
    public string Name { get; private set; }
    public string Email { get; private set; }

    public Employee(string name, string email)
    {
        Name = name;
        Email = email;
    }
}

// Ruim: EmployeeTaxData não é um tipo de Employee
public class EmployeeTaxData : Employee
{
    public string Ssn { get; private set; }
    public decimal Salary { get; private set; }

    public EmployeeTaxData(string name, string email, string ssn, decimal salary)
        : base(name, email)
    {
        Ssn = ssn;
        Salary = salary;
    }
}
```

**Bom:** (Usando composição)
```csharp
public class EmployeeTaxData
{
    public string Ssn { get; private set; }
    public decimal Salary { get; private set; }

    public EmployeeTaxData(string ssn, decimal salary)
    {
        Ssn = ssn;
        Salary = salary;
    }
}

public class Employee
{
    public string Name { get; private set; }
    public string Email { get; private set; }
    public EmployeeTaxData TaxData { get; private set; }

    public Employee(string name, string email)
    {
        Name = name;
        Email = email;
    }

    public Employee SetTaxData(string ssn, decimal salary)
    {
        TaxData = new EmployeeTaxData(ssn, salary);
        return this;
    }
}
```

---