# Classes

As classes são blocos fundamentais na programação orientada a objetos e permitem organizar e estruturar o código de maneira eficiente.

Em **C#**, toda aplicação consiste em pelo menos uma classe.

- `.NET Framework Class Library` - uma vasta coleção de classes pré-criadas que permitem que você desenvolva aplicativos rapidamente

> Observação de engenharia de software: _As classes simplificam a programação porque o cliente pode usar apenas os membros públicos expostos pela classe. Esses membros geralmente são orientados ao cliente, em vez de à implementação. Os clientes não estão cientes nem envolvidos na implementação de uma classe. Os clientes geralmente se importam com_ o que _a classe faz, mas não_ como _a classe faz. Os clientes, é claro, se importam que a classe opere correta e eficientemente._

## Declaração de Classes

Cada aplicativo consiste em pelo menos uma declaração de classe definida pelo programador. Essas classes são conhecidas como classes definidas pelo usuário.

A palavra-chave `class` introduz a declaração de uma classe, seguida imediatamente pelo nome da classe.

## Convenções de Nomenclatura:

Por convenção, os nomes de classes em **C#** iniciam com uma letra maiúscula.

Além disso, a primeira letra de cada palavra subsequente no nome da classe também é maiúscula.

- Exemplo: `MinhaClasse`.

* Importante: Por convenção, os nomes das classes na linguagem C# devem seguir o padrão “pascal case” também conhecido como “upper camel case”.

Em C#, a convenção é que cada declaração de classe seja armazenada em um arquivo com o mesmo nome que a classe e terminando com a extensão de nome de arquivo `.cs`. Por exemplo, a classe `Account` estaria no arquivo `Account.cs`.

Um erro de compilação ocorre se o nome do arquivo da classe pública não for exatamente igual ao nome dessa classe (incluindo ortografia e capitalização), seguido pela extensão `.cs`.

- Por exemplo, se a classe se chama `MinhaClasse`, o arquivo deve ser `MinhaClasse.cs`.

## Cada classe Novo tipo

Cada _classe_ que você cria se torna um novo _tipo_ que você pode usar para criar objetos, então C# é uma **linguagem de programação extensível**. Grandes equipes de desenvolvimento na indústria trabalham em aplicativos que contêm centenas, ou até milhares, de classes.

## classe driver

Uma pessoa dirige um carro dizendo a ele o que fazer (ir mais rápido, ir mais devagar, virar à esquerda, virar à direita, etc.) — sem precisar saber como os mecanismos internos do carro funcionam. Da mesma forma, um método (como `Main`) “dirige” um objeto chamando seus métodos — sem precisar saber como os mecanismos internos da classe funcionam. Nesse sentido, a classe que contém o método `Main` é chamada de **classe driver**.

## Estrutura Básica de uma Classe

```csharp
class Account
{
    private string name; // variável de instância

    // Método que define o nome da conta
    public void SetName(string accountName)
    {
        name = accountName; // armazena o nome da conta
    }

    // Método que obtém o nome da conta
    public string GetName()
    {
        return name; // retorna o valor de name
    }
}
```

Em geral, as declarações de classe podem incluir os seguintes componentes:

- Modificadores como public, private e um número de outros que veremos mais tarde
- O nome da classe, com a primeira letra em maiúscula
- O nome da classe pai (superclasse), quando houver. Neste caso teremos que usar a palavra chave extends para indicar qual é a classe pai.
- Uma lista de interfaces implementadas pela classe, separadas por vírgula. Neste caso temos que usar a palavra chave implements para indicar as interfaces.
- O corpo da classe, rodeada pelas chaves { e }.

O corpo da classe, delimitado por `{}` contém todos os elementos necessários para tratar do ciclo de vida dos objetos: construtores, declarações de campos e métodos.

## UML - Representação de uma Classe

Um diagrama UML (Unified Modeling Language) pode representar uma classe, mostrando seu nome, atributos e métodos.

