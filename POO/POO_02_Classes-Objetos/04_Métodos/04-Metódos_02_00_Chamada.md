# Métodos: Pilha de Chamadas e Registros de Ativação

## 1. O que é uma Pilha?

Uma **pilha** é uma estrutura de dados que segue o princípio **LIFO** (_Last In, First Out_ - último a entrar, primeiro a sair). Podemos compará-la a uma pilha de pratos:

- **Empurrar (Push)**: Adiciona um prato no topo da pilha.
- **Retirar (Pop)**: Remove o prato do topo da pilha.

### Exemplo Simples de Pilha em C#:

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        Stack<int> pilha = new Stack<int>();

        pilha.Push(1); // Empurra 1
        pilha.Push(2); // Empurra 2
        pilha.Push(3); // Empurra 3

        Console.WriteLine(pilha.Pop()); // Retira 3 (último a entrar)
        Console.WriteLine(pilha.Pop()); // Retira 2
    }
}
```

Esse comportamento **LIFO** é essencial para entender a pilha de chamadas de método.

## 2. O que é a Pilha de Chamadas de Método?

A **pilha de chamadas de método** é uma estrutura usada pelo C# para gerenciar a execução de métodos em um programa. Cada vez que um método é chamado:

1. Um **registro de ativação** (chamado de _stack frame_) é criado na pilha.
2. O registro contém:
   - Parâmetros do método.
   - Variáveis locais.
   - O endereço de retorno (onde o programa deve continuar após o método terminar).
3. O registro é **empurrado** para a pilha.
4. Quando o método termina, o registro é **retirado** da pilha, e o fluxo retorna ao método chamador.

## 3. Funcionamento da Pilha de Chamadas em C#

Considere um programa simples:

```csharp
using System;

class Program
{
    static void Main()
    {
        MetodoA();
    }

    static void MetodoA()
    {
        MetodoB();
    }

    static void MetodoB()
    {
        Console.WriteLine("Executando Método B");
    }
}
```

### Fluxo da Pilha:

1. `Main()` é chamado → **Empurrado** para a pilha.
2. `Main()` chama `MetodoA()` → `MetodoA()` é **empurrado** para a pilha.
3. `MetodoA()` chama `MetodoB()` → `MetodoB()` é **empurrado** para a pilha.
4. `MetodoB()` executa e termina → **Retirado** da pilha.
5. `MetodoA()` termina → **Retirado** da pilha.
6. `Main()` termina → **Retirado** da pilha.

A pilha sempre mantém a ordem correta de execução, garantindo que o controle retorne ao método chamador após a conclusão da chamada.

## 4. Registros de Ativação em Detalhe

Cada **registro de ativação** na pilha contém:

- **Parâmetros do método** (valores passados para o método).
- **Variáveis locais** (criadas dentro do método).
- **Endereço de retorno** (para onde ir depois que o método termina).

Exemplo:

```csharp
using System;

class Program
{
    static void Main()
    {
        int resultado = Soma(3, 7);
        Console.WriteLine(resultado);
    }

    static int Soma(int a, int b)
    {
        return a + b;
    }
}
```

Durante a chamada de `Soma(3,7)`, a pilha conterá:

| Endereço | Variável | Valor |
| -------- | -------- | ----- |
| ...      | ...      | ...   |
| 0x100    | a        | 3     |
| 0x104    | b        | 7     |

Quando `Soma()` terminar, suas variáveis locais são **removidas** da pilha.

## 5. Importância e Limitações da Pilha

A pilha de chamadas é essencial porque:

- **Gerencia escopo**: Variáveis locais existem apenas enquanto o método está na pilha.
- **Controla o fluxo**: Mantém o rastro de onde retornar após cada método.
- **Suporta recursão**: Métodos podem chamar a si mesmos.

### Atenção: Estouro de Pilha (_Stack Overflow_)

A pilha tem **tamanho limitado**. Se muitos métodos forem empilhados sem serem retirados, um erro **Stack Overflow** pode ocorrer, geralmente causado por **recursão infinita**:

```csharp
void Recursao()
{
    Recursao(); // Chamando a si mesmo infinitamente
}
```

Isso fará com que a pilha cresça indefinidamente, levando ao erro.

---
