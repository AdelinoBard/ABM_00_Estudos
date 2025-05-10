# Atributos

Atributos em C# representam **propriedades ou características** dos objetos, que são armazenadas como variáveis dentro da classe que define o objeto.

- **Um atributo é uma variável que pertence a um objeto.**
- **Os dados de um objeto são armazenados nos seus atributos.**

Esses atributos são essenciais para guardar informações relevantes ao domínio da aplicação.

No exemplo abaixo, a classe `Cliente` possui três atributos: `Nome`, `DataDeNascimento`, e `Sexo`. Cada um desses atributos é uma propriedade da classe que encapsula os dados do cliente.

```csharp
public class Cliente
{
    public string Nome { get; set; }
    public DateTime DataDeNascimento { get; set; }
    public string Sexo { get; set; }
}
```

## Detalhes importantes

1. **Propriedades com get/set**:

- A declaração `public string Nome { get; set; }` utiliza propriedades automáticas para definir os atributos.
- O `get` permite acessar o valor da propriedade, e o `set` permite atribuir um valor.
- É uma forma mais moderna e prática de gerenciar atributos, sem necessidade de declarar explicitamente campos privados.

2. **Modificadores de acesso**:

- Você pode controlar o acesso aos atributos usando modificadores como `public`, `private`, `protected`, entre outros. Por exemplo:

```csharp
private string Nome;
public string GetNome() { return Nome; }
public void SetNome(string nome) { Nome = nome; }
```

Nesse caso, o atributo é protegido por um encapsulamento mais rigoroso.

3. **Tipos de dados**:

- Atributos podem ser de vários tipos de dados: primitivos (`int`, `float`, `bool`), objetos (`DateTime`, `string`), ou até mesmo coleções (`List<T>`, `Array`).

4. **Validação e lógica**:

- Você pode incluir lógica e validação nos métodos `get` e `set`. Por exemplo:

```csharp
private DateTime dataDeNascimento;
public DateTime DataDeNascimento
    {
        get { return dataDeNascimento; }
        set
        {
            if (value > DateTime.Now)
                throw new ArgumentException("Data de nascimento não pode ser no futuro.");
                dataDeNascimento = value;
        }
    }
```

5. **Atributos estáticos**:

- Se um atributo pertence à classe em vez de aos objetos individuais, você pode declará-lo como `static`. Por exemplo:

```csharp
public static string Empresa = "Exemplo Corp.";
```
