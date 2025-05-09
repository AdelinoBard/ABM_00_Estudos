# Variáveis: Escopo de Bloco

O escopo de bloco refere-se à região do código onde uma variável pode ser acessada. Em C#, variáveis declaradas dentro de blocos (como `if`, `for`, `while`, etc.) só são visíveis dentro desses blocos.

> **Variáveis locais de bloco**

## Definição e Características

- **Variáveis Locais de Bloco**: São declaradas dentro de um bloco de código.

- **Escopo**: Restrita ao bloco onde foram criadas.

- **Persistência**: Existem apenas enquanto o bloco está em execução. São criadas quando o bloco começa a ser executado e destruídas quando termina.

## Exemplos Práticos

```csharp
if (true)
{
    int numero = 10; // Variável de bloco
    Console.WriteLine(numero); // Funciona
}
// Console.WriteLine(numero); // Erro: 'numero' não existe aqui
```

**Exemplo de Má Prática:**

```csharp
void ExemploRuim()
{
    int x = 5;
    if (true)
    {
        int x = 10; // Erro: Variável 'x' já declarada no escopo superior
    }
}
```

**Exemplo: Bloco `if`**

```csharp
void VerificarIdade(int idade)
{
    if (idade >= 18)
    {
        string mensagem = "Maior de idade"; // Variável de bloco
        Console.WriteLine(mensagem);
    }
    // Console.WriteLine(mensagem); // Erro: 'mensagem' não existe aqui
}
```

**Exemplo: Bloco `for`**

Em loops como `for`, a variável de iteração tem escopo restrito ao loop.

```csharp
void Contar()
{
    for (int i = 0; i < 3; i++) // 'i' é uma variável de bloco
    {
        Console.WriteLine(i);
    }
    // Console.WriteLine(i); // Erro: 'i' não existe aqui
}
```

```csharp
void LoopExemplo()
{
    for (int j = 0; j < 2; j++)
    {
        Console.WriteLine(j);
    }
    // j não está acessível aqui
}
```

## Limitações e Boas Práticas

- **Evite repetição**: Não declare a mesma variável em blocos aninhados se não for necessário.

- **Organização**: Use nomes claros para variáveis de bloco, já que seu escopo é limitado.

## Conceitos Correlatos

### Escopo de Método

Variáveis declaradas dentro de um método são acessíveis apenas dentro dele.

### Escopo Global (Classe)

Variáveis declaradas em nível de classe podem ser acessadas por todos os métodos da classe.
