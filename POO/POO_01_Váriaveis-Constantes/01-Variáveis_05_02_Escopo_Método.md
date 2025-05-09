# Variáveis: Escopo de Método

O escopo de um método define onde uma variável pode ser acessada dentro do código. Variáveis declaradas dentro de um método são chamadas de **variáveis locais** e possuem um escopo restrito ao bloco onde foram criadas. Declaradas dentro de métodos, acessíveis apenas no método onde foram criadas.

> **Variáveis locais de Método**

## Variáveis Locais

Uma variável declarada no corpo de um método é uma variável local e pode ser usada somente da linha de sua declaração até a chave direita de fechamento do bloco no qual a variável é declarada. A declaração de uma variável local deve aparecer _antes_ da variável ser usada; caso contrário, ocorre um erro de compilação.

## Definição e Características

- **Onde são declaradas**: Dentro de métodos, construtores ou blocos (como `if`, `for`, etc.).

- **Escopo**: Acessíveis apenas dentro do método ou bloco onde foram declaradas.

- **Persistência**: Existem apenas enquanto o bloco está em execução. São criadas no início e destruídas no fim do bloco.

## Exemplos Simples

### Exemplo 1: Variável Local em um Método

```csharp
void Saudacao()
{
    string mensagem = "Olá, mundo!"; // Variável local
    Console.WriteLine(mensagem);
}
// 'mensagem' não pode ser acessada aqui
```

### Exemplo 2: Variável Local em um Bloco `if`

```csharp
void VerificarIdade(int idade)
{
    if (idade >= 18)
    {
        string status = "Adulto"; // Variável local no bloco 'if'
        Console.WriteLine(status);
    }
    // 'status' não pode ser acessada aqui
}
```

## Parâmetros como Variáveis Locais

Os parâmetros de um método também são tratados como variáveis locais, acessíveis apenas dentro do método.

```csharp
void Somar(int a, int b) // 'a' e 'b' são variáveis locais
{
    int resultado = a + b;
    Console.WriteLine(resultado);
}
// 'a', 'b' e 'resultado' não podem ser acessados aqui
```

## Resumo e Pontos Chave

- Variáveis locais são declaradas dentro de métodos ou blocos.

- Seu escopo é limitado ao bloco onde foram criadas.

- Devem ser declaradas antes do uso para evitar erros de compilação.

- Parâmetros de métodos também são variáveis locais.

## Tópicos Correlatos

1. **Escopo de Classe**: Variáveis declaradas em nível de classe (campos) e seu escopo.

2. **Modificadores de Acesso**: Como `public`, `private`, etc., afetam a visibilidade das variáveis.

3. **Variáveis Globais**: Uso e boas práticas (quando aplicável).

4. **Blocos de Código**: Como `for`, `while`, e `try-catch` influenciam o escopo.
