# **Atributos Privados + Métodos Públicos (Abordagem Tradicional)**

Esta abordagem é um dos pilares da programação orientada a objetos, especialmente no que diz respeito ao **encapsulamento**. A ideia central é proteger os dados internos de uma classe (atributos privados) e fornecer acesso controlado através de métodos públicos.

## **Estrutura Básica**

No exemplo da `ContaBancaria`, o saldo é um atributo privado (`_saldo`), e todas as operações (como depósito e consulta) são realizadas por meio de métodos públicos:

```csharp
public class ContaBancaria
{
    // Atributo privado - só pode ser modificado dentro da classe
    private double _saldo;

    // Método público para depósito (com validação)
    public void Depositar(double valor)
    {
        if (valor > 0)
            _saldo += valor;
        else
            Console.WriteLine("Valor de depósito inválido!");
    }

    // Método público para consultar o saldo (sem permitir modificação direta)
    public double ObterSaldo()
    {
        return _saldo;
    }
}
```

## **Por que Usar Atributos Privados e Métodos Públicos?**

### **1. Controle Total sobre as Operações**

- O atributo `_saldo` não pode ser alterado diretamente de fora da classe.
- Qualquer modificação passa obrigatoriamente por um método (`Depositar`), onde podemos incluir regras de validação.

**Exemplo de proteção:**

```csharp
var conta = new ContaBancaria();
conta.Depositar(-100); // Inválido! Mensagem de erro será exibida.
// conta._saldo = 1000; // ERRO! _saldo é privado e inacessível fora da classe.
```

### **2. Validações e Regras de Negócio**

- Pode-se adicionar lógicas complexas nos métodos para garantir consistência.
- Exemplo: verificar limite máximo de depósito, taxas, etc.

**Melhorando o método `Depositar`:**

```csharp
public void Depositar(double valor)
{
    if (valor <= 0)
        Console.WriteLine("Valor deve ser positivo!");
    else if (valor > 10_000)
        Console.WriteLine("Depósitos acima de R$ 10.000 exigem validação!");
    else
        _saldo += valor;
}
```

### **3. Clareza na Intenção**

- Métodos como `Depositar()` e `ObterSaldo()` deixam explícito o que a classe permite fazer.
- Evita manipulação incorreta dos dados (como alterar o saldo sem passar por uma regra).

## **Uso Prático**

```csharp
var conta = new ContaBancaria();

conta.Depositar(300); // Válido
conta.Depositar(-50); // Inválido (mensagem de erro)

double saldoAtual = conta.ObterSaldo(); // Consulta segura
Console.WriteLine($"Saldo atual: R$ {saldoAtual}");
```

**Saída:**

```
Valor de depósito inválido!
Saldo atual: R$ 300
```

## **Quando Usar Essa Abordagem?**

- Quando você precisa **proteger os dados** contra modificações indevidas.
- Quando **operações precisam de validações** antes de alterar o estado do objeto.
- Quando deseja **deixar claro** quais ações a classe permite.

## **Alternativas (Quando Não Usar?)**

- Se um atributo **não precisa de validação ou lógica adicional**, pode-se usar uma **propriedade pública** (mais simples).
  ```csharp
  public double Saldo { get; private set; } // Pode ser lido, mas só alterado dentro da classe
  ```
- Se a classe for **apenas um repositório de dados** (sem regras), talvez um **registro (record)** seja mais adequado.

---
