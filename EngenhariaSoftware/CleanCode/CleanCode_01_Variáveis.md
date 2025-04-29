# **Variáveis**

---

## Use nomes de variáveis que tenham significado e sejam pronunciáveis

**Ruim:**
```csharp
string yyyymmddStr = DateTime.Now.ToString("yyyy/MM/dd");
```

**Bom:**
```csharp
string currentDate = DateTime.Now.ToString("yyyy/MM/dd");
```

O nome `yyyymmddStr` é confuso e difícil de pronunciar. `currentDate` transmite claramente o propósito da variável.

---

## Use o mesmo vocabulário para o mesmo tipo de variável

**Ruim:**
```csharp
GetUserInfo();
GetClientData();
GetCustomerRecord();
```

**Bom:**
```csharp
GetUser();
```

Manter um padrão único (`GetUser()`) para métodos que retornam informações de usuários evita inconsistências e melhora a legibilidade do código.

---

## Use nomes pesquisáveis

Nós leremos muito mais código do que escreveremos, por isso a legibilidade é fundamental. **Variáveis e constantes com nomes pouco descritivos dificultam a compreensão do código e prejudicam os leitores.** Escolha nomes que tenham significado e que sejam facilmente pesquisáveis. 

Ferramentas como [StyleCop](https://github.com/StyleCop/StyleCop) e [Roslyn Analyzers](https://github.com/dotnet/roslyn-analyzers) podem ajudar a identificar problemas como números mágicos e variáveis mal nomeadas.

**Ruim:**  
```csharp
// O que significa 86400000?
Thread.Sleep(86400000);
```

**Bom:**  
```csharp
// Declare constantes globais em letras maiúsculas para facilitar a identificação.
const int MILLISECONDS_PER_DAY = 86400000;

Thread.Sleep(MILLISECONDS_PER_DAY);
```

---

## Use variáveis explicativas

**Variáveis devem expressar claramente sua função no código.** Se o nome não deixa evidente o propósito, o código se torna difícil de entender e modificar. Prefira decompor expressões complexas para melhorar a legibilidade.

**Ruim:**  
```csharp
string address = "One Infinite Loop, Cupertino 95014";
Regex cityZipCodeRegex = new Regex(@"^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$");
SaveCityZipCode(
    cityZipCodeRegex.Match(address).Groups[1].Value, 
    cityZipCodeRegex.Match(address).Groups[2].Value
);
```

**Bom:**  
```csharp
string address = "One Infinite Loop, Cupertino 95014";
Regex cityZipCodeRegex = new Regex(@"^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$");

Match match = cityZipCodeRegex.Match(address);
string city = match.Groups[1].Value;
string zipCode = match.Groups[2].Value;

SaveCityZipCode(city, zipCode);
```

---

## Evite Mapeamento Mental  

Explícito é sempre melhor que implícito. **Escolha nomes de variáveis que comuniquem claramente seu propósito**. Evite siglas ou abreviações excessivas que tornem o código confuso.

**Ruim:**  
```csharp
List<string> locations = new() { "Austin", "New York", "San Francisco" };
locations.ForEach(l => 
{
    DoStuff();
    DoSomeOtherStuff();
    // ...
    // ...
    // ...
    Dispatch(l); // O que era "l" mesmo?
});
```

**Bom:**  
```csharp
List<string> locations = new() { "Austin", "New York", "San Francisco" };
locations.ForEach(location => 
{
    DoStuff();
    DoSomeOtherStuff();
    // ...
    // ...
    // ...
    Dispatch(location); // Nome mais claro e intuitivo
});
```

---

## Não adicione contextos desnecessários  

Se o nome da classe ou objeto já fornece um contexto, evite repetições desnecessárias nas variáveis. Isso deixa o código mais limpo e menos redundante.

**Ruim:**  
```csharp
class Car
{
    public string CarMake { get; set; }
    public string CarModel { get; set; }
    public string CarColor { get; set; }
}

void PaintCar(Car car, string color)
{
    car.CarColor = color;
}
```

**Bom:**  
```csharp
class Car
{
    public string Make { get; set; }
    public string Model { get; set; }
    public string Color { get; set; }
}

void PaintCar(Car car, string color)
{
    car.Color = color;
}
```

---

## Use argumentos padrões ao invés de curto-circuitar ou usar condicionais  

Os **parâmetros padrão** permitem evitar verificações redundantes e tornam o código mais limpo e previsível. No **C#**, valores padrão são atribuídos diretamente no cabeçalho do método.

**Ruim:**  
```csharp
void CreateMicrobrewery(string name)
{
    string breweryName = name ?? "Hipster Brew Co."; // Uso desnecessário de curto-circuito
    // ...
}
```

**Bom:**  
```csharp
void CreateMicrobrewery(string breweryName = "Hipster Brew Co.")
{
    // Código mais limpo e intuitivo
}
```

Além disso, ao trabalhar com **construtores**, podemos aplicar o mesmo conceito:

```csharp
class Microbrewery
{
    public string Name { get; }

    public Microbrewery(string name = "Hipster Brew Co.")
    {
        Name = name;
    }
}
```

---