1. **Nome da Classe** – Representa o identificador da classe.
2. **Atributos** – Definem os dados que a classe armazena.
3. **Métodos** – Indicam as operações que a classe pode realizar.

```
-----------------
|   Cliente     |
-----------------
| -nome: String |
| -idade: int   |
-----------------
| +comprar()    |
| +cadastrar()  |
-----------------
```

Nesse exemplo, a classe `Cliente` tem dois atributos (`nome` e `idade`) e dois métodos (`comprar()` e `cadastrar()`). Os sinais de `+` e `-` indicam visibilidade: `+` para público e `-` para privado.

## Acesso padrão para membros da classe

Por padrão, tudo em uma classe é `privado`, a menos que você especifique o contrário fornecendo modificadores de acesso.

```csharp
class Conta {
   public int numero;
   public double saldo;
   public double limite;
}
```

No exemplo acima, utilizamos a palavra-chave `class` para definir a classe `Conta`. Os atributos `numero`, `saldo` e `limite` são declarados como `public` para serem acessíveis de qualquer ponto do código.

Como a linguagem C# é estaticamente tipada, os tipos dos atributos são definidos no código.

## Exemplos Práticos

### Exemplo Prático 01

Suponha que você esteja criando uma classe simples em C# para representar um carro:

```csharp
public class Carro {
    private string marca;
    private string modelo;

    public Carro(string marca, string modelo) {
        this.marca = marca;
        this.modelo = modelo;
    }

    public void ExibirDetalhes() {
        Console.WriteLine("Marca: " + marca);
        Console.WriteLine("Modelo: " + modelo);
    }

    public static void Main(string[] args) {
        Carro meuCarro = new Carro("Toyota", "Corolla");
        meuCarro.ExibirDetalhes();
    }
}
```

Nesse exemplo:

- `Carro` é uma classe pública.
- `ExibirDetalhes()` é um método público que exibe informações sobre o carro.

### Exemplo Prático 02 - Bicicleta

Para entender melhor, considere o exemplo de uma bicicleta. Diferentes tipos de bicicletas, como speed, mountain bike e padrão, compartilham algumas características e comportamentos comuns. Em POO, dizemos que uma bicicleta é uma instância da classe `Bicicleta`.

Classe Bicicleta: Representada por um retângulo com **três** compartimentos:

1.  Nome da classe: “Bicicleta”

2.  Atributos:

    - cadencia (int)
    - velocidade (int)
    - marcha (int)

3.  Métodos:
    - mudarCadencia(int novoValor)
    - mudarMarcha(int novoValor)
    - acelerar(int incremento)
    - brecar(int decremento)
    - imprimirEstado()

```
+---------------------+
|    Bicicleta        |
+---------------------+
| - cadencia: int     |
| - velocidade: int   |
| - marcha: int       |
+---------------------+
| + mudarCadencia(novoValor: int) |
| + mudarMarcha(novoValor: int)   |
| + acelerar(incremento: int)     |
| + brecar(decremento: int)       |
| + imprimirEstado()              |
+---------------------+
```

#### Atributos

- As variáveis cadência, velocidade e marcha representam os estados do objeto e;

#### Métodos

- Os métodos mudarCadencia, mudarMarcha, acelerar, brecar e imprimirEstado definem a interação do objeto com o mundo real.

### Exemplo Prático 03

Vamos considerar a classe `Conta`, comum em sistemas bancários. Todos os objetos criados a partir da classe `Conta` terão os atributos e métodos definidos na classe, mas os valores desses atributos podem variar entre os objetos.

Um diagrama UML da classe `Conta` pode ser representado da seguinte forma:

```
+----------------------+
|        Conta         |
+----------------------+
| - numero: int        |
| - saldo: double      |
| - limite: double     |
+----------------------+
| + depositar(valor: double) |
| + sacar(valor: double)     |
| + consultarSaldo(): double |
+----------------------+
```
