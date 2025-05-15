# **Chamada e Execução de Métodos**

Um método é um bloco de código que executa uma tarefa específica. Para utilizá-lo, precisamos **chamá-lo** (invocá-lo) em nosso programa.

## **Componentes de uma Chamada de Método**

1. **Objeto/referência** (para métodos de instância)
2. **Operador ponto (.)**
3. **Nome do método**
4. **Parênteses ()** (podendo conter ou não argumentos)

## **Tipos de Chamada de Métodos**

### **Chamada Simples (Sem Argumentos)**

Métodos que não requerem parâmetros podem ser chamados com parênteses vazios.

```csharp
// Definição do método
void ExibirCabecalho()
{
    Console.WriteLine("=== SISTEMA ACADÊMICO ===");
    Console.WriteLine("========================");
}

// Chamada do método
ExibirCabecalho();
```

**Características:**

- Não recebe parâmetros
- Executa uma ação fixa
- Pode ou não retornar valor (no exemplo acima é `void`)

### **Chamada com Argumentos**

Quando o método foi definido com parâmetros, devemos passar argumentos correspondentes.

```csharp
// Definição
string FormatarNome(string nome, string sobrenome)
{
    return $"{sobrenome.ToUpper()}, {nome}";
}

// Chamada
string nomeCompleto = FormatarNome("João", "Silva");
Console.WriteLine(nomeCompleto); // Saída: SILVA, João
```

**Regras importantes:**

- A quantidade e tipo dos argumentos devem corresponder aos parâmetros
- A ordem dos argumentos importa (a menos que use parâmetros nomeados)

### **Chamada de Métodos de Instância**

Métodos que pertencem a objetos exigem uma instância para serem chamados.

**Exemplo com classe:**

```csharp
class ContaBancaria
{
    private string _titular;

    public void DefinirTitular(string nome)
    {
        _titular = nome;
    }

    public string ObterTitular()
    {
        return _titular;
    }
}

// Uso:
ContaBancaria minhaConta = new ContaBancaria();
minhaConta.DefinirTitular("Carlos Oliveira"); // Chamada de método de instância
Console.WriteLine(minhaConta.ObterTitular()); // Outra chamada
```

**Processo passo a passo:**

1. Criamos uma instância com `new ContaBancaria()`
2. Usamos o operador ponto para acessar o método
3. Chamamos o método com os parênteses (e argumentos se necessário)

## **Formas Especiais de Chamada**

### **Chamada Encadeada (Method Chaining)**

Quando métodos retornam objetos, podemos chamar métodos subsequentes na mesma linha.

**Exemplo:**

```csharp
public class StringBuilder
{
    private string _texto;

    public StringBuilder Append(string texto)
    {
        _texto += texto;
        return this; // Retorna o próprio objeto
    }

    public override string ToString() => _texto;
}

// Uso com encadeamento:
var sb = new StringBuilder();
sb.Append("Hello").Append(" ").Append("World!");
Console.WriteLine(sb.ToString());
```

**Vantagens:**

- Código mais limpo e conciso
- Redução de variáveis temporárias

### **Chamada Recursiva**

Um método que chama a si mesmo, útil para algoritmos como fatorial ou navegação em árvores.

**Exemplo (Fatorial):**

```csharp
int Fatorial(int n)
{
    if (n <= 1)
        return 1;
    else
        return n * Fatorial(n - 1); // Chamada recursiva
}

Console.WriteLine(Fatorial(5)); // 120
```

**Cuidados:**

- Sempre deve ter uma condição de parada
- Pode causar stack overflow se muito profunda

### **Chamada com Argumentos Nomeados**

Permite especificar os parâmetros pelo nome, independente da ordem.

**Exemplo:**

```csharp
void RegistrarAluno(string nome, int idade, bool matriculado)
{
    // Implementação
}

// Chamada tradicional (por posição)
RegistrarAluno("Maria", 20, true);

// Chamada com argumentos nomeados
RegistrarAluno(idade: 22, nome: "Pedro", matriculado: false);
```

**Vantagens:**

- Melhor legibilidade
- Flexibilidade na ordem dos argumentos

## **Boas Práticas na Chamada de Métodos**

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
