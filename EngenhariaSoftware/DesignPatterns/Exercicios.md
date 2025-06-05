# Questão 01

Em um sistema de gerenciamento de pedidos online, você precisa implementar um padrão de design que permita a adição de novos métodos de pagamento de forma flexível, sem modificar o código existente. Qual padrão de design você escolheria?

1. Padrão Singleton.

2. Padrão Adapter.

3. Padrão Observer.

4. Padrão Decorator.

5. Padrão Strategy. (**Correto**)

---

## Detalhes da Resposta Correta?

### Padrão Strategy

**O que é:** O Padrão Strategy (Estratégia) define uma família de algoritmos, encapsula cada um deles e os torna intercambiáveis. Ele permite que o algoritmo varie independentemente dos clientes que o utilizam.

**Como se aplica ao problema:** No contexto de métodos de pagamento, você teria:

- **Uma interface ou classe abstrata `PaymentStrategy` (ou `MetodoPagamento`):** Esta interface definiria um método comum para processar um pagamento, por exemplo, `processarPagamento(valor)`.

- **Concretas Strategies (Estratégias Concretas):** Cada método de pagamento (e.g., `CartaoDeCreditoStrategy`, `BoletoBancarioStrategy`, `PayPalStrategy`, `PixStrategy`) seria uma implementação concreta da interface `PaymentStrategy`. Cada uma implementaria o método `processarPagamento` de forma específica para aquele método.

- **Um Contexto (`OrderProcessor` ou `GerenciadorDePedidos`):** Esta classe conteria uma referência para um objeto `PaymentStrategy`. O contexto não sabe qual estratégia específica está usando, apenas que ela implementa a interface `PaymentStrategy`.

- **Flexibilidade:** Quando um novo método de pagamento surge (e.g., uma nova carteira digital), basta criar uma nova classe que implementa a interface `PaymentStrategy`. Você não precisa modificar o código do `OrderProcessor` ou de qualquer outro código existente que utilize o sistema de pagamento.

**Exemplo prático:**

```c#
// Interface da estratégia
interface PaymentStrategy {
    void processPayment(double amount);
}

// Estratégias concretas
class CreditCardPayment implements PaymentStrategy {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processando pagamento de R$" + amount + " via Cartão de Crédito.");
        // Lógica específica para cartão de crédito
    }
}

class BoletoPayment implements PaymentStrategy {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processando pagamento de R$" + amount + " via Boleto Bancário.");
        // Lógica específica para boleto
    }
}

class PixPayment implements PaymentStrategy {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processando pagamento de R$" + amount + " via Pix.");
        // Lógica específica para Pix
    }
}

// Contexto
class OrderProcessor {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void checkout(double amount) {
        if (paymentStrategy == null) {
            System.out.println("Nenhum método de pagamento selecionado.");
            return;
        }
        paymentStrategy.processPayment(amount);
    }
}

// Uso
public class Main {
    public static void main(String[] args) {
        OrderProcessor processor = new OrderProcessor();

        // Usando Cartão de Crédito
        processor.setPaymentStrategy(new CreditCardPayment());
        processor.checkout(100.00);

        // Usando Boleto
        processor.setPaymentStrategy(new BoletoPayment());
        processor.checkout(250.00);

        // Adicionando um novo método de pagamento (Pix) sem alterar o OrderProcessor
        processor.setPaymentStrategy(new PixPayment());
        processor.checkout(50.00);
    }
}
```

### Por que os outros padrões não seriam a melhor escolha:

1.  **Padrão Singleton:**

    - **O que é:** Garante que uma classe tenha apenas uma instância e fornece um ponto de acesso global a ela.
    - **Por que não se aplica:** Embora você possa ter uma única instância de um _gerenciador_ de pagamentos, o Singleton não aborda a flexibilidade de adicionar _novos tipos_ de métodos de pagamento. Ele lida com a restrição de instâncias, não com a variação de algoritmos.

2.  **Padrão Adapter:**

    - **O que é:** Converte a interface de uma classe para outra interface que o cliente espera. O Adapter permite que classes trabalhem juntas que de outra forma não poderiam devido a interfaces incompatíveis.
    - **Por que não se aplica:** O Adapter seria útil se você tivesse um sistema de pagamento legado com uma interface diferente e precisasse integrá-lo ao seu novo sistema. Ele adapta interfaces existentes, mas não é a solução principal para _adicionar novas_ funcionalidades de forma flexível desde o início, sem ter uma interface incompatível para adaptar.

3.  **Padrão Observer:**

    - **O que é:** Define uma dependência um-para-muitos entre objetos, de modo que quando um objeto muda de estado, todos os seus dependentes são notificados e atualizados automaticamente.
    - **Por que não se aplica:** O Observer é para notificação de eventos (e.g., "o pedido foi pago", "o status do pedido mudou"). Ele não se encaixa no problema de como o pagamento em si é _processado_ ou como _novos métodos_ de pagamento são introduzidos.

