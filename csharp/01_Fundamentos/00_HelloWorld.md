- Estrutura: 01_Fundamentos
- Seq: 00
- Título: HelloWorld

---

# 1. "Hello, World" em C#:

```csharp
using System;

class Hello
{
    static void Main()
    {
        Console.WriteLine("Hello, World");
    }
}
```

## 1.1 Diretiva `using` e Namespaces
- A linha `using System;` faz referência ao namespace `System`.
- **Namespaces** organizam bibliotecas e tipos em hierarquias.
- O namespace `System` contém vários tipos, incluindo a classe `Console`.

## 1.2 Classe `Hello`
- Em C#, o código deve estar contido dentro de uma **classe**.
- A classe `Hello` define um contêiner para o método `Main()`.

## 1.3 Método `Main()`
- O **método `Main()`** é o ponto de entrada de um programa em C#.
- Ele é declarado com o modificador `static`, o que significa que pode ser chamado sem criar uma instância de objeto.
- Por convenção, o método `Main()` é o primeiro a ser executado quando o programa é carregado.

## 1.4 Saída do Programa
- O comando `Console.WriteLine("Hello, World");` exibe a mensagem **"Hello, World"** no console.
- A classe `Console` pertence ao namespace `System` e fornece funcionalidades de entrada e saída.

---

# 2. Executando o Programa

Suponha que você tenha instalado o SDK do .NET e criado um arquivo chamado `HelloWorld.cs`. Você pode compilar e executar o programa com os seguintes comandos:

```bash
csc HelloWorld.cs  # Compila o código
HelloWorld.exe     # Executa o programa
```

Caso esteja utilizando o .NET Core, você pode rodar:

```bash
dotnet new console -o HelloWorld  # Cria um novo projeto console
cd HelloWorld
code .  # Abre o VS Code (opcional)
dotnet run  # Executa o programa
```

---
