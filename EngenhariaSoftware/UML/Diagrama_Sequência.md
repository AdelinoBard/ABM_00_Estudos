# **Diagrama de Sequência UML**

O **Diagrama de Sequência** é um modelo da UML utilizado para **visualizar a interação temporal entre objetos** dentro de um cenário específico. Ele mostra a **troca de mensagens** e a **ordem das interações**, sendo essencial para entender o **fluxo de execução de um caso de uso ou processo**.

Em **.NET/C#**, esse diagrama auxilia no **compreendimento do fluxo de controle** entre diferentes **classes e métodos**, principalmente em **lógicas de negócios complexas**.

---

## **Elementos Principais do Diagrama de Sequência**

### **1. Objetos (`▭`)**
   - Representam **entidades que interagem** no fluxo do sistema.
   - Nomeados como `Objeto:Classe` (ex.: `Cliente:Usuario`).
   - Geralmente exibidos **no topo do diagrama**, dentro de **retângulos**.

### **2. Linha de Vida (`|`)**
   - Vertical e contínua abaixo de cada **objeto**, indicando **o tempo de existência** no processo.
   - Permite visualizar **quando um objeto é ativo ou inativo** durante a interação.

### **3. Mensagens (`→`)**
   - Representam a **troca de mensagens** entre objetos.
   - São exibidas como **setas horizontais**:
     - **Síncronas (`→`)**: O remetente **espera** a resposta antes de continuar.
     - **Assíncronas (`⇢`)**: O remetente **não espera** pela resposta.

### **4. Ativação (`▯`)**
   - Barras verticais sobre uma **linha de vida**.
   - Indicam **quando um objeto está ativo**, executando **uma operação**.

### **5. Retorno de Mensagem (`←`)**
   - Indica **respostas enviadas de volta** ao remetente.
   - Representadas por **setas tracejadas** (`---→`).

### **6. Criando e Destruindo Objetos**
   - **Criação (`→▭`)**: Uma mensagem pode **instanciar um novo objeto**.
   - **Destruição (`X`)**: Um objeto pode ser **removido**, encerrando sua linha de vida.

---

## **Exemplo de Diagrama de Sequência UML**

Vamos modelar um cenário em que um cliente faz login no sistema:

```
   Cliente         Sistema         BD
     |               |              |
     | → Solicitar Login → |        |
     |               | → Validar Credenciais → |
     |               |        | → Consultar Dados → |
     |               |        | ← Retornar Usuário |
     |               | ← Autenticação Sucesso |
     | ← Exibir Confirmação |
```

Neste exemplo:
- O **cliente** solicita login.
- O **sistema** verifica as credenciais no **banco de dados**.
- O **banco de dados retorna informações** ao **sistema**.
- O **sistema responde ao cliente**, confirmando o login.

---

## **Resumo**
✅ **Objetos (`▭`)** representam **entidades no sistema**.  
✅ **Linhas de vida (`|`)** indicam **tempo de existência dos objetos**.  
✅ **Mensagens (`→` e `⇢`)** mostram **interações entre objetos**.  
✅ **Ativação (`▯`)** indica **execução de operações**.  
✅ **Retorno (`←`)** representa **respostas** entre os objetos.  
✅ **Criação (`→▭`) e destruição (`X`)** representam **objetos sendo instanciados ou encerrados**.  

---