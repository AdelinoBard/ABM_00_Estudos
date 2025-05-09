# Variáveis: Escopo

O escopo de uma variável define onde ela pode ser acessada no código. Em C#, o escopo determina a visibilidade e a vida útil de uma variável, limitando seu uso a partes específicas do programa. Entender o escopo é essencial para evitar erros e escrever código organizado.

## Tipos de Escopo

Em C#, podemos identificar quatro tipos principais de escopo de uma variável:

### 1. Escopo de Classe

Variáveis declaradas no nível da classe são acessíveis em todos os métodos da classe. Podem ser públicas, privadas ou estáticas.

> **Variáveis globais**

**Exemplo:**

```csharp
class Exemplo
{
    private int valor = 10; // Variável de classe (escopo global dentro da classe)

    public void MostrarValor()
    {
        Console.WriteLine(valor); // Acessível aqui
    }
}
```

### 2. Escopo de Método

Variáveis declaradas dentro de um método são locais e só podem ser usadas dentro dele.

> **Variáveis locais**

**Exemplo:**

```csharp
void Metodo()
{
    int numero = 5; // Variável local
    Console.WriteLine(numero);
}
// 'numero' não é acessível aqui
```

### 3. Escopo de Bloco

Variáveis declaradas dentro de blocos (como `if`, `for`, `while`) só existem dentro desses blocos. Acessíveis apenas dentro do bloco onde foram criadas.

> **Variáveis locais de bloco**

**Exemplo:**

```csharp
if (true)
{
    int temp = 20; // Variável de bloco
    Console.WriteLine(temp);
}
// 'temp' não é acessível aqui
```

### 4. Escopo de Parâmetro

Parâmetros de métodos têm escopo limitado ao corpo do método.

> **Variáveis locais de parâmetros**

**Exemplo:**

```csharp
void Saudacao(string nome) // 'nome' é um parâmetro
{
    Console.WriteLine($"Olá, {nome}!");
}
// 'nome' não é acessível aqui
```

## Variáveis Locais vs. Globais

### 1. Variáveis Locais

- **Definição**: Declaradas dentro de métodos ou blocos.

- **Escopo**: Limitado ao bloco onde foram declaradas.

- **Inicialização**: Devem ser inicializadas antes do uso.

**Exemplo:**

```csharp
void Calcular()
{
    int x = 10; // Inicialização obrigatória
    Console.WriteLine(x * 2);
}
```

No C#, é obrigatório que variáveis locais sejam **definitivamente atribuídas**, ou seja, cada variável local deve receber um valor antes que seu uso seja permitido.

_Todas as variáveis locais precisam estar devidamente inicializadas antes que seus valores possam ser empregados em expressões. Caso contrário, tentar utilizar uma variável local sem que ela tenha sido definitivamente atribuída resultará em um erro de compilação._

_Uma prática recomendada para evitar erros desse tipo é inicializar variáveis locais no momento da declaração. Apesar de o C# não exigir que a inicialização aconteça diretamente na declaração, ele assegura que as variáveis locais sejam inicializadas antes de serem usadas em qualquer expressão._

### 2. Variáveis Globais

- **Definição**: Declaradas no nível da classe.

- **Escopo**: Acessíveis em toda a classe.

- **Uso**: Evite variáveis globais desnecessárias para manter o código modular.

**Exemplo:**

```csharp
class Calculadora
{
    private int resultado; // Variável global

    public void Somar(int a, int b)
    {
        resultado = a + b;
        Console.WriteLine(resultado);
    }
}
```

```csharp
class Exemplo {
    public int global = 20; // Variável global
        void Metodo() {
            Console.WriteLine(global); // Acessível aqui
    }
}
```

## Sombreamento de Variáveis

Se um método contiver uma variável local com o _mesmo_ nome de uma variável de instância, diz-se que a variável local _sombreia_ (ou oculta) a variável de instância no corpo do método.

Ocorre quando uma variável local tem o mesmo nome de uma variável global. Use `this` para referenciar a variável global.

**Exemplo:**

```csharp
class Exemplo
{
    private int valor = 100;

    public void Atualizar(int valor) // Parâmetro 'valor' sombreia a variável de instância
    {
        this.valor = valor; // 'this' evita ambiguidade
    }
}
```

- Use `this` para acessar a variável de instância quando houver sombreamento

- Adote convenções de nomenclatura diferentes para parâmetros e variáveis de instância

> Observação de Engenharia de Software: _Usar propriedades em uma classe para acessar as variáveis de instância da classe normalmente elimina o sombreamento porque os nomes de propriedade usam a nomenclatura Pascal Case (primeira letra maiúscula) e os nomes de parâmetros usam Camel Case (primeira letra minúscula)._

### Exemplo Prático

```csharp
class Pessoa
{
    private string nome; // Variável global

    public Pessoa(string nome)
    {
        this.nome = nome; // 'this' resolve sombreamento
    }

    public void Cumprimentar()
    {
        string mensagem = "Bem-vindo"; // Variável local
        Console.WriteLine($"{mensagem}, {nome}!");
    }
}
```

## Boas Práticas

1. **Encapsulamento**: Use `private` para variáveis de classe e exponha-as via propriedades. Prefira variáveis privadas com acesso via propriedades

2. **Inicialização**: Sempre inicialize variáveis locais.

3. **Nomenclatura**: Use nomes descritivos - Use `camelCase` para variáveis e `PascalCase` para propriedades.

4. **Imutabilidade**: Use `readonly` para dados que não devem mudar.

5. **Organização**: Declare variáveis no início do método ou classe.

6. **Globais**: Evite variáveis globais desnecessárias.

## Conceitos Correlatos

1. **Modificadores de Acesso**: `public`, `private`, `protected`, `internal`.

2. **Ciclo de Vida de Variáveis**: Tempo de vida de uma variável no programa.

3. **Constantes**: Uso de `const` para valores imutáveis.

4. **Propriedades**: Controle de acesso a variáveis de classe.

5. **Namespaces**: Organização de escopo em projetos maiores.
