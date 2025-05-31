# Modificadores de Acesso em C#

Os modificadores de acesso são palavras-chave em C# que controlam a visibilidade e acessibilidade de classes, métodos, propriedades e outros membros. Eles são fundamentais para implementar o princípio de encapsulamento na Programação Orientada a Objetos (POO).

> Lembre-se: comece sempre com o modificador mais restritivo (`private`) e só aumente a visibilidade quando necessário.

## Conceitos Básicos

### O que são Modificadores de Acesso?

Modificadores de acesso definem **quem pode acessar** determinados membros de uma classe. Eles ajudam a:

- Proteger dados sensíveis
- Controlar o acesso a funcionalidades
- Organizar a estrutura do código

### Por que são importantes?

1. **Segurança**: Previne acesso indevido a dados críticos
2. **Organização**: Facilita a manutenção do código
3. **Encapsulamento**: Esconde detalhes de implementação

## Principais Modificadores de Acesso em C#

### 1. `private` (Privado)

O nível mais restritivo, limitando o acesso a membros e tipos apenas ao código da mesma classe em que foram declarados.

- **Visibilidade:** Restrito à própria classe.

- **Acesso**: Somente dentro da própria classe
- **Uso padrão**: Membros de classe são privados por padrão
- **Quando usar**: Para dados internos que não devem ser expostos

```csharp
class ContaBancaria {
    private double saldo; // Só acessível dentro desta classe

    public void Depositar(double valor) {
        saldo += valor; // Acesso permitido
    }
}
```

### 2. `public` (Público)

O nível mais permissivo, concedendo acesso a membros e tipos por qualquer código dentro da aplicação.

- **Visibilidade:** Acessível em qualquer parte do código.

- **Acesso**: De qualquer lugar do código
- **Quando usar**: Para interfaces públicas e utilitários

```csharp
public class Calculadora {
    public static int Somar(int a, int b) {
        return a + b;
    }
}

// Uso em outro arquivo:
int resultado = Calculadora.Somar(5, 3);
```

### 3. `protected` (Protegido)

O acesso a membros e tipos protegidos é restrito à classe em que foram declarados e a classes derivadas.

Usar o acesso `protected` oferece um nível intermediário de acesso entre `public` e `private`.

- **Visibilidade:** Acessível na própria classe e em classes derivadas (herança). Os membros `protected` de uma classe base podem ser acessados por membros dessa classe base _e_ por membros de suas classes derivadas, mas não por clientes da classe.

- **Acesso**: Na própria classe e em classes derivadas (herança)
- **Quando usar**: Para compartilhar funcionalidades com subclasses

```csharp
class Animal {
    protected void Comer() {
        Console.WriteLine("Comendo...");
    }
}

class Cachorro : Animal {
    public void Alimentar() {
        Comer(); // Acesso permitido na subclasse
    }
}
```

### 4. `internal` (Interno)

Membros e tipos internos só podem ser acessados por código dentro do mesmo assembly (.exe ou .dll) da classe em que foram declarados.

- **Visibilidade:** Acessível apenas dentro do mesmo assembly (projeto).

- **Acesso**: Dentro do mesmo projeto/assembly
- **Quando usar**: Para compartilhar código dentro de um projeto

```csharp
internal class Logger {
    public static void Log(string mensagem) {
        Console.WriteLine(mensagem);
    }
}
```

### 5. `protected internal` (Protegido Interno)

Uma combinação dos níveis protegido e interno, permitindo acesso a membros e tipos por código do mesmo assembly ou por classes derivadas em outros assemblies.

- **Visibilidade:** Combina `protected` e `internal`. Acessível no mesmo assembly ou em subclasses de outros assemblies.

- **Acesso**: Combinação de `protected` e `internal`
- **Quando usar**: Em bibliotecas que precisam ser estendidas

```csharp
protected internal class Config {
    public static string ObterChave() {
        return "chave-secreta";
    }
}
```

### 6. `private protected` (Privado Protegido) (C# 7.2+)

