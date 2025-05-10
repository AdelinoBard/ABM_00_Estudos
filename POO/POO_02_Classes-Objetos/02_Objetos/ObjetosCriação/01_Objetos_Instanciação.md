# Instanciação (Criação) de Objetos em C#

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

## 1. Instanciação

Em C#, objetos são instâncias de classes que representam entidades do mundo real ou conceitos abstratos. A criação de objetos envolve alocação de memória e inicialização, processos gerenciados pela máquina virtual (VM) do .NET.

## 2. Processo de Instanciação

- Instanciação é o processo de criar o objeto em si.

Para utilizar uma classe, precisamos criar objetos a partir dela. Isso é feito através de uma expressão de criação de objetos, que utiliza a palavra-chave `new`:

```c#
Objeto myObjeto = new Objeto();
```

Para instanciar (criar) um objeto da classe `Objeto`, atribuímos o resultado à variável `myObjeto`. Essa variável possui o tipo `Objeto`, que corresponde à classe previamente definida. A palavra-chave `new` é utilizada para criar uma nova instância da classe especificada — neste caso, `Objeto`. Mesmo que o construtor não receba parâmetros, os parênteses à direita de `Objeto` são obrigatórios, pois indicam que o construtor está sendo chamado.

- Variável do tipo "Objeto": `myObjeto`
- A variável `myObjeto` armazena uma referência ao novo objeto criado.
- Tipo da variável: "Objeto" (similar a outros tipos como inteiro, float, char, etc.)
- `new Objeto()` é uma **expressão de criação de objeto** que aloca memória e inicializa o objeto.

```csharp
Carro meuCarro = new Carro();
```

- `meuCarro` é uma variável do tipo `Carro`.
- `new Carro()` aloca memória e inicializa o objeto.

_Você não pode chamar um método de uma classe até criar um objeto dessa classe (Os métodos estáticos (e outros membros da classe estática) são uma exceção)._

## 3. Palavra-chave `new`

A palavra-chave `new`:

1. Aloca memória no heap para armazenar um novo objeto e, em seguida;
2. Invoca implicitamente o construtor da classe para inicializar o objeto. (inicializando-o conforme as especificações da classe.)

**Sintaxe:**

```csharp
Tipo objeto = new Tipo();
```

## 4. Inferência de Tipo com `var`

A declaração de variáveis pode ser simplificada usando a palavra-chave `var`, onde o compilador infere o tipo da variável:

```csharp
var carro2 = new Carro("Azul", 2021);
```

- `carro2` é automaticamente reconhecido como `Carro`.

Conforme as **convenções de codificação da Microsoft**, é recomendado usar a inferência de tipo quando o tipo é evidente.

**Vantagens:**

- Reduz redundância.
- Mantém a segurança de tipos (o compilador infere o tipo)
- Alinha-se com as convenções da Microsoft

## 5. Uma classe e seu construtor: A planta da casa

Imagine que você é um arquiteto e precisa construir casas. Antes de construir, você cria uma planta baixa, certo? Essa planta define as características de cada casa: número de quartos, cor, tamanho da garagem, etc.

Em C#, a **classe** é como essa planta baixa. Ela define os atributos (características) e métodos (ações) que um objeto (a casa construída) terá.

No exemplo abaixo, a classe `Casa` define os atributos `matricula`, `cor`, `comodos` e `garagem`, e um construtor para inicializar esses atributos:

```csharp
public class Casa
{
    // Atributos (características da casa)
    public string Matricula { get; set; }
    public string Cor { get; set; }
    public int Comodos { get; set; }
    public int Garagem { get; set; }

    // Construtor: inicializa os atributos ao criar um objeto Casa
    public Casa(string matricula, string cor, int comodos, int garagem)
    {
        Matricula = matricula;
        Cor = cor;
        Comodos = comodos;
        Garagem = garagem;
    }

    // Método: exibe as informações da casa
    public void ExibirDetalhes()
    {
        Console.WriteLine($"Matrícula: {Matricula}, Cor: {Cor}, Cômodos: {Comodos}, Garagem: {Garagem}");
    }
}
```

**Observações:**

- **`public`**: Indica que os atributos e métodos podem ser acessados de qualquer lugar do código.
- **`{ get; set; }`**: Cria automaticamente os métodos para acessar e modificar os valores dos atributos (propriedades).

## 5.1 Construindo as casas: Instanciação da classe

Com a planta baixa (classe `Casa`) pronta, podemos construir as casas (objetos). Para isso, usamos a palavra-chave `new`:

```csharp
public class Programa
{
    public static void Main(string[] args)
    {
        // Cria 3 objetos Casa com características diferentes
        Casa casa1 = new Casa("0001", "azul", 6, 2);
        Casa casa2 = new Casa("0002", "verde", 4, 1);
        Casa casa3 = new Casa("0003", "branca", 2, 0);

        // Exibe as informações de cada casa
        casa1.ExibirDetalhes();
        casa2.ExibirDetalhes();
        casa3.ExibirDetalhes();
    }
}
```

**Entendendo a analogia:**

- A **classe `Casa`** é a planta baixa.
- **`casa1`, `casa2`, `casa3`** são as casas construídas a partir da planta baixa. Cada casa é um objeto único com suas próprias características.
- O **construtor** é como o pedreiro que segue a planta baixa para construir a casa, definindo os valores iniciais dos atributos.
- O **método `ExibirDetalhes()`** é como um tour pela casa, mostrando suas características.

**Pontos-chave:**

- Uma classe é um modelo para criar objetos.
- Um objeto é uma instância de uma classe.
- O construtor inicializa os atributos de um objeto.
- Métodos definem as ações que um objeto pode realizar.
- A instanciação é o processo de criação de um objeto.
