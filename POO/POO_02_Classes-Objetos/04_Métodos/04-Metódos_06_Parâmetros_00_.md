# Métodos: Parâmetros

Os métodos em C# são blocos de código reutilizáveis que realizam tarefas específicas. Para tornar os métodos mais flexíveis, podemos definir **parâmetros**, que permitem a passagem de dados externos.

## **1. Métodos sem Parâmetros**

Um método pode ser definido sem parâmetros e chamado diretamente. Métodos que não requerem parâmetros podem ser chamados com parênteses vazios.

```csharp
void MostrarMensagem()
{
    Console.WriteLine("Bem-vindo ao sistema!");
}

// Chamada do método
MostrarMensagem();
```

Aqui, o método simplesmente exibe uma mensagem sempre que for chamado.

**Explicação:**

- Não recebe parâmetros.
- Executa uma ação fixa (exibir uma mensagem).
- Pode ou não retornar um valor (`void` significa que não há retorno).

## **2. Métodos com Parâmetros**

Os parâmetros permitem que os métodos recebam valores no momento da chamada, tornando-os mais versáteis.

Parâmetros permitem que os métodos recebam valores externos, aumentando sua versatilidade. Os métodos em C# podem receber **parâmetros**, que são variáveis definidas em sua assinatura. Quando chamamos um método, devemos fornecer **argumentos correspondentes**, que são os valores reais usados na execução.

### **2.1. Parâmetro Único**

```csharp
void Cumprimentar(string nome)
{
    Console.WriteLine($"Olá, {nome}!");
}

// Chamada do método
Cumprimentar("Ana"); // Saída: Olá, Ana!
```

Agora o método recebe um nome como entrada e personaliza a saudação.

### **2.2. Múltiplos Parâmetros**

Quando um método tem mais de um parâmetro, os parâmetros são listados **separados por vírgula**. Cada argumento deve ter um **tipo correspondente**, garantindo que o método funcione corretamente.

```csharp
void Somar(int a, int b)
{
    Console.WriteLine($"Resultado: {a + b}");
}

// Chamada do método
Somar(3, 5); // Saída: Resultado: 8
```

O método acima recebe dois números e os soma.

Se houver um erro na correspondência de tipos, o compilador exibirá um erro de **tipo incompatível**.

```csharp
// Erro: argumento inválido (string em vez de double)
double area = CalcularAreaRetangulo("cinco", 3.5); // Erro de compilação
```

## **3. Ordem dos Parâmetros**

Os argumentos são atribuídos **na ordem dos parâmetros** definidos no método.

```csharp
void Apresentar(string nome, int idade)
{
    Console.WriteLine($"{nome} tem {idade} anos.");
}

// Chamada correta
Apresentar("Ana", 25); // Saída: Ana tem 25 anos.
```

Se a ordem for trocada incorretamente, o resultado pode não fazer sentido.

## **4. Parâmetros Nomeados**

Podemos definir explicitamente os nomes dos parâmetros ao chamar um método, alterando sua ordem.

```csharp
Apresentar(idade: 30, nome: "Carlos"); // Saída: Carlos tem 30 anos.
```

Isso melhora a legibilidade, especialmente em métodos com muitos parâmetros.

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

## **5. Parâmetros Especiais**

### **5.1. Parâmetros Opcionais**

Podemos definir valores padrão para parâmetros, tornando-os opcionais.

```csharp
void ConfigurarTema(string tema, bool modoEscuro = true)
{
    Console.WriteLine($"Tema: {tema}, Modo Escuro: {modoEscuro}");
}

// Chamada do método
ConfigurarTema("Azul");       // Saída: Tema: Azul, Modo Escuro: True
ConfigurarTema("Verde", false); // Saída: Tema: Verde, Modo Escuro: False
```

Caso não seja informado um valor para `modoEscuro`, ele assume `true` por padrão.

### **5.2. Parâmetro Variável (`params`)**

Quando queremos permitir um número variável de argumentos **do mesmo tipo**, usamos `params`.

```csharp
void SomarValores(params int[] numeros)
{
    int soma = 0;
    foreach (int num in numeros)
    {
        soma += num;
    }
    Console.WriteLine($"Soma: {soma}");
}

// Chamada do método
SomarValores(1, 2, 3);  // Saída: Soma: 6
SomarValores(10, 20);   // Saída: Soma: 30
```

Isso evita a necessidade de passar um array manualmente.

Podemos passar qualquer quantidade de números sem declarar um array explicitamente.

- **`params` é útil**, mas evite abusar em métodos com muitos parâmetros fixos.

- **Alternativa sem `params` (menos elegante):**

```csharp
SomarValores(new int[] {1, 2, 3}); // Funciona, mas é verboso
```

- **Regras:**

- Só pode haver **um `params`** por método.
- Deve ser o **último parâmetro** na lista.

## **6. Argumentos de Linha de Comando**

Em muitos aplicativos, é possível fornecer **argumentos de linha de comando** ao executá-los. Esses argumentos permitem passar informações externas para o programa sem necessidade de interação direta.

### **Como funciona?**

O método `Main` pode receber um array de strings (`string[] args`) contendo os argumentos fornecidos na execução do programa.

```csharp
class Programa
{
    static void Main(string[] args)
    {
        Console.WriteLine($"Número de argumentos: {args.Length}");

        foreach (string arg in args)
        {
            Console.WriteLine($"Argumento: {arg}");
        }
    }
}
```

### **Executando com argumentos**

Se esse programa for compilado e executado no terminal com o seguinte comando:

```bash
Programa.exe "Primeiro" "Segundo" "Terceiro"
```

A saída será:

```bash
Número de argumentos: 3
Argumento: Primeiro
Argumento: Segundo
Argumento: Terceiro
```

### **Regras e Observações**

- Os argumentos são separados por **espaços**, não por vírgulas.
- O número de argumentos pode ser verificado com `args.Length`.
- Caso nenhum argumento seja passado, `args` será um array vazio (`args.Length == 0`).

### **Exemplo de uso**

Argumentos de linha de comando são úteis para:

- Passar **nomes de arquivos** ao programa.
- Configurar opções de execução (exemplo: **modo escuro ativado**).
- Automatizar **tarefas sem necessidade de entrada manual**.

```csharp
static void ConfigurarModo(string[] args)
{
    bool modoEscuro = args.Length > 0 && args[0] == "dark";
    Console.WriteLine($"Modo Escuro: {modoEscuro}");
}
```

Com a execução:

```bash
Programa.exe dark
```

Saída:

```bash
Modo Escuro: True
```

## **7. Tuplas como Parâmetros**

Podemos usar tuplas para passar múltiplos valores como argumento.

```csharp
void ExibirDados((string nome, int idade) pessoa)
{
    Console.WriteLine($"Nome: {pessoa.nome}, Idade: {pessoa.idade}");
}

var usuario = ("Carlos", 35);
ExibirDados(usuario); // Saída: Nome: Carlos, Idade: 35
```

## **8. Sobrecarga de Métodos**

Podemos definir métodos com o mesmo nome, mas com **diferentes conjuntos de parâmetros**. Permite definir **múltiplas versões** de um método com o mesmo nome, mas com parâmetros diferentes (tipo, quantidade ou ordem).

### **Regras:**

- Os métodos devem diferir na **assinatura** (lista de parâmetros).
- O tipo de retorno **não** diferencia sobrecargas.
- **Sobrecarregue com cuidado:** Métodos com nomes iguais devem ter propósitos semelhantes para evitar confusão.
- O C# escolhe automaticamente **qual método chamar** com base nos argumentos fornecidos.

```csharp
void MostrarMensagem()
{
    Console.WriteLine("Mensagem padrão.");
}

void MostrarMensagem(string texto)
{
    Console.WriteLine(texto);
}

// Chamada dos métodos
MostrarMensagem(); // Saída: Mensagem padrão.
MostrarMensagem("Bem-vindo!"); // Saída: Bem-vindo!
```

Isso permite usar o mesmo nome para múltiplas funções semelhantes.

### **Exemplo 02**

```csharp
double CalcularArea(double lado)
{
    return lado * lado; // Quadrado
}

double CalcularArea(double largura, double altura)
{
    return largura * altura; // Retângulo
}

Console.WriteLine(CalcularArea(5)); // Saída: 25 (quadrado)
Console.WriteLine(CalcularArea(4, 3)); // Saída: 12 (retângulo)
```

### **Exemplo 03**

```csharp
// Versão para calcular área do quadrado (1 parâmetro)
static double CalcularArea(double lado)
{
    return lado * lado;
}

// Versão para calcular área do retângulo (2 parâmetros)
static double CalcularArea(double largura, double altura)
{
    return largura * altura;
}

// Versão para calcular área do círculo (usando Math.PI)
static double CalcularArea(double raio, bool isCirculo)
{
    return isCirculo ? Math.PI * raio * raio : 0;
}
```

**Uso:**

