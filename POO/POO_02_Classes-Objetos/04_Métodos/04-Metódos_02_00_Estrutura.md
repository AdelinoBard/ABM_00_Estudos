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

1. **Nomes claros**: O nome do método deve indicar claramente sua função

   - Bom: `CalcularImposto()`
   - Ruim: `FazCoisa()`

2. **Coesão**: Cada método deve ter uma única responsabilidade

   - Ruim: `ProcessarPedidoEEnviarEmail()`
   - Bom: `ProcessarPedido()` + `EnviarEmailConfirmacao()`

3. **Evite muitos parâmetros**: Se precisa de muitos, considere usar um objeto

   - Ruim: `CriarUsuario(string nome, string email, string telefone, DateTime nascimento, ...)`
   - Bom: `CriarUsuario(UsuarioDTO dados)`

4. **Tratamento de erros**: Considere validar entradas importantes

   ```csharp
   public void Depositar(decimal valor)
   {
       if (valor <= 0)
           throw new ArgumentException("Valor deve ser positivo");

       // Resto da implementação
   }
   ```

---

# **Sintaxe Simplificada no C# 6+: Expressões de Corpo Único (`=>`)**

O C# 6 introduziu uma sintaxe mais **concisa e legível** para a definição de métodos e propriedades. Essa abordagem, conhecida como **expressão de corpo único (`=>`)**, torna o código mais enxuto ao eliminar a necessidade de blocos `{}` e `return` explícito.

Esta sintaxe é especialmente útil para:

- Métodos que possuem **apenas uma única operação**.
- Propriedades de **somente leitura**, cujo `get` retorna uma expressão simples.

## **Métodos com Corpo de Expressão (`=>`)**

Se um método retorna o resultado de **uma única operação**, ele pode ser escrito usando **expressões de corpo único**.

### **Forma tradicional**

```csharp
public int Quadrado(int x)
{
    return x * x;
}
```

### **Forma simplificada**

```csharp
public int Quadrado(int x) => x * x;
```

🔹 Ambos os métodos produzem o mesmo resultado.  
🔹 A versão simplificada **elimina** `{}` e `return`, melhorando a legibilidade.  
🔹 O operador `=>` substitui `return` automaticamente quando há **apenas uma expressão**.

## **Propriedades Somente Leitura com Corpo de Expressão**

Propriedades **somente leitura** que retornam uma **expressão simples** também podem ser simplificadas.

### **Forma tradicional**

```csharp
public bool IsAdult
{
    get { return idade >= 18; }
}
```

### **Forma simplificada**

```csharp
public bool IsAdult => idade >= 18;
```

🔹 Elimina a necessidade do bloco `get { return ... }`.  
🔹 Garante um código **mais enxuto e limpo**.

---

## **Exemplos Práticos**

### **Método que retorna o cubo de um número**

```csharp
public int Cube(int x) => x * x * x;
```

**Uso:**

```csharp
int resultado = Cube(3); // resultado = 27
Console.WriteLine(resultado);
```

### **Propriedade que verifica se um estado tem seguro obrigatório**

```csharp
public bool IsNoFaultState =>
   State == "MA" || State == "NJ" || State == "NY" || State == "PA";
```

🔹 Retorna `true` se o estado estiver na lista, caso contrário `false`.

### **Método `void` com Corpo de Expressão**

Se um método **não retorna um valor**, a sintaxe também pode ser aplicada:

```csharp
public void MostrarMensagem() => Console.WriteLine("Olá, bem-vindo!");
```

**Uso:**

```csharp
MostrarMensagem(); // Saída: Olá, bem-vindo!
```

## **Benefícios da Sintaxe Simplificada**

- **Código mais enxuto** – elimina blocos desnecessários.
- **Facilidade de leitura** – o objetivo do método fica mais claro.
- **Ideal para métodos simples** – reduz repetição e melhora organização.

---
