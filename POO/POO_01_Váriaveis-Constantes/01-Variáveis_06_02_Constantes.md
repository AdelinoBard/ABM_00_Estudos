# Variáveis: `const` Constantes

Em programação, uma **constante** é um valor que não pode ser alterado durante a execução de um programa. Diferentemente das variáveis, que podem ter seus valores modificados, as constantes são imutáveis e garantem a estabilidade de valores essenciais. Elas são declaradas com um tipo e um identificador específicos, seguindo convenções de nomenclatura claras.

Constantes são ferramentas essenciais para criar código seguro, legível e de fácil manutenção. Elas garantem que valores fundamentais permaneçam imutáveis, evitando erros e melhorando a organização do programa.

> _Constantes também são chamadas de \*\*\_constantes nomeadas_\*\*.

## Declaração de Constantes

A palavra-chave `const` é usada para declarar constantes em C#.

Uma constante deve ser inicializada no momento da declaração e não pode ser modificada posteriormente.

**Pontos importantes:**

- Constantes não podem ser declaradas sem inicialização.
- Tentar modificar uma constante após sua declaração resulta em um erro de compilação.
- As constantes usam as mesmas convenções de nomenclatura **Pascal Case** que classes, métodos e propriedades.

## Exemplos Simples:

```csharp
const int IdadeMinima = 18;
const double TaxaJuros = 0.05;

Console.WriteLine($"Idade mínima: {IdadeMinima}");
Console.WriteLine($"Taxa de juros: {TaxaJuros}");
```

```csharp
const float Pi = 3.14f;
const int Meses = 12;

Console.WriteLine(Pi);
Console.WriteLine(Meses);
```

```csharp
const int HorasPorDia = 24;
const int MinutosPorHora = 60;

int minutosPorDia = HorasPorDia * MinutosPorHora;
Console.WriteLine($"Minutos em um dia: {minutosPorDia}");
```

## Comparação entre Constantes e Variáveis

| Característica | Constante | Variável |
| --- | --- | --- |
| Mutabilidade | Imutável | Mutável |
| Inicialização | Obrigatória na declaração | Pode ser declarada sem valor |
| Uso | Valores fixos (ex: PI, dias da semana) | Valores dinâmicos (ex: contadores, entradas de usuário) |

- **Constante**: Espaço na memória para armazenamento de um valor que não será modificado. Ao definir uma constante, garantimos que o valor armazenado permanece o mesmo durante toda a execução do programa. Por exemplo, uma constante para o valor de PI (π) em cálculos matemáticos evita que esse valor fundamental seja alterado acidentalmente.

- **Variável**: Espaço na memória para armazenamento de um valor que pode ser modificado. As variáveis são essenciais para armazenar dados que podem mudar conforme a execução do programa. Por exemplo, a pontuação de um jogador em um jogo de vídeo é armazenada em uma variável, pois é atualizada continuamente.

### Exemplo de Variável:

```csharp
int pontuacao = 100;
pontuacao = 150; // Permitido
Console.WriteLine($"Pontuação: {pontuacao}");
```

### Exemplo de Erro com Constante:

```csharp
const int DiasSemana = 7;
DiasSemana = 10; // Erro de compilação!
```

No exemplo acima, a constante `DiasSemana` é inicializada com o valor 7. Qualquer tentativa de modificar `DiasSemana` após sua inicialização resultará em um erro de compilação, pois o valor de uma constante é imutável.

## Importância das Constantes

1. **Segurança**: Evita modificações acidentais em valores críticos.

2. **Legibilidade**: Torna o código mais claro, substituindo "números mágicos" por nomes significativos.

3. **Manutenção**: Facilita atualizações, pois o valor é definido em um único local.

## Boas Práticas

- Use constantes para valores repetidos ou significativos.

- Evite "números mágicos" no código.

## Conceitos Correlatos

1. **Enumerações (Enums)**:  
   Usadas para definir conjuntos de constantes relacionadas, como dias da semana ou estados de um processo.

   ```csharp
   enum Dias { Segunda, Terca, Quarta, Quinta, Sexta, Sabado, Domingo }
   ```

2. **Readonly vs Const**:

   - `const`: Valor definido em tempo de compilação.
   - `readonly`: Valor definido em tempo de execução (pode ser inicializado no construtor).

   ```csharp
   readonly string NomeAplicacao = "MeuApp";
   ```

3. **Escopo de Constantes**:  
   Constantes declaradas em classes são implicitamente `static` e acessíveis via nome da classe (ex: `Math.PI`).

_Constantes declaradas em uma classe, mas não dentro de um método ou propriedade, são implicitamente estáticas — é um erro de sintaxe declarar tal constante com a palavra-chave static explicitamente._

Campos declarados `const` são implicitamente `static`, então você pode acessá-los por meio do nome da classe `Math` e do operador de acesso a membros (`.`), como em `Math.PI` e `Math.E`.
