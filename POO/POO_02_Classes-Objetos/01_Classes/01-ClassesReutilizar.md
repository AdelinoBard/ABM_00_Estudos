# Criando e Usando Classes Reutilizáveis em C#

Quando desenvolvemos um software, muitas vezes queremos reutilizar certas funcionalidades sem precisar reescrevê-las toda vez. Para isso, usamos **bibliotecas de classes**, onde armazenamos classes que podem ser reaproveitadas em diferentes projetos.

## 1. Criando uma Classe Pública

Para que uma classe seja reutilizável, ela deve ser declarada como `public`. Isso permite que outras partes do programa, ou mesmo outros projetos, possam acessá-la.

### Exemplo:

```c#
public class Mensagem
{
    public void Exibir()
    {
        Console.WriteLine("Olá! Esta é uma classe reutilizável.");
    }
}
```

Se a classe não for `public`, ela só poderá ser utilizada dentro do mesmo assembly (arquivo **.dll** ou **.exe**).

## 2. Definindo um Namespace

Um **namespace** é uma maneira de organizar classes dentro de um projeto. Ele evita conflitos de nomes e facilita a reutilização.

### Exemplo:

```c#
namespace Utilitarios
{
    public class Mensagem
    {
        public void Exibir()
        {
            Console.WriteLine("Olá! Esta é uma classe reutilizável.");
        }
    }
}
```

Agora, para usar essa classe em outro código, basta referenciar o namespace:

```c#
using Utilitarios;

class Programa
{
    static void Main()
    {
        Mensagem msg = new Mensagem();
        msg.Exibir();
    }
}
```

## 3. Compilando a Classe em uma Biblioteca (.DLL)

Para tornar a classe reutilizável em diferentes projetos, devemos empacotá-la em uma **biblioteca de classes**.

### Passos:

1. No **Visual Studio**, crie um novo projeto do tipo **Biblioteca de Classes**.
2. Adicione sua classe ao projeto.
3. Compile o projeto para gerar um arquivo **.dll**.

Esse **.dll** poderá ser usado em outros projetos.

## 4. Adicionando uma Referência à Biblioteca de Classes

Após criar a biblioteca, é necessário adicioná-la ao projeto que deseja utilizá-la.

### Passos:

1. No **Visual Studio**, clique com o botão direito em "Referências" dentro do seu projeto.
2. Selecione **Adicionar Referência...**.
3. Escolha **Procurar** e localize o arquivo **.dll** gerado.

Agora, o projeto já pode utilizar a classe reutilizável.

## 5. Utilizando a Classe

Com a biblioteca referenciada, podemos usar a classe normalmente em nosso código.

### Exemplo:

```c#
using Utilitarios;

class Programa
{
    static void Main()
    {
        Mensagem msg = new Mensagem();
        msg.Exibir();
    }
}
```

Agora podemos chamar métodos da classe reutilizável sem precisar reescrevê-la.
