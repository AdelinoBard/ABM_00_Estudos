# **Encapsulamento de Métodos em C#**

## **O que é Encapsulamento?**

O encapsulamento é um dos **pilares da Programação Orientada a Objetos (POO)** que consiste em:

- **Proteger os dados internos** de uma classe, evitando acesso indevido.
- **Controlar como os atributos são modificados** por meio de métodos.
- **Ocultar detalhes de implementação**, expondo apenas o necessário.

**Benefícios:**

- **Segurança**: Impede modificações incorretas no estado do objeto.
- **Manutenibilidade**: Facilita alterações internas sem afetar quem usa a classe.
- **Controle**: Validações e regras podem ser aplicadas antes de modificar dados.

## **Modificadores de Acesso**

Em C#, os principais modificadores que controlam o encapsulamento são:

- `private`: **Padrão**. Acesso **apenas dentro da própria classe**.
- `public` : Acesso **livre em qualquer parte do código**.
- `protected`: Acesso **na classe e em classes derivadas (herança)**.
- `internal`: Acesso **apenas dentro do mesmo assembly (projeto)**.
- `protected internal` : Combinação de `protected` e `internal`.

## **Como Aplicar o Encapsulamento?**

### **a) Atributos Privados + Métodos Públicos**

A prática mais comum é declarar campos como `private` e fornecer métodos `public` para interação.

**Exemplo:**

```csharp
public class ContaBancaria
{
    private double saldo; // Campo privado

    // Método público para depósito (controlado)
    public void Depositar(double valor)
    {
        if (valor > 0)
            saldo += valor;
        else
            Console.WriteLine("Valor inválido!");
    }

    // Método público para consulta (sem alteração direta)
    public double ObterSaldo()
    {
        return saldo;
    }
}
```

**Por que não deixar `saldo` como `public`?**

- **Problema**: Qualquer código externo poderia fazer `conta.saldo = -1000;`, violando regras de negócio.
- **Solução**: Usar métodos para **validar operações** (ex: depósitos apenas com valores positivos).

### **b) Propriedades (Encapsulamento Elegante)**

Em C#, as **propriedades** (`get` e `set`) simplificam o encapsulamento.

**Exemplo:**

```csharp
public class ContaBancaria
{
    private double saldo;

    // Propriedade com validação no "set"
    public double Saldo
    {
        get { return saldo; }
        set
        {
            if (value >= 0)
                saldo = value;
            else
                Console.WriteLine("Saldo não pode ser negativo!");
        }
    }
}
```

**Uso:**

```csharp
ContaBancaria conta = new ContaBancaria();
conta.Saldo = 1000;  // Válido (set)
Console.WriteLine(conta.Saldo);  // 1000 (get)
conta.Saldo = -500;  // Inválido (imprime mensagem de erro)
```

## **Quando Usar Métodos vs. Propriedades?**

| **Métodos** | **Propriedades** |
| --- | --- |
| Úteis para **ações** (`Depositar`, `Sacar`). | Ideais para **acesso controlado a atributos** (`Saldo`, `Nome`). |
| Podem ter **parâmetros**. | Geralmente não usam parâmetros (exceto em casos avançados). |
| Exemplo: `Transferir(double valor, Conta destino)`. | Exemplo: `public int Idade { get; set; }`. |

## **Encapsulamento em Herança**

- Membros `private` **não são acessíveis** em classes filhas.
- Use `protected` para permitir acesso **apenas na hierarquia de herança**.

**Exemplo:**

```csharp
public class Veiculo
{
    protected int velocidadeMaxima; // Acessível em classes derivadas

    public void Acelerar(int incremento)
    {
        velocidadeMaxima += incremento;
    }
}

public class Carro : Veiculo
{
    public void ExibirVelocidadeMaxima()
    {
        Console.WriteLine(velocidadeMaxima); // OK (protected)
    }
}
```

## **Boas Práticas**

- **Sempre comece com `private`**: Exponha apenas o necessário.
- **Use propriedades para campos simples**: `public string Nome { get; set; }`.
- **Valide dados em métodos `set` ou métodos públicos**: Evite estados inválidos.
- **Documente regras de acesso**: Comente se um método/propriedade tem restrições.

## **Exemplo Completo**

```csharp
public class Pessoa
{
    private string nome;
    private int idade;

    // Propriedade com encapsulamento
    public string Nome
    {
        get { return nome; }
        set
        {
            if (!string.IsNullOrEmpty(value))
                nome = value;
            else
                throw new ArgumentException("Nome não pode ser vazio!");
        }
    }

    // Método público para modificar idade com validação
    public void DefinirIdade(int novaIdade)
    {
        if (novaIdade >= 0 && novaIdade <= 120)
            idade = novaIdade;
        else
            throw new ArgumentOutOfRangeException("Idade inválida!");
    }

    // Método público para ler idade
    public int ObterIdade()
    {
        return idade;
    }
}
```

---
