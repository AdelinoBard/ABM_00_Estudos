# Variáveis: `readonly` (Somente Leitura)

Variáveis `readonly` em C# são usadas para declarar campos que só podem ser atribuídos uma vez, seja na declaração ou no construtor da classe. Após a inicialização, seu valor não pode ser alterado. Isso é útil para garantir imutabilidade e segurança em partes críticas do código.

## Características Principais

1. **Inicialização**:

   - Devem ser inicializadas na declaração **ou** no construtor.
   - Não podem ser modificadas após a construção do objeto.

2. **Comparação com `const`**:

   - `const`: Valor constante em tempo de compilação (deve ser conhecido antecipadamente).
   - `readonly`: Valor pode ser definido em tempo de execução (por exemplo, com base em parâmetros do construtor).

3. **Convenção nomenclatura**:
   - Como uma constante `const`, o identificador de uma variável `readonly` usa Pascal Case por convenção.

## Exemplo Básico

```csharp
class Configuracao
{
    private readonly string _conexaoBanco;  // Declaração

    public Configuracao(string conexao)
    {
        _conexaoBanco = conexao;  // Inicialização no construtor
    }

    public void ExibirConexao()
    {
        Console.WriteLine($"Conexão: {_conexaoBanco}");
        // _conexaoBanco = "nova_conexao";  // ERRO: Não pode ser modificada!
    }
}
```

### Uso:

```csharp
var config = new Configuracao("Server=localhost;Database=Teste");
config.ExibirConexao();  // Saída: "Conexão: Server=localhost;Database=Teste"
```

## Princípio do Menor Privilégio

O **princípio do menor privilégio** é fundamental para uma boa engenharia de software. No contexto de um aplicativo, o princípio afirma que _o código deve receber a quantidade de privilégio e acesso necessária para realizar sua tarefa designada, mas não mais_.

Declarar variáveis como `readonly` reforça o princípio de que o código deve ter apenas os privilégios necessários para sua função. Isso:

- **Reduz bugs**: Evita modificações acidentais após a inicialização.
- **Melhora a clareza**: Deixa explícito que o valor é imutável.

> Observação de Engenharia de Software: _Declarar uma variável de instância como somente leitura (`readonly`) ajuda a reforçar o princípio do menor privilégio. Se uma variável de instância não deve ser modificada após o objeto ser construído, declare-a como somente leitura para evitar modificações._

## Quando Usar `readonly` vs `const`

| **`readonly`** | **`const`** |
| --- | --- |
| Valor definido em tempo de execução. | Valor definido em tempo de compilação. |
| Pode ser inicializado no construtor. | Deve ser inicializado na declaração. |
| Aceita tipos complexos (como objetos). | Só aceita tipos primitivos ou `string`. |

Algumas variáveis de instância precisam ser modificáveis, e outras não. É possível usar a palavra-chave `const` para declarar uma constante, que deve ser inicializada em sua declaração — todos os objetos da classe têm o mesmo valor para essa constante. Suponha, no entanto, que queremos uma constante que pode ter um valor _diferente_ para cada objeto de uma classe. Para esse propósito, C# fornece a palavra-chave `readonly` para especificar que uma variável de instância de um objeto _não_ é modificável e que qualquer tentativa de modificá-la _após_ o objeto ser construído é um erro.

> Observação de Engenharia de Software: _Se uma variável de instância somente leitura for inicializada para uma constante somente em sua declaração, não é necessário ter uma cópia separada da variável de instância para cada objeto da classe. A variável deve ser declarada `const` em vez disso. Constantes declaradas com `const` são implicitamente estáticas, então haverá apenas uma cópia para toda a classe._

Embora variáveis de instância `readonly` possam ser inicializadas quando são declaradas, isso não é necessário. Uma variável `readonly` deve ser inicializada _por cada_ dos construtores da classe ou na declaração da variável. Cada construtor pode atribuir valores a uma variável de instância `readonly` várias vezes — a variável não se torna inalterável até _depois_ que o construtor conclui a execução. Se um construtor não inicializar a variável `readonly`, a variável usa o mesmo valor padrão de qualquer outra variável de instância (`0` para tipos simples numéricos, `false` para o tipo `bool` e `null` para tipos de referência) — esses valores são realmente definidos antes de um construtor executar e podem ser substituídos pelo construtor chamado.

Os membros `const` devem receber valores em tempo de compilação. Portanto, os membros `const` podem ser inicializados _somente_ com outros valores constantes, como inteiros, literais `string`, caracteres e outros membros `const`. Os membros constantes com valores que não podem ser determinados em tempo de compilação — como constantes que são inicializadas com o resultado de uma chamada de método — devem ser declarados com a palavra-chave `readonly`, para que possam ser inicializados em _tempo de execução_. Variáveis que são `readonly` podem ser inicializadas com expressões mais complexas, como um inicializador de array ou uma chamada de método que retorna um valor ou uma referência a um objeto.

### Exemplo:

```csharp
class Exemplo
{
    public const int MaxItems = 100;  // Constante fixa
    public readonly int Limite;       // Pode variar por instância

    public Exemplo(int limite)
    {
        Limite = limite;  // Válido para 'readonly'
        // MaxItems = 200;  // ERRO: 'const' não pode ser alterada!
    }
}
```

## Erros Comuns e Boas Práticas

- **Erro**: Tentar modificar um campo `readonly` fora do construtor.
  ```csharp
  _conexaoBanco = "outro_valor";  // Erro de compilação!
  ```

> Erro de programação comum: _Tentar modificar uma variável de instância somente leitura em qualquer lugar que não seja sua declaração ou os construtores do objeto é um erro de compilação._

> Dica de prevenção de erros: _Tentativas de modificar uma variável de instância somente leitura são capturadas no momento da compilação em vez de causar erros no momento da execução. É sempre preferível eliminar os bugs no momento da compilação, se possível, em vez de permitir que eles passem para o momento da execução (onde estudos descobriram que consertar bugs costuma ser muito mais custoso)._

- **Boas Práticas**:
  - Use `readonly` para campos que não devem mudar após a construção.
  - Prefira `const` para valores verdadeiramente constantes e conhecidos em tempo de compilação.

## Tópicos Correlatos Não Abordados

### 1. **`readonly struct`**

- Estruturas imutáveis onde todos os campos são `readonly`.

```csharp
readonly struct Ponto
{
    public readonly int X;
    public readonly int Y;
    public Ponto(int x, int y) => (X, Y) = (x, y);
}
```

### 2. **Propriedades com `init` (C# 9+)**

- Permitem inicialização apenas durante a construção, semelhante a `readonly`.

```csharp
class Cliente
{
    public string Nome { get; init; }  // Pode ser definido apenas no construtor ou inicializador
}
```

### 3. **Campos `static readonly`**

- Variáveis compartilhadas entre todas as instâncias, imutáveis após a inicialização.

```csharp
class ConfigGlobal
{
    public static readonly string Versao = "1.0";
}
```

### 4. **Imutabilidade em Coleções**

- Uso de `ReadOnlyCollection<T>` ou `IReadOnlyList<T>` para evitar modificações em listas.

```csharp
private readonly List<int> _numeros = new List<int> { 1, 2, 3 };
public IReadOnlyList<int> Numeros => _numeros.AsReadOnly();
```
