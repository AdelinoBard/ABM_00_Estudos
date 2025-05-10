# A Classe `Object` no .NET

Na programação, os objetos são fundamentais para modelar e representar entidades do mundo real. No contexto do .NET Framework, todos os tipos de dados são herdados direta ou indiretamente da classe `Object`. Essa classe é a raiz da hierarquia de tipos e, portanto, é possível converter qualquer tipo para `Object`.

## Boxing e Unboxing

1. **Boxing**:

- O termo "boxing" refere-se ao processo de converter uma variável de um tipo de valor (value type) para um objeto do tipo `Object`.

- Quando fazemos boxing, estamos essencialmente empacotando o valor em um objeto.

- **Boxing:** Conversão de um tipo de valor (ex: `int`) para `object`.

2. **Unboxing**:

- O termo "unboxing" é usado quando queremos extrair o valor de um objeto (do tipo `Object`) e convertê-lo de volta para um tipo de valor.

- Isso é necessário quando queremos usar o valor original em operações específicas.

- **Unboxing:** Conversão de volta para o tipo original.

3. **Exemplo:**

```csharp
int valor = 42;
object boxed = valor;   // Boxing
int unboxed = (int)boxed; // Unboxing
```

## Métodos Úteis da Classe `Object`

A classe `Object` é a base para todos os tipos no .NET Framework. Ela fornece alguns métodos e propriedades comuns a todos os objetos, como:

- `ToString()`: Retorna uma representação em string.
- `Equals()`: Compara objetos.
- `GetType()`: Retorna o tipo do objeto.
- `GetHashCode()`: Retorna um código hash para o objeto.

**Exemplo:**

```csharp
object texto = "Hello";
Console.WriteLine(texto.GetType()); // Saída: System.String
```
