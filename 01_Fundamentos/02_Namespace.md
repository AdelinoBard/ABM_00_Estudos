- `csharp`
- Estrutura: 01_Fundamentos
- Seq: 02
- Título: Namespace

> csharp\01_Fundamentos\02_Namespace.md

---

# Namespaces
Os **namespaces** são usados para organizar e agrupar tipos relacionados em um programa. Eles ajudam a evitar conflitos de nomes e permitem reutilizar tipos com o mesmo nome desde que estejam em namespaces diferentes.

No .NET, os namespaces fazem parte da **Biblioteca de Classes do .NET Framework**, agrupando classes predefinidas para facilitar a reutilização e manutenção do código.

Os aplicativos C# são escritos combinando suas propriedades, métodos e classes com propriedades, métodos e classes predefinidos disponíveis na Biblioteca de Classes do .NET Framework e em outras bibliotecas de classes.

> Coletivamente, os namespaces predefinidos do .NET são conhecidos como **Biblioteca de Classes do .NET Framework**. 

---

## Organização Lógica em Programação
Em um projeto de software, o código-fonte geralmente é distribuído em vários arquivos. À medida que a quantidade de arquivos aumenta, surge a necessidade de organizá-los para facilitar a localização e a manutenção. A solução para essa organização lógica é o uso de **namespaces**.

> As classes relacionadas são frequentemente agrupadas em namespaces e compiladas em bibliotecas de classes para que possam ser reutilizadas em outros aplicativos.

---

## Conceito de Namespaces

Os namespaces funcionam como pastas ou diretórios que contêm classes e interfaces relacionadas. Eles fornecem um **escopo** para os identificadores (como nomes de tipos, funções e variáveis) dentro deles. Ao utilizar namespaces, podemos evitar conflitos de nomes e organizar nosso código de maneira mais eficiente.
- Ou seja, Um `namespace` é uma região declarativa que fornece um escopo para os identificadores (nomes dos tipos, função, variáveis etc.) dentro dele.  

Um namespace pode conter **classes, structs, interfaces, enumerações e outros namespaces**. Essa estrutura evita conflitos entre nomes idênticos de diferentes partes do código.

Para definir um namespace em C#, utilizamos a palavra-chave `namespace`.

```csharp
namespace MinhaSolucao
{
    class Conta
    {
        // Corpo da classe Conta
    }
}
```

Nesse exemplo, criamos um namespace chamado `MinhaSolucao` e dentro dele declaramos a classe `Conta`. É comum criar uma pasta com o mesmo nome do namespace e salvar todos os arquivos-fonte relacionados a esse namespace nessa pasta.

---

## Hierarquia de Namespaces
Um programa C# pode consistir em vários arquivos, e cada arquivo pode conter zero ou mais namespaces.

Assim como pastas em um sistema operacional, os namespaces podem ser aninhados dentro de outros namespaces. Isso ajuda a organizar logicamente os arquivos de uma aplicação.

Um namespace pode conter outro:

```csharp
namespace NomeSolucao
{
    namespace Contas
    {
        class Conta
        {
            // Corpo da classe Conta
        }
    }
}
```

Outra forma de aninhar namespaces é utilizar o símbolo `.`:

```csharp
namespace NomeSolucao.Contas
{
    class Conta
    {
        // Corpo da classe
    }
}
```

Nesse exemplo, temos um namespace chamado `NomeSolucao` que contém outro namespace chamado `Contas`, que, por sua vez, contém a classe `Conta`.

---

## Nome Simples vs. Nome Completo

- **Nome Simples (Unqualified Name):** 

    - Apenas o nome da classe ou interface dentro do namespace.

    - É o identificador declarado à direita do comando `class` ou `interface`. Por exemplo, na classe acima, o nome simples é `Conta`.

- **Nome Completo (Fully Qualified Name):** 
    
    - Inclui a estrutura hierárquica do namespace.

    - É formado pela concatenação dos nomes dos namespaces com o nome simples, usando o caractere `.`. No exemplo, o nome completo é `NomeSolucao.Contas.Conta`.

```csharp
namespace NomeSolucao.Contas
{
    class Conta {}
}
```
O nome completo da classe acima é `NomeSolucao.Contas.Conta`.

---

## Conflito de nomes
Os namespaces organizam grupos de classes relacionadas. Lembre-se que o nome de cada classe é, na verdade, uma combinação do nome do namespace, um ponto (`.`) e o nome da classe — novamente, isso é conhecido como o nome totalmente qualificado da classe. 

Se outro namespace também contiver uma classe com o mesmo nome, os nomes de classe totalmente qualificados devem ser usados para distinguir entre as classes no aplicativo e evitar um **conflito de nomes** (também chamado de **colisão de nomes**).

