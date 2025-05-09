# Variáveis: Nomenclatura

Nomes de variáveis são fundamentais para escrever códigos claros e fáceis de entender. Eles devem ser descritivos e seguir convenções para garantir consistência e legibilidade.

## Convenções de Nomenclatura em C# (Camel Case)

Na convenção de nomes da linguagem C#, os nomes das variáveis devem seguir o padrão **camel case** com a primeira letra minúscula. Esse padrão também é conhecido como **lower camel case**.

- A primeira letra da primeira palavra é minúscula.

- As primeiras letras das palavras subsequentes são maiúsculas.

**Exemplos**:

```csharp
string nomeCompleto;
double saldoBancario;
bool ehValido;
```

**Comparação**:

```csharp
int numeroDaConta;   // Correto (camel case)
int Numerodaconta;   // Incorreto
```

A convenção de nomes da linguagem C# pode ser consultada na seguinte URL: [Naming Guidelines](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines?redirectedfrom=MSDN).

Em algumas linguagens de programação, delimitadores são utilizados para separar as palavras que formam o nome de uma variável:

- `numero_de_candidatos_aprovados;`
- `numero-de-candidatos-aprovados;`

Em outras linguagens de programação, letras maiúsculas e minúsculas são utilizadas para separar as palavras:

- `NumeroDeCandidatosAprovados;`
- `numeroDeCandidatosAprovados;`

## Sensibilidade a Maiúsculas e Minúsculas (Case Sensitivity)

C# é **case sensitive**, ou seja, diferencia letras maiúsculas e minúsculas. Variáveis com nomes similares, mas com diferenças de caixa, são consideradas distintas.

**Exemplo**:

```csharp
int idade;
int Idade;
int IDADE;
// Todas são variáveis diferentes!
```

## Regras para Nomes de Variáveis

Em geral, os identificadores de variáveis podem conter letras e números, não devem conter espaços em branco nem caracteres especiais, e não podem começar com números. O único caractere especial que costuma ser aceito em nomes de variáveis é o sublinhado `_`.

- **Caracteres permitidos**: Letras (A-Z, a-z), números (0-9) e sublinhado (`_`). Os outros caracteres podem ser letras, números e sublinhado.

- **Restrições**:
  - Não pode começar com número.
  - Não pode conter espaços ou caracteres especiais (ex: `#`, `@`, `ç`, `ã`).
  - Não pode ser igual a palavras reservadas da linguagem (ex: `int`, `double`).
  - Não é permitido o uso de pontuação.

**Exemplo simples**:

```csharp
int idade;          // Válido
int _idade;         // Válido (mas evite começar com _)
int idade1;         // Válido
int 1idade;         // Inválido (começa com número)
```

- **Palavras reservadas**: Nomes de variáveis não podem ser iguais a palavras reservadas nem aos tipos nativos. Se precisar usar uma palavra reservada, adicione `@` antes.

- **Caracteres especiais** (inclusive acentos) e espaços em branco não podem ser utilizados.

  - **Importante:** Considere um código C# que declara uma variável chamada `pontuação`. Note o uso dos caracteres “ç” e “ã” no nome dessa variável. Geralmente, os códigos desses caracteres são diferentes em cada padrão de codificação. Por exemplo, no UTF-8, o código do caractere “ç” é 50087, enquanto que no ISO-8859-1 é 231. Suponha que esse código tenha sido salvo em um arquivo que utiliza a codificação UTF-8. Se ele for aberto em um editor que utiliza a codificação ISO-8859-1, o caractere “ç” não será apresentado corretamente, dificultando a leitura ou a modificação do código fonte. Para evitar esse tipo de problema, a recomendação é utilizar apenas as letras de A a Z (tanto maiúsculas quanto minúsculas) e os dígitos de 0 a 9, pois geralmente os códigos desses caracteres não variam de codificação para codificação.

- **Tamanho do nome**: Não há limite rígido, mas prefira nomes curtos e descritivos.

- **Constantes**: Use letras maiúsculas e sublinhados para separar palavras.

**Exemplos**:

```csharp
int @int;           // Válido (usa palavra reservada com @)
const int MAX_TENTATIVAS = 3;   // Constante em maiúsculas
```

- Evite prefixos como `_` ou `m_` (comuns em códigos legados).

- Embora seja possível ter uma variável com o nome `_var` (começando com “\_”), estes são reservados para a implementação interna do programa, e seu uso é bem restrito e desaconselhado. O compilador não vai mostrar erro quando criamos variáveis desse jeito, mas o programa criado se comportará de forma inesperada.

## Boas Práticas

- **Seja descritivo**: Use nomes que expliquem o propósito da variável.

  - Ruim: `int x;`
  - Bom: `int quantidadeItens;`

- **Evite abreviações obscuras**: Prefira `numeroClientes` em vez de `numCli`.

- **Mantenha a consistência**: Siga o mesmo padrão em todo o projeto.

## Exemplos de Declaração de Variáveis

```csharp
string nome = "João";       // Texto
int idade = 25;             // Número inteiro
double altura = 1.75;       // Número decimal
bool temCarteira = true;    // Valor booleano
int @static;                // válido pois apesar de ser igual a uma palavra reservada possui o prefixo
int umaVariavelComUmNomeSuperHiperMegaUltraGigante; // válido
int numeroDaContaCom8Digitos_semPontos; // válido
```

**Inválidos**:

```csharp
int 2nome;                 // Começa com número
double salario total;      // Contém espaço
string #email;             // Caractere especial
double double;             // inválido pois o nome de uma variável não pode ser igual a uma palavra reservada
double saldo Da Conta;     // inválido pois o nome de uma variável não pode conter espaços
```
