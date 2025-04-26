# Estruturas de Controle em C#

## Execução Sequencial e Transferência de Controle

Normalmente, as instruções em um programa são executadas uma após a outra, na ordem em que são escritas. Esse processo é chamado de **execução sequencial**. No entanto, em muitos casos, é necessário alterar o fluxo de execução do programa, desviando para diferentes partes do código com base em condições específicas. Isso é conhecido como **transferência de controle**.

## A Evolução da Programação Estruturada

Na década de 1960, o uso indiscriminado de transferências de controle, especialmente com a instrução `goto`, causava dificuldades no desenvolvimento de software. A pesquisa de Bohm e Jacopini[^1] mostrou que todos os programas poderiam ser escritos sem o uso de `goto`, utilizando apenas três estruturas de controle: **sequência**, **seleção** e **iteração**. Essa abordagem, conhecida como **programação estruturada**, trouxe benefícios significativos, como programas mais claros, fáceis de depurar e modificar, e com menos bugs.

[^1]: C. Bohm e G. Jacopini, “Diagramas de fluxo, máquinas de Turing e linguagens com apenas duas regras de formação”, _Communications of the ACM_, Vol. 9, No. 5, maio de 1966, pp. 336–371.

## 1. Estrutura de Sequência _sequence_

> **Algoritmos Sequenciais (Lineares):**

A **estrutura de sequência** é a mais simples e básica. Nela, as instruções são executadas na ordem em que aparecem no código, sem desvios ou repetições. Essa estrutura é adequada para tarefas simples e diretas.

**Exemplo:**

```csharp
int a = 5;
int b = 10;
int soma = a + b;
Console.WriteLine(soma); // Saída: 15
```

## 2. Estrutura de Seleção (Decisão) _selection_

> **Algoritmos com Seleção/Decisão:**

As **estruturas de seleção** permitem que o programa tome decisões com base em condições. Dependendo do valor de uma expressão booleana, o programa pode escolher entre diferentes caminhos de execução.

### Tipos de Estruturas de Seleção em C#

- **Instrução `if`:** Executa um bloco de código se uma condição for verdadeira.

  ```csharp
  if (idade >= 18)
  {
      Console.WriteLine("Você é maior de idade.");
  }
  ```

- **Instrução `if...else`:** Executa um bloco de código se a condição for verdadeira e outro bloco se for falsa.

  ```csharp
  if (altura >= 1.50)
  {
      Console.WriteLine("Acesso permitido ao brinquedo.");
  }
  else
  {
      Console.WriteLine("Acesso negado.");
  }
  ```

- **Instrução `switch`:** Permite selecionar entre múltiplos blocos de código com base no valor de uma expressão.
  ```csharp
  switch (diaDaSemana)
  {
      case 1:
          Console.WriteLine("Domingo");
          break;
      case 2:
          Console.WriteLine("Segunda-feira");
          break;
      // ...
      default:
          Console.WriteLine("Dia inválido");
          break;
  }
  ```

## 3. Estrutura de Iteração (Repetição) _iteration_

> **Algoritmos com Repetição:**

As **estruturas de iteração** permitem que um bloco de código seja executado repetidamente enquanto uma condição for verdadeira (chamada de **condição de continuação de loop**). Isso é útil para tarefas que precisam ser repetidas várias vezes, como processar listas de dados ou gerar sequências.

### Tipos de Estruturas de Iteração em C#

- **Instrução `while`:** Executa um bloco de código enquanto uma condição for verdadeira. O bloco pode não ser executado nenhuma vez se a condição for falsa desde o início.

  ```csharp
  int contador = 0;
  while (contador < 5)
  {
      Console.WriteLine(contador);
      contador++;
  }
  ```

- **Instrução `do...while`:** Semelhante ao `while`, mas o bloco de código é executado pelo menos uma vez, mesmo que a condição seja falsa.

  ```csharp
  int contador = 0;
  do
  {
      Console.WriteLine(contador);
      contador++;
  } while (contador < 5);
  ```

- **Instrução `for`:** Executa um bloco de código um número específico de vezes, com controle sobre a inicialização, condição e incremento.

  ```csharp
  for (int i = 0; i < 5; i++)
  {
      Console.WriteLine(i);
  }
  ```

- **Instrução `foreach`:** Usada para iterar sobre elementos de uma coleção, como arrays ou listas.
  ```csharp
  int[] numeros = { 1, 2, 3, 4, 5 };
  foreach (int numero in numeros)
  {
      Console.WriteLine(numero);
  }
  ```

## Resumo das Estruturas de Controle

O C# oferece três tipos principais de estruturas de controle:

1. **Sequência: _sequence_** Executa instruções em ordem linear.
2. **Seleção: _selection_** Permite a execução condicional de blocos de código (3 tipos: `if`, `if...else`, `switch`).
3. **Iteração: _iteration_** Repete a execução de blocos de código (4 tipos: `while`, `do...while`, `for`, `foreach`).

Essas estruturas podem ser combinadas de duas maneiras:

- **Empilhamento:** Conectar o ponto de saída de uma instrução ao ponto de entrada da próxima.

  - **Instruções de controle de entrada única/saída única** facilitam a construção de programas — simplesmente conectamos o ponto de saída de uma ao ponto de entrada da próxima. Chamamos isso de **empilhamento de instruções de controle**.

- **Aninhamento:** Colocar uma instrução de controle dentro de outra.

  - Há apenas uma outra maneira pela qual as instruções de controle podem ser conectadas — **aninhamento de instruções de controle** — na qual uma instrução de controle aparece _dentro_ de outra.

---

> Portanto, os algoritmos em aplicativos C# são construídos a partir de apenas três tipos de instruções de controle, combinadas de apenas duas maneiras. Esta é a essência da simplicidade.

---