---

## Namespaces e Relacionamento entre Classes

### Classes no Mesmo Namespace
Classes dentro do mesmo namespace podem se referir umas às outras sem especificar o nome do namespace.

Conversa entre Classes no Mesmo Namespace. Quando duas classes pertencem ao mesmo namespace, elas podem "conversar" entre si usando apenas o **nome simples** de cada uma.

```csharp
namespace NomeSolucao.Contas
{
    class Conta {}
    class ContaPoupanca : Conta {}
}
```

Aqui, `ContaPoupanca` pode herdar de `Conta` diretamente, pois ambas estão no mesmo namespace.

```csharp
// Arquivo: NomeSolucao\Contas\Conta.cs

namespace NomeSolucao.Contas
{
    class Conta
    {
        // Corpo da classe Conta
    }
}

// Arquivo: NomeSolucao\Contas\ContaPoupanca.cs

namespace NomeSolucao.Contas
{
    class ContaPoupanca : Conta // herança
    {
        // Corpo da classe ContaPoupanca
    }
}
```

Nesse exemplo, a classe `ContaPoupanca` herda da classe `Conta` usando apenas o nome simples.

### Classes em Namespaces Diferentes
Para referenciar uma classe de outro namespace, usamos o nome completo ou a diretiva `using`.

Comunicação entre Classes em Diferentes Namespaces. Quando duas classes pertencem a namespaces diferentes, é necessário usar o **nome completo** de cada uma para que possam "conversar" entre si.

```csharp
namespace NomeSolucao.Contas
{
    class Conta {}
}

namespace NomeSolucao.Clientes
{
    class Cliente
    {
        private NomeSolucao.Contas.Conta conta;
    }
}
```

Nesse caso, `Cliente` precisa especificar `NomeSolucao.Contas.Conta` para acessar a classe `Conta`.

```csharp
// Arquivo: NomeSolucao\Contas\Conta.cs

namespace NomeSolucao.Contas
{
    class Conta
    {
        // Corpo da classe Conta
    }
}

// Arquivo: NomeSolucao\Clientes\Cliente.cs

namespace NomeSolucao.Clientes
{
    class Cliente
    {        
        private NomeSolucao.Contas.Conta conta; // herança
    }
}
```

Nesse caso, a classe `Cliente` utiliza o nome completo `NomeSolucao.Contas.Conta` para se referir à classe `Conta`.

---

## Namespace Global

Todas as classes, interfaces ou namespaces que não são explicitamente colocados em um namespace são automaticamente colocados no **namespace global**.

O namespace global é como o diretório raiz onde todos os elementos não especificamente organizados em outros namespaces residem.

```csharp
class MinhaClasse {}
```

Aqui, `MinhaClasse` está no namespace global e pode ser referenciada sem prefixo de namespace.

---

## Diretivas `using` e Namespaces do .NET
A diretiva `using` permite usar classes de um namespace sem precisar do nome completo.

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```
Sem `using System;`, precisaríamos escrever `System.Console.WriteLine();`.

> Observação de engenharia: _O compilador C# não requer o uso de declarações em um arquivo de código-fonte se o nome de classe totalmente qualificado for especificado toda vez que um nome de classe for usado. Muitos programadores preferem o estilo de programação mais conciso habilitado pelo uso de declarações._

---

## Localizando informações adicionais sobre os métodos de uma classe .NET

O .NET possui vários namespaces padrões, como:
- `System` (operações básicas)
- `System.IO` (manipulação de arquivos)
- `System.Net` (operações de rede)
- `System.Collections.Generic` (coleções genéricas)

Você pode localizar informações adicionais sobre os métodos de uma classe .NET na referência _.NET Framework Class Library_

`[https://msdn.microsoft.com/library/mt472912](https://msdn.microsoft.com/library/mt472912)`

Ao visitar este site, você verá uma lista alfabética de todos os namespaces na Framework Class Library. Localize o namespace e clique em seu link para ver uma lista alfabética de todas as suas classes, com uma breve descrição de cada uma. Clique no link de uma classe para ver uma descrição mais completa da classe. Clique no link Methods na coluna da esquerda para ver uma lista dos métodos da classe.

---

## Conceitos Relacionados

- **Assemblies:** Um assembly é um contêiner de código compilado que pode conter múltiplos namespaces.
- **Bibliotecas de Classes:** Conjuntos de classes organizadas em namespaces, reutilizáveis em diferentes projetos.
- **Modularização:** Uso de namespaces para dividir aplicações em partes menores e gerenciáveis.
- **Espaço de Nomes Dinâmico:** Namespaces podem ser definidos dinamicamente em tempo de execução em algumas linguagens.

---