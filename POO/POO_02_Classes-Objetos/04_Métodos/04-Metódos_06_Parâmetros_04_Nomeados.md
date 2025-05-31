# Métodos: Parâmetros

## **4. Parâmetros Nomeados**

Em C#, ao chamar métodos, geralmente fornecemos argumentos na ordem em que os parâmetros foram definidos. No entanto, o recurso de **parâmetros nomeados** permite especificar argumentos explicitamente, independentemente da ordem. Isso melhora a legibilidade e evita erros relacionados à posição dos argumentos.

## **1. Chamada Tradicional vs. Parâmetros Nomeados**

Por padrão, ao chamar um método, os argumentos são atribuídos na ordem da esquerda para a direita:

```csharp
void Apresentar(string nome, int idade)
{
    Console.WriteLine($"{nome} tem {idade} anos.");
}

// Chamada tradicional (por posição)
Apresentar("Carlos", 30); // Saída: Carlos tem 30 anos.
```

No exemplo acima, a ordem dos argumentos é crucial. Se forem invertidos, pode ocorrer um erro ou um resultado inesperado.

Agora, utilizando **parâmetros nomeados**, podemos alterar a ordem sem impactar o funcionamento:

```csharp
Apresentar(idade: 30, nome: "Carlos"); // Saída: Carlos tem 30 anos.
```

Aqui, informamos explicitamente quais valores pertencem a quais parâmetros, tornando o código mais claro.

## **2. Benefícios dos Parâmetros Nomeados**

Os parâmetros nomeados são úteis em várias situações, como:

- Melhor legibilidade em chamadas de métodos com muitos argumentos.
- Evitar confusão ao lidar com parâmetros opcionais.
- Permitir a omissão de argumentos não necessários quando usados junto com **valores padrão**.

Exemplo prático:

```csharp
void RegistrarAluno(string nome, int idade, bool matriculado = true)
{
    Console.WriteLine($"{nome}, idade {idade}, matrícula: {matriculado}");
}

// Chamada tradicional
RegistrarAluno("Maria", 20); // Saída: Maria, idade 20, matrícula: True

// Com parâmetros nomeados e alterando a ordem
RegistrarAluno(idade: 22, nome: "Pedro", matriculado: false);
// Saída: Pedro, idade 22, matrícula: False
```

## **3. Parâmetros Nomeados com Valores Padrão**

Se um método possui **valores padrão** nos parâmetros, podemos optar por informar apenas aqueles que desejamos alterar. Por exemplo:

```csharp
void ConfigurarHora(int hora = 0, int minuto = 0, int segundo = 0)
{
    Console.WriteLine($"Hora configurada: {hora}:{minuto}:{segundo}");
}

// Sem argumentos, usa valores padrão
ConfigurarHora(); // Saída: Hora configurada: 0:0:0

// Apenas define a hora
ConfigurarHora(hora: 12); // Saída: Hora configurada: 12:0:0

// Define a hora e os segundos, mantendo o valor padrão do minuto
ConfigurarHora(hora: 12, segundo: 30); // Saída: Hora configurada: 12:0:30
```

Como o C# não permite que pulamos um argumento sem usar parâmetros nomeados (`ConfigurarHora(12, , 30);` resulta em erro), a melhor prática é especificar explicitamente os nomes dos parâmetros.

---
