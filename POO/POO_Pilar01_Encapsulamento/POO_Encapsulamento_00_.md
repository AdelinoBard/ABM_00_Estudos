# **Encapsulamento**

O **encapsulamento** é um dos princípios fundamentais da **Programação Orientada a Objetos (POO)** e tem como objetivo **proteger os dados de uma classe**, expondo apenas o necessário e garantindo a integridade do código.

## **Objetos na Programação Orientada a Objetos (POO)**

Compreender o conceito de **objeto** é essencial para a programação orientada a objetos. Objetos são a base dessa abordagem e podem ser encontrados em nosso cotidiano: seu computador, seu carro e até mesmo este texto são exemplos de objetos.

### **Características dos Objetos no Mundo Real**

Os objetos do mundo real possuem duas características fundamentais: **estado** e **comportamento**.

- **Estado:** Representa os atributos ou propriedades de um objeto. Por exemplo, um cachorro possui estados como nome, raça, tamanho e peso. Da mesma forma, uma bicicleta tem estados como marcha atual e velocidade.

- **Comportamento:** Diz respeito às ações que um objeto pode realizar. Um cachorro pode latir, brincar, correr e dormir, enquanto uma bicicleta pode trocar de marcha, acelerar e frear.

Observar objetos do cotidiano e identificar seus estados e comportamentos é uma abordagem prática para compreender a POO. Além disso, muitos objetos são compostos por outros e podem depender uns dos outros, refletindo relações que também existem na modelagem de software.

### **Objetos no Software**

No contexto da programação, um **objeto** apresenta características similares às dos objetos do mundo real, possuindo **estado** e **comportamento**.

- **Estado:** Armazenado em campos (ou variáveis) do objeto.

- **Comportamento:** Definido por métodos (ou funções), que determinam as ações que o objeto pode realizar.

Os métodos manipulam o estado interno do objeto e servem como o principal meio de comunicação entre diferentes objetos. Uma prática fundamental da POO é ocultar os detalhes internos de um objeto, permitindo que interações externas ocorram exclusivamente por meio de métodos — um conceito conhecido como **encapsulamento**.

## **Encapsulamento**

O encapsulamento, na programação orientada a objetos, refere-se à separação e proteção dos dados de um objeto, garantindo que ele controle sua própria lógica interna. Esse princípio torna o software mais flexível, facilitando modificações e melhorias na implementação.

Com o encapsulamento, um objeto pode controlar como o mundo externo interage com ele. Por exemplo, se uma bicicleta tem um limite de 10 marchas, o método para mudar de marcha pode impedir qualquer valor fora dessa faixa, garantindo a integridade do estado do objeto.

**Exemplo em C#:**

```csharp
public class Bicicleta
{
    private int marchaAtual;
    private const int marchaMaxima = 10;
    private const int marchaMinima = 1;

    public int MarchaAtual => marchaAtual;

    public void MudarMarcha(int novaMarcha)
    {
        if (novaMarcha >= marchaMinima && novaMarcha <= marchaMaxima)
        {
            marchaAtual = novaMarcha;
        }
        else
        {
            Console.WriteLine("Marcha inválida. Escolha um valor entre 1 e 10.");
        }
    }
}
```

## **1. O Que é Encapsulamento?**

O **encapsulamento** consiste em **esconder os detalhes internos** de uma classe e fornecer formas controladas de acesso aos seus dados. Isso evita que informações sejam modificadas diretamente e permite adicionar validações e lógica de controle.

- **Definição:** O encapsulamento envolve a combinação de dados (atributos) e métodos (comportamentos) em uma única unidade chamada **classe**.
- **Princípio:** Cada classe deve ser responsável por gerenciar seus próprios dados e comportamentos.
- **Objetivo:** Isolar os detalhes internos da classe, ocultando-os do mundo exterior. Isso promove segurança, manutenção e flexibilidade do código.

### **Analogias**

O encapsulamento separa a **interface de uso** da **implementação interna**, tornando os objetos mais intuitivos, seguros e fáceis de manter. Essa técnica permite criar sistemas robustos e escaláveis.

#### **1. Celular**

O funcionamento de um celular envolve diversas tecnologias, mas o usuário não precisa entender cada detalhe técnico para utilizá-lo.

- **Interface de Uso:** Tela sensível ao toque, botões, menus e aplicativos permitem interação intuitiva.
- **Implementação:** Processadores, sensores, antenas e sistemas operacionais trabalham nos bastidores.
- **Exemplo:** Ao fazer uma ligação, basta digitar o número e pressionar um botão. O usuário não precisa conhecer os processos internos de transmissão de sinais.

