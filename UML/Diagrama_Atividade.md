# **Diagrama de Atividades UML**

O **Diagrama de Atividades** é um dos principais tipos de diagramas da UML e serve para modelar o **fluxo de trabalho** ou processos dentro de um sistema. Ele representa a **sequência de ações**, **decisões**, **paralelismo** e **condições** que podem ocorrer durante a execução de um processo.

## **Elementos Principais do Diagrama de Atividades**

Os diagramas de atividade são compostos por **símbolos interconectados**, que definem o fluxo da atividade. Vamos detalhá-los:

### **1. Estado Inicial (`●`)**
   - Representado por um **círculo sólido** no topo do diagrama.
   - Indica **o início do fluxo de trabalho**, antes da execução das ações modeladas.

### **2. Estado Final (`◎`)**
   - Representado por um **círculo sólido cercado por um círculo oco** na parte inferior do diagrama.
   - Indica **o término da atividade**, após todas as ações serem concluídas.

### **3. Ação-Estado (Retângulos com Arcos)**
   - Representam **passos individuais** dentro da atividade.
   - São desenhados como **retângulos** com os **lados esquerdo e direito arredondados**.
   - Cada **ação** dentro do sistema é representada por um **símbolo de ação-estado**.

### **4. Setas de Transição (`→`)**
   - Conectam os estados e representam **o fluxo da atividade**.
   - Indicam **a ordem na qual as ações ocorrem**.

### **5. Decisão (`◇`)**
   - Representada por um **losango**.
   - Indica **um ponto onde o fluxo pode seguir diferentes caminhos**, dependendo de uma **condição de guarda**.
   - Uma **única seta de entrada** e **duas ou mais setas de saída**, cada uma com sua **condição** (ex.: `[saldo > 100] → Aprovar`).

### **6. Símbolo de Mesclagem (`◇`)**
   - Também representado por um **losango**, mas com **múltiplas setas de entrada** e **uma única saída**.
   - **Combina diferentes fluxos de atividade** em um único fluxo contínuo.
   - **Não possui condições de guarda**, ao contrário dos **símbolos de decisão**.

### **7. Notas UML (`▭📄`)**
   - Retângulos com o **canto superior direito dobrado**.
   - Funcionam como **comentários explicativos** no diagrama, indicando **propósitos específicos**.

### **8. Linha Pontilhada (`- - - -`)**
   - Usada para **dividir responsabilidades** entre diferentes partes do sistema.
   - Ajuda a visualizar **quem executa cada ação** dentro do fluxo de atividade.

---

## **Exemplo de Diagrama de Atividade UML**

Imagine um fluxo de atividade para um sistema bancário onde um cliente deseja **sacar dinheiro**. O processo pode ser modelado como segue:

```
        ● Estado Inicial
                |
                ▼
        ◌ [Inserir Cartão]
                |
                ▼
        ◌ [Digitar Senha]
                |
                ▼
       ╔════Senha Correta?╗
       ║                 ║
       ▼                 ▼
[Sim] ◌           [Não] ◌
 |                      |
 ▼                      ▼
◌ [Selecionar Valor]    ◌ [Exibir Erro]
 |                      |
 ▼                      │
◌ [Validar Saldo]       │
 |                      │
 ▼                      │
╔════Saldo Suficiente?╗ │
║                     ║ │
▼                     ▼ ▼
◌ [Aprovado]          ◌ [Negado]
 |                     |
 ▼                     ▼
◌ [Entregar Dinheiro]  ◌ [Exibir Aviso]
 |
 ▼
 ◎ Estado Final
```

Neste exemplo, o **símbolo de decisão** separa o fluxo entre senha correta ou errada, e o **símbolo de mesclagem** reúne diferentes fluxos para continuar o processo.

---

## **Resumo**
✅ **Cada diagrama de atividade** modela **fluxos de trabalho** de um sistema.  
✅ **O estado inicial** (`●`) representa **o início do fluxo**.  
✅ **O estado final** (`◎`) indica **o término da atividade**.  
✅ **Os símbolos de ação-estado** representam **passos individuais** dentro do processo.  
✅ **Decisões (`◇`) têm condições de guarda** para diferentes caminhos.  
✅ **Mesclagens (`◇`) unem múltiplos fluxos**, sem condições de guarda.  
✅ **Setas de transição (`→`) indicam a sequência das ações**.  
✅ **Notas UML** podem ser adicionadas para **explicações** dentro do diagrama.  

---