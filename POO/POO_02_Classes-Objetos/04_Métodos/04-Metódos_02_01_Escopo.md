# Métodos: Escopo

Métodos em C# podem ser classificados pelo seu escopo - se pertencem à classe como um todo ou a instâncias específicas.

Lembre-se: métodos de instância trabalham com objetos específicos, enquanto métodos estáticos trabalham com a classe como um todo.

---

## **Diferença entre Métodos Estáticos e de Instância**

Os métodos em C# podem ser classificados em **estáticos** e **de instância**. A escolha entre eles depende do **contexto de uso** e da necessidade de manipular estados de objetos.

- Métodos de instância manipulam os **dados do objeto**.
- Métodos estáticos fornecem **funções auxiliares** independentes de instâncias.
- A escolha entre **instância** ou **estático** depende do **propósito do método**.

### **Comparação Direta**

| Característica | Métodos Estáticos | Métodos de Instância |
| --- | --- | --- |
| **Pertencem a...** | Classe | Instância (objeto) |
| **Chamados por...** | Nome da classe | Objeto criado (`new`) |
| **Acessam atributos...** | Apenas membros estáticos | Tanto estáticos quanto de instância |
| **Uso típico** | Funções utilitárias, cálculos | Manipulação do estado do objeto |

## **Métodos de Instância**

Os **métodos de instância** operam sobre um objeto específico e precisam de uma **instância** da classe para serem chamados.

### **Características:**

- **Exigem um objeto** (`new`) para serem chamados.
- **Podem acessar atributos não estáticos**, ou seja, modificam e usam dados pertencentes ao objeto.
- **Representam comportamentos específicos** de uma instância da classe.

### **Exemplo Simples**

```csharp
public class Pessoa
{
    public string Nome { get; set; }

    public void Apresentar() // Método de instância
    {
        Console.WriteLine($"Olá, meu nome é {Nome}!");
    }
}

// Uso:
Pessoa pessoa1 = new Pessoa();
pessoa1.Nome = "Ana";
pessoa1.Apresentar();  // Saída: "Olá, meu nome é Ana!"
```

**Explicação:**

- O método `Apresentar()` acessa o atributo `Nome` do objeto.
- Ele precisa de uma **instância** (`pessoa1`) para ser chamado.

## **Métodos Estáticos**

Os **métodos estáticos** pertencem à classe e **não precisam de uma instância** para serem chamados.

### **Características:**

- **Chamados diretamente pelo nome da classe.**
- **Podem acessar apenas membros estáticos** da classe.
- **Úteis para operações independentes de estado**, como cálculos matemáticos ou funções auxiliares.

### **Exemplo Simples**

```csharp
public class Calculadora
{
    public static int Somar(int a, int b)
    {
        return a + b;
    }
}

// Uso:
int resultado = Calculadora.Somar(3, 4);
Console.WriteLine(resultado);  // Saída: 7
```

**Explicação:**

- O método `Somar()` pertence à classe `Calculadora` e pode ser chamado sem criar um objeto.

## **Diferenças Fundamentais**

### **Comparação entre Métodos Estáticos e de Instância**

| Método | Como é chamado? | Pode acessar atributos não estáticos? | Relacionado a um objeto? |
| --- | --- | --- | --- |
| **Estático (`static`)** | Pelo nome da classe | ❌ Não | ❌ Não |
| **De Instância** | Pelo nome do objeto | ✅ Sim | ✅ Sim |

### **Regras Importantes**

1. **Métodos estáticos NÃO podem acessar diretamente atributos ou métodos de instância.**
2. **Métodos de instância podem chamar métodos estáticos** sem problemas.

#### **Erro comum**

```csharp
public class Exemplo
{
    public int valor = 10;

    public static void Mostrar()
    {
        Console.WriteLine(valor);  // ERRO! Método estático tentando acessar atributo de instância
    }
}
```

#### **Forma correta**

```csharp
public class Exemplo
{
    public int valor = 10;

    public static void Mostrar(Exemplo obj)
    {
        Console.WriteLine(obj.valor);  // Correto! Recebe um objeto como parâmetro
    }
}

// Uso:
Exemplo exemplo1 = new Exemplo();
Exemplo.Mostrar(exemplo1); // Saída: 10
```

## **Quando Usar Cada Tipo de Método?**

### **Use métodos de instância quando:**

- O comportamento depende dos dados do objeto.
- Você precisa acessar ou modificar o estado do objeto.
- Cada objeto pode ter valores e comportamentos diferentes.

### **Use métodos estáticos quando:**

- A operação é independente de estado (ex: cálculos matemáticos).
- Precisa de funções auxiliares que não dependem de objetos.
- Quer agrupar métodos relacionados logicamente.

## **Exemplo Prático Combinado**

Aqui está um exemplo mostrando métodos **estáticos** e **de instância** trabalhando juntos:

```csharp
public class Loja
{
    public static int TotalVendas = 0;

    public void RegistrarVenda(int valor)
    {
        TotalVendas += valor;
        Console.WriteLine($"Venda de {valor} registrada.");
    }

    public static void ExibirTotalVendas()
    {
        Console.WriteLine($"Total de vendas: {TotalVendas}");
    }
}

// Uso:
Loja.ExibirTotalVendas();  // Total de vendas: 0

Loja loja1 = new Loja();
Loja loja2 = new Loja();

loja1.RegistrarVenda(100);
loja2.RegistrarVenda(200);

Loja.ExibirTotalVendas();  // Total de vendas: 300
```

---

# **1. Métodos de Instância em C#**

Os métodos de instância são funções definidas dentro de uma classe que operam sobre um **objeto específico** dessa classe. Esses métodos só podem ser utilizados após a criação de uma instância (um objeto) e possuem acesso direto aos **atributos e estados** do objeto.

Os métodos de instância permitem que cada objeto tenha seu próprio comportamento e estado, tornando o código mais modular e reutilizável. Eles são fundamentais para manipular dados específicos de um objeto e organizar funcionalidades dentro de uma classe.

## **Por que usar métodos de instância?**

1. **Encapsulam comportamento**: Eles ajudam a organizar funcionalidades que pertencem a um objeto específico.
2. **Facilitam a reutilização de código**: Cada instância pode chamar métodos sem repetir código.
3. **Permitem modificar o estado do objeto**: Os métodos podem alterar atributos internos da instância.

## **Características dos métodos de instância**

- **Exigem uma instância da classe** (`new`) para serem chamados.
- **Acessam atributos e métodos não estáticos do objeto**.
- **Podem modificar o estado do objeto** ao longo da execução.
- **Representam comportamentos específicos** de um objeto.

## **Exemplo Simples de Métodos de Instância em C#**

Vamos ver um exemplo básico:

```csharp
public class Pessoa
{
    public string Nome { get; set; }

    // Método de instância
    public void Apresentar()
    {
        Console.WriteLine($"Olá, meu nome é {Nome}.");
    }
}

// Uso:
Pessoa pessoa1 = new Pessoa();
pessoa1.Nome = "Ana";
pessoa1.Apresentar();  // Saída: "Olá, meu nome é Ana."
```

Neste código:

- Criamos uma classe `Pessoa` com um atributo `Nome`.
- Definimos um método de instância `Apresentar`, que imprime o nome da pessoa.
- Criamos uma instância (`pessoa1`), atribuímos um valor a `Nome` e chamamos o método.

## **Chamadas de Métodos de Instância**

### **1. Chamada direta dentro da mesma classe**

Se um método está na mesma classe onde será chamado, ele pode ser invocado diretamente.

```csharp
public class Exemplo
{
    public void MostrarMensagem()
    {
        Console.WriteLine("Método chamado dentro da mesma classe.");
    }

    public void Executar()
    {
        MostrarMensagem();  // Chamada direta
    }
}
```

### **2. Chamada através de um objeto**

Quando um método **não é estático**, é necessário criar um objeto para chamá-lo:

```csharp
public class Carro
{
    public void Ligar()
    {
        Console.WriteLine("O carro está ligado!");
    }
}

// Uso:
Carro meuCarro = new Carro();
meuCarro.Ligar();  // Saída: "O carro está ligado!"
```

---

# **2. Métodos Estáticos (`static`)**

Os **métodos estáticos** pertencem à classe como um todo e não a uma instância específica. Isso significa que podem ser chamados sem que um objeto seja criado. São úteis para operações que não dependem de valores individuais de objetos.

### **Características dos Métodos Estáticos**

- **Pertencem à classe**, não a um objeto específico.
- **Chamados diretamente pelo nome da classe**, sem precisar criar instâncias.
- **Podem acessar apenas membros estáticos** da mesma classe diretamente.
- **Úteis para operações genéricas**, como cálculos matemáticos e manipulação de dados globais.

## **Definição e Uso de Métodos Estáticos**

Em algumas situações, um método realiza uma tarefa que **não depende dos dados de um objeto específico**, apenas dos argumentos passados. Quando isso ocorre, o método é considerado **estático**, pois se aplica à classe como um todo e não a instâncias individuais.

A palavra-chave `static` é usada na definição de um método para indicar que ele não precisa de um objeto para ser chamado.

### **Exemplo Simples**

```csharp
public class Calculadora
{
    // Método estático
    public static int Somar(int a, int b)
    {
        return a + b;
    }
}

// Uso:
int resultado = Calculadora.Somar(3, 4);
Console.WriteLine(resultado);  // Saída: 7
```

**Explicação:**

- O método `Somar` pertence à classe `Calculadora`, e não a uma instância específica.
- Podemos chamá-lo diretamente com `Calculadora.Somar(3, 4)`, sem criar um objeto.

## **Acesso a Membros Estáticos**

Os métodos `estáticos` podem chamar **somente** outros membros estáticos diretamente. Para acessar membros não estáticos, é necessário criar uma instância.

```csharp
public class Exemplo
{
    public int valor = 10;

    public static void Mostrar()
    {
        // Console.WriteLine(valor);  // ERRO! Métodos estáticos não podem acessar membros não estáticos
        Console.WriteLine("Método estático chamado.");
    }
}
```

**Regra Importante:** Um método `estático` **não pode** acessar atributos ou métodos de instância diretamente, pois ele não pertence a um objeto específico.

## **Por que `Main` é Estático?**

O método `Main` é declarado como `static` porque ele **precisa ser executado sem a criação de um objeto**. Como é o ponto de entrada do programa, ele deve ser acessível diretamente pelo sistema operacional ou pelo ambiente de execução.

## **Uso de Variáveis Estáticas**

Enquanto variáveis de instância pertencem a **cada objeto individualmente**, **variáveis estáticas** pertencem à classe como um todo.

### **Exemplo: Contador de Objetos**

```csharp
public class Usuario
{
    public static int TotalUsuarios = 0;  // Variável estática compartilhada por todas as instâncias

    public Usuario()
    {
        TotalUsuarios++;  // Incrementa o contador a cada novo usuário criado
    }
}

// Uso:
Usuario u1 = new Usuario();
Usuario u2 = new Usuario();
Console.WriteLine(Usuario.TotalUsuarios); // Saída: 2
```

**Vantagens de Variáveis Estáticas:**

- **Economia de memória**, pois evitamos cópias redundantes.
- **Consistência dos dados**, todos os objetos acessam a mesma variável.
- **Facilidade de controle**, pois qualquer objeto pode atualizar o valor sem precisar sincronizar diversas cópias.

---
