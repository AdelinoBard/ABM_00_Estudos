# **Diagrama de Caso de Uso UML**

O **Diagrama de Caso de Uso** é uma ferramenta essencial da UML que modela as **interações entre os usuários (atores) e o sistema**. Ele ajuda a definir **requisitos funcionais**, identificar **funcionalidades essenciais** e guiar o desenvolvimento em **.NET/C#**, garantindo que todas as funcionalidades correspondam às expectativas dos usuários.

## **Elementos Principais do Diagrama de Caso de Uso**

Os diagramas de caso de uso utilizam **símbolos padronizados** para representar as interações do sistema. Vamos analisar seus componentes principais:

### **1. Atores (`👤`)**
   - Representam **usuários ou sistemas externos** que **interagem** com o sistema.
   - Podem ser **humanos**, **dispositivos**, **outros sistemas** ou **bases de dados externas**.
   - São representados por **ícones de "stickman" (boneco palito)** ou por **retângulos nomeados**.

### **2. Casos de Uso (`○`)**
   - Representam **funcionalidades** ou **ações específicas** realizadas pelo sistema.
   - São desenhados como **ovais**, contendo o **nome da funcionalidade**.
   - Exemplo:  
     - `○ Realizar Login`  
     - `○ Efetuar Pagamento`  

### **3. Relacionamentos**
   - **Associação (`→`)**: Indica a **interação entre um ator e um caso de uso**.  
   - **Inclusão (`<<include>>`)**: Define um **comportamento obrigatório** dentro de outro caso de uso.  
   - **Extensão (`<<extend>>`)**: Indica um **comportamento opcional**, ativado apenas sob certas condições.

### **4. Sistema (`▭`)**
   - Representado por um **retângulo**, que contém **todos os casos de uso** que pertencem ao sistema.
   - Define **o escopo do sistema** e **delimita as funcionalidades modeladas**.

---

## **Exemplo de Diagrama de Caso de Uso UML**

Imagine um sistema de compras online, onde um cliente pode fazer login, escolher produtos e efetuar pagamento.

```
┌───────────────────────────────────────┐
│           INTERAÇÃO DO CLIENTE        │
└───────────────────────────────────────┘
                │
                ▼
┌───────────────────────────────────────┐
│            👤 Cliente                 │
├───────────────────────────────────────┤
│ • Navega no catálogo                  │
│ • Seleciona itens                     │
│ • Preenche dados de entrega           │
└───────────────────────────────────────┘
                │
                ▼
┌───────────────────────────────────────┐
│         🛒 Sistema de Compras         │
├───────────────────────────────────────┤
│ 1. ○ Realizar Login                   │
│ 2. ○ Escolher Produto                 │
│ 3. ○ Processar Pagamento              │
│ 4. ○ Gerar Confirmação                │
└───────────────────────────────────────┘
                │
                ▼
┌───────────────────────────────────────┐
│           ✅ Processamento            │
├───────────────────────────────────────┤
│ • Validar estoque                     │
│ • Confirmar pagamento                 │
│ • Enviar notificação                  │
└───────────────────────────────────────┘
```

Este diagrama mostra **as principais interações entre o cliente e o sistema**.

Se quisermos modelar **ações obrigatórias e opcionais**, podemos usar **inclusão** (`<<include>>`) e **extensão** (`<<extend>>`):


```
┌───────────────────────────────────────────────┐
│             🛒 SISTEMA DE COMPRAS             │
├───────────────────────────────────────────────┤
│                                               │
│  ○ Efetuar Pagamento                          │
│    ├──────┬───────────────────────────────────┤
│    │      │                                   │
│    ▼      ▼                                   │
│  ┌─────────────┐  <<include>>  ┌─────────────┐│
│  │ Validar     │               │ Aplicar     ││
│  │ Cartão      │◄─────────────►│ Cupom       ││
│  └─────────────┘  <<extend>>   └─────────────┘│
│     (obrigatório)     (opcional)              │
│                                               │
└───────────────────────────────────────────────┘
          ▲
          │
┌─────────┴──────────┐
│      👤 CLIENTE    │
├────────────────────┤
│  • Inicia pagamento│
│  • Fornece dados   │
└────────────────────┘
```

Versão alternativa mais técnica (UML-style):

```
┌───────────────────────────────────────┐
│        Efetuar Pagamento              │
├───────────────────────────────────────┤
│                                       │
│   ┌───────────────┐                   │
│   │  <<include>>  │                   │
│   └───────────────┘                   │
│            │                          │
│            ▼                          │
│   ┌─────────────────┐                 │
│   │   Validar       │                 │
│   │   Cartão        │◄──┐             │
│   └─────────────────┘   │             │
│                         │             │
│   ┌───────────────┐     │             │
│   │   <<extend>>  │     │             │
│   └───────────────┘     │             │
│            ▲            │             │
│            │            │             │
│   ┌─────────────────┐   │             │
│   │   Aplicar       │   │             │
│   │   Cupom         │───┘             │
│   └─────────────────┘                 │
│                                       │
└───────────────────────────────────────┘
```

- **O pagamento inclui a validação do cartão** (`<<include>>`), porque **é um passo obrigatório**.
- **O cupom de desconto é opcional**, então usamos `<<extend>>`.

---

## **Resumo**
✅ **Atores (`👤`)** representam **usuários ou sistemas externos**.  
✅ **Casos de uso (`○`)** modelam **funcionalidades do sistema**.  
✅ **Associação (`→`)** conecta **atores e casos de uso**.  
✅ **Inclusão (`<<include>>`)** define **ações obrigatórias** dentro de um caso de uso.  
✅ **Extensão (`<<extend>>`)** indica **ações opcionais** realizadas sob certas condições.  
✅ **O retângulo (`▭`) delimita o sistema**, mostrando **o escopo das interações**.  

---