# Variáveis: Escopo de Parâmetros

Em programação, o **escopo de um parâmetro** refere-se à região do código onde uma variável de parâmetro pode ser acessada.

Parâmetros são variáveis locais declaradas na assinatura de um método ou construtor e são essenciais para a passagem de dados entre diferentes partes do programa.

> **Variáveis locais de parâmetros**

## Definição e Características

**O que são Parâmetros?**

Parâmetros são variáveis locais que aparecem na assinatura de um método e recebem valores quando o método é chamado. Eles permitem que informações sejam passadas para dentro do método.

**Características Principais:**

- **Escopo Limitado**: Acessíveis apenas dentro do método onde foram declarados.

- **Persistência**: Existem apenas durante a execução do método.

- **Inicialização**: São inicializados com os valores passados na chamada do método.

## Exemplos Práticos

**Exemplo 1: Parâmetro Simples**

```csharp
void Saudacao(string nome)
{
    Console.WriteLine($"Olá, {nome}!");
}

// Chamada do método
Saudacao("Maria"); // Saída: Olá, Maria!
```

**Explicação**:

- O parâmetro `nome` é declarado na assinatura do método `Saudacao`.
- Ele só pode ser usado dentro do corpo do método.

**Exemplo 2: Parâmetro em Cálculo**

```csharp
void DobrarNumero(int numero)
{
    int resultado = numero * 2;
    Console.WriteLine($"O dobro de {numero} é {resultado}.");
}

// Chamada do método
DobrarNumero(5); // Saída: O dobro de 5 é 10.
```

**Explicação**:

- O parâmetro `numero` recebe o valor `5` quando o método é chamado.
- O escopo do parâmetro está restrito ao método `DobrarNumero`.

```csharp
void ExemploParametro(int parametro)
  {
    Console.WriteLine(parametro);
  }
```

```csharp
void ExibirMensagem(string mensagem) { // parâmetro
    Console.WriteLine(mensagem);
}
ExibirMensagem("Olá, Adelino!"); // valor passado ao parâmetro
```

## Conceitos Correlatos

### Variáveis Locais

Variáveis declaradas dentro de um método, com escopo restrito ao bloco onde foram definidas.

### Passagem de Parâmetros por Valor vs. por Referência

- **Por Valor**: Uma cópia do valor é passada para o método (o original não é alterado).

- **Por Referência**: O endereço de memória da variável é passado (o original pode ser alterado).

### Sobrecarga de Métodos

Múltiplos métodos com o mesmo nome, mas parâmetros diferentes, permitindo comportamentos distintos.

### Parâmetros Opcionais

Parâmetros com valores padrão, que podem ser omitidos na chamada do método.