4.  **Padrão Decorator:**

    - **O que é:** Anexa responsabilidades adicionais a um objeto dinamicamente. Os Decorators fornecem uma alternativa flexível à subclasse para estender a funcionalidade.
    - **Por que não se aplica:** O Decorator seria mais útil se você quisesse adicionar funcionalidades extras a um método de pagamento existente (e.g., um método de pagamento com desconto, ou um método de pagamento que aplica uma taxa de serviço). Ele estende a funcionalidade de um objeto existente, mas não é a forma primária de introduzir _novos tipos_ de métodos de pagamento com suas próprias lógicas distintas.

---

# Questão 02

Em um sistema de gerenciamento de conteúdo, você deseja implementar um mecanismo que permita a criação de diferentes tipos de conteúdo de forma extensível. Qual padrão de design seria mais apropriado para essa situação:

1. Padrão Factory Method. (**Correto**)

2. Padrão Builder.

3. Padrão Prototype.

4. Padrão Abstract Factory.

5. Padrão Composite.

---

## Detalhes da Resposta Correta

Para a situação descrita, onde você deseja implementar um mecanismo que permita a criação de diferentes tipos de conteúdo de forma extensível em um sistema de gerenciamento de conteúdo, o padrão de design mais apropriado seria o **1. Padrão Factory Method**.

### 1. Padrão Factory Method (Método de Fábrica)

**O que é:** O Padrão Factory Method define uma interface para criar um objeto, mas permite que as subclasses decidam qual classe instanciar. Ele delega a responsabilidade de instanciação para as subclasses.

**Como se aplica ao problema:** No contexto de um sistema de gerenciamento de conteúdo, onde você precisa criar diferentes tipos de conteúdo (por exemplo, `Artigo`, `Noticia`, `Video`, `Imagem`), o Factory Method é perfeito:

- **Produto (Interface/Classe Abstrata):** Você teria uma interface ou classe abstrata `Conteudo` que define as operações comuns a todos os tipos de conteúdo (e.g., `exibir()`, `publicar()`).
- **Produtos Concretos:** Cada tipo de conteúdo específico (e.g., `ArtigoConcreto`, `NoticiaConcreta`, `VideoConcreto`) implementaria essa interface `Conteudo`.
- **Criador (Interface/Classe Abstrata):** Você teria uma interface ou classe abstrata `CriadorConteudo` (ou `ContentCreator`) que declara o método `criarConteudo()`. Este método retorna um objeto do tipo `Conteudo`. O criador pode ter outros métodos para manipulação do conteúdo.
- **Criadores Concretos:** Cada tipo específico de criador (e.g., `CriadorArtigo`, `CriadorNoticia`, `CriadorVideo`) implementaria o método `criarConteudo()` para instanciar o tipo de conteúdo correspondente.

**Benefícios:**

- **Extensibilidade:** Quando você precisa adicionar um novo tipo de conteúdo (e.g., `Podcast`), basta criar uma nova classe `PodcastConcreto` que implementa `Conteudo` e um novo `CriadorPodcast` que implementa `CriadorConteudo`. O código que utiliza os criadores não precisa ser alterado.
- **Acoplamento Fraco:** O código cliente que solicita a criação de conteúdo não precisa saber as classes concretas dos conteúdos. Ele interage apenas com a interface `Conteudo` e a interface `CriadorConteudo`, promovendo um baixo acoplamento.
- **Princípio Open/Closed:** O sistema está aberto para extensão (novos tipos de conteúdo podem ser adicionados) e fechado para modificação (o código existente que usa os criadores não precisa ser alterado).

**Exemplo prático:**

```csharp
using System;

// Produto (Interface)
// Em C#, interfaces são declaradas com a palavra-chave `interface`.
// Métodos em interfaces são implicitamente públicos e abstratos.

public interface IConteudo
{
    void Exibir();
    void Publicar();
}
```

## Produtos Concretos

Classes em C# que implementam uma interface usam a sintaxe `: NomeDaInterface`. Os métodos da interface devem ser implementados.

```csharp
public class Artigo : IConteudo
{
    public void Exibir()
    {
        Console.WriteLine("Exibindo Artigo.");
        // Lógica específica para exibir um artigo
    }

    public void Publicar()
    {
        Console.WriteLine("Publicando Artigo.");
        // Lógica específica para publicar um artigo
    }
}

public class Noticia : IConteudo
{
    public void Exibir()
    {
        Console.WriteLine("Exibindo Notícia.");
        // Lógica específica para exibir uma notícia
    }

    public void Publicar()
    {
        Console.WriteLine("Publicando Notícia.");
        // Lógica específica para publicar uma notícia
    }
}
```

## Criador (Classe Abstrata)

Classes abstratas em C# são declaradas com `abstract class`. Métodos abstratos são declarados com `abstract` e não têm implementação. Métodos não abstratos (como `OperarComConteudo`) têm uma implementação padrão.

