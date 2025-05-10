# Valores Padrão

Em linguagens de programação orientadas a objetos, como C#, os atributos de uma classe são inicializados com valores padrão se não forem explicitamente inicializados pelo programador. Esta característica garante que os atributos tenham valores definidos mesmo antes de serem atribuídos explicitamente.

## 2. Valores Padrão dos Atributos

- **Atributos de tipos numéricos** (como `int`, `float`, `double`) são inicializados com `0`.
- **Atributos do tipo `boolean`** são inicializados com `false`.
- **Atributos de tipos de referência** (como `string` e objetos) são inicializados com `null`.

A inicialização dos atributos com valores padrão ocorre no momento da instanciação, ou seja, quando o comando `new` é utilizado. Dessa forma, todo objeto é criado com valores padrão atribuídos aos seus atributos.

## 3. Exemplo em C#

```csharp
class Conta
{
    public double limite;
}

class TestaConta
{
    static void Main(string[] args)
    {
        Conta conta = new Conta();

        // Imprime 0, que é o valor padrão de um double
        Console.WriteLine(conta.limite);
    }
}
```

No exemplo acima, o atributo `limite` é automaticamente inicializado com `0`, que é o valor padrão para tipos numéricos em C#.

## 4. Inicializando Atributos com Valores Diferentes

Em alguns casos, é necessário substituir os valores padrão. Para alterar o valor padrão de um atributo, podemos inicializá-lo na sua declaração. Por exemplo, suponha que o limite padrão das contas de um banco seja R$ 500. Podemos definir esse valor como padrão para o atributo `limite`.

```csharp
class Conta
{
    public double limite = 500;
}

class TestaConta
{
    static void Main(string[] args)
    {
        Conta conta = new Conta();

        // Imprime 500
        Console.WriteLine(conta.limite);
    }
}
```

Neste exemplo, o atributo `limite` é inicializado com `500`, que será o valor padrão atribuído quando um novo objeto `Conta` for criado.

## 5. Conceitos Correlatos

- **Construtores**: Métodos especiais usados para inicializar objetos.
- **Sobrecarga de Construtores**: Definir múltiplos construtores com diferentes parâmetros.
- **Encapsulamento**: Prática de restringir o acesso direto a alguns dos componentes de um objeto.