#### **2. Carro**

Os fabricantes de automóveis aplicam encapsulamento para garantir que mudanças internas não afetem o modo de dirigir.

- **Interface de Uso:** Volante, pedais, alavanca de câmbio e painel de controle.
- **Implementação:** Motores, sistemas eletrônicos e transmissão interna.
- **Exemplo:** Mesmo que um carro mude de carburador para injeção eletrônica, a interface de uso permanece a mesma.

#### **3. Máquina de Vendas**

Máquinas automáticas impedem interferências externas em seu funcionamento interno.

- **Interface de Uso:** Botões para escolha, entrada para pagamento e saída do produto.
- **Implementação:** Sensores verificam o pagamento, mecanismos internos liberam os produtos.
- **Exemplo:** O usuário compra um refrigerante apenas interagindo com a interface, sem acesso direto ao mecanismo interno.

## **2. Benefícios do Encapsulamento**

O encapsulamento **protege a integridade dos dados**, **facilita a manutenção** e **torna o código mais adaptável a mudanças**.

### **1. Segurança dos Dados**

- **Atributos privados** evitam modificações indevidas.
- **Métodos públicos** controlam o acesso e garantem valores válidos.

### **2. Facilidade de Manutenção**

- **Mudanças internas** não afetam o código externo.
- **Evolução sem impacto**: Novas regras podem ser adicionadas sem quebrar o código existente.

### **3. Flexibilidade e Extensibilidade**

- **Herança segura**: Classes derivadas podem reutilizar comportamentos sem expor detalhes internos.
- **Novos métodos podem ser adicionados** sem interferir no código que já utiliza a classe.

### **4. Validação Centralizada**

- **Regras de negócio são aplicadas em um único lugar**, evitando inconsistências.

### **5. Modularidade e Ocultação de Detalhes**

- **Cada classe gerencia seus próprios dados**, sem expor sua implementação interna.
- **Código mais limpo e desacoplado**, facilitando testes e reutilização.

## **3. Como Implementar Encapsulamento em C#**

O encapsulamento é um dos pilares fundamentais da Programação Orientada a Objetos (POO). Em C#, ele é implementado principalmente através de modificadores de acesso e propriedades, permitindo controlar rigorosamente como os dados de uma classe são acessados e modificados.

### **3.1 Implementação Básica**

#### **a) Atributos Privados + Métodos Públicos (Abordagem Tradicional)**

```csharp
public class ContaBancaria
{
    // Atributo privado - só acessível dentro da classe
    private double _saldo;

    // Método público para operação de depósito
    public void Depositar(double valor)
    {
        if (valor > 0)
            _saldo += valor;
        else
            Console.WriteLine("Valor de depósito inválido!");
    }

    // Método público para consulta segura
    public double ObterSaldo()
    {
        return _saldo;
    }
}
```

**Vantagens:**

- Controle total sobre as operações
- Possibilidade de adicionar validações complexas
- Clareza na intenção (métodos como ações)

**Uso:**

```csharp
var conta = new ContaBancaria();
conta.Depositar(500);
Console.WriteLine($"Saldo: {conta.ObterSaldo()}");
```

#### **b) Propriedades (Abordagem Moderna)**

```csharp
public class ContaBancaria
{
    private double _saldo;

    // Propriedade com lógica de validação
    public double Saldo
    {
        get => _saldo;
        private set  // Set pode ser restrito
        {
            if (value >= 0)
                _saldo = value;
            else
                Console.WriteLine("Saldo não pode ser negativo!");
        }
    }

    // Método que utiliza a propriedade internamente
    public void AplicarJuros(double taxa)
    {
        Saldo *= (1 + taxa/100); // Usa o setter da propriedade
    }
}
```

**Vantagens:**

- Sintaxe mais limpa e intuitiva
- Combina acesso direto com lógica de validação
- Pode ter níveis de acesso diferentes para get/set

**Uso:**

```csharp
var conta = new ContaBancaria();
// conta.Saldo = -100; // Erro - set é privado
Console.WriteLine(conta.Saldo); // Get público
```

### **3.2 Padrões Avançados de Encapsulamento**

#### **a) Propriedades Auto-Implementadas**

Para casos simples sem lógica adicional:

```csharp
public class Cliente
{
    public string Nome { get; set; } // Getter e setter padrão
    public int Id { get; } // Somente leitura (set apenas no construtor)

    public Cliente(int id)
    {
        Id = id; // Pode ser setado apenas no construtor
    }
}
```

