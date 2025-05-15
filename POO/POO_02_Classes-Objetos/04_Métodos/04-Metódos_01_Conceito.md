# Métodos (Procedimento/Função/Subalgoritmo)

No mundo da programação, os **métodos** são blocos de código reutilizáveis que encapsulam funcionalidades específicas. Eles ajudam a organizar o código, tornando os programas mais **modulares, legíveis e fáceis de manter**. Além disso, os métodos evitam a repetição de código, facilitando futuras modificações e garantindo um desenvolvimento mais eficiente.

## O que são métodos?

Um método pode ser visto como um grupo de comandos que executa uma tarefa específica. Essa execução ocorre quando o método é chamado dentro do programa principal. Quando isso acontece, o fluxo do programa se desloca para esse método, executa suas instruções e, ao final, retorna à continuidade da execução do código original.

## Métodos em Objetos

Dentro da programação orientada a objetos, cada objeto deve ser capaz de realizar operações sobre seus próprios **atributos** (dados internos). Essas operações são implementadas nos **métodos** do objeto. Além disso, os métodos podem ser usados para interações entre diferentes objetos dentro de um sistema.

Um exemplo prático: quando um cliente faz um saque em um caixa eletrônico, o objeto que representa o **caixa eletrônico** precisa interagir com o objeto que representa a **conta bancária** do cliente. Esse tipo de interação entre objetos é facilitado através dos métodos.

- **As ações que um objeto pode realizar são definidas pelos seus métodos.**
- **Um objeto é composto por atributos e métodos.**

## Diferença entre Funções e Procedimentos

Embora muitas vezes usados como sinônimos, funções e procedimentos possuem uma diferença sutil:

- **Função:** Executa uma ação e retorna um valor como resultado.
- **Procedimento:** Executa uma ação, mas **não retorna** um valor.

> Em C#, o termo "procedimento" não é utilizado oficialmente. Todas as funções, independentemente de retornarem valores ou não, são chamadas de **métodos**. A distinção ocorre pelo uso (ou não) da palavra-chave `return`.

## **Benefícios dos Métodos:**

- **Reutilização de Código:** Evita a duplicação de código, reduzindo o tamanho do programa e facilitando a leitura e o entendimento do código.
- **Manutenção Simplificada:** Qualquer alteração no cabeçalho precisa ser feita apenas no método, e não em cada instância replicada, diminuindo o risco de erros e inconsistências.
- **Modularidade:** Aumenta a modularidade do código, dividindo-o em blocos de funções bem definidas, facilitando a organização e a compreensão do programa.
- **Legibilidade Aprimorada:** Torna o código mais legível e expressivo, pois cada método encapsula uma funcionalidade específica, com um nome descritivo que indica sua função.

## Exemplo de Métodos em C#

```csharp
public class Conta
{
    public int Numero { get; set; }
    public decimal Saldo { get; private set; }

    public void Depositar(decimal valor)
    {
        Saldo += valor;
    }

    public void Sacar(decimal valor)
    {
        if (valor <= Saldo)
        {
            Saldo -= valor;
        }
        else
        {
            throw new InvalidOperationException("Saldo insuficiente.");
        }
    }
}
```

## **Métodos Predefinidos em C#**

C# oferece um conjunto de **métodos predefinidos** que facilitam diversas operações comuns na programação. Esses métodos fazem parte da biblioteca padrão da linguagem e ajudam os desenvolvedores a realizarem tarefas como:

- **Operações matemáticas** (cálculos, arredondamentos, geração de números aleatórios);
- **Manipulação de strings** (busca, substituição, formatação de texto);
- **Entrada e saída de dados** (interação com o usuário via console, leitura e escrita de arquivos).

Esses métodos já vêm integrados ao C# e podem ser utilizados sem a necessidade de implementação manual, tornando o desenvolvimento mais rápido e eficiente.
