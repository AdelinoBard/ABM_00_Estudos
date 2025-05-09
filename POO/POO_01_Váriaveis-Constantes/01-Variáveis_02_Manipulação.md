# Variáveis: Declaração

A forma como a declaração de variáveis é feita depende da sintaxe da linguagem de programação utilizada.

Lembre-se: Nas linguagens de programação, é importante seguir convenções e sintaxe adequadas para a declaração de variáveis.

## Identificador - Nome da Variável

Ao criar uma variável, é necessário atribuir a ela um identificador. Esse identificador funciona como um rótulo para a área da memória onde a variável está armazenada, permitindo que seu valor seja acessado e modificado ao longo da execução do programa.

As regras para definir identificadores variam conforme a linguagem de programação utilizada. Portanto, ao programar em uma nova linguagem, é essencial conhecer essas regras para garantir nomes válidos e funcionais.

As variáveis são sempre referenciadas por um nome (identificador), escolhido pelo programador durante o desenvolvimento do algoritmo. Exemplos comuns incluem `produto`, `idade`, `a`, `x`, `nota1`, `peso` e `preço`. Esses identificadores tornam possível atribuir e recuperar valores com facilidade, promovendo a clareza e organização do código.

## Tipo de Dado

Além de um identificador, cada variável deve possuir um tipo de dado definido, que determina o tipo de informação que ela pode armazenar. Esse tipo pode variar entre números inteiros, caracteres, valores booleanos, entre outros, garantindo que os dados sejam manipulados corretamente dentro do programa.

## Escopo da Variável

Além do identificador e do tipo de dado, é fundamental definir o escopo da variável, ou seja, determinar onde ela poderá ser acessada dentro do programa. O escopo é influenciado pelos modificadores de acesso e pode ser classificado, por exemplo, como local — quando a variável está restrita a uma função específica — ou global, permitindo seu uso em diferentes partes do programa.

## Resumindo

Para criar uma variável, precisamos:

1. **Dar um nome (identificador)**: Um nome descritivo que ajuda a identificar o propósito da variável.
2. **Definir o tipo de dado**: Indica que tipo de informação será armazenada (números, texto, etc.).
3. **Determinar o escopo**: Define em quais partes do programa a variável será acessível.

Exemplo em C#:

```csharp
int idade = 25; // Declara uma variável chamada 'idade' do tipo inteiro, com valor inicial 25.
```

![alt text](image.png)

## Sintaxe padrão

A sintaxe padrão utilizada para declarar uma variável é: `Tipo nome`

```csharp
Tipo nome;
```

Destaca-se que as declarações terminam com `;`.

```c#
int idade = 25;  // Correto
```

```csharp
// Uma variável do tipo int chamada numeroDaConta.
int numeroDaConta;

// Uma variável do tipo double chamada precoDoProduto.
double precoDoProduto;
```

Em C#, as variáveis devem ser declaradas antes de serem utilizadas. Isso significa que, se um programa utilizar 300 variáveis, todas devem ser declaradas previamente.

A declaração de uma variável pode ser realizada em qualquer linha de um bloco. Não é necessário declarar todas as variáveis no começo do bloco, como acontece em algumas linguagens de programação.

```csharp
{
    // Declaração com Inicialização
    int numero = 10;

    // Uso da variável
    Console.WriteLine(numero);

    // Outra Declaração com Inicialização
    double preco = 137.6;

    // Uso da variável
    Console.WriteLine(preco);
}
```

Um erro comum é tentar declarar duas variáveis com o mesmo nome no mesmo bloco ou escopo, o que gera um erro de compilação:

```csharp
{
    // Declaração
    int numero = 10;

    // Erro de Compilação
    int numero = 20;
}
```

## Lembre-se:

- Em C#, todas as variáveis precisam ser declaradas antes de serem utilizadas.
- Os tipos de dados determinam a quantidade de memória que será reservada para a variável.
- Os nomes das variáveis devem ser descritivos e curtos, facilitando a leitura e a escrita do código.

# Variáveis: Inicialização

A inicialização de variáveis é um passo fundamental na programação, pois assegura que as variáveis contenham valores válidos antes de serem utilizadas. Em linguagens como C# e C++, uma variável deve ser inicializada antes do seu uso para evitar erros de compilação e comportamento indesejado.

Quando declaramos uma variável, estamos reservando um espaço na memória para armazenar seu valor. Contudo, até que essa variável seja inicializada, o conteúdo desse espaço de memória é indeterminado, podendo conter "lixo" (valores residuais de usos anteriores da memória). Para ilustrar, considere a seguinte declaração em C#:

```csharp
int x;
```

Se tentarmos utilizar `x` sem inicializá-la, como em:

```csharp
Console.WriteLine(x);
```

Receberemos um erro de compilação, pois `x` não foi inicializada. Para evitar isso, podemos inicializá-la diretamente:

```csharp
int x = 0;
```

Ou utilizando o operador `new`, que atribui o valor padrão do tipo de dados:

```csharp
x = new int();
```

Isso é funcionalmente equivalente a `int x = 0;`.

# Variáveis: Alteração

O conteúdo de uma variável pode ser alterado, consultado ou apagado quantas vezes forem necessárias durante o algoritmo. Mas, ao alterar o conteúdo da variável, a informação anterior é perdida, ou seja, sempre "vale" a última informação armazenada na variável. Uma variável armazena 'apenas' um conteúdo de cada vez.

O valor de uma variável pode ser alterado durante a execução do programa. No entanto, uma variável só pode armazenar um valor de cada vez, e esse valor deve ser do tipo definido inicialmente.

Exemplo:

```csharp
int contador = 0;  // Inicializamos a variável.
contador = 10;     // Alteramos o valor armazenado.
```

Ao alterar o valor de uma variável, o valor anterior é perdido.
