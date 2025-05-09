# Variáveis: Tamanho Indefinido

Em programação, frequentemente encontramos dados cujo tamanho varia, como textos. C# oferece maneiras eficazes e seguras para lidar com isso, principalmente através da classe `string`. Este guia explicará como trabalhar com strings de tamanho variável em C#.

## O Conceito de Strings em C#

A classe `string` em C# é projetada para armazenar sequências de caracteres (texto) de tamanho variável. Ao contrário de algumas linguagens onde você precisa gerenciar a memória manualmente, C# lida com a alocação e liberação de memória para strings automaticamente.

### Exemplo Básico

```csharp
using System;

string mensagem; // Declara uma variável do tipo string

mensagem = "Olá";  // Atribui um texto de 3 caracteres
Console.WriteLine(mensagem);

mensagem = "Mundo C#"; // Atribui um texto de 9 caracteres
Console.WriteLine(mensagem);
```

**Explicação:**

- `string mensagem;` declara uma variável chamada `mensagem` capaz de armazenar qualquer texto.
- Podemos atribuir diferentes textos (de diferentes tamanhos) a `mensagem` sem nos preocuparmos com o gerenciamento de memória. C# cuida disso para nós.
- `Console.WriteLine()` exibe o conteúdo da string no console.

## Vantagens da Classe `string`

- **Gerenciamento Automático de Memória:** C# aloca e libera a memória necessária para as strings, evitando erros e simplificando o desenvolvimento.
- **Flexibilidade:** Uma única variável `string` pode armazenar textos de comprimentos variados.
- **Segurança:** O uso da classe `string` previne muitos problemas que podem ocorrer com a manipulação direta de ponteiros (como em C++), tornando o código mais seguro.

## Operações Comuns com Strings

### Atribuição e Concatenação

```csharp
using System;

string primeiroNome = "Ana";
string ultimoNome = "Santos";
string nomeCompleto = primeiroNome + " " + ultimoNome; // Concatenação

Console.WriteLine(nomeCompleto); // Saída: Ana Santos
```

**Explicação:**

- Usamos o operador `+` para juntar (concatenar) strings.

### Imutabilidade

É importante entender que strings em C# são _imutáveis_. Isso significa que quando você "modifica" uma string, na verdade está criando uma nova string na memória.

```csharp
using System;

string texto = "Oi";
texto = texto + "!"; // Cria uma nova string "Oi!"

Console.WriteLine(texto);
```

**Explicação:**

- `texto = texto + "!";` não altera a string original "Oi". Em vez disso, cria uma nova string "Oi!" e atribui essa nova string à variável `texto`.

## Alternativas para Casos Especiais

Na maioria das situações, a classe `string` é a melhor escolha. No entanto, existem alternativas para cenários específicos:

### `StringBuilder`

Quando você precisa fazer muitas modificações em uma string (especialmente dentro de um loop), usar a classe `StringBuilder` é mais eficiente. Ela evita a criação excessiva de novas strings.

```csharp
using System;
using System.Text; // Importante para usar StringBuilder

StringBuilder construtor = new StringBuilder();
construtor.Append("Olá ");
construtor.Append("Mundo!");

string fraseFinal = construtor.ToString();
Console.WriteLine(fraseFinal);  // Saída: Olá Mundo!
```

**Explicação:**

- `StringBuilder` é otimizado para modificações de strings.
- `Append()` adiciona texto ao final do `StringBuilder`.
- `ToString()` converte o `StringBuilder` final em uma string comum.

### Código Inseguro (`unsafe`) e Ponteiros

Em circunstâncias muito raras, como interagir diretamente com a memória ou bibliotecas de baixo nível, C# permite o uso de ponteiros dentro de um bloco de código `unsafe`.

```csharp
unsafe
{
    char* ponteiro;
    // ... código avançado com ponteiros ...
}
```

**Importante:**

- O código `unsafe` é complexo e requer muito cuidado.
- Para a grande maioria das tarefas de programação em C#, especialmente ao trabalhar com texto, a classe `string` e `StringBuilder` são as opções mais seguras e eficientes. Evite `unsafe` a menos que seja absolutamente necessário.
