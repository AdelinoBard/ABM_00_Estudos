# Classes Públicas e Privadas em C#

Em C#, as classes podem ser declaradas como públicas ou privadas, controlando onde e como podem ser acessadas.

- **Classes públicas** são ideais para funcionalidades que precisam ser compartilhadas em todo o projeto ou entre projetos.
- **Classes privadas** são úteis para encapsular lógica interna, evitando acesso indevido.

## 1. Classes Públicas

### Definição

Uma classe pública é declarada com o modificador `public`, permitindo que seja acessada de qualquer parte do código, inclusive de outros projetos.

### Exemplo Básico

```csharp
public class Animal
{
    public string Nome { get; set; }

    public void EmitirSom()
    {
        Console.WriteLine($"{Nome} faz um som.");
    }
}
```

### Características

- **Acesso global**: Pode ser usada em qualquer arquivo ou projeto.
- **Propriedades e métodos públicos**: Membros marcados como `public` são acessíveis externamente.

### Como Usar

```csharp
Animal cachorro = new Animal();
cachorro.Nome = "Rex";
cachorro.EmitirSom(); // Saída: "Rex faz um som."
```

## 2. Classes Privadas

### Definição

Uma classe privada é declarada com o modificador `private` e só pode ser acessada dentro do escopo onde foi definida, como dentro de outra classe.

### Exemplo Básico

```csharp
public class Escola
{
    private class Aluno
    {
        public string Nome { get; set; }

        public void Estudar()
        {
            Console.WriteLine($"{Nome} está estudando.");
        }
    }

    public void CriarAluno()
    {
        Aluno aluno = new Aluno();
        aluno.Nome = "Maria";
        aluno.Estudar(); // Saída: "Maria está estudando."
    }
}
```

### Características

- **Acesso restrito**: Só pode ser usada dentro da classe que a contém.
- **Uso interno**: Ideal para encapsular lógica que não precisa ser exposta externamente.

### Como Usar

```csharp
Escola escola = new Escola();
escola.CriarAluno(); // A classe Aluno não pode ser acessada diretamente aqui.
```

## 3. Comparação entre Classes Públicas e Privadas

| Característica | Classe Pública | Classe Privada |
| --- | --- | --- |
| **Acesso** | Global (qualquer lugar) | Restrito (dentro da classe) |
| **Modificador** | `public` | `private` |
| **Uso Recomendado** | Para funcionalidades gerais | Para encapsular detalhes internos |

## 4. Exemplo Prático Combinado

```csharp
public class Carro
{
    private class Motor
    {
        public void Ligar()
        {
            Console.WriteLine("Motor ligado.");
        }
    }

    public void Iniciar()
    {
        Motor motor = new Motor();
        motor.Ligar();
        Console.WriteLine("Carro pronto para uso.");
    }
}
```

### Como Usar

```csharp
Carro meuCarro = new Carro();
meuCarro.Iniciar(); // Saída: "Motor ligado." seguido de "Carro pronto para uso."
// A classe Motor não pode ser acessada diretamente aqui.
```