```csharp
public abstract class CriadorConteudo
{
    // O Factory Method - deve ser implementado pelas subclasses
    public abstract IConteudo CriarConteudo();

    public void OperarComConteudo()
    {
        IConteudo conteudo = CriarConteudo(); // Usa o Factory Method
        conteudo.Exibir();
        conteudo.Publicar();
    }
}
```

## Criadores Concretos

Classes concretas que herdam de uma classe abstrata usam a sintaxe `: NomeDaClasseAbstrata`. Métodos abstratos da classe pai devem ser implementados usando a palavra-chave `override`.

```csharp
public class CriadorArtigo : CriadorConteudo
{
    public override IConteudo CriarConteudo()
    {
        return new Artigo();
    }
}

public class CriadorNoticia : CriadorConteudo
{
    public override IConteudo CriarConteudo()
    {
        return new Noticia();
    }
}
```

## Uso no Sistema de Gerenciamento de Conteúdo

O ponto de entrada de um aplicativo de console C# geralmente é o método `Main` dentro de uma classe `Program`.

```csharp
public class SistemaGerenciamentoConteudo
{
    public static void Main(string[] args)
    {
        // Criando e operando com um Artigo
        CriadorConteudo criador1 = new CriadorArtigo();
        criador1.OperarComConteudo();

        Console.WriteLine("---");

        // Criando e operando com uma Notícia
        CriadorConteudo criador2 = new CriadorNoticia();
        criador2.OperarComConteudo();

        Console.WriteLine("---");

        // Exemplo de como você adicionaria um novo tipo de conteúdo (e.g., Vídeo):
        // 1. Crie a classe 'Video' que implementa 'IConteudo'.
        // 2. Crie a classe 'CriadorVideo' que estende 'CriadorConteudo'
        //    e sobrescreve 'CriarConteudo()' para retornar um 'Video'.
        // Nenhum código neste método Main ou nas classes CriadorConteudo existentes precisaria ser modificado,
        // apenas a adição das novas classes.

        // CriadorConteudo criador3 = new CriadorVideo(); // Descomente e teste após criar Video e CriadorVideo
        // criador3.OperarComConteudo();

        Console.WriteLine("\nPressione qualquer tecla para sair...");
        Console.ReadKey();
    }
}
```

### Por que os outros padrões não seriam a melhor escolha:

2.  **Padrão Builder:**

    - **O que é:** Separa a construção de um objeto complexo de sua representação, de modo que o mesmo processo de construção possa criar diferentes representações.
    - **Por que não se aplica:** O Builder é excelente para construir objetos complexos passo a passo, onde a ordem ou os parâmetros da construção podem variar. No seu caso, a questão é mais sobre _qual tipo de objeto_ criar, não como um único objeto complexo é construído. Se um `Artigo` tivesse muitas partes opcionais e configurações complexas, um Builder poderia ser usado _dentro_ da fábrica para construir o `Artigo`, mas não para a escolha inicial do tipo de conteúdo.

3.  **Padrão Prototype:**

    - **O que é:** Especifica os tipos de objetos a serem criados usando uma instância prototípica e cria novos objetos copiando este protótipo.
    - **Por que não se aplica:** O Prototype é útil quando a criação de objetos é cara ou quando você precisa criar muitos objetos semelhantes a partir de um "molde". Embora possa ser usado para criar instâncias de conteúdo, o Factory Method é mais direto para o problema de _qual tipo_ de conteúdo criar de forma flexível, sem a necessidade de manter e clonar instâncias de protótipo.

4.  **Padrão Abstract Factory:**

    - **O que é:** Fornece uma interface para criar famílias de objetos relacionados ou dependentes sem especificar suas classes concretas.
    - **Por que não se aplica:** O Abstract Factory seria apropriado se você tivesse _famílias_ de objetos de conteúdo (por exemplo, "Conteúdos para web" vs. "Conteúdos para impressão", onde cada família tem seus próprios artigos, notícias, etc.). Se seu sistema tem apenas um tipo de `Artigo`, um tipo de `Noticia`, etc., sem a necessidade de agrupar variações por "família", o Factory Method é uma solução mais simples e suficiente. O Abstract Factory adicionaria complexidade desnecessária se não houver a necessidade de gerenciar famílias de produtos.

5.  **Padrão Composite:**

    - **O que é:** Compõe objetos em estruturas de árvore para representar hierarquias de parte-todo. Permite que os clientes tratem objetos individuais e composições de objetos de forma uniforme.
    - **Por que não se aplica:** O Composite é para estruturar dados e permitir que partes e todos sejam tratados da mesma forma (e.g., um "Documento" que pode conter vários "Parágrafos" e "Imagens", onde "Parágrafo" e "Imagem" são tratados como "Componentes"). Ele não lida com o problema de _criar_ diferentes tipos de conteúdo de forma extensível, mas sim com a _organização_ e _manipulação_ de conteúdos existentes.

---
