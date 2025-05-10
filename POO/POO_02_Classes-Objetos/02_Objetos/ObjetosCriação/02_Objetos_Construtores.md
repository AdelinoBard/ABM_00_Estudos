# Construtores em C#

## Resumo

### O que é uma Classe e um Objeto?

- **Classe**: É um modelo ou "planta" que define atributos (dados) e métodos (comportamentos) de um objeto.
- **Objeto**: É uma instância concreta criada a partir de uma classe, ocupando espaço na memória.

**Exemplo Simplificado de uma classe:**

```csharp
class Carro
{
    public string Cor;
    public int Ano;
}
```

### Instanciação Vs. Construtores

- **Instanciação**: Criar objetos com `new`.
- **Construtores**: Inicializam o objeto.

1. **Instanciação**: É o processo de criar uma instância (objeto) a partir de uma classe usando a palavra-chave `new`. Durante a instanciação, a VM aloca memória para o objeto e chama seu construtor, ou seja, reserva espaço na memória para o obj

2. **Construtor**: Construtores são métodos especiais chamados durante a instanciação para configurar o objeto. O construtor é chamado automaticamente durante a instanciação. Ele prepara o objeto, configurando-o com valores ou comportamentos iniciais que foram definidos.

- Portanto, primeiro você instancia, depois o construtor é chamado, e então a inicialização completa o ciclo.

## 1. Construtores

Construtores são métodos especiais em C# usados para inicializar objetos de uma classe. Eles garantem que o objeto comece em um estado válido, definindo valores iniciais para suas propriedades ou executando lógicas necessárias durante a criação.

## 2. O que é um Construtor?

Um construtor é um método especial de uma classe, invocado automaticamente durante a criação de um objeto.

### **Definição**

- Tem o mesmo nome da classe.
- Não possui tipo de retorno (nem mesmo `void`).

### **Propósito**

Inicializar o objeto, garantindo valores consistentes para os atributos da classe.

### **Exemplo Básico**

```csharp
class Carro
{
    public Carro()
    {
        Console.WriteLine("Objeto Carro criado!");
    }
}
```

### **Características Principais**

1. **Presença Obrigatória**:

- Toda classe tem pelo menos um construtor (implícito ou explícito).

2. **Construtor Padrão implícito**:

- Gerado automaticamente pelo compilador se nenhum construtor for declarado.
- Características:
  - Não possui parâmetros.
  - Não executa inicializações específicas.
  - Pode ser substituído por uma declaração explícita.

3. **Sobrecarga e Encadeamento**:

- **Sobrecarga**: Permite múltiplas versões com parâmetros diferentes.

- **Encadeamento**: Um construtor pode invocar outro da mesma classe usando `this()`.

4. **Observações Adicionais**:

- Uma diferença importante entre construtores e métodos é que _constructors não podem especificar um tipo de retorno_ (nem mesmo `void`). Normalmente, construtores são declarados `public` para que possam ser usados pelo código cliente da classe para inicializar objetos da classe.
  - Construtores são tipicamente declarados como `public` para permitir a criação de objetos por código externo.
  - Diferença-chave em relação a métodos: a ausência de tipo de retorno.

## 4. Declaração do Construtor

As declarações de construtores são semelhantes às declarações de métodos, com uma diferença essencial: elas devem ter exatamente o mesmo nome da classe e não apresentam tipos de retorno.

### **Sintaxe e Estrutura**

Construtores são membros especiais de uma classe com as seguintes características:

- **Nome**: **Obrigatoriamente idêntico** ao nome da classe.

- **Retorno**: **Não possui** tipo de retorno (nem mesmo `void`).

- **Modificadores**: Pode incluir modificadores de acesso (`public`, `private`, `protected`, etc.).

### **Componentes do Construtor**

#### **Header (Cabeçalho _constructor header_)**

