# **Encapsulamento**

O **encapsulamento** é um dos princípios fundamentais da **Programação Orientada a Objetos (POO)** e tem como objetivo **proteger os dados de uma classe**, expondo apenas o necessário e garantindo a integridade do código.

## **Objetos na Programação Orientada a Objetos (POO)**

Compreender o conceito de **objeto** é essencial para a programação orientada a objetos. Objetos são a base dessa abordagem e podem ser encontrados em nosso cotidiano: seu computador, seu carro e até mesmo este texto são exemplos de objetos.

### **Características dos Objetos no Mundo Real**

Os objetos do mundo real possuem duas características fundamentais: **estado** e **comportamento**.

- **Estado:** Representa os atributos ou propriedades de um objeto. Por exemplo, um cachorro possui estados como nome, raça, tamanho e peso. Da mesma forma, uma bicicleta tem estados como marcha atual e velocidade.

- **Comportamento:** Diz respeito às ações que um objeto pode realizar. Um cachorro pode latir, brincar, correr e dormir, enquanto uma bicicleta pode trocar de marcha, acelerar e frear.

Observar objetos do cotidiano e identificar seus estados e comportamentos é uma abordagem prática para compreender a POO. Além disso, muitos objetos são compostos por outros e podem depender uns dos outros, refletindo relações que também existem na modelagem de software.

### **Objetos no Software**

No contexto da programação, um **objeto** apresenta características similares às dos objetos do mundo real, possuindo **estado** e **comportamento**.

- **Estado:** Armazenado em campos (ou variáveis) do objeto.

- **Comportamento:** Definido por métodos (ou funções), que determinam as ações que o objeto pode realizar.

Os métodos manipulam o estado interno do objeto e servem como o principal meio de comunicação entre diferentes objetos. Uma prática fundamental da POO é ocultar os detalhes internos de um objeto, permitindo que interações externas ocorram exclusivamente por meio de métodos — um conceito conhecido como **encapsulamento**.

## **Encapsulamento**

O encapsulamento, na programação orientada a objetos, refere-se à separação e proteção dos dados de um objeto, garantindo que ele controle sua própria lógica interna. Esse princípio torna o software mais flexível, facilitando modificações e melhorias na implementação.

Com o encapsulamento, um objeto pode controlar como o mundo externo interage com ele. Por exemplo, se uma bicicleta tem um limite de 10 marchas, o método para mudar de marcha pode impedir qualquer valor fora dessa faixa, garantindo a integridade do estado do objeto.

**Exemplo em C#:**

```csharp
public class Bicicleta
{
    private int marchaAtual;
    private const int marchaMaxima = 10;
    private const int marchaMinima = 1;

    public int MarchaAtual => marchaAtual;

    public void MudarMarcha(int novaMarcha)
    {
        if (novaMarcha >= marchaMinima && novaMarcha <= marchaMaxima)
        {
            marchaAtual = novaMarcha;
        }
        else
        {
            Console.WriteLine("Marcha inválida. Escolha um valor entre 1 e 10.");
        }
    }
}
```

## **1. O Que é Encapsulamento?**

O **encapsulamento** consiste em **esconder os detalhes internos** de uma classe e fornecer formas controladas de acesso aos seus dados. Isso evita que informações sejam modificadas diretamente e permite adicionar validações e lógica de controle.

- **Definição:** O encapsulamento envolve a combinação de dados (atributos) e métodos (comportamentos) em uma única unidade chamada **classe**.
- **Princípio:** Cada classe deve ser responsável por gerenciar seus próprios dados e comportamentos.
- **Objetivo:** Isolar os detalhes internos da classe, ocultando-os do mundo exterior. Isso promove segurança, manutenção e flexibilidade do código.

### **Analogias**

O encapsulamento separa a **interface de uso** da **implementação interna**, tornando os objetos mais intuitivos, seguros e fáceis de manter. Essa técnica permite criar sistemas robustos e escaláveis.

#### **1. Celular**

O funcionamento de um celular envolve diversas tecnologias, mas o usuário não precisa entender cada detalhe técnico para utilizá-lo.

- **Interface de Uso:** Tela sensível ao toque, botões, menus e aplicativos permitem interação intuitiva.
- **Implementação:** Processadores, sensores, antenas e sistemas operacionais trabalham nos bastidores.
- **Exemplo:** Ao fazer uma ligação, basta digitar o número e pressionar um botão. O usuário não precisa conhecer os processos internos de transmissão de sinais.

#### **2. Carro**

Os fabricantes de automóveis aplicam encapsulamento para garantir que mudanças internas não afetem o modo de dirigir.

- **Interface de Uso:** Volante, pedais, alavanca de câmbio e painel de controle.
- **Implementação:** Motores, sistemas eletrônicos e transmissão interna.
- **Exemplo:** Mesmo que um carro mude de carburador para injeção eletrônica, a interface de uso permanece a mesma.

#### **3. Máquina de Vendas**

Máquinas automáticas impedem interferências externas em seu funcionamento interno.

- **Interface de Uso:** Botões para escolha, entrada para pagamento e saída do produto.
- **Implementação:** Sensores verificam o pagamento, mecanismos internos liberam os produtos.
- **Exemplo:** O usuário compra um refrigerante apenas interagindo com a interface, sem acesso direto ao mecanismo interno.

## **2. Benefícios do Encapsulamento**

O encapsulamento **protege a integridade dos dados**, **facilita a manutenção** e **torna o código mais adaptável a mudanças**.

### **1. Segurança dos Dados**

- **Atributos privados** evitam modificações indevidas.
- **Métodos públicos** controlam o acesso e garantem valores válidos.

### **2. Facilidade de Manutenção**

- **Mudanças internas** não afetam o código externo.
- **Evolução sem impacto**: Novas regras podem ser adicionadas sem quebrar o código existente.

### **3. Flexibilidade e Extensibilidade**

- **Herança segura**: Classes derivadas podem reutilizar comportamentos sem expor detalhes internos.
- **Novos métodos podem ser adicionados** sem interferir no código que já utiliza a classe.

### **4. Validação Centralizada**

- **Regras de negócio são aplicadas em um único lugar**, evitando inconsistências.

### **5. Modularidade e Ocultação de Detalhes**

- **Cada classe gerencia seus próprios dados**, sem expor sua implementação interna.
- **Código mais limpo e desacoplado**, facilitando testes e reutilização.

---
