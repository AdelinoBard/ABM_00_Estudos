# Métodos de Extensão em C#

Métodos de extensão em C# são um recurso poderoso que permite "adicionar" métodos a tipos existentes sem precisar:

- Modificar o código original do tipo
- Criar uma nova classe derivada
- Recompilar o assembly onde o tipo está definido

Eles são especialmente úteis para estender funcionalidades de:

- Classes da biblioteca padrão do .NET (como `string`, `int`, `DateTime`)
- Interfaces
- Classes de terceiros onde você não tem acesso ao código-fonte
- Seus próprios tipos para manter a organização do código

## Sintaxe Básica

Para criar um método de extensão, você precisa:

1. Criar uma classe **estática** (static) para conter seus métodos de extensão
2. Definir métodos **estáticos** dentro desta classe
3. O primeiro parâmetro do método deve usar a palavra-chave `this` seguida do tipo que você está estendendo

```csharp
public static class MinhasExtensoes
{
    public static int ContarPalavras(this string str)
    {
        if (string.IsNullOrEmpty(str))
            return 0;

        return str.Split(new[] {' '}, StringSplitOptions.RemoveEmptyEntries).Length;
    }
}
```

## Como Usar

Uma vez definido, o método de extensão aparece como um método de instância do tipo estendido:

```csharp
string texto = "Métodos de extensão em C#";
int contagem = texto.ContarPalavras(); // Retorna 4
```

## Características Importantes

1. **Descoberta Inteligente**: Aparecem no IntelliSense do Visual Studio com um ícone de extensão (↓)
2. **Escopo**: Só estão disponíveis quando o namespace que os contém está em uso com `using`
3. **Precedência**: Têm menor prioridade que métodos de instância reais
4. **Herança**: Funcionam com a hierarquia de herança - um método de extensão para uma classe base estará disponível para classes derivadas

## Exemplos Avançados

### Extendendo Interfaces

```csharp
public static class IEnumerableExtensions
{
    public static IEnumerable<T> MeuWhere<T>(this IEnumerable<T> source, Func<T, bool> predicate)
    {
        foreach (var item in source)
        {
            if (predicate(item))
                yield return item;
        }
    }
}
```

### Métodos com Parâmetros Adicionais

```csharp
public static class DateTimeExtensions
{
    public static bool EstaEntre(this DateTime data, DateTime inicio, DateTime fim)
    {
        return data >= inicio && data <= fim;
    }
}

// Uso:
DateTime hoje = DateTime.Now;
bool estaNoIntervalo = hoje.EstaEntre(DateTime.Today, DateTime.Today.AddDays(7));
```

### Encadeamento de Métodos

```csharp
public static class StringExtensions
{
    public static string RemoverEspacos(this string str)
    {
        return str.Replace(" ", "");
    }

    public static string ConverterParaMaiusculas(this string str)
    {
        return str.ToUpper();
    }
}

// Uso encadeado:
string resultado = " texto exemplo ".RemoverEspacos().ConverterParaMaiusculas();
```

## Boas Práticas

1. **Nomes Descritivos**: Use nomes que indiquem claramente a funcionalidade
2. **Namespaces Organizados**: Agrupe métodos relacionados em namespaces lógicos
3. **Documentação**: Comente seus métodos de extensão como faria com métodos normais
4. **Moderação**: Não sobrecarregue tipos com muitos métodos de extensão
5. **Performance**: Evite operações custosas em métodos de extensão frequentemente chamados

## Limitações

- Não podem acessar membros privados/protegidos do tipo que estão estendendo
- Não podem substituir métodos existentes (só complementar)
- Se um método com mesma assinatura for adicionado ao tipo original, o método de extensão não será mais chamado

## Casos de Uso Comuns

1. **Utilidades para strings**: Formatação, parsing, validação
2. **Operações matemáticas**: Métodos úteis para tipos numéricos
3. **Manipulação de coleções**: Operações adicionais em `IEnumerable<T>`
4. **Conversões**: Entre tipos diferentes
5. **Sintaxe fluente**: Para criar APIs mais legíveis

## Exemplo Completo

```csharp
using System;
using System.Collections.Generic;

namespace Extensoes
{
    public static class ColecaoExtensoes
    {
        // Método de extensão para qualquer IEnumerable<T>
        public static void ParaCada<T>(this IEnumerable<T> colecao, Action<T> acao)
        {
            foreach (var item in colecao)
            {
                acao(item);
            }
        }

        // Método de extensão para List<int>
        public static double Media(this List<int> numeros)
        {
            if (numeros == null || numeros.Count == 0)
                throw new InvalidOperationException("Lista vazia");

            double soma = 0;
            numeros.ParaCada(n => soma += n);
            return soma / numeros.Count;
        }
    }

    class Program
    {
        static void Main()
        {
            var numeros = new List<int> { 1, 2, 3, 4, 5 };

            // Usando ambos métodos de extensão
            numeros.ParaCada(n => Console.WriteLine(n));
            Console.WriteLine($"Média: {numeros.Media()}");
        }
    }
}
```

## Considerações Finais

Métodos de extensão são uma ferramenta poderosa no C# que permitem:

- Escrever código mais expressivo e legível
- Adicionar funcionalidades a tipos existentes sem modificá-los
- Criar APIs fluentes e intuitivas
- Organizar código utilitário de forma coesa

Porém, devem ser usados com critério para não poluir namespaces ou criar confusão na arquitetura do código. Quando bem aplicados, podem significativamente melhorar a produtividade e a clareza do código.

---