#### **b) Encapsulamento com Expressões Corporadas (C# 7+)**

```csharp
public class Retangulo
{
    private double _largura;
    private double _altura;

    public double Area => _largura * _altura; // Propriedade somente-leitura

    public Retangulo(double largura, double altura)
    {
        _largura = largura > 0 ? largura : throw new ArgumentException();
        _altura = altura > 0 ? altura : throw new ArgumentException();
    }
}
```

#### **c) Padrão de Backing Field**

```csharp
public class Temperatura
{
    private double _celsius;

    public double Celsius
    {
        get => _celsius;
        set => _celsius = value >= -273.15 ? value : _celsius;
    }

    public double Fahrenheit
    {
        get => (_celsius * 9/5) + 32;
        set => _celsius = (value - 32) * 5/9;
    }
}
```

### **3.3 Encapsulamento em Hierarquias de Herança**

#### **Modificador `protected`**

```csharp
public class Veiculo
{
    protected string _chassi; // Acessível por classes derivadas

    public void Ligar() => Console.WriteLine("Veículo ligado");
}

public class Carro : Veiculo
{
    public void ExibirChassi() => Console.WriteLine(_chassi);
}
```

#### **Classes e Membros `sealed`**

```csharp
public sealed class ContaPoupanca : ContaBancaria
{
    public void AplicarRendimento() { /* ... */ }
}

// Erro: Não pode herdar de classe sealed
// public class ContaPremium : ContaPoupanca { }
```

### **3.4 Boas Práticas de Encapsulamento**

1. **Princípio do Menor Privilégio**

   - Comece com `private` e aumente a visibilidade apenas quando necessário

2. **Imutabilidade para Thread Safety**

   ```csharp
   public class Configuracao
   {
       public string Servidor { get; }
       public int Porta { get; }

       public Configuracao(string servidor, int porta)
       {
           Servidor = servidor;
           Porta = porta;
       }
   }
   ```

3. **Validação Centralizada**

   ```csharp
   public class Pedido
   {
       private DateTime _data;

       public DateTime Data
       {
           get => _data;
           set => _data = value <= DateTime.Now ? value
               : throw new ArgumentException("Data futura inválida");
       }
   }
   ```

4. **Encapsulamento de Coleções**

   ```csharp
   public class Biblioteca
   {
       private readonly List<Livro> _livros = new List<Livro>();

       // Expõe coleção como somente-leitura
       public IReadOnlyCollection<Livro> Livros => _livros.AsReadOnly();

       public void AdicionarLivro(Livro livro) => _livros.Add(livro);
   }
   ```

### **3.5 Exemplo Completo: Sistema de Usuários**

```csharp
public class Usuario
{
    private string _email;
    private string _senha;
    private DateTime _dataCadastro;

    public string Nome { get; set; }

    public string Email
    {
        get => _email;
        set => _email = ValidarEmail(value) ? value
            : throw new FormatException("Email inválido");
    }

    public int Idade { get; private set; }

    public string Senha
    {
        private get => _senha;
        set => _senha = CriptografarSenha(value);
    }

    public TimeSpan TempoCadastro => DateTime.Now - _dataCadastro;

    public Usuario(string nome, string email, int idade)
    {
        Nome = nome;
        Email = email;
        DefinirIdade(idade);
        _dataCadastro = DateTime.Now;
    }

    public bool VerificarSenha(string senha)
    {
        return CriptografarSenha(senha) == _senha;
    }

    public void DefinirIdade(int idade)
    {
        if (idade >= 0 && idade <= 120)
            Idade = idade;
    }

    private bool ValidarEmail(string email) => email.Contains("@");
    private string CriptografarSenha(string senha) => /* lógica */;
}
```

### **3.6 Perguntas Frequentes**

**Q: Quando usar métodos vs propriedades?**

- Use métodos para:
  - Ações que modificam estado significativamente (`TransferirFundos()`)
  - Operações com parâmetros complexos
  - Quando o nome do verbo é importante (`CalcularImposto()`)
- Use propriedades para:
  - Características do objeto (`Cor`, `Tamanho`)
  - Valores simples com get/set básico
  - Quando a sintaxe de campo faz sentido (`obj.Valor = 10`)

**Q: Como proteger classes de alterações indevidas?**

