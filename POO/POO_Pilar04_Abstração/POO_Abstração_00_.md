# **Abstração**

A **Abstração** é um dos conceitos fundamentais da **Programação Orientada a Objetos (POO)**, juntamente com **Encapsulamento**, **Herança** e **Polimorfismo**. Seu objetivo é **simplificar a complexidade do mundo real**, focando apenas nos aspectos essenciais de um objeto ou sistema, enquanto oculta detalhes irrelevantes.

## **1. O que é Abstração?**

A abstração permite representar entidades do mundo real de maneira simplificada, considerando apenas **suas características e comportamentos essenciais**.

### **Exemplo Simples**

Imagine um **carro**:

- **Atributos relevantes:** modelo, cor, velocidade.
- **Métodos relevantes:** acelerar, frear, trocar marcha.
- **Detalhes ignorados:** tipo de tinta, estrutura interna do motor.

Em C#, podemos representar essa abstração com uma **classe**:

```csharp
class Carro
{
    public string Modelo { get; set; }
    public string Cor { get; set; }

    public void Acelerar()
    {
        Console.WriteLine("O carro está acelerando...");
    }

    public void Frear()
    {
        Console.WriteLine("O carro está freando...");
    }
}
```

## **2. Benefícios da Abstração**

- **Redução da complexidade**, focando apenas no essencial.
- **Reutilização de código**, permitindo generalizar objetos abstratos.
- **Facilidade na manutenção**, pois mudanças internas não afetam quem usa a abstração.
- **Maior segurança**, ocultando detalhes sensíveis.

## **3. Como implementar a Abstração em C#?**

Existem duas formas principais:

### **a) Classes Abstratas**

- **Não podem ser instanciadas diretamente.**
- Servem como modelo para outras classes.
- Podem conter **métodos abstratos** (sem implementação) e **métodos concretos** (com implementação).

#### **Exemplo Simples**

```csharp
abstract class Veiculo
{
    public abstract void Acelerar(); // Método abstrato
    public void Frear() // Método concreto
    {
        Console.WriteLine("O veículo está freando...");
    }
}

class Carro : Veiculo
{
    public override void Acelerar()
    {
        Console.WriteLine("O carro está acelerando...");
    }
}
```

Uso:

```csharp
Carro meuCarro = new Carro();
meuCarro.Acelerar(); // Saída: O carro está acelerando...
meuCarro.Frear(); // Saída: O veículo está freando...
```

### **b) Interfaces**

- **Definem um contrato** que deve ser seguido pelas classes que as implementam.
- Permitem **polimorfismo**, pois uma interface pode ser implementada por várias classes.

#### **Exemplo Simples**

```csharp
interface IVeiculo
{
    void Acelerar();
    void Frear();
}

class Moto : IVeiculo
{
    public void Acelerar()
    {
        Console.WriteLine("A moto está acelerando...");
    }

    public void Frear()
    {
        Console.WriteLine("A moto está freando...");
    }
}
```

Uso:

```csharp
Moto minhaMoto = new Moto();
minhaMoto.Acelerar(); // Saída: A moto está acelerando...
minhaMoto.Frear(); // Saída: A moto está freando...
```

## **4. Diferença entre Abstração e Encapsulamento**

| **Abstração** | **Encapsulamento** |
| --- | --- |
| Foca no **"o que"** um objeto faz, não **"como"**. | Foca em **proteger** dados internos de um objeto. |
| **Simplifica** a representação de um objeto. | **Esconde** detalhes de implementação. |
| Usa **classes abstratas** e **interfaces**. | Usa **modificadores de acesso** (`private`, `protected`). |

## **5. Quando usar Abstração?**

- Quando há **múltiplas classes com comportamentos similares**.
- Para definir **contratos** que garantem consistência na implementação de diferentes classes.
- Quando **detalhes internos devem ser ocultados**, focando apenas na funcionalidade principal.

---
