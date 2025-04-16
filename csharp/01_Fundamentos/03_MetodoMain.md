# O Método Main em C#

O método `Main` é o ponto de entrada de um aplicativo em C#. Ele define onde a execução do programa começa.

## Estrutura do Método `Main`

O `Main` é um método especial que pode ser declarado de diferentes formas. A sintaxe mais comum é:

```c#
static void Main()
```

Os **parênteses** após o identificador `Main` indicam que ele é um **método**.

---

## Por que `Main` é declarado como `static`?

O `Main` deve ser declarado como `static` porque, durante a inicialização do aplicativo, **nenhum objeto** da classe foi criado. Isso permite que o ambiente de execução invoque `Main` sem instanciar um objeto.

### Variações na Declaração do `Main`

Além da sintaxe padrão, `Main` pode ser declarado de outras formas:

1. **Com argumentos de linha de comando:**
   ```c#
   static void Main(string[] args)
   ```
   Isso permite que o programa receba parâmetros externos na execução.

2. **Com retorno do tipo `int` (em vez de `void`)**:
   ```c#
   static int Main()
   ```
   Isso pode ser útil quando um programa precisa retornar um código de sucesso ou falha para outro aplicativo.

---

## Múltiplos Métodos `Main` em um Projeto

Qualquer classe pode conter um método `Main`, e alguns programadores aproveitam isso para incluir pequenos aplicativos de teste em cada classe. No entanto, se houver mais de um `Main` em um projeto, é necessário especificar qual será o ponto de entrada.

### Como Definir o Ponto de Entrada no Visual Studio:

1. Com o projeto aberto no Visual Studio, selecione **Projeto > [ProjectName] Propriedades...**

2. Escolha a classe que contém o `Main` desejado na opção **Objeto de inicialização**.

---

## Conceitos Relacionados

### 1. Argumentos de Linha de Comando (`args`)

Os argumentos passados ao método `Main(string[] args)` são fundamentais para personalizar a execução de um programa, permitindo a entrada de dados externos no momento da execução.

#### **Usando argumentos de linha de comando**

Em diversos sistemas operacionais, os aplicativos podem receber **argumentos de linha de comando**, que são fornecidos diretamente ao serem executados. Para isso, o método `Main` deve incluir um parâmetro do tipo `string[]`, convencionalmente chamado de `args`.

Para executar um aplicativo e fornecer argumentos, basta:
1. Abrir o **Prompt de Comando**.
2. Navegar até o diretório onde está o arquivo `.exe` do aplicativo.
3. Digitar o nome do programa seguido dos argumentos e pressionar _Enter_.

O ambiente de execução então repassa esses argumentos ao método `Main`, armazenando-os como elementos na matriz `args`. O número de argumentos pode ser determinado por `args.Length`.

##### **Exemplo de uso**

Considere o comando abaixo:

```sh
MyApp a b
```

Nesse caso, o aplicativo `MyApp` recebe dois argumentos: `"a"` e `"b"`, que serão acessíveis no método `Main` através da matriz:

- `args[0]` conterá `"a"`
- `args[1]` conterá `"b"`
- `args.Length` será `2`

Os argumentos devem ser separados por espaços, e não por vírgulas. Essa abordagem é amplamente usada para fornecer opções de configuração e especificar nomes de arquivos.

#### **Especificando argumentos de linha de comando no Visual Studio**

Embora seja possível executar o aplicativo a partir do Prompt de Comando, o Visual Studio também permite definir argumentos diretamente no ambiente de desenvolvimento. Para isso:

1. No **Solution Explorer**, clique com o botão direito no nome do projeto e selecione **Propriedades**.
2. Acesse a guia **Depurar**.
3. Na caixa de texto **Argumentos de linha de comando**, insira os argumentos desejados.
4. Execute o aplicativo normalmente.

Dessa forma, o IDE transmite os argumentos especificados para o método `Main` na execução do programa.

### 2. Retorno de Status (`int Main()`)

Quando `Main` retorna um inteiro, ele pode ser usado para indicar o status de saída de um programa, geralmente **0** para sucesso e outros valores para erros.

### 3. Classes e Objetos em C#

Embora `Main` seja estático e não precise de uma instância, a maior parte dos programas em C# envolvem a criação e manipulação de objetos.

### 4. Estrutura do Projeto em C#

Projetos em C# normalmente contêm arquivos `.cs` organizados em namespaces, com `Main` atuando como ponto de entrada.

---
