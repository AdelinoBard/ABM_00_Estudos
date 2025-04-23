# Programação Orientada a Objetos (POO)

A Programação Orientada a Objetos (POO) é um paradigma de programação que organiza o código em "objetos", que representam entidades do mundo real ou conceitos abstratos. 

Esses objetos contêm dados (**atributos**) e comportamentos (**métodos**).

- Existem objetos de data, objetos de tempo, objetos de áudio, objetos de vídeo, objetos de automóvel, objetos de pessoas, etc. Quase qualquer substantivo pode ser razoavelmente representado como um objeto de software em termos de atributos (por exemplo, nome, cor e tamanho) e comportamentos (por exemplo, calcular, mover e comunicar).

**Analogia:** Imagine uma biblioteca. Cada livro pode ser considerado um objeto com atributos (título, autor, ISBN) e comportamentos (ser emprestado, ser devolvido). A classe seria o "modelo" para criar esses livros.

## Por que usar POO?
- **Organização:** Estrutura clara para código complexo
- **Reutilização:** Classes podem ser usadas em vários projetos
- **Manutenção:** Mais fácil de entender e modificar
- **Escalabilidade:** Adequada para sistemas grandes
- **Modularidade:** Código dividido em componentes independentes
- **Extensibilidade:** Novas funcionalidades podem ser adicionadas facilmente
- **Segurança:** Encapsulamento protege os dados internos

## Conceitos Fundamentais

### 1. Classes e Objetos

**Classe:** Molde/planta que define atributos e métodos  
**Objeto:** Instância concreta criada a partir de uma classe

**Exemplo em C#:**
```csharp
// Definindo uma classe simples
public class Cachorro
{
    // Atributos
    public string Nome;
    public int Idade;
    
    // Método
    public void Latir()
    {
        Console.WriteLine($"{Nome} diz: Au Au!");
    }
}

// Criando objetos
class Program
{
    static void Main()
    {
        Cachorro meuCachorro = new Cachorro();
        meuCachorro.Nome = "Rex";
        meuCachorro.Idade = 3;
        meuCachorro.Latir(); // Saída: Rex diz: Au Au!
    }
}
```

### 2. Encapsulamento

Protege os dados internos de um objeto, expondo apenas o necessário.

**Exemplo melhorado:**
```csharp
public class ContaBancaria
{
    private double saldo; // Privado = acesso restrito

    // Métodos públicos para interação
    public void Depositar(double valor)
    {
        if (valor > 0)
            saldo += valor;
    }

    public bool Sacar(double valor)
    {
        if (valor <= saldo)
        {
            saldo -= valor;
            return true;
        }
        return false;
    }

    public double VerSaldo()
    {
        return saldo;
    }
}
```

### 3. Herança

Permite criar novas classes baseadas em classes existentes.

**Exemplo simplificado:**
```csharp
// Classe base
public class Animal
{
    public void Comer()
    {
        Console.WriteLine("Comendo...");
    }
}

// Classe derivada
public class Gato : Animal
{
    public void Miar()
    {
        Console.WriteLine("Miau!");
    }
}

// Uso
Gato meuGato = new Gato();
meuGato.Comer();  // Herdado de Animal
meuGato.Miar();   // Específico de Gato
```

### 4. Polimorfismo

Objetos diferentes podem responder ao mesmo comando de maneiras distintas.

**Exemplo prático:**
```csharp
public class Forma
{
    public virtual void Desenhar()
    {
        Console.WriteLine("Desenhando forma genérica");
    }
}

public class Circulo : Forma
{
    public override void Desenhar()
    {
        Console.WriteLine("Desenhando um círculo");
    }
}

public class Quadrado : Forma
{
    public override void Desenhar()
    {
        Console.WriteLine("Desenhando um quadrado");
    }
}

// Uso polimórfico
Forma[] formas = new Forma[] { new Circulo(), new Quadrado() };
foreach (var forma in formas)
{
    forma.Desenhar(); // Chama o método apropriado para cada tipo
}
```

### 5. Abstração

Foca no essencial, ignorando detalhes irrelevantes.

**Exemplo em C#:**
```csharp
public abstract class Veiculo
{
    public abstract void Mover();
}

public class Carro : Veiculo
{
    public override void Mover()
    {
        Console.WriteLine("Carro andando na estrada");
    }
}

public class Barco : Veiculo
{
    public override void Mover()
    {
        Console.WriteLine("Barco navegando no mar");
    }
}
```

---