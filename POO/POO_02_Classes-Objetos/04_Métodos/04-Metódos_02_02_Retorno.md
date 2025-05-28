# Métodos: Retorno de Valores

Métodos em C# podem ser divididos em duas categorias principais baseadas em seu comportamento de retorno:

1. Métodos que **retornam valores** (usam `return`)
2. Métodos que **não retornam valores** (usam `void`)

---

# Métodos com Retorno

Métodos com retorno são fundamentais na programação, permitindo reutilizar blocos de código que realizam cálculos ou produzem dados. Eles funcionam como **fábricas de valores**: recebem entradas (parâmetros), processam e devolvem um resultado para quem os chamou.

## **Estrutura Básica**

A estrutura de um método com retorno segue o seguinte formato:

```csharp
public TipoDeRetorno NomeDoMetodo(parâmetros)
{
    // Código a ser executado
    return valor; // Retorna algo do tipo especificado
}
```

1. **Tipo de retorno:** Define o tipo de dado que será devolvido (`int`, `string`, `bool`, etc.).
2. **Nome do método:** Identificador do método.
3. **Parâmetros:** Entradas que o método recebe (opcionais).
4. **`return` valor:** Finaliza a execução e retorna um resultado.

## **Exemplo Simples**

Aqui está um método que retorna a soma de dois números:

```csharp
public int Somar(int a, int b)
{
    return a + b;
}
```

### **Uso:**

```csharp
int resultado = Somar(3, 5);
Console.WriteLine(resultado); // Saída: 8
```

## **Tipos Comuns de Retorno**

### **1. Retorno numérico (`int`)**

```csharp
public int CalcularIdade(int anoNascimento)
{
    return DateTime.Now.Year - anoNascimento;
}
```

**Uso:**

```csharp
int idade = CalcularIdade(2000);
Console.WriteLine("Idade: " + idade);
```

### **2. Retorno textual (`string`)**

```csharp
public string CriarSaudacao(string nome)
{
    return $"Olá, {nome}!";
}
```

**Uso:**

```csharp
Console.WriteLine(CriarSaudacao("Ana")); // Saída: Olá, Ana!
```

### **3. Retorno booleano (`bool`)**

```csharp
public bool VerificarPar(int numero)
{
    return numero % 2 == 0;
}
```

**Uso:**

```csharp
if (VerificarPar(10))
{
    Console.WriteLine("Número é par.");
}
```

## **Boas Práticas**

- Sempre defina **claramente** o tipo de retorno do método.
- Certifique-se de que o valor retornado **corresponde** ao tipo declarado.
- **Evite retornos desnecessários**, simplificando a lógica.

---

# **Métodos sem Retorno (`void`)**

Métodos `void` são como **comandos**, pois realizam ações sem devolver um resultado. São usados para tarefas como exibir mensagens, modificar estados ou interagir com o usuário.

Se métodos com retorno funcionam como **calculadoras**, métodos `void` são como **operadores de máquinas**: realizam ações sem responder perguntas.

## **2. Estrutura Básica**

```csharp
public void NomeDoMetodo(parâmetros)
{
    // Código que executa a ação
}
```

- `void` indica **ausência de retorno**.
- O nome do método descreve sua ação.
- Pode ter **parâmetros** ou nenhum.
- O código dentro do método **executa a tarefa**.

## **Exemplo Simples**

```csharp
public void ExibirMensagem()
{
    Console.WriteLine("Bem-vindo ao sistema!");
}
```

```csharp
ExibirMensagem(); // Saída: "Bem-vindo ao sistema!"
```

## **Aplicações Comuns**

### **1. Exibir informações**

Métodos `void` são úteis para imprimir dados na tela.

```csharp
public void MostrarDataAtual()
{
    Console.WriteLine("Data: " + DateTime.Now.ToShortDateString());
}
```

```csharp
MostrarDataAtual(); // Exibe a data atual
```

### **2. Modificar estados**

Métodos podem **alterar variáveis globais** sem retornar valores.

```csharp
int contador = 0; // Variável global

public void IncrementarContador()
{
    contador++;
    Console.WriteLine($"Contador: {contador}");
}
```

```csharp
IncrementarContador(); // Contador: 1
IncrementarContador(); // Contador: 2
```

## **Retorno Implícito e Uso de `return;`**

### **Retorno implícito**

Métodos `void` **finalizam automaticamente** quando atingem `}`.

```csharp
public void Cumprimentar()
{
    Console.WriteLine("Olá, bem-vindo!");
} // Método termina aqui
```

### **Usando `return;` para sair antecipadamente**

Podemos encerrar um método `void` antes do final com `return;`.

```csharp
public void VerificarNumero(int numero)
{
    if (numero < 0)
    {
        Console.WriteLine("Número negativo detectado.");
        return; // Sai do método
    }

    Console.WriteLine("Número válido: " + numero);
}
```

```csharp
VerificarNumero(-3); // Saída: "Número negativo detectado."
VerificarNumero(10); // Saída: "Número válido: 10"
```

## **Boas Práticas**

- Nomeie métodos `void` como **ações** (`ExibirMensagem`, `SalvarDados`).
- Utilize `return;` para interromper execuções complexas.
- Evite cálculos em métodos `void`, prefira métodos **com retorno**.

---

# **Comparação: Métodos com Retorno vs Métodos `void` em C#**

- **Métodos com retorno**: Respondem a uma pergunta e devolvem um valor.
- **Métodos `void`**: Executam uma ação, mas não retornam nada.

Uma maneira fácil de lembrar:

- Métodos com retorno são como **calculadoras** (você fornece dados e recebe um resultado).
- Métodos `void` são como **comandos** (algo é feito, mas nenhum valor é devolvido).

A escolha entre métodos com retorno e métodos `void` depende do objetivo do código:

- Se **precisamos de um resultado**, usamos métodos **com retorno**.
- Se **apenas queremos executar uma ação**, usamos métodos **`void`**.

## **Comparação Geral**

| Característica | Métodos com Retorno | Métodos `void` |
| --- | --- | --- |
| **Retorna valor?** | Sim | Não |
| **Palavra-chave** | Tipo do retorno (`int`, `string`...) | `void` |
| **Uso principal** | Calcular valores | Executar ações |
| **Pode usar `return`?** | Sim (com valor) | Sim (sem valor) |

## **Formas de Retorno em Métodos**

### **1. Retorno Implícito (`void`)**

Métodos `void` **finalizam automaticamente** ao atingir `}`.

```csharp
public void Cumprimentar()
{
    Console.WriteLine("Olá!");
} // Método termina aqui
```

### **2. Retorno Explícito (`void`)**

Podemos usar `return;` para sair antecipadamente de um método `void`.

```csharp
public void VerificarLogin(bool estaLogado)
{
    if (!estaLogado)
    {
        Console.WriteLine("Faça login primeiro");
        return; // Sai do método antes do fim
    }

    Console.WriteLine("Bem-vindo!");
}
```

```csharp
VerificarLogin(false); // Saída: "Faça login primeiro"
VerificarLogin(true);  // Saída: "Bem-vindo!"
```

### **3. Retorno de Valor**

Métodos que **retornam um valor** precisam de um tipo de retorno e um `return` com valor.

```csharp
public int Dobro(int numero)
{
    return numero * 2;
}
```

```csharp
int resultado = Dobro(4); // resultado = 8
Console.WriteLine(resultado); // Saída: 8
```

## **Exemplos Comparativos**

### **1. Método `void` (Executa ação, não retorna)**

```csharp
public void ContarAteCinco()
{
    for (int i = 1; i <= 5; i++)
    {
        Console.WriteLine(i);
    }
}
```

**Uso:**

```csharp
ContarAteCinco();
// Saída:
// 1
// 2
// 3
// 4
// 5
```

**Por que esse método é `void`?**

1. **Não retorna nenhum valor** - Ele apenas **executa ações**.
2. **Não tem `return` com um valor** - Se tentássemos devolver `i`, daria erro.
3. **Sua função é "fazer" algo, não "responder" algo** - Ele imprime os números na tela, mas não fornece um valor utilizável.

### **2. Método com Retorno (Retorna valor)**

Agora, se quisermos armazenar os números de 1 a 5 em uma lista, precisaremos de um método **com retorno**:

```csharp
public List<int> GerarListaDeUmACinco()
{
    List<int> numeros = new List<int>();
    for (int i = 1; i <= 5; i++)
    {
        numeros.Add(i);
    }
    return numeros; // Retorna a lista
}
```

**Uso:**

```csharp
List<int> lista = GerarListaDeUmACinco();
Console.WriteLine(string.Join(", ", lista)); // Saída: 1, 2, 3, 4, 5
```

**Por que esse método NÃO poderia ser `void`?**

1. **Ele retorna um valor (`List<int>`)**, que precisa ser capturado pelo código.
2. **A informação gerada precisa ser reutilizada**, não apenas exibida na tela.

## **6. Boas Práticas**

- Use **verbos** para nomear métodos `void` (`ExibirMensagem`, `SalvarDados`).
- Use **substantivos** para nomear métodos com retorno (`GerarLista`, `ObterNome`).
- Evite misturar **execução de ação** e **cálculo de valores** no mesmo método.
- **Mantenha métodos curtos**, cada um deve ter **um único propósito**.

---

# **Retorno de Múltiplos Valores (Tuplas) em C#**

Em muitas linguagens de programação, uma função normalmente retorna **um único valor**. Entretanto, **C#** possui uma maneira conveniente de **retornar múltiplos valores** sem a necessidade de criar uma classe ou uma estrutura específica. Isso é feito através de **Tuplas**.

## 🔹 **O Que São Tuplas?**

Tuplas são um tipo de estrutura de dados que permite **agrupamento de múltiplos valores** em um único objeto. Com elas, podemos retornar **mais de um valor** a partir de um método sem precisar criar uma classe.

## **Sintaxe Básica de uma Tupla**

A definição de uma tupla segue o formato:

```csharp
(tipo1, tipo2, ...) NomeDaTupla = (valor1, valor2, ...);
```

Ou seja, podemos armazenar múltiplos valores de **tipos diferentes** dentro de uma tupla.

## **Retornando Múltiplos Valores em um Método**

Imagine que precisamos retornar **um nome** e **uma idade** a partir de um método. Sem tuplas, precisaríamos criar uma classe para armazenar esses valores. Com tuplas, isso se torna muito mais simples:

```csharp
(string, int) ObterDados()
{
    return ("Maria", 28);
}

var dados = ObterDados();
Console.WriteLine($"Nome: {dados.Item1}, Idade: {dados.Item2}");
// Saída: Nome: Maria, Idade: 28
```

1. O método `ObterDados()` retorna **uma tupla contendo uma string e um inteiro**.
2. Ao chamar `ObterDados()`, recebemos essa tupla e acessamos os valores com `Item1` (nome) e `Item2` (idade).

## **Nomeando os Elementos da Tupla**

Em vez de usar `Item1` e `Item2`, podemos **nomear os elementos** para tornar o código mais legível:

```csharp
(string nome, int idade) ObterDados()
{
    return ("Maria", 28);
}

var dados = ObterDados();
Console.WriteLine($"Nome: {dados.nome}, Idade: {dados.idade}");
// Saída: Nome: Maria, Idade: 28
```

Agora, acessamos os valores **pelos nomes** (`dados.nome` e `dados.idade`), tornando o código mais intuitivo.

## **Usando Tuplas como Parâmetros**

Além de **retornar** tuplas, também podemos usá-las como **parâmetros** em métodos:

```csharp
void ExibirDados((string nome, int idade) pessoa)
{
    Console.WriteLine($"Nome: {pessoa.nome}, Idade: {pessoa.idade}");
}

var dados = ("Carlos", 35);
ExibirDados(dados);
// Saída: Nome: Carlos, Idade: 35
```

Aqui, o método `ExibirDados()` recebe **uma tupla como argumento**.

---
