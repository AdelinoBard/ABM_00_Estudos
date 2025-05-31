# Métodos: Parâmetros

## **9. Passagem de Parâmetros**

Quando chamamos um método em C#, podemos passar informações para ele por meio de **parâmetros**. Há diferentes formas de passagem de parâmetros, que afetam como os dados são manipulados dentro do método.

Os três principais tipos de passagem de parâmetros são:

1. **Passagem por Valor** (padrão)
2. **Passagem por Referência** (`ref`)
3. **Parâmetros de Saída** (`out`)

## **1. Passagem por Valor (Padrão)**

Na passagem por valor, o método recebe uma **cópia** do valor do argumento passado. Isso significa que qualquer alteração feita dentro do método **não afeta** a variável original.

### **Exemplo em C#:**

```csharp
void AdicionarCinco(int numero)
{
    numero += 5;
    Console.WriteLine($"Dentro do método: {numero}"); // Saída: 10
}

int valor = 5;
AdicionarCinco(valor);
Console.WriteLine($"Fora do método: {valor}"); // Saída: 5
```

**Explicação:**

- A variável `valor` mantém seu valor original (`5`), pois o método recebeu apenas uma cópia.
- Alterações dentro do método não impactam a variável original.

## **2. Passagem por Referência (`ref`)**

Se precisarmos modificar a variável original dentro do método, usamos a palavra-chave **`ref`**. Aqui, o método recebe **uma referência** para a variável original e pode alterá-la diretamente.

### **Exemplo em C#:**

```csharp
void DobrarValor(ref int numero)
{
    numero *= 2;
}

int valor = 5;
DobrarValor(ref valor);
Console.WriteLine($"Fora do método: {valor}"); // Saída: 10
```

**Explicação:**

- O método `DobrarValor` altera diretamente `valor`, pois ele é passado por referência.
- **O valor original é modificado!**

**Regras do `ref`:**

- A variável deve ser **inicializada** antes de ser passada ao método.
- Útil quando queremos que o método altere o valor da variável original.

## **3. Parâmetros de Saída (`out`)**

Os parâmetros `out` permitem que um método **retorne múltiplos valores** sem usar `return`. Diferente do `ref`, um parâmetro `out` **não precisa ser inicializado** antes da chamada.

### **Exemplo em C#:**

```csharp
void CalcularQuadrado(int numero, out int resultado)
{
    resultado = numero * numero;
}

int valor = 4;
CalcularQuadrado(valor, out int quadrado);
Console.WriteLine($"O quadrado de {valor} é {quadrado}"); // Saída: O quadrado de 4 é 16
```

**Explicação:**

- A variável `quadrado` não foi inicializada antes da chamada do método.
- O método atribui um valor a `resultado`, que é retornado ao chamador.

**Diferença entre `ref` e `out`:** | `ref` | `out` | |-------|-------| | Variável deve ser inicializada antes da chamada | Não precisa ser inicializada antes da chamada | | Pode ser usada tanto para leitura quanto para escrita | Apenas escrita (deve obrigatoriamente receber um valor no método) |

## **Resumo e Melhores Práticas**

- **Use `valor`** quando não precisar modificar a variável original.
- **Use `ref`** quando quiser que o método altere diretamente o valor passado.
- **Use `out`** quando precisar retornar múltiplos valores de um método.

### **Exemplo comparativo final**

```csharp
void ModificarValores(int entrada, ref int porReferencia, out int porSaida)
{
    entrada += 10;
    porReferencia += 10;
    porSaida = entrada * 2;
}

int valor1 = 5, valor2 = 5, valor3;
ModificarValores(valor1, ref valor2, out valor3);

Console.WriteLine($"Valor1 (por valor): {valor1}");   // Saída: 5
Console.WriteLine($"Valor2 (por referência): {valor2}"); // Saída: 15
Console.WriteLine($"Valor3 (por saída): {valor3}");   // Saída: 30
```

**Observação:**

- O `valor1` não foi modificado porque foi passado **por valor**.
- O `valor2` foi alterado porque foi passado **por referência**.
- O `valor3` recebeu um novo valor porque foi um **parâmetro de saída**.

---
