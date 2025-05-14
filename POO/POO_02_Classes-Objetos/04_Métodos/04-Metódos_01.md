# Métodos (funções)

No universo da programação, os métodos se destacam como blocos de código reutilizáveis que encapsulam funcionalidades específicas, promovendo organização, modularidade e eficiência no desenvolvimento de software. Através dos métodos, podemos evitar a duplicação de código, simplificar a manutenção e aumentar a legibilidade do código.

O procedimento/função/sub-algoritimo é um grupo de comandos que realiza uma determinada tarefa específica que é executada quando este é chamado. Quando o programa principal chama o procedimento ou função, o fluxo do programa é desviado para este, o qual é executado em seguida, e após a sua finalização, volta-se à execução do programa principal normalmente.

O próprio objeto deve realizar operações de consulta ou alteração dos valores de seus atributos. Essas operações são definidas nos métodos do objeto. Os métodos também são utilizados para possibilitar interações entre os objetos de uma aplicação. Por exemplo, quando um cliente requisita um saque através de um caixa eletrônico do banco, o objeto que representa o caixa eletrônico deve interagir com o objeto que representa a conta do cliente.

- **As tarefas que um objeto pode realizar são definidas pelos seus métodos.**
- **Um objeto é composto por atributos e métodos.**

**Diferenças entre Funções e Procedimentos:**

Embora os termos "função" e "procedimento" sejam frequentemente usados de forma intercambiável, há uma distinção sutil entre eles:

- **Função:** Uma função retorna um valor após a execução do corpo da função.
- **Procedimento:** Um procedimento não retorna valor após a execução do corpo da função.

> Em C#, a palavra "procedimento" não é utilizada oficialmente, e o termo "função" abrange tanto os casos que retornam valores quanto os que não retornam.
>
> Em C#, todos são chamados de métodos, mas a diferença está no uso (ou não) de return.

## **Benefícios dos Métodos:**

- **Reutilização de Código:** Evita a duplicação de código, reduzindo o tamanho do programa e facilitando a leitura e o entendimento do código.
- **Manutenção Simplificada:** Qualquer alteração no cabeçalho precisa ser feita apenas no método, e não em cada instância replicada, diminuindo o risco de erros e inconsistências.
- **Modularidade:** Aumenta a modularidade do código, dividindo-o em blocos de funções bem definidas, facilitando a organização e a compreensão do programa.
- **Legibilidade Aprimorada:** Torna o código mais legível e expressivo, pois cada método encapsula uma funcionalidade específica, com um nome descritivo que indica sua função.

## Exemplo de Métodos em C#

```csharp
public class Conta
{
    public int Numero { get; set; }
    public decimal Saldo { get; private set; }

    public void Depositar(decimal valor)
    {
        Saldo += valor;
    }

    public void Sacar(decimal valor)
    {
        if (valor <= Saldo)
        {
            Saldo -= valor;
        }
        else
        {
            throw new InvalidOperationException("Saldo insuficiente.");
        }
    }
}
```

## **Métodos Funções Predefinidas em C#:**

C# possue um conjunto de funções predefinidas que oferecem funcionalidades básicas, como operações matemáticas, manipulação de strings e entrada/saída de dados.

## Definindo Métodos

Os métodos são funções definidas dentro de uma classe que executam tarefas específicas.

Em C#, os nomes dos métodos seguem as mesmas convenções de capitalização que os nomes de classe, utilizando o estilo CamelCase.

```csharp
public void SetName(string accountName)
{
    name = accountName;
}
```

## **Estrutura Geral de um Método:**

Um método em C# possui uma estrutura composta por elementos essenciais que definem sua funcionalidade e comportamento:

- **Modificador de Acesso:** Define o nível de acesso do método, como `public`, `private` ou `protected`.
- **Palavra-chave `static`:** Indica se o método é _estático_ (não precisa de um objeto para ser chamado) ou de _instância_ (precisa ser chamado através de um objeto).
- **Tipo de Retorno:** Especifica o tipo de dado que o método retorna após sua execução, podendo ser `void` (sem retorno) ou um tipo de dado específico.
- **Nome do Método:** Identifica o método de forma única e descritiva, permitindo sua invocação.
- **Lista de Parâmetros:** Define os parâmetros que o método recebe como entrada, geralmente entre parênteses. Cada parâmetro possui um tipo de dado e um nome.
- **Corpo do Método:** Contém as instruções que serão executadas quando o método for chamado.