Esse modificador de acesso combina `private` e `protected`, garantindo que o membro seja acessível **apenas por classes derivadas que estejam no mesmo assembly**. Isso significa que o código externo e classes derivadas em **outros** assemblies não podem acessá-lo.

- **Visibilidade:** Combina `private` e `protected`. Somente acessível por subclasses **dentro do mesmo assembly**.

- **Acesso:** Apenas classes derivadas no mesmo assembly podem utilizar o membro.
- **Quando usar:** Útil quando se deseja restringir o acesso a membros **apenas para herança dentro do mesmo projeto**, evitando que outras bibliotecas os acessem indevidamente.

```csharp
private protected class Configuracao {
    protected string ObterToken() {
        return "token-secreto";
    }
}
```

### 7. `sealed` (Selada)

O modificador `sealed` aplicado a uma classe impede que outras classes herdem dela. Quando aplicado a um método, impede que seja sobrescrito em classes derivadas.

1. Quando aplicado a uma **classe**: impede que outras classes herdem dela
2. Quando aplicado a um **método**: impede que seja sobrescrito em classes derivadas
3. Não afeta a visibilidade dos membros, apenas a capacidade de herança
4. Uma classe `sealed` pode ter qualquer modificador de acesso (`public`, `internal`, etc.)

Exemplo:

```csharp
public sealed class Pagamento {  // Não pode ser herdada
    public void Processar() {
        Console.WriteLine("Processando pagamento");
    }
}

// ERRO: Não pode herdar de sealed
// class PagamentoCartao : Pagamento {}
```

## Tabela Comparativa

| Modificador | Própria Classe | Classes Derivadas | Mesmo Assembly | Outros Assemblies | Pode ser Herdada? |
| --- | --- | --- | --- | --- | --- |
| `private` | Sim | Não | Não | Não | - |
| `protected` | Sim | Sim | Não | Não | Sim |
| `internal` | Sim | Não | Sim | Não | Sim |
| `protected internal` | Sim | Sim | Sim | Apenas derivadas | Sim |
| `private protected` | Sim | Sim | Sim | Não | Sim |
| `public` | Sim | Sim | Sim | Sim | Sim |
| `sealed` | Sim | - | Sim | Sim | **Não** |

## Práticas Recomendadas

- **Privado (`private`)**  
  Use para membros internos que não devem ser expostos. É ideal para proteger dados e funcionalidades restritas dentro da própria classe, garantindo encapsulamento e segurança.

- **Público (`public`)**  
  Exponha membros para uso geral. Essencial para APIs e utilitários que precisam ser acessíveis globalmente, promovendo interoperabilidade entre projetos.

- **Interno (`internal`)**  
  Compartilhe código dentro do mesmo assembly. Permite que membros sejam acessíveis dentro do projeto, promovendo modularidade sem exposição pública.

- **Protegido (`protected`)**  
  Facilita a reutilização em hierarquias de herança. Permite que classes derivadas acessem membros e tipos da classe base, promovendo extensão de funcionalidades sem violar encapsulamento.

- **Protegido Interno (`protected internal`)**  
  Permite que classes derivadas em outros assemblies acessem membros protegidos. Útil para bibliotecas que precisam ser estendidas sem expor completamente seus membros.

- **Privado Protegido (`private protected`)**  
  Restringe acesso a classes derivadas dentro do mesmo assembly. Ideal para garantir que apenas componentes internos possam herdar membros sem risco de exposição pública.

- **Selado (`sealed`)**  
  Impede herança. Use em classes que não devem ser estendidas, garantindo comportamento específico e impedindo modificações inesperadas.

## Boas Práticas

1. **Princípio do menor privilégio**: Use o modificador mais restritivo possível
2. **Evite `public` para campos**: Prefira propriedades
3. **`private` para implementação**: Mantenha detalhes internos ocultos
4. **`protected` com cuidado**: Pode quebrar encapsulamento

```csharp
// Boa prática: usar propriedades em vez de campos públicos
class Pessoa {
    private string nome; // Privado

    public string Nome { // Público com controle
        get => nome;
        set {
            if (!string.IsNullOrEmpty(value))
                nome = value;
        }
    }
}
```