- Primeira linha da declaração, contendo:
  - Modificador de acesso (opcional, padrão é `internal` em C#).
  - Nome do construtor (igual ao da classe).
  - Parâmetros (se aplicável).

#### **Body (Corpo _constructor body_)**

- Delimitado por chaves `{}`.
- Contém as instruções executadas durante a criação do objeto.

### **Exemplo Prático**

```csharp
class Pessoa
{
    // Construtor padrão
    public Pessoa()
    {
        Console.WriteLine("Instância de Pessoa criada.");
    }
}
```

## 5. Modificadores de acesso em construtores

Os modificadores de acesso em construtores definem quais classes podem instanciar um objeto através daquele construtor. Ao utilizar esses modificadores, você controla com precisão onde e como as instâncias da classe podem ser criadas.

### Funcionamento:

- **public**: Qualquer classe pode invocar o construtor
- **protected**: Apenas a própria classe e suas subclasses podem usar o construtor
- **private**: Restrito apenas à própria classe
- _(padrão/package-private)_: Acessível somente por classes do mesmo pacote

Esta funcionalidade permite implementar padrões de projeto como:

- Singletons (com construtor private)
- Fábricas (com construtores protected)
- Controle de herança

## 6. Inicialização Segura

### Diferenças Fundamentais Inicialização de Variáveis de Instância e Variáveis Locais

- **Variáveis de instância**: São inicializadas automaticamente com valores padrão (0, `null`, `false`, etc.).

- **Variáveis locais**: _Não_ têm inicialização automática. **Devem ser inicializadas explicitamente** antes do uso para evitar erros de compilação.

### Boas Práticas em Construtores

Construtores podem chamar métodos durante a inicialização, mas exigem atenção:

1. **Risco de uso prematuro**: Variáveis de instância podem ainda não estar inicializadas quando o método é chamado.

2. **Consequências**: Utilizar variáveis de instância antes de sua completa inicialização pode levar a **erros lógicos** ou comportamentos inesperados.

_Um construtor pode chamar métodos de sua classe. Esteja ciente de que as variáveis de instância podem ainda não ter sido inicializadas, porque o construtor está no processo de inicialização do objeto. Usar variáveis de instância antes de serem inicializadas corretamente é um erro lógico._

#### Exemplo Seguro (C#):

```csharp
class Conta
{
    private double saldo;

    public Conta(double saldoInicial)
    {
        Depositar(saldoInicial);  // Uso seguro: saldoInicial é parâmetro, não depende do estado do objeto
    }

    public void Depositar(double valor)
    {
        saldo += valor > 0 ? valor : 0;  // Lógica direta e sem efeitos colaterais
    }
}
```

#### Recomendações Críticas:

✔ **Garanta a inicialização completa** antes de usar variáveis de instância em métodos chamados pelo construtor.

✔ Prefira inicializar variáveis diretamente no construtor quando a lógica é simples.

✔ Documente restrições de uso se métodos da classe assumirem estado inicializado.

## 7. Tipos de Construtores

### 7.1 Construtor Padrão (Construtor Sem Argumentos)

O construtor padrão é fundamental para o sistema de tipos do C#, garantindo que todos os objetos sejam inicializados de maneira previsível, mesmo quando não explicitamente configurados.

#### Definição

O **construtor padrão** é um construtor que não recebe nenhum parâmetro e é utilizado para criar instâncias de uma classe sem a necessidade de fornecer argumentos iniciais.

#### Características Principais

**1. Invocação Automática**

- É chamado automaticamente quando um objeto é instanciado sem parâmetros:
  ```csharp
  var pessoa = new Pessoa();  // Chama o construtor padrão
  ```

**2. Geração Automática pelo Compilador**

- Se nenhum construtor for explicitamente definido na classe, o compilador C# gera automaticamente um construtor padrão vazio.
- Exemplo de **construtor implícito**:
  ```csharp
  class Animal
  {
      public string Nome;  // Construtor padrão gerado automaticamente
  }
  ```

**3. Sobrescrita**

- Quando qualquer construtor é declarado explicitamente, o compilador **cessa** a geração automática do construtor padrão.
- Nesses casos, se desejar manter a capacidade de instanciação sem parâmetros, você deve declarar manualmente:
  ```csharp
  class Pessoa
  {
      public Pessoa()  // Construtor padrão explícito
      {
          Console.WriteLine("Construtor executado!");
      }
  }
  ```

#### Comportamento Especial

Em C#, o **construtor padrão** de uma classe executa automaticamente uma tarefa especial: **ele inicializa os membros da classe com seus valores padrão**.

Isso significa que, mesmo que você não declare um construtor explícito, o construtor padrão já está garantindo que os membros da classe sejam inicializados de maneira consistente.

**Inicialização de Valores Padrão**

O construtor padrão realiza automaticamente:

- **Tipos primitivos/números**: `0` (int), `0.0` (float), `false` (bool)

- **Tipos referência**: `null` (string, objetos)

- **Estruturas**: Valor padrão de cada campo

Exemplo ilustrativo:

```csharp
class DadosCliente
{
    public int Id;          // 0
    public bool Ativo;      // false
    public string Nome;     // null
    public DateTime Data;   // 01/01/0001 00:00:00
}

var cliente = new DadosCliente();
```

#### Considerações Importantes

**1. Herança**

- Em hierarquias de classes, o construtor padrão implicitamente chama o construtor sem parâmetros da classe pai.

  - Se a classe herdar de outra, o construtor padrão implicitamente chama o construtor sem parâmetros da superclasse.

- Se a superclasse não tiver um construtor sem argumentos, ocorrerá erro de compilação:

  ```csharp
  class Base { public Base(int x) {} }
  class Derivada : Base {}  // Erro! Não existe Base()
  ```

**2. Alternativas com Parâmetros Opcionais**

- Um construtor com todos os parâmetros opcionais (ex: `public Produto(string nome = null)`) pode ser usado como alternativa ao construtor padrão, mas não é considerado tecnicamente um construtor padrão pelo compilador.

- Embora não seja tecnicamente um construtor padrão, pode simular o comportamento:

  ```csharp
  class Produto
  {
      public Produto(string nome = null, decimal preço = 0) {}
  }
  // Uso equivalente:
  new Produto();  // Válido
  ```

#### Boas Práticas Recomendadas

1. **Explicitação**: **Declare sempre explicitamente** pelo menos um construtor (mesmo que vazio) para evitar comportamentos inesperados.

   ```csharp
   class ContaBancaria
   {
       public ContaBancaria() {}  // Melhor que depender do implícito
   }
   ```

2. **Inicialização Robusta**: **Inicialize campos críticos** no construtor para garantir consistência do objeto. _Definir valores iniciais para os atributos de um objeto logo após sua criação é essencial para garantir a consistência e integridade dos dados._

   ```csharp
   class Usuario
   {
       public string Nome;
       public List<string> Permissoes;

       public Usuario()
       {
           Nome = "Convidado";
           Permissoes = new List<string>();  // Evita null
       }
   }
   ```

3. **Documentação Clara**: **Documente** construtores não óbvios com XML comments.

   ```csharp
   /// <summary>
   /// Cria uma nova transação com valores padrão
   /// </summary>
   public Transacao()
   {
       // ...
   }
   ```

4. **Consistência Inicial**
   - Sempre inicialize coleções e campos críticos no construtor para evitar `NullReferenceException`.

### 7.2 Construtor Parametrizado

**Definição**:  
Um construtor parametrizado é um método especial que permite inicializar objetos com valores específicos no momento de sua criação, garantindo que o objeto comece em um estado válido e consistente.

**Características principais**:

- Substitui o construtor padrão (sem parâmetros) gerado automaticamente pelo compilador, ou seja, ao declarar qualquer construtor, o compilador não gera mais o construtor padrão automaticamente

- Exige a passagem de argumentos obrigatórios durante a instanciação

- Permite maior controle sobre o estado inicial do objeto

- Pode incluir lógica de validação dos parâmetros recebidos

- Ideal para classes com dependências obrigatórias ou configurações iniciais complexas

- _A menos que a inicialização padrão das variáveis de instância da sua classe seja aceitável, forneça um construtor personalizado para garantir que suas variáveis de instância sejam inicializadas corretamente com valores significativos quando cada novo objeto da sua classe for criado._

**Exemplo de implementação**:

```csharp
public class Pessoa
{
    // Propriedade readonly - só pode ser definida no construtor
    public string Nome { get; }
    public int Idade { get; private set; }

    // Construtor parametrizado com validação básica
    public Pessoa(string nome, int idade)
    {
        if (string.IsNullOrWhiteSpace(nome))
            throw new ArgumentException("Nome não pode ser vazio", nameof(nome));

        if (idade <= 0)
            throw new ArgumentException("Idade deve ser positiva", nameof(idade));

        Nome = nome;
        Idade = idade;
    }
}

// Exemplo de uso:
var pessoa = new Pessoa("Ana", 30);
Console.WriteLine($"Nome: {pessoa.Nome}, Idade: {pessoa.Idade}");
```

**Vantagens**:

1. **Segurança**: Garante que o objeto seja criado apenas com valores válidos

2. **Imutabilidade**: Permite criar objetos com propriedades readonly (como no exemplo acima)

3. **Clareza**: Torna explícitos os requisitos para criação de um objeto

4. **Manutenibilidade**: Centraliza a lógica de inicialização em um único ponto

**Boas práticas**:

- Utilize propriedades em vez de campos públicos quando possível
- Considere fazer validações dos parâmetros no construtor
- Documente os requisitos e possíveis exceções usando XML comments
- Para classes complexas, considere usar o padrão Builder

**Observação importante**:  
Quando uma classe define qualquer construtor (parametrizado ou não), o compilador C# não gera mais o construtor padrão automaticamente. Se você ainda precisar dele, deve declará-lo explicitamente.

**Casos de uso típicos**:

- Quando a classe possui dependências obrigatórias
- Para objetos que devem ser inicializados em estado válido
- Quando a inicialização requer configurações complexas
- Para implementar objetos imutáveis

### 7.3 Construtor Estático

#### **Definição**

Um construtor estático é um membro especial de uma classe que inicializa membros estáticos e é executado **apenas uma vez**, antes de qualquer acesso à classe (seja para instanciá-la, acessar membros estáticos ou herdar dela).

#### **Características Principais**

- **Invocação automática**: Chamado pelo runtime .NET antes do primeiro uso da classe
- **Única execução**: Garante que a inicialização ocorra apenas uma vez
- **Sem parâmetros**: Não pode ter modificadores de acesso ou parâmetros
- **Ordem de execução**: Rodado antes de qualquer acesso a membros estáticos

#### **Exemplo Prático**

```csharp
class ConfiguracaoSistema
{
    public static string Versao { get; }
    public static DateTime DataCompilacao { get; }

    // Construtor estático
    static ConfiguracaoSistema()
    {
        Versao = "2.3.1";
        DataCompilacao = DateTime.Now;
        Console.WriteLine("Configurações inicializadas");
    }
}

class Program
{
    static void Main()
    {
        Console.WriteLine("Aplicação iniciada");

        // Primeiro acesso - dispara o construtor estático
        Console.WriteLine($"Versão: {ConfiguracaoSistema.Versao}");
        Console.WriteLine($"Compilado em: {ConfiguracaoSistema.DataCompilacao}");

        // Acessos subsequentes não disparam novamente
        Console.WriteLine($"Versão (novo acesso): {ConfiguracaoSistema.Versao}");
    }
}
```

**Saída esperada**:

```
Aplicação iniciada
Configurações inicializadas
Versão: 2.3.1
Compilado em: 01/04/2025 10:00:00
Versão (novo acesso): 2.3.1
```

#### **Casos de Uso Comuns**

🔹 Inicializar valores padrão para configurações  
🔹 Carregar recursos estáticos (ex: dicionários)  
🔹 Registrar factories ou serviços em padrões de design  
🔹 Validar ambientes antes do uso da classe

#### **Boas Práticas**

- **Evite** lógica complexa que possa lançar exceções
- **Não dependa** da ordem de inicialização entre classes
- Prefira propriedades estáticas somente-leitura quando possível

**Exemplo Avançado**:

```csharp
class BancoDeDados
{
    private static readonly Dictionary<int, string> Cache;

    static BancoDeDados()
    {
        Cache = CarregarCacheDoBanco();
    }

    private static Dictionary<int, string> CarregarCacheDoBanco()
    {
        // Simulação de carga pesada
        Thread.Sleep(2000);
        return new Dictionary<int, string>
        {
            {1, "Cliente A"},
            {2, "Cliente B"}
        };
    }

    public static string GetCliente(int id) => Cache.TryGetValue(id, out var nome) ? nome : "Não encontrado";
}
```

## 8. Encadeamento de Construtores (Constructor Chaining)

### Conceito e Objetivo

Técnica que permite um construtor chamar outro construtor da mesma classe usando `this()`, promovendo:

- Reutilização de código
- Redução de duplicação
- Consistência na inicialização de objetos

- Utiliza-se a palavra-chave `this` seguida de parênteses com os parâmetros correspondentes.

### Exemplo Básico

```csharp
class Retangulo
{
    public int Largura { get; }
    public int Altura { get; }

    // Construtor padrão encadeia ao principal
    public Retangulo() : this(1, 1) { }

    // Construtor principal
    public Retangulo(int largura, int altura)
    {
        Largura = largura;
        Altura = altura;
    }
}
```

### Implementação Detalhada

**Sintaxe:**

```csharp
public class ContaBancaria
{
    public string NumeroConta { get; }
    public decimal Saldo { get; private set; }
    public decimal LimiteCredito { get; }

    // Construtor base
    public ContaBancaria(string numeroConta)
    {
        NumeroConta = numeroConta ?? throw new ArgumentNullException(nameof(numeroConta));
    }

    // Construtor secundário
    public ContaBancaria(string numeroConta, decimal limiteCredito)
        : this(numeroConta) // Encadeamento
    {
        LimiteCredito = limiteCredito;
    }

    // Construtor completo
    public ContaBancaria(string numeroConta, decimal saldoInicial, decimal limiteCredito)
        : this(numeroConta, limiteCredito)
    {
        Saldo = saldoInicial;
    }
}
```

### Benefícios

1. **Evita duplicação de código**: A inicialização comum fica centralizada

2. **Manutenção simplificada**: Alterações precisam ser feitas em apenas um lugar

3. **Consistência**: Garante que todos os construtores inicializem os campos obrigatórios

### Boas Práticas e Observações

1. **Ordem de Execução**: O construtor referenciado por `this()` sempre executa primeiro

2. **Validações**: Centralize validações no construtor principal

3. **Imutabilidade**: Combine com propriedades readonly para objetos imutáveis

4. **Hierarquia**: Construtores mais específicos devem chamar os mais genéricos

```csharp
// Exemplo com validação
public class Produto
{
    public int Id { get; }
    public string Nome { get; }

    public Produto(int id) : this(id, "Sem nome") { }

    public Produto(int id, string nome)
    {
        if(id <= 0) throw new ArgumentException("ID inválido");
        if(string.IsNullOrWhiteSpace(nome)) throw new ArgumentNullException(nameof(nome));

        Id = id;
        Nome = nome.Trim();
    }
}
```

### Casos de Uso Típicos

- Quando múltiplos construtores compartilham lógica comum
- Em classes que exigem diferentes combinações de parâmetros
- Para implementar valores padrão em construtores simplificados
- O encadeamento de construtores é particularmente útil em classes com múltiplas sobrecargas de construtores. Ele segue o princípio DRY (Don't Repeat Yourself) e facilita a evolução do código, pois mudanças na inicialização básica do objeto requerem modificação em apenas um ponto.

**Padrão Recomendado**:  
Sempre que possível, exponha apenas o construtor mais completo publicamente e utilize métodos factory para outras variações.

## 9. Sobrecarga de Construtores

A sobrecarga de construtores é uma técnica que permite definir múltiplos construtores em uma classe, cada um com diferentes parâmetros, proporcionando flexibilidade na criação de objetos.

Assim como os métodos, os construtores podem ser sobrecarregados, permitindo a definição de múltiplos construtores com o mesmo nome em uma classe, mas com assinaturas diferentes (número e/ou tipo de parâmetros).

O compilador C# é capaz de distinguir entre esses construtores com base nas assinaturas, escolhendo o construtor apropriado a ser chamado durante a instanciação do objeto.

O que não é permitido é escrever dois construtores com assinaturas iguais (número e/ou tipo de parâmetros).

### Benefícios

- **Flexibilidade**: Permite inicializar objetos com diferentes conjuntos de dados
- **Reutilização**: Construtores podem chamar outros construtores da mesma classe
- **Segurança**: Garante que objetos sejam criados sempre em estados válidos

### Exemplos Básicos

```csharp
public class Pessoa
{
    public string nome;
    public string rg;
    public string cpf;

    // Construtor 1: Inicializa nome e RG
    public Pessoa(string nome, string rg)
    {
        this.nome = nome;
        this.rg = rg;
    }

    // Construtor 2: Inicializa nome e CPF
    public Pessoa(string nome, string cpf)
    {
        this.nome = nome;
        this.cpf = cpf;
    }

    // Construtor 3: Inicializa nome, RG e CPF
    public Pessoa(string nome, string rg, string cpf)
    {
        this.nome = nome;
        this.rg = rg;
        this.cpf = cpf;
    }

    // Construtor 4: Inicializa apenas o nome
    public Pessoa(string nome)
    {
        this.nome = nome;
    }
}
```

**Utilizando os Construtores Sobrecarregados**

```csharp
// Instanciando objetos com diferentes construtores
Pessoa pessoa1 = new Pessoa("João", "1234567");
Pessoa pessoa2 = new Pessoa("Maria", "987654321");
Pessoa pessoa3 = new Pessoa("Carlos", "5555555", "111111111");
Pessoa pessoa4 = new Pessoa("Ana");
```

```csharp
class Livro
{
    public string Titulo { get; }
    public string Autor { get; }

    // Construtor com apenas título
    public Livro(string titulo)
    {
        Titulo = titulo;
        Autor = "Desconhecido";
    }

    // Construtor com título e autor
    public Livro(string titulo, string autor) : this(titulo)
    {
        Autor = autor;
    }
}
```

### Boas Práticas

1. **Encadeamento de construtores**: Use `: this()` para evitar duplicação de código. É possível chamar um construtor dentro de outro construtor usando a palavra chave `this`.
2. **Valores padrão**: Considere propriedades com valores padrão como alternativa
3. **Validação**: Adicione validação nos parâmetros

### Exemplo Avançado com Validação

```csharp
class ContaBancaria
{
    public string Numero { get; }
    public decimal Saldo { get; private set; }
    public string Titular { get; }

    // Construtor básico
    public ContaBancaria(string numero, string titular)
    {
        if (string.IsNullOrWhiteSpace(numero))
            throw new ArgumentException("Número da conta inválido");

        Numero = numero;
        Titular = titular ?? "Cliente não identificado";
    }

    // Construtor com saldo inicial
    public ContaBancaria(string numero, string titular, decimal saldoInicial)
        : this(numero, titular)
    {
        if (saldoInicial < 0)
            throw new ArgumentException("Saldo não pode ser negativo");

        Saldo = saldoInicial;
    }
}
```

### Quando Usar

1. Quando diferentes combinações de propriedades são obrigatórias
2. Para fornecer maneiras alternativas de inicialização
3. Para manter compatibilidade com versões anteriores

### Alternativas Modernas

Em versões mais recentes do C#, você pode considerar:

```csharp
// Usando parâmetros opcionais
public Livro(string titulo, string autor = "Desconhecido")
{
    Titulo = titulo;
    Autor = autor;
}

// Usando inicializadores de objeto
var livro = new Livro("Dom Casmurro")
{
    Autor = "Machado de Assis"
};
```

## 10. Boas Práticas com Construtores em C#

### Princípios Fundamentais

- **Inicialização Completa**: Todo objeto deve estar em um estado válido após a construção.
- **Simplicidade**: Construtores devem ser focados em inicialização, não em lógica complexa.
- **Flexibilidade**: Ofereça opções de construção claras sem sobrecarregar o usuário.

### Boas Práticas Detalhadas

1. **Inicialização de Campos Críticos**

   - Campos obrigatórios devem ser parâmetros do construtor
   - Use inicializadores de campo quando valores padrão fazem sentido

   ```csharp
   public class Cliente {
       private readonly string _cpf;  // Campo crítico

       public Cliente(string cpf, string nome) {
           _cpf = cpf ?? throw new ArgumentNullException(nameof(cpf));
           Nome = nome;
       }
   }
   ```

2. **Encapsulamento com Propriedades**

   - Prefira propriedades auto-implementadas para campos públicos
   - Use `init` para propriedades imutáveis pós-construção

   ```csharp
   public class Produto {
       public string Codigo { get; }
       public decimal Preco { get; private set; }

       public Produto(string codigo) {
           Codigo = codigo;
       }
   }
   ```

3. **Documentação Clara**

   - Documente exceções lançadas, pré-condições e semântica dos parâmetros
   - Use XML comments para construtores não óbvios

   ```csharp
   /// <summary>
   /// Cria uma nova conta bancária
   /// </summary>
   /// <param name="saldoInicial">Deve ser ≥ 0</param>
   /// <exception cref="ArgumentOutOfRangeException">Saldo negativo</exception>
   public ContaBancaria(decimal saldoInicial) { ... }
   ```

4. **Gerenciamento de Complexidade**

   - Para objetos complexos, considere o padrão Builder ou Factory Method
   - Separe a construção da inicialização tardia quando necessário

   ```csharp
   public class RelatorioComplexo {
       private RelatorioComplexo() { }  // Construtor privado

       public static async Task<RelatorioComplexo> CriarAsync(FonteDados dados) {
           var relatorio = new RelatorioComplexo();
           await relatorio.CarregarDadosAsync(dados);
           return relatorio;
       }
   }
   ```

5. **Hierarquia de Classes**

   - Construtores de classes base devem ser simples para herança segura
   - Use o modificador `protected` para construtores destinados a herança

   ```csharp
   public abstract class Forma {
       protected Forma(string nome) {
           Nome = nome;
       }
       public string Nome { get; }
   }

   public class Circulo : Forma {
       public Circulo(double raio) : base("Círculo") {
           Raio = raio;
       }
   }
   ```

### Padrões Avançados

- **Injeção de Dependência**: Construtores são o local ideal para receber dependências
- **Objetos Imutáveis**: Use `readonly` e `init` para thread-safety
- **Validação Defensiva**: Valide parâmetros no construtor e lance exceções precoces

### Anti-Padrões a Evitar

- Sobrecarregar com muitas variações de construtores
- Realizar I/O, acesso a rede ou processamento pesado
- Lançar exceções não relacionadas à inicialização
- Deixar o objeto em estado inválido após construção

### Exemplo Completo

```csharp
public class Pedido {
    public int Id { get; }
    public Cliente Cliente { get; }
    public DateTime DataCriacao { get; }
    private readonly List<ItemPedido> _itens = new();

    // Construtor principal
    public Pedido(int id, Cliente cliente) {
        Id = id > 0 ? id : throw new ArgumentException("ID inválido", nameof(id));
        Cliente = cliente ?? throw new ArgumentNullException(nameof(cliente));
        DataCriacao = DateTime.UtcNow;
    }

    // Construtor secundário com valores padrão
    public Pedido(Cliente cliente) : this(GeradorId.Proximo(), cliente) { }

    // Método para adição tardia (não no construtor)
    public void AdicionarItem(Produto produto, int quantidade) {
        _itens.Add(new ItemPedido(produto, quantidade));
    }
}
```