```csharp
Console.WriteLine(CalcularArea(5));           // Quadrado: 25
Console.WriteLine(CalcularArea(4, 3));        // Retângulo: 12
Console.WriteLine(CalcularArea(2, true));     // Círculo: ~12.566
```

## **9. Passagem de Parâmetros**

### **9.1 Passagem por Valor (Padrão)**

Quando passamos um argumento por valor, uma cópia do dado é usada dentro do método.

```csharp
void Incrementar(int numero)
{
    numero += 10;
    Console.WriteLine($"Dentro do método: {numero}"); // Saída: 15
}

int valor = 5;
Incrementar(valor);
Console.WriteLine($"Fora do método: {valor}"); // Saída: 5
```

A variável original `valor` **não é modificada**, pois apenas sua cópia foi usada.

- Uma cópia do valor é passada.
- Alterações no método não afetam o original. _(O valor original permanece inalterado.)_
- Ideal quando queremos trabalhar com o valor sem modificar o original.

### **9.2 Passagem por Referência (`ref`)**

Se precisarmos modificar a variável original dentro do método, usamos `ref`.

**Prefira passagem por valor** para evitar efeitos colaterais, a menos que a modificação externa seja necessária.

```csharp
void Dobrar(ref int numero)
{
    numero *= 2;
}

int valor = 3;
Dobrar(ref valor);
Console.WriteLine(valor); // Saída: 6
```

Aqui, `valor` é realmente alterado porque foi passado por referência.

- Permite modificar a variável original.
- O método recebe uma **referência** à variável original. Alterações internas **afetam** a variável externa.
- A variável deve ser **inicializada antes de ser passada**.

### **9.3 Parâmetros de Saída (`out`)**

Permite que um método retorne múltiplos valores sem usar `return`.

**Use `out`** para retornar múltiplos valores sem criar estruturas complexas.

```csharp
void CalcularDobro(int numero, out int resultado)
{
    resultado = numero * 2;
}

CalcularDobro(4, out int dobro);
Console.WriteLine(dobro); // Saída: 8
```

- **Diferença entre `ref` e `out`:**
  - `ref`: Exige que a variável seja inicializada antes da chamada.
  - `out`: Não requer inicialização prévia (o método deve atribuir um valor).

**Exemplo com `ref`:**

```csharp
static void Duplicar(ref int numero)
{
    numero *= 2;
}

int valorOriginal = 3;
Duplicar(ref valorOriginal);
Console.WriteLine(valorOriginal); // Saída: 6
```

**Exemplo com `out`:**

```csharp
static bool TentarDividir(int dividendo, int divisor, out int resultado)
{
    if (divisor == 0)
    {
        resultado = 0;
        return false;
    }
    resultado = dividendo / divisor;
    return true;
}

if (TentarDividir(10, 2, out int resultado))
{
    Console.WriteLine($"Resultado: {resultado}"); // Saída: 5
}
```

## **10. Promoção e Conversão de Argumentos**

Em C#, quando um método recebe um argumento de um tipo diferente do esperado, o compilador pode realizar a **promoção de argumento**, convertendo implicitamente o valor para um tipo mais adequado, se possível.

### **Conversão Implícita (Promoção)**

Alguns tipos podem ser convertidos automaticamente sem perda de dados. Por exemplo, ao chamar o método `Math.Sqrt`, que espera um `double`, podemos passar um `int`, e ele será promovido automaticamente:

```csharp
Console.WriteLine(Math.Sqrt(4)); // Saída: 2.0
```

Aqui, o número inteiro `4` é convertido para `4.0` antes de ser passado ao método `Sqrt`, garantindo que a operação matemática ocorra corretamente.

### **Conversão Explícita (Casting)**

Nem todas as conversões são automáticas. Algumas requerem uma conversão manual (**casting**) para evitar erros:

```csharp
double numero = 7.8;
int inteiro = (int) numero; // Converte para 7, truncando a parte decimal

Console.WriteLine(inteiro); // Saída: 7
```

Ao converter um `double` para `int`, a parte fracionária é **removida**, o que pode resultar em perda de precisão.

### **Conversão de Tipos Inteiros**

A conversão entre tipos inteiros pode causar problemas se o valor for muito grande para o tipo de destino.

```csharp
long numeroGrande = 1_000_000;
int pequeno = (int) numeroGrande; // Pode causar erro se o valor for muito alto
```

Se `numeroGrande` for maior que o limite de `int`, o resultado pode ser **incorreto ou causar uma exceção**.

---
