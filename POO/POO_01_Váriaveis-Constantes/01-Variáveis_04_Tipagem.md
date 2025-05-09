# Variáveis: Tipagem

Em programação, os tipos de dados definem o tipo de valor que uma variável pode armazenar. Em C#, cada variável deve ser declarada com um tipo específico, o que ajuda o compilador a entender como manipular os dados.

Alguns tipos comuns em C# incluem:

- `int`: Números inteiros.
- `float`/`double`: Números com ponto decimal.
- `char`: Um único caractere.
- `string`: Sequência de caracteres (texto).
- `bool`: Valores lógicos (verdadeiro/falso).

## Tipagem Forte vs. Fraca

### Linguagens Fortemente Tipadas (Tipagem Forte (Strongly Typed))

Em uma linguagem fortemente tipada, cada variável deve ter um tipo de dado declarado explicitamente, e os valores atribuídos a essa variável devem ser compatíveis com o tipo declarado. Isso significa que se você declarar uma variável como `int`, ela só poderá armazenar valores inteiros. Essa característica ajuda a prevenir erros de tipo, tornando o código mais robusto e fácil de manter.

A linguagem C# é conhecida por ser fortemente tipada (strongly typed).

**Exemplo:**

```csharp
int idade = 30; // Correto
idade = "trinta"; // Erro: não é possível atribuir uma string a um int
```

### Linguagens Fracamente Tipadas

Em contraste, linguagens fracamente tipadas permitem que o tipo de uma variável seja alterado durante a execução do programa. Isso proporciona mais flexibilidade, mas pode levar a erros de tipo difíceis de detectar. Exemplos de linguagens fracamente tipadas incluem PHP, Python, Ruby e JavaScript.

**Exemplo em Python:**

```python
# Em Python (fracamente tipada)
idade = 25
idade = "vinte e cinco" # Válido
```

Aqui, a variável `idade` inicialmente armazena um número inteiro, mas depois armazena uma string, algo que não seria permitido em uma linguagem fortemente tipada.

Podemos especificar um tipo para um dado, mas usá-lo como outro tipo. Nesse caso, a conversão de tipos é realizada automaticamente. Veja o exemplo:

```python
# Código em Python
soma = "2" + 2
print(soma)  # Saída: 22
```

O resultado armazenado na variável `soma` é `22` porque o número `2` é tratado como um caractere e concatenado com o caractere `"2"`. O mesmo código geraria um erro em uma linguagem fortemente tipada.

### Linguagens Não Tipadas

Algumas linguagens são consideradas não tipadas, o que significa que não há necessidade de declarar explicitamente o tipo das variáveis, ou existe apenas um tipo genérico para todos os dados. Perl é um exemplo de linguagem não tipada.

**Exemplo em Perl:**

```perl
$idade = 25;
$nome = "Maria";
```

Em Perl, a mesma notação (`$`) é usada para variáveis de diferentes tipos, e o tipo é interpretado contextualmente.

## Tipagem Estática vs. Dinâmica

Além da força da tipagem, as linguagens de programação também podem ser classificadas como estaticamente ou dinamicamente tipadas.

### Linguagens de Tipo Estático (Estaticamente Tipadas (Statically Typed))

O tipo da variável é verificado em tempo de compilação e não pode mudar.

Além de ser fortemente tipada, C# também é uma linguagem estaticamente tipada (statically typed). Isso significa que os tipos de todas as variáveis devem ser definidos em tempo de compilação, antes do programa ser executado. Esse requisito permite que muitos erros sejam detectados pelo compilador, antes mesmo de o código ser executado, aumentando a segurança e a previsibilidade do programa.

**Exemplo:**

```csharp
string nome = "João";
int idade = 25;
// Se tentar atribuir um valor de tipo diferente, o compilador sinalizará um erro
nome = 25; // Erro: incompatibilidade de tipos
```

### Linguagens de Tipo Dinâmico (Dinamicamente Tipadas)

O tipo é verificado em tempo de execução, permitindo maior flexibilidade.

Linguagens de tipo dinâmico determinam o tipo das variáveis em tempo de execução. Isso proporciona maior flexibilidade e simplicidade na escrita do código, mas pode resultar em erros de tipo que só se manifestam durante a execução. Exemplos incluem PHP, Python e Ruby.

**Comparação em Python:**

```python
texto = "Hello"
texto = 123  # Válido
```

```ruby
idade = 25
idade = "vinte e cinco"
```

Em Ruby, como em outras linguagens de tipo dinâmico, o tipo da variável `idade` é determinado em tempo de execução e pode mudar conforme necessário.

## Conceitos Correlatos

### Conversão de Tipos (Type Casting)

- **Conversão Implícita:** Automática, quando não há perda de dados.
  ```csharp
  int a = 10;
  double b = a; // Conversão implícita de int para double
  ```
- **Conversão Explícita:** Requer intervenção do programador.
  ```csharp
  double c = 10.5;
  int d = (int)c; // Conversão explícita (perde a parte decimal)
  ```

### Tipos Genéricos

- Permitem criar classes e métodos que funcionam com qualquer tipo.
  ```csharp
  List<string> nomes = new List<string>();
  nomes.Add("Ana");
  ```

### Nullable Types

- Permitem que variáveis de tipos valor (como `int`) aceitem `null`.
  ```csharp
  int? valor = null; // "int?" é um nullable type
  ```

### Inferência de Tipos (`var`)

- O compilador infere o tipo da variável durante a compilação.
  ```csharp
  var mensagem = "Olá, mundo!"; // O compilador define como string
  ```