- Use `readonly` para campos que não devem mudar após construção
- Considere `init` (C# 9+) para propriedades imutáveis pós-construção
- Para coleções, exponha interfaces (`IReadOnlyList`) em vez da coleção real

**Q: Propriedades auto-implementadas vs campos completos?**

- Auto-implementadas quando não precisa de lógica adicional
- Campos completos quando precisa:
  - Validação
  - Notificações (ex: INotifyPropertyChanged)
  - Lógica complexa no get/set

## **4. Atributos e Métodos Estáticos em C#**

Em C#, os **atributos e métodos estáticos** pertencem à própria classe, e não às instâncias individuais. Isso significa que todos os objetos dessa classe compartilham o mesmo valor do atributo estático, e métodos estáticos podem ser chamados sem a necessidade de criar um objeto.

### **4.1. Atributos Estáticos**

Um atributo estático é um campo que pertence à classe e não às suas instâncias. Ou seja, independentemente de quantos objetos existam dessa classe, todos compartilharão o mesmo valor desse atributo.

#### **Exemplo: Funcionários de um Banco**

Imagine um sistema que gerencia funcionários de um banco. Inicialmente, podemos definir a classe `Funcionario` da seguinte maneira:

```csharp
class Funcionario
{
    public string Nome;
    public double Salario;

    public void AumentaSalario(double aumento)
    {
        Salario += aumento;
    }
}
```

Agora, suponha que o banco oferece **um mesmo valor de vale-refeição diário para todos os funcionários**. Se definirmos esse atributo na classe sem o modificador `static`, cada funcionário teria um valor independente, o que não faz sentido, pois o benefício é uniforme para todos.

A solução correta é tornar `ValeRefeicaoDiario` um **atributo estático**, garantindo que ele pertença à classe e não às instâncias:

```csharp
class Funcionario
{
    public string Nome;
    public double Salario;
    public static double ValeRefeicaoDiario;

    public void AumentaSalario(double aumento)
    {
        Salario += aumento;
    }
}
```

Agora, `ValeRefeicaoDiario` deve ser acessado **pelo nome da classe**, e não por instâncias:

```csharp
Funcionario.ValeRefeicaoDiario = 15.0;
Console.WriteLine("Valor do vale-refeição diário: " + Funcionario.ValeRefeicaoDiario);
```

#### **Características dos Atributos Estáticos**

- São compartilhados entre todas as instâncias da classe.
- Devem ser acessados diretamente pelo nome da classe (`Classe.Atributo`).
- São úteis para armazenar valores globais da classe.

### **4.2. Métodos Estáticos**

Assim como podemos ter **atributos estáticos**, também podemos definir **métodos estáticos**, que pertencem à classe e não exigem a criação de um objeto para serem chamados.

#### **Exemplo: Reajuste do Vale-Refeição**

Imagine que o banco decide reajustar o valor do vale-refeição de acordo com uma taxa. Podemos criar um método estático para realizar esse ajuste:

```csharp
class Funcionario
{
    public string Nome;
    public double Salario;
    public static double ValeRefeicaoDiario;

    public static void ReajustaValeRefeicaoDiario(double taxa)
    {
        ValeRefeicaoDiario += ValeRefeicaoDiario * taxa;
    }
}
```

Agora, chamamos esse método pelo nome da classe:

```csharp
Funcionario.ValeRefeicaoDiario = 15.0; // Definindo valor inicial
Funcionario.ReajustaValeRefeicaoDiario(0.1); // Reajustando em 10%
Console.WriteLine("Novo valor do vale-refeição diário: " + Funcionario.ValeRefeicaoDiario);
```

#### **Características dos Métodos Estáticos**

- São chamados diretamente pelo nome da classe (`Classe.Metodo()`).
- Não têm acesso a atributos de instância, pois não operam em objetos individuais.
- São úteis para operações gerais que envolvem a classe como um todo.

### **4.3. Diferenças entre Estático e Instância**

| Característica | Estático | Instância |
| --- | --- | --- |
| Pertence a | Classe | Objeto (instância) |
| Modificador | `static` | Sem `static` |
| Necessário criar objeto? | Não | Sim |
| Acesso | `Classe.Atributo` | `objeto.Atributo` |
| Exemplo | `Funcionario.ValeRefeicaoDiario` | `meuFuncionario.Salario` |

---

# **Encapsulamento: Exemplos Práticos**

## **1. Classe `Pessoa` - Controle de Dados Básicos**

### **Versão sem Encapsulamento (Problema)**

```csharp
public class Pessoa
{
    public string Nome;  // Acesso direto sem proteção
    public int Idade;    // Pode receber valores inválidos (ex: -10)
}
```

**Problema**: Ausência de validação permite dados inconsistentes.

### **Versão com Encapsulamento (Solução)**

```csharp
public class Pessoa
{
    private string _nome;
    private int _idade;

    public string Nome
    {
        get => _nome;
        set => _nome = value; // Pode adicionar validações se necessário
    }

    public int Idade
    {
        get => _idade;
        set => _idade = value >= 0 ? value : throw new ArgumentException("Idade não pode ser negativa!");
    }
}
```

### **Versão Simplificada (Propriedades Automáticas)**

```csharp
public class Pessoa
{
    public string Nome { get; set; }  // Encapsulamento básico
    public int Idade { get; set; }    // Validação pode ser adicionada depois
}
```

**Vantagens**:

- Controle centralizado das regras de validação
- Flexibilidade para evoluir a implementação
- Proteção contra acesso indevido

## **2. Classe `ContaBancaria` - Gerenciamento Seguro de Saldo**

### **Implementação com Encapsulamento**

```csharp
public class ContaBancaria
{
    private double _saldo;

    public double Saldo => _saldo; // Somente leitura

    public ContaBancaria(double saldoInicial) => _saldo = saldoInicial;

    public void Depositar(double valor)
    {
        if (valor <= 0)
            throw new ArgumentException("Valor deve ser positivo");

        _saldo += valor;
        Console.WriteLine($"Depósito de R${valor:F2} realizado.");
    }

    public void Sacar(double valor)
    {
        if (valor <= 0)
            throw new ArgumentException("Valor deve ser positivo");

        if (_saldo < valor)
            throw new InvalidOperationException("Saldo insuficiente");

        _saldo -= valor;
        Console.WriteLine($"Saque de R${valor:F2} realizado.");
    }
}
```

### **Exemplo de Uso**

```csharp
var conta = new ContaBancaria(1000);
conta.Depositar(500);
conta.Sacar(200);
Console.WriteLine($"Saldo atual: R${conta.Saldo:F2}");
```

**Proteções Implementadas**:

- Saldo não pode ser modificado diretamente
- Validação de valores positivos
- Verificação de saldo suficiente para saques

## **3. Classe `Funcionario` - Controle de Salário**

### **Evolução da Implementação**

```csharp
public class Funcionario
{
    private double _salario;

    public double Salario => _salario; // Somente leitura

    public Funcionario(double salarioInicial) => _salario = salarioInicial;

    public void AumentarSalario(double percentual)
    {
        if (percentual <= 0)
            throw new ArgumentException("Percentual deve ser positivo");

        _salario *= (1 + percentual/100);
        Console.WriteLine($"Aumento aplicado. Novo salário: R${_salario:F2}");
    }
}
```

**Melhorias**:

- Controle rígido sobre modificações salariais
- Validação de percentual positivo
- Histórico de alterações pode ser adicionado posteriormente

## **4. Classe `Conta` - Métodos Auxiliares Privados**

### **Implementação com Método Privado**

```csharp
public class Conta
{
    private double _saldo;
    private const double TARIFA = 0.10;

    public Conta(double saldoInicial) => _saldo = saldoInicial;

    public void Depositar(double valor)
    {
        ValidarValor(valor);
        _saldo += valor;
        AplicarTarifa();
        Console.WriteLine($"Depósito realizado. Saldo: R${_saldo:F2}");
    }

    public void Sacar(double valor)
    {
        ValidarValor(valor);
        if (_saldo < valor + TARIFA)
            throw new InvalidOperationException("Saldo insuficiente");

        _saldo -= valor;
        AplicarTarifa();
        Console.WriteLine($"Saque realizado. Saldo: R${_saldo:F2}");
    }

    private void ValidarValor(double valor)
    {
        if (valor <= 0)
            throw new ArgumentException("Valor deve ser positivo");
    }

    private void AplicarTarifa() => _saldo -= TARIFA;
}
```

**Benefícios**:

- Tarifa aplicada automaticamente em cada operação
- Validação centralizada
- Lógica complexa escondida do usuário da classe

## **Padrões Recomendados**

1. **Prefira propriedades** a campos públicos
2. **Métodos auxiliares** devem ser privados
3. **Validações** devem ocorrer nos setters e métodos
4. **Exceções** são melhores que mensagens no console
5. **Constantes** para valores fixos (como tarifas)

Estes exemplos demonstram como o encapsulamento:

- Protege a integridade dos dados
- Facilita manutenção futura
- Esconde detalhes de implementação
- Oferece interfaces claras e seguras para interação

---