### Sintaxe Básica

A sintaxe básica de uma função/método é:

```c#
tipo_de_retorno nome_da_funcaoMétodo(parâmetros) {
    // corpo da função/método
}
```

```c#
public tipo_retorno nome_funcao(parametro1, parametro2, ...)
{
  // Corpo da função
  return valor_retorno;
}
```

### Estrutura de um método

A primeira linha de cada declaração de método é o _cabeçalho do método_.

O _tipo de retorno_ do método (que aparece à esquerda do nome do método) especifica o tipo de dados que o método retorna ao seu _chamador_ após executar sua tarefa.

- O tipo de retorno void indica que quando o método conclui sua tarefa, ele não retorna (ou seja, devolve) nenhuma informação ao seu _método de chamada_.

```c#
public void SetName(string accountName) // cabeçalho do método
{
   name = accountName; // store the account name
}
```

## Execução do Método:

Para executar um método, utilizamos seu nome seguido de parênteses, que podem conter argumentos (valores) para os parâmetros, se necessário.

```c#
ExibirCabecalho(); // Chamada do método sem argumentos
```

## Chamada de Método:

```c#
Console.WriteLine($"Initial name is: {myAccount.GetName()}");
```

Para chamar um método para um objeto específico, você especifica

- o nome do objeto (`myAccount`) seguido por
- o **operador de acesso de membro (**.**)**,
- o nome do método (`GetName`) e
- um conjunto de parênteses.

Os parênteses _vazios_ indicam que `GetName` não requer nenhuma informação adicional para executar sua tarefa.

## **Métodos com Retorno:**

Os métodos podem retornar valores após sua execução. O tipo de retorno é definido antes do nome do método.

Um método pode retornar um valor após sua execução, utilizando a palavra-chave `return`. O valor retornado pode ser utilizado na chamada do método para realizar operações subsequentes.

**Exemplo:**

```c#
public static int ObterMaior(int valor1, int valor2)
{
    if (valor1 > valor2)
    {
        return valor1;
    }
    else
    {
        return valor2;
    }
}

int maiorValor = ObterMaior(10, 5); // Chamada do método e armazenamento do valor retornado
Console.WriteLine($"Maior valor: {maiorValor}");
```

## **Tipos de Retorno:**

Um método pode retornar diferentes tipos de dados, como `int`, `double`, `char`, `string` e até mesmo objetos de outras classes. O tipo de retorno deve ser especificado antes do nome do método.

- **Retorno Simples:** A função retorna um único valor.
- **Retorno Múltiplo:** A função retorna mais de um valor, geralmente em forma de uma tupla ou lista.

**Exemplo:**

```c#
static double CalcularMedia(double nota1, double nota2)
{
    return (nota1 + nota2) / 2;
}

static string ObterNomeCompleto(string nome, string sobrenome)
{
    return nome + " " + sobrenome;
}
```

## Parâmetros são variáveis locais

Variáveis declaradas no corpo de um método específico (como `Main`) são **variáveis locais** que podem ser usadas _somente_ naquele método. Cada método pode acessar apenas suas próprias variáveis locais, não as de outros métodos. Quando um método termina, os valores de suas variáveis locais são perdidos. Os parâmetros de um método também são variáveis locais do método.

_Uma tentativa de um método que não é membro de uma classe específica de acessar um membro privado dessa classe é um erro de compilação._

**Parâmetros de Funções:**

- **Parâmetros Formais:** São os parâmetros definidos na declaração da função.
- **Parâmetros Reais:** São os valores fornecidos à função quando ela é chamada.
- **Passagem por Valor:** Os valores dos parâmetros são copiados para dentro da função, e as alterações feitas dentro da função não afetam os valores originais.
- **Passagem por Referência:** A função recebe uma referência à variável original, e as alterações feitas dentro da função afetam diretamente o valor original.

## **Passagem de Parâmetros:**

