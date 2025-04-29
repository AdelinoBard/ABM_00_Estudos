# **Diagrama de Estado UML**

O **Diagrama de Estado** é uma ferramenta da UML que **descreve os estados pelos quais um objeto passa durante seu ciclo de vida** e as **transições entre esses estados**, desencadeadas por **eventos**. Ele é essencial para **modelar comportamentos de objetos** que possuem **estados bem definidos**, como um **pedido em um e-commerce**, um **documento em um sistema de aprovação** ou até uma **máquina de estados em .NET/C#**.

Em **.NET/C#**, os diagramas de estado ajudam na implementação de **máquinas de estado**, usando:
- **Enums**, para definir estados possíveis.
- **Estruturas de controle (`switch`/`if-else`)**, para gerenciar transições.
- **Bibliotecas específicas**, como `Stateless` e `Workflow Foundation`.

---

## **Elementos Principais do Diagrama de Estado**

### **1. Estado Inicial (`●`)**
   - Representado por um **círculo sólido** no início do diagrama.
   - Indica **o começo do ciclo de vida** do objeto antes de ele entrar em um estado específico.

### **2. Estado (`▭`)**
   - Cada **estado** é um **retângulo arredondado** com o nome dentro dele.
   - Representa **uma condição específica** do objeto em determinado momento.

### **3. Transições (`→`)**
   - **Setas direcionais** conectam estados e representam **mudanças disparadas por eventos**.
   - Cada transição é **gatilhada por uma ação**, como:
     ```
     [Evento] → Novo Estado
     ```
   - Exemplo: Um **pedido** pode transitar de **"Criado"** para **"Pago"** quando o evento `"Confirmar Pagamento"` ocorre.

### **4. Estado Final (`◎`)**
   - Representado por um **círculo sólido cercado por um círculo oco**.
   - Indica **o encerramento do ciclo de vida do objeto**.

### **5. Estados Compostos**
   - Alguns estados podem ter **subestados internos**, modelando situações mais complexas.
   - Representados por **um estado maior** contendo **estados menores** dentro dele.

### **6. Condições de Guarda (`[ ]`)**
   - Indicam **regras que devem ser satisfeitas** para uma transição ocorrer.
   - Exemplo:
     ```
     [saldo > 100] → Aprovar Pedido
     ```

---

## **Exemplo de Diagrama de Estado UML**

Vamos modelar o ciclo de vida de um **pedido em um e-commerce**:

```
┌───────────────────────────────────────────────┐
│             📦 FLUXO DE PEDIDOS               │
└───────────────────────────────────────────────┘
        ● Estado Inicial
               │
               ▼
┌───────────────────────────────┐
│         🆃 Pedido Criado       │
├───────────────────────────────┤
│ • Cliente finaliza compra     │
│ • Sistema gera ID único       │
└───────────────────────────────┘
               │
               ▼ [✅ Pagamento Confirmado]
┌───────────────────────────────┐
│         💳 Pedido Pago        │
├───────────────────────────────┤
│ • Pagamento aprovado          │
│ • Estoque reservado           │
└───────────────────────────────┘
               │
               ▼ [🚚 Produto Enviado]
┌───────────────────────────────┐
│         ✈️ Pedido Enviado     │
├───────────────────────────────┤
│ • Nota fiscal emitida         │
│ • Código de rastreio gerado   │
└───────────────────────────────┘
               │
               ▼ [📦 Entrega Confirmada]
        ◎ Estado Final
```

Versão alternativa minimalista:

```
● → [Pedido Criado] → [✅] → [Pedido Pago] → [🚚] → [Pedido Enviado] → [📦] → ◎
```

Versão técnica (para documentação):

```
       +----------------+       +---------------+       +----------------+
       |  Pedido Criado |       |  Pedido Pago  |       | Pedido Enviado |
       +----------------+       +---------------+       +----------------+
          |                       |                       |
          | [Pagamento Confirmado]| [Produto Enviado]     | [Entrega Confirmada]
          ↓                       ↓                       ↓
       +----------------+       +---------------+       +----------------+
       |  Aguardando    |       |  Processando  |       |    Concluído   |
       |  Pagamento    |       |  Envio        |       |                |
       +----------------+       +---------------+       +----------------+
```

Neste exemplo:
- **Cada estado** representa um estágio do pedido.
- **Cada transição** ocorre quando um evento acontece (`Confirmar Pagamento`, `Produto Enviado`).
- **O pedido termina quando a entrega é confirmada**.

---

## **Resumo**
✅ **Estados (`▭`)** representam **condições de um objeto ao longo do tempo**.  
✅ **Transições (`→`)** mostram **mudanças entre estados** disparadas por eventos.  
✅ **Estado inicial (`●`)** marca o **começo do ciclo de vida**.  
✅ **Estado final (`◎`)** representa **o encerramento do ciclo de vida**.  
✅ **Condições de guarda (`[ ]`)** controlam **quando uma transição pode ocorrer**.  
✅ **Estados compostos** organizam **subestados dentro de um estado maior**.  

---