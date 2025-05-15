## **Estrutura Básica de um Método em C#**

Um método em C# possui a seguinte sintaxe:

```csharp
[modificador de acesso] [tipo de retorno] NomeDoMetodo([parâmetros])
{
    // Corpo do método
}
```

### **Componentes**

- **Modificador de acesso**: Define a visibilidade (`public`, `private`, `protected`, etc.).
- **Tipo de retorno**: O tipo do valor retornado (`void` se não retornar nada).
- **Nome do método**: Segue **PascalCase** (convenção do C#). Ex: `CalcularSalario()`.
- **Parâmetros**: Dados de entrada (opcionais). Ex: `(string nome, int idade)`.
- **Corpo do método**: Bloco de código que executa a lógica.

### **Exemplo Prático**

```csharp
public int Somar(int a, int b)
{
    return a + b;
}
```

## **Convenção de Nomenclatura**

Em C#, os métodos devem seguir o padrão **PascalCase** (não CamelCase, que é usado para variáveis e parâmetros).

- **Correto**:

```csharp
public void ImprimirDetalhes() { ... }
```

- **Incorreto**:

```csharp
public void imprirDetalhes() { ... } // camelCase é para parâmetros/variáveis
```

## **Boas Práticas**

- **Nomes descritivos**: Use verbos para indicar ações (`CalcularTotal`, `ValidarSenha`).
- **Responsabilidade única**: Cada método deve fazer **uma única tarefa**.
- **Evite métodos longos**: Se ultrapassar 20 linhas, considere dividi-lo.
- **Documentação**: Use XML comments para explicar o propósito.
