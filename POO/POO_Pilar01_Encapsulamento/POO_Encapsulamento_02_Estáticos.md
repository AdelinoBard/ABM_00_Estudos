## **4. Atributos e Métodos Estáticos em C#**

Em C#, os **atributos e métodos estáticos** pertencem à própria classe, e não às instâncias individuais. Isso significa que todos os objetos dessa classe compartilham o mesmo valor do atributo estático, e métodos estáticos podem ser chamados sem a necessidade de criar um objeto.

### **4.1. Atributos Estáticos**

Um atributo estático é um campo que pertence à classe e não às suas instâncias. Ou seja, independentemente de quantos objetos existam dessa classe, todos compartilharão o mesmo valor desse atributo.

#### **Exemplo: Funcionários de um Banco**

Imagine um sistema que gerencia funcionários de um banco. Inicialmente, podemos definir a classe `Funcionario` da seguinte maneira:

```csharp
class Funcionario
{
    public string Nome;
    public double Salario;

    public void AumentaSalario(double aumento)
    {
        Salario += aumento;
    }
}
```

Agora, suponha que o banco oferece **um mesmo valor de vale-refeição diário para todos os funcionários**. Se definirmos esse atributo na classe sem o modificador `static`, cada funcionário teria um valor independente, o que não faz sentido, pois o benefício é uniforme para todos.

A solução correta é tornar `ValeRefeicaoDiario` um **atributo estático**, garantindo que ele pertença à classe e não às instâncias:

```csharp
class Funcionario
{
    public string Nome;
    public double Salario;
    public static double ValeRefeicaoDiario;

    public void AumentaSalario(double aumento)
    {
        Salario += aumento;
    }
}
```

Agora, `ValeRefeicaoDiario` deve ser acessado **pelo nome da classe**, e não por instâncias:

```csharp
Funcionario.ValeRefeicaoDiario = 15.0;
Console.WriteLine("Valor do vale-refeição diário: " + Funcionario.ValeRefeicaoDiario);
```

#### **Características dos Atributos Estáticos**

- São compartilhados entre todas as instâncias da classe.
- Devem ser acessados diretamente pelo nome da classe (`Classe.Atributo`).
- São úteis para armazenar valores globais da classe.

### **4.2. Métodos Estáticos**

Assim como podemos ter **atributos estáticos**, também podemos definir **métodos estáticos**, que pertencem à classe e não exigem a criação de um objeto para serem chamados.

#### **Exemplo: Reajuste do Vale-Refeição**

Imagine que o banco decide reajustar o valor do vale-refeição de acordo com uma taxa. Podemos criar um método estático para realizar esse ajuste:

```csharp
class Funcionario
{
    public string Nome;
    public double Salario;
    public static double ValeRefeicaoDiario;

    public static void ReajustaValeRefeicaoDiario(double taxa)
    {
        ValeRefeicaoDiario += ValeRefeicaoDiario * taxa;
    }
}
```

Agora, chamamos esse método pelo nome da classe:

```csharp
Funcionario.ValeRefeicaoDiario = 15.0; // Definindo valor inicial
Funcionario.ReajustaValeRefeicaoDiario(0.1); // Reajustando em 10%
Console.WriteLine("Novo valor do vale-refeição diário: " + Funcionario.ValeRefeicaoDiario);
```

#### **Características dos Métodos Estáticos**

- São chamados diretamente pelo nome da classe (`Classe.Metodo()`).
- Não têm acesso a atributos de instância, pois não operam em objetos individuais.
- São úteis para operações gerais que envolvem a classe como um todo.

### **4.3. Diferenças entre Estático e Instância**

| Característica | Estático | Instância |
| --- | --- | --- |
| Pertence a | Classe | Objeto (instância) |
| Modificador | `static` | Sem `static` |
| Necessário criar objeto? | Não | Sim |
| Acesso | `Classe.Atributo` | `objeto.Atributo` |
| Exemplo | `Funcionario.ValeRefeicaoDiario` | `meuFuncionario.Salario` |
