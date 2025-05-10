# Relacionamentos: Associação, Agregação e Composição

## Associação

A associação é um vínculo entre duas classes que permite que uma classe faça uso dos serviços de outra. Esse relacionamento pode ser unidirecional ou bidirecional.

```csharp
class Cliente
{
    public string Nome { get; set; }
}

class Pedido
{
    public int Numero { get; set; }
    public Cliente Cliente { get; set; }
}
```

Aqui, `Cliente` e `Pedido` estão associados. Um cliente pode fazer vários pedidos, mas a existência dos pedidos não depende da existência do cliente.

## Agregação

A agregação representa um relacionamento "todo-parte" onde a parte pode existir independentemente do todo. No exemplo de um banco, um cliente pode ter vários cartões de crédito.

```csharp
class Cliente
{
    public string Nome { get; set; }
}

class CartaoDeCredito
{
    public int Numero { get; set; }
    public string DataDeValidade { get; set; }
    public Cliente Cliente { get; set; } // Agregação
}
```

Neste caso, um `CartaoDeCredito` está agregado a um `Cliente`. Se o cliente for removido do sistema, os cartões de crédito ainda podem existir, representando a agregação.

## Composição

A composição é um tipo mais forte de relacionamento "todo-parte" onde a parte não pode existir sem o todo. Se o todo for destruído, a parte também será.

```csharp
class Motor
{
    public int Potencia { get; set; }
}

class Carro
{
    public Motor Motor { get; private set; }

    public Carro()
    {
        Motor = new Motor(); // Composição
    }
}
```

Aqui, `Carro` compõe `Motor`. Se um `Carro` for destruído, seu `Motor` também será, pois o motor não pode existir independentemente do carro.

# Detalhamento

## Composição

Uma classe pode ter objetos de tipos de valores ou referências a objetos de outras classes como membros. Isso é chamado de **composição** e às vezes é chamado de um **_tem-um_** **relacionamento**. Por exemplo, um objeto da classe `AlarmClock` precisa saber a hora atual _e_ a hora em que deve soar seu alarme, então é razoável incluir _duas_ referências a objetos `Time` em um objeto `AlarmClock`.

> Observação de Engenharia de Software: _Uma forma de reutilização de software é a composição, na qual uma classe contém referências a outros objetos. Lembre-se de que classes são tipos de referência. Uma classe pode ter uma propriedade de seu próprio tipo — por exemplo, uma classe Person pode ter propriedades Mother e Father do tipo Person que referenciam outros objetos Person._

Você viu que a composição permite que uma classe tenha referências a objetos de outras classes como membros.

_composition_ — uma capacidade que permite que uma classe tenha referências a objetos de outras classes como membros.

### Analogia

Para facilitar a compreensão, podemos usar a analogia de um controle remoto e uma TV para associação. Um controle remoto (associação) pode controlar várias TVs, e cada TV pode ter vários controles remotos. Em uma agregação, pense em um clube (Cliente) e seus membros (CartaoDeCredito). Os membros podem existir independentemente do clube. Em uma composição, pense em um livro (Carro) e seus capítulos (Motor). Se o livro for destruído, seus capítulos também serão.
