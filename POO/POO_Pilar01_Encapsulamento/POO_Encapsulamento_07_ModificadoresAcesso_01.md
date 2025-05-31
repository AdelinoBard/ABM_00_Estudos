# Diferenças entre `public` e `private` em C#

- `public`: Acessível de qualquer lugar, usado para métodos e propriedades que devem ser expostos publicamente.
- `private`: Acessível apenas dentro da classe, essencial para proteção de dados e boas práticas de encapsulamento.

> Para um código bem estruturado, é sempre recomendado usar `private` e fornecer métodos públicos para manipulação segura dos dados.

## 1. **Membros `public`**

Os membros marcados como `public` são acessíveis de qualquer lugar onde houver uma referência ao objeto. Isso significa que qualquer classe pode interagir diretamente com esses membros, facilitando o compartilhamento de informações.

### Exemplo Simples:

```csharp
public class MinhaClasse
{
    public int MeuNumero; // Pode ser acessado diretamente

    public void MostrarNumero()
    {
        Console.WriteLine(MeuNumero);
    }
}

class Program
{
    static void Main()
    {
        MinhaClasse obj = new MinhaClasse();
        obj.MeuNumero = 10; // Acessível
        obj.MostrarNumero(); // Acessível
    }
}
```

- **Explicação:** Como `MeuNumero` é `public`, qualquer classe pode modificar e acessar seu valor diretamente. O método `MostrarNumero` também é acessível externamente.

## 2. **Membros `private`**

Os membros `private` são acessíveis **apenas** dentro da própria classe, impedindo que outras classes os utilizem diretamente. Isso ajuda a encapsular informações e proteger dados sensíveis.

### Exemplo Simples:

```csharp
public class MinhaClasse
{
    private int MeuNumero; // Não pode ser acessado diretamente

    public void DefinirNumero(int numero)
    {
        MeuNumero = numero; // Modificando um membro privado dentro da própria classe
    }

    public void MostrarNumero()
    {
        Console.WriteLine(MeuNumero);
    }
}

class Program
{
    static void Main()
    {
        MinhaClasse obj = new MinhaClasse();
        // obj.MeuNumero = 10; // ❌ Erro: Não acessível diretamente
        obj.DefinirNumero(10); // ✅ Acessível através de um método público
        obj.MostrarNumero(); // ✅ Acessível
    }
}
```

- **Explicação:** O atributo `MeuNumero` é privado e **não pode** ser acessado diretamente fora da classe. No entanto, métodos públicos (`DefinirNumero` e `MostrarNumero`) permitem modificar e exibir seu valor de forma controlada.

## 3. **Encapsulamento e Boas Práticas**

Ao usar `private`, garantimos que os dados de uma classe **não podem ser alterados arbitrariamente**, prevenindo erros. A melhor abordagem é:

- **Manter os atributos privados** e acessá-los apenas por **métodos públicos** (getter/setter).
- **Evitar acesso direto a atributos públicos**, pois pode levar a inconsistências.

### Exemplo com Propriedades (Getter e Setter):

```csharp
public class Pessoa
{
    private string nome;

    public string Nome
    {
        get { return nome; } // Recuperar valor
        set { nome = value; } // Definir valor
    }
}

class Program
{
    static void Main()
    {
        Pessoa pessoa = new Pessoa();
        pessoa.Nome = "Alice"; // ✅ Acessível via propriedade
        Console.WriteLine(pessoa.Nome); // ✅ Acessível via propriedade
    }
}
```

- **Explicação:** Em vez de acessar diretamente um atributo público, usamos uma **propriedade** para controlar seu acesso, seguindo o princípio de encapsulamento.

---
