# Modificadores de Acesso e Herança em C#

Os modificadores de acesso em C# controlam a visibilidade e acessibilidade dos membros de uma classe:

- `public`: Acessível de qualquer lugar
- `protected`: Acessível apenas na classe e em classes derivadas
- `private`: Acessível apenas na classe que os declara

## 1. Herança de Modificadores de Acesso

Quando uma classe herda de outra, os modificadores de acesso se comportam da seguinte forma:

### 1.1 Membros Públicos

Mantêm sua visibilidade na classe derivada.

```csharp
public class Animal {
    public string Nome;
}

public class Cachorro : Animal {
    public void Latir() {
        Console.WriteLine(Nome + " está latindo!"); // Nome é acessível
    }
}
```

### 1.2 Membros Protegidos

Permanecem acessíveis apenas na classe derivada.

```csharp
public class Veiculo {
    protected int Rodas;
}

public class Carro : Veiculo {
    public void MostrarRodas() {
        Rodas = 4; // Acessível
        Console.WriteLine("Número de rodas: " + Rodas);
    }
}
```

Métodos de classe derivada podem se referir a membros `public` e `protected` herdados da classe base simplesmente usando os nomes dos membros. Quando um método de classe derivada substitui um método de classe base, a versão da classe base pode ser acessada da classe derivada precedendo o nome do método de classe base com a palavra-chave `base` e o operador de acesso de membro (`.`).

Todos os membros da classe base não `privada` mantêm seu modificador de acesso original quando se tornam membros da classe derivada — membros `públicos` da classe base tornam-se membros `públicos` da classe derivada, e membros `protegidos` da classe base tornam-se membros `protegidos` da classe derivada.

_Declarar variáveis de instância de classe base privadas (em oposição a protegidas) permite que a implementação de classe base dessas variáveis de instância mude sem afetar implementações de classe derivada._

### 1.3 Membros Privados

Não são acessíveis diretamente na classe derivada.

_Propriedades e métodos de uma classe derivada não podem acessar diretamente membros privados da classe base. Uma classe derivada pode alterar o estado de campos privados da classe base somente por meio de métodos e propriedades não privados fornecidos na classe base._

_Declarar campos privados em uma classe base ajuda a testar, depurar e modificar corretamente os sistemas. Se uma classe derivada pudesse acessar os campos privados de sua classe base, as classes que herdam dessa classe derivada também poderiam acessar os campos. Isso propagaria o acesso ao que deveriam ser campos privados, e os benefícios da ocultação de informações seriam perdidos._

Os membros `private` de uma classe base _são_ herdados por suas classes derivadas, mas _não_ são diretamente acessíveis por métodos e propriedades da classe derivada.

```csharp
public class Conta {
    private double saldo;

    public void Depositar(double valor) {
        saldo += valor;
    }
}

public class ContaPoupanca : Conta {
    public void MostrarSaldo() {
        // Console.WriteLine(saldo); // Erro - saldo é privado
        Console.WriteLine("Saldo disponível: " + VerSaldo());
    }

    public double VerSaldo() {
        return base.ObterSaldo(); // Acessível apenas via métodos públicos
    }
}
```

## 2. Acessando Membros da Classe Base

### 2.1 Usando a palavra-chave `base`

```csharp
public class Forma {
    public virtual void Desenhar() {
        Console.WriteLine("Desenhando forma genérica");
    }
}

public class Circulo : Forma {
    public override void Desenhar() {
        base.Desenhar(); // Chama o método da classe base
        Console.WriteLine("Desenhando círculo");
    }
}
```

### 2.2 Problemas com campos protegidos

Embora campos `protected` permitam acesso direto em classes derivadas, isso pode:

1. Violar o encapsulamento
2. Permitir valores inválidos
3. Criar dependência da implementação

```csharp
// Má prática - uso de protected para campos
public class Funcionario {
    protected double salario; // Pode ser alterado diretamente sem validação
}

// Boa prática - uso de private com métodos de acesso
public class FuncionarioCorreto {
    private double salario;

    public void DefinirSalario(double valor) {
        if (valor >= 0) {
            salario = valor;
        }
    }
}
```

## 3. Exemplo Completo

```csharp
public class Pessoa {
    private string nome; // Privado - melhor prática
    protected int idade; // Protegido - use com cautela

    public Pessoa(string nome, int idade) {
        this.nome = nome;
        this.idade = idade;
    }

    public string ObterNome() {
        return nome;
    }

    public virtual void Apresentar() {
        Console.WriteLine($"Olá, meu nome é {nome} e tenho {idade} anos.");
    }
}

public class Estudante : Pessoa {
    private string matricula;

    public Estudante(string nome, int idade, string matricula)
        : base(nome, idade) {
        this.matricula = matricula;
    }

    public override void Apresentar() {
        base.Apresentar(); // Chama o método da classe base
        Console.WriteLine($"Minha matrícula é {matricula}.");
    }

    public void MostrarIdade() {
        Console.WriteLine($"Tenho {idade} anos."); // idade é acessível (protected)
    }
}

class Program {
    static void Main() {
        Estudante estudante = new Estudante("Ana", 20, "12345");
        estudante.Apresentar();
        estudante.MostrarIdade();
        Console.WriteLine(estudante.ObterNome()); // Acessa nome via método público
    }
}
```

## 4. Resumo e Boas Práticas

- Prefira campos `private` com métodos/propriedades públicas para acesso
- Use `protected` com moderação, apenas quando necessário
- Lembre-se que membros `private` são herdados, mas não acessíveis diretamente
- A palavra-chave `base` permite acessar membros da classe base
- O encapsulamento adequado facilita a manutenção e evita erros
