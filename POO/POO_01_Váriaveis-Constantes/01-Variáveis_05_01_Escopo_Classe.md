# Variáveis: Escopo de Classe, Variáveis de Instância e Estáticas

Variáveis declaradas dentro de uma classe, mas fora de métodos, são chamadas de **variáveis membro**.

- Termos genéricos:

  - **Variáveis globais**
  - **Variáveis Membro**

- **Definição**: Essas são variáveis declaradas diretamente dentro de uma classe, mas fora de métodos, construtores ou blocos.

- **Escopo**: Acessíveis por todos os métodos da classe.

- **Persistência**: Existe enquanto o objeto instanciado da classe existir.

- **Valores padrão**: Se nenhum valor inicial for atribuído, recebem valores padrão (como `0` para inteiros e `null` para objetos).

## Tipos de Variáveis de Classe

Elas podem ser:

- **Variáveis de instância**: Pertencem a objetos criados da classe (não são compartilhadas entre instâncias).

- **Variáveis estáticas**: Pertencem à classe como um todo e são compartilhadas entre todas as instâncias.

```csharp
class Exemplo {
    public int instancia;  // Variável de instância
    public static int compartilhada; // Variável estática
}
```

Juntas, as variáveis `estáticas` e as variáveis de `instância` de uma classe são conhecidas como seus **campos**.

Variáveis devem ser declaradas como campos de uma classe (ou seja, como variáveis de instância ou variáveis `estáticas`) _somente_ se forem necessárias para uso em mais de um método da classe ou se o aplicativo deve salvar seus valores entre chamadas para um determinado método.

### Variáveis de Instância

Uma classe possui _atributos_, que são implementados como **variáveis de instância**. Essas variáveis acompanham os objetos da classe durante todo o seu ciclo de vida. Cada objeto mantém sua própria cópia das variáveis de instância da classe, permitindo que sejam independentes umas das outras.

Normalmente, uma classe também define **métodos** e **propriedades** que manipulam as variáveis de instância específicas de cada objeto. Aqui estão algumas características importantes sobre as variáveis de instância:

- São declaradas dentro de uma declaração de classe, mas fora dos corpos de métodos e propriedades.
- Cada objeto tem sua própria cópia dessas variáveis.
- Elas representam o estado da classe e são carregadas com os objetos ao longo de seu ciclo de vida.
- Persistem enquanto o objeto existir.
- Podem possuir **modificadores de acesso** que controlam sua visibilidade.
- Não são perdidas quando um método termina (ao contrário de variáveis locais).

- **Resumindo**: Toda variável de instância é uma variável membro, mas nem toda variável membro é de instância (pois as variáveis estáticas são membros também).

- **Definição**: Um subconjunto das variáveis membro que **pertencem exclusivamente a uma instância específica da classe**. Cada objeto criado da classe tem sua própria cópia dessas variáveis.

- **Não são estáticas**: Elas existem apenas no contexto da instância e não são compartilhadas entre objetos.

#### Definição e Características

- Existem enquanto o objeto existir
- Cada objeto tem sua própria cópia
- Representam o estado do objeto

#### Onde declarar?

Você pode listar as variáveis ​​de instância da classe em qualquer lugar da classe fora de suas declarações de método (e propriedade), mas espalhar as variáveis ​​de instância pode levar a um código difícil de ler. Preferimos listar as variáveis ​​de instância de uma classe primeiro no corpo da classe, para que você veja os nomes e tipos das variáveis ​​antes que elas sejam usadas nos métodos e propriedades da classe.

#### Declaração Básica

A estrutura básica de uma variável de instância inclui:

1. **Modificador de acesso** (`opcional`) - definem a visibilidade da variável para outras partes do código.

2. **Tipo da variável** - define que tipo de dado a variável armazenará.

3. **Nome da variável** - Um identificador único para que ela seja acessada e referenciada.

4. **Valor inicial** (`opcional`)

```csharp
class Pessoa {
    public string nome;     // Pública
    private int idade;      // Privada - só acessível dentro da classe
    protected double altura; // Acessível na classe e herdeiras
}
```

#### Valores Padrão

Cada variável de instância tem um \_valor inicial padrão — \_um valor fornecido pelo C# se você não especificar o valor inicial da variável de instância. Portanto, variáveis de instância não precisam ser explicitamente inicializadas antes de serem usadas em um programa—a menos que elas devam ser inicializadas com valores diferentes de seus valores padrão.

Quando não inicializadas explicitamente, as variáveis recebem valores padrão:

- Tipos de Valor (Value Types)
  - **numéricos**
    - `int`, `long`, `short`, `byte`, `sbyte`: `0`
    - `float`: `0.0f`
    - `double`: `0.0d`
    - `decimal`: `0.0m`
    - `ulong`, `uint`, `ushort`: `0`
  - **bool**: `false`
  - **char**: `'\0'` (caractere nulo)
- Tipos de Referência (Reference Types) Variáveis de instância do tipo referência são inicializadas por padrão com o valor `null`.

  - **string**: `null`
  - **object**: `null`

- Structs e Enums
  - **Structs**: Cada membro da struct será inicializado com o valor padrão correspondente ao seu tipo.
  - **Enum**: O valor padrão será o elemento cujo valor é `0`.

### Variáveis Estáticas

- **Definição**: Variáveis `static` pertencem à **classe** em si, e não a instâncias individuais dela. Isso significa que há apenas **uma única cópia** dessas variáveis na memória, compartilhada por todos os objetos da classe.

- **Modificador estático**: Se definido como `static`, o campo pertence à classe e não às instâncias individuais.

- **Quando usar**: São úteis para armazenar dados ou estados que são comuns a todas as instâncias de uma classe.

Ao criar objetos de uma classe que contém variáveis **estáticas**, todos os objetos compartilham **uma única cópia** dessas variáveis. Isso significa que não é necessário que cada objeto tenha sua própria cópia individual.

> Observação de Engenharia de Software:
>
> _Variáveis estáticas devem ser utilizadas quando todos os objetos de uma classe precisam compartilhar a mesma cópia da variável._

#### Definição e Uso

- Compartilhada por todas as instâncias
- Acessada pelo nome da classe
- Existe enquanto o programa estiver em execução

```csharp
class Contador {
    public static int Total; // Variável estática

    public Contador() {
        Total++; // Incrementa o contador a cada nova instância
    }
}
```

#### Comportamento das variáveis estáticas

1. **Escopo**:

- Uma variável estática é acessível por todos os métodos da classe, independentemente de estarem marcados como `static` ou não. O escopo de uma variável `estática` é o corpo de sua classe.
- Pode ser acessada diretamente pela classe, sem a necessidade de instanciar um objeto.

2. **Persistência**:

- A variável existe na memória durante toda a execução do programa, mesmo que nenhum objeto da classe tenha sido criado.

> Observação de engenharia de software:
>
> _variáveis, métodos e propriedades estáticos existem e podem ser usados, mesmo que nenhum objeto dessa classe tenha sido instanciado. membros estáticos ficam disponíveis assim que a classe é carregada na memória no momento da execução._

3. **Acesso**:

- Pode ser acessada diretamente usando o nome da classe:
  ```csharp
  NomeDaClasse.VariavelEstatica;
  ```
- Não é necessário usar o nome de uma instância.

> Observação de engenharia de software:
>
> Os membros de classe `public static` podem ser acessados diretamente, bastando qualificar o nome do membro com o nome da classe e o operador de acesso (`.`), como em `Math.PI`.
>
> Já os membros de classe `private static` são acessíveis _exclusivamente_ pelos métodos e propriedades da própria classe. Para permitir o acesso a um membro `private static` fora de sua classe, pode-se oferecer um método ou propriedade `public static`.
>
> _Tentar acessar ou invocar um membro estático por meio de uma instância da classe, como se fosse um membro não estático, resulta em erro de compilação._
>
> Um método ou propriedade `estático` não consegue acessar diretamente membros de classe não `estáticos`, pois métodos ou propriedades `estáticos` podem ser chamados mesmo quando _nenhum_ objeto da classe está instanciado. Por esse motivo, o uso da referência `this` também não é permitido em métodos `estáticos`. Isso ocorre porque `this` sempre aponta para um _objeto específico_ da classe. Ao chamar um método `estático`, ele não tem como identificar qual objeto manipular, e pode ser que não exista _nenhum_ objeto da classe na memória naquele momento.

4. **Valor Padrão**:

- Quando você declara uma variável `static` e não a inicializa, o compilador a inicializa para o valor padrão do tipo

#### Quando usar variáveis estáticas?

- Para armazenar contadores globais.
- Para valores constantes ou estados que devem ser compartilhados entre todas as instâncias.
- Para configurar comportamentos estáticos relacionados à classe como um todo.

#### Acesso e Limitações de Variáveis Estáticas Públicas.

Variáveis estáticas são atributos pertencentes à classe e não às instâncias dela. Quando possuem o modificador de acesso `public`, tornam-se acessíveis fora da classe onde foram declaradas, podendo ser utilizadas em outras partes do mesmo programa. Isso significa que qualquer parte do código que tenha uma referência à classe pode acessar essas variáveis, sem a necessidade de criar objetos da classe.

Entretanto, é importante ressaltar que essas variáveis **não são acessíveis além do programa** onde estão definidas. Elas permanecem restritas ao ambiente em que o código é executado, salvo situações em que haja integração explícita, como o uso de APIs ou mecanismos específicos de comunicação entre programas.

Por isso, o uso de variáveis estáticas públicas deve ser feito com responsabilidade, garantindo que informações sensíveis não sejam expostas inadvertidamente, promovendo segurança e organização no desenvolvimento do software.

#### uso de variáveis `estáticas`

Por outro lado, cada objeto possui sua _própria_ cópia das variáveis de instância da classe a que pertence. Entretanto, em situações específicas, pode ser necessário que apenas uma única cópia de determinada variável seja _compartilhada_ por todos os objetos de uma classe. Nesse caso, utilizamos uma **variável estática** (ou propriedade estática). Uma variável ou propriedade `estática` armazena **informações relacionadas à classe como um todo** — todos os objetos da classe acessam os mesmos dados. A declaração de uma variável ou propriedade `estática` é feita com a palavra-chave `static`.

Para ilustrar o uso de variáveis `estáticas`, vejamos um exemplo. Suponha que temos um jogo com `Marcianos` e outras criaturas espaciais. Cada `Marciano` tende a ser corajoso e disposto a atacar quando sabe que há pelo menos quatro outros `Marcianos` presentes. Caso contrário, quando menos de cinco `Marcianos` estão por perto, cada um deles se torna covarde. Assim, todos os `Marcianos` precisam estar cientes do número total de `Marcianos` existentes, representado pela variável `martianCount`.

Inicialmente, poderíamos criar a classe `Marciano` com `martianCount` como uma variável de instância. No entanto, isso faria com que cada `Marciano` tivesse uma cópia separada dessa variável. A cada novo `Marciano` criado, seria necessário atualizar manualmente a variável `martianCount` em cada objeto individual, o que desperdiçaria memória, aumentaria o tempo de execução e deixaria o código suscetível a erros.

Para resolver esse problema, declaramos `martianCount` como `estático`, permitindo que a variável represente um dado compartilhado por toda a classe. Assim, todos os `Marcianos` podem acessar o mesmo `martianCount`, mas apenas uma única cópia dessa variável é mantida. Isso economiza espaço e simplifica o código, já que o construtor de `Marciano` precisa apenas incrementar o valor de `martianCount` _uma única vez_, sem a necessidade de atualizações redundantes em múltiplas instâncias.

### Comparação: Estática vs Instância

| Característica | Instância                 | Estática                   |
| -------------- | ------------------------- | -------------------------- |
| Cópias         | Uma por objeto            | Única para toda classe     |
| Acesso         | Por objeto (`obj.nome`)   | Por classe (`Classe.nome`) |
| Tempo de vida  | Enquanto o objeto existir | Toda execução do programa  |

### Exemplos Práticos

#### Exemplo 1: Contador de Instâncias

```csharp
class Carro {
    public static int Quantidade; // Estática
    public string Modelo;         // De instância

    public Carro(string modelo) {
        Modelo = modelo;
        Quantidade++;
    }
}

// Uso:
var carro1 = new Carro("Fusca");
var carro2 = new Carro("Gol");
Console.WriteLine(Carro.Quantidade); // Mostra 2
```

#### Exemplo 2: Configuração Global

```csharp
class Config {
    public static string Idioma = "pt-BR"; // Configuração compartilhada
}

// Acesso em qualquer lugar:
Console.WriteLine(Config.Idioma);
```

## Tópicos Correlatos (Não Abordados em Detalhe)

### Variáveis Locais

- Declaradas dentro de métodos
- Existem apenas durante a execução do método

### Constantes

- Valores imutáveis declarados com `const`
- Implicitamente estáticas

### Propriedades

- Forma controlada de acessar variáveis membro
- Podem ter lógica de validação

### Modificadores de Acesso Adicionais

- `internal`: Visível apenas no assembly
- `protected internal`: Combinação de protegido e interno

### Inicializadores de Variáveis

- Sintaxe para atribuir valores iniciais
- Útil para coleções e valores complexos