Os parâmetros de um método funcionam como variáveis ​​especiais que permitem que valores diferentes sejam passados ​​a cada chamada do método. Ao chamar um método, podemos fornecer valores para seus parâmetros, permitindo que o método realize operações com esses dados.

Ao chamar um método com parâmetros, fornecemos valores para cada parâmetro, respeitando seus tipos de dados. Os argumentos são passados entre parênteses, separados por vírgulas.

**Exemplo:**

```c#
public static void CalcularMedia(double nota1, double nota2) // Método com 2 parâmetros
{
    double media = (nota1 + nota2) / 2;
    Console.WriteLine($"Média: {media}");
}

CalcularMedia(8.5, 9.2); // Chamada do método com argumentos
```

O número e a ordem dos _argumentos_ em uma chamada de método _devem corresponder_ ao número e à ordem dos _parâmetros_ na lista de parâmetros da declaração do método.

## **Passagem de Parâmetros por Valor e por Referência:**

Em C#, a passagem de parâmetros para métodos é geralmente realizada por valor. Isso significa que uma cópia do valor do argumento é passada para o parâmetro do método, e qualquer alteração feita no parâmetro dentro do método não afeta o valor original do argumento.

No entanto, também é possível passar parâmetros por referência, utilizando a palavra-chave `ref` antes do tipo do parâmetro. Nesse caso, o método recebe uma referência direta à variável original, permitindo que ele modifique o valor da variável original.

## Sobrecarga de Métodos:

A sobrecarga de métodos permite que você defina diversos métodos com o mesmo nome, desde que suas listas de parâmetros sejam diferentes em quantidade ou tipo. Isso torna o código mais flexível e intuitivo, pois permite que você utilize o mesmo nome de método para realizar diferentes operações com base nos tipos de dados dos parâmetros.

Um método pode ter várias versões. Ou seja, uma classe pode definir vários métodos que têm o _mesmo_ nome, desde que tenham _diferentes_ números e/ou tipos de parâmetros — um conceito conhecido como _métodos sobrecarregados_. Esses métodos normalmente executam tarefas semelhantes.

**Exemplo:**

```c#
static void CalcularArea(double lado) // Cálculo da área de um quadrado
{
    Console.WriteLine($"Área do quadrado: {lado * lado}");
}

static void CalcularArea(double base, double altura) // Cálculo da área de um retângulo
{
    Console.WriteLine($"Área do retângulo: {base * altura}");
}
```

## **Parâmetros Variáveis (Parameter Arrays):**

Os parâmetros variáveis (parameter arrays) permitem que um método receba um número variável de argumentos do mesmo tipo. Eles são declarados utilizando a palavra-chave `params` antes do tipo do parâmetro.

**Exemplo:**

```c#
static void ExibirNumeros(params int[] numeros)
{
    foreach (int numero in numeros)
    {
        Console.WriteLine(numero);
    }
}
```

**Regras para Parâmetros Variáveis:**

- Um método só pode ter no máximo um parâmetro variável.
- O parâmetro variável deve ser o último parâmetro da lista de parâmetros.
- Não é possível combinar parâmetros variáveis ​​com parâmetros nomeados.

## Encapsulamento de Métodos

Por padrão, tudo em uma classe é `privado`, a menos que você especifique o contrário fornecendo modificadores de acesso.

Métodos (e outros membros de classe) que são declarados `públicos` estão “disponíveis ao público”. Eles podem ser usados

- por métodos (e outros membros) da classe na qual são declarados,
- pelos clientes da classe, ou seja, métodos (e outros membros) de quaisquer outras classes

## **Considerações Adicionais:**

- **Funções Recursivas:** Abordar o conceito de funções recursivas, que são funções que se chamam a si mesmas, e demonstrar como utilizá-las para resolver problemas de forma elegante.
- **Funções com Escopo:** Explicar o conceito de escopo de variáveis em funções e como as variáveis locais e globais são acessíveis dentro de uma função.
- **Lambdas:** Apresentar as funções lambda em Python, que são funções anônimas definidas em uma única linha de código.
- **Funções Decoradoras:** Descrever o conceito de funções decoradoras em Python, que permitem adicionar funcionalidades extras a outras funções.

---
