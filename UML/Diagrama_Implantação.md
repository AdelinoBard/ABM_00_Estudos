# **Diagrama de Implantação UML**

O **Diagrama de Implantação** representa a **arquitetura física** do sistema, detalhando os **nós (servidores, dispositivos físicos)** e os **artefatos de software implantados nesses nós**. Esse diagrama é essencial para **planejar a infraestrutura**, garantindo que a implantação seja **eficiente e bem estruturada**.

Em **.NET/C#**, ele auxilia no planejamento de **deploy de aplicações web (`ASP.NET`)**, **serviços (`WCF`, `Web API`)** e **aplicações desktop**, organizando a **distribuição dos componentes na infraestrutura**.

---

## **Elementos Principais do Diagrama de Implantação**

### **1. Nós (`▭`)**
   - Representam **servidores, dispositivos ou máquinas virtuais** onde os sistemas são implantados.
   - Indicados por **retângulos com o nome do nó** dentro.
   - Exemplos:
     ```
     ▭ Servidor Web
     ▭ Banco de Dados
     ```

### **2. Artefatos (`📄`)**
   - Representam **arquivos físicos do sistema**, como **executáveis (`EXE`), assemblies (`DLL`), scripts e containers (`Docker`)**.
   - Geralmente são **implantados dentro dos nós**.
   - Exemplo:
     ```
     📄 WebApp.dll
     ```

### **3. Conexões (`→`)**
   - Setas indicam **comunicação entre nós**.
   - Representam **protocolos como HTTP, TCP/IP ou WebSocket**.

### **4. Instâncias de Componentes (`▭+`)**
   - Mostram **instâncias de componentes rodando nos nós**.
   - Podem representar serviços **(API, Backend, Middleware)**.

### **5. Dispositivos Físicos**
   - Representam **servidores físicos, máquinas clientes, dispositivos móveis ou IoT**.

---

## **Exemplo de Diagrama de Implantação UML**

Vamos modelar a infraestrutura de um **sistema web implantado em nuvem**, onde um **servidor web se comunica com um banco de dados**:

```
           ▭ Servidor Web
              📄 WebApp.dll
              📄 API.dll
                  |
                  v
    ---→ HTTP (Requisição)
                  |
                  v
           ▭ Banco de Dados
              📄 DataStore.sql
```

Neste exemplo:
- **O Servidor Web hospeda a aplicação (`WebApp.dll`)** e a **API (`API.dll`)**.
- **Ele se comunica com o banco de dados via HTTP**.
- **O Banco de Dados contém o artefato `DataStore.sql`**, que representa **os dados armazenados**.

---

## **Resumo**
✅ **Nós (`▭`)** representam **servidores e dispositivos físicos**.  
✅ **Artefatos (`📄`)** são **arquivos implantados**, como `DLLs`, `EXEs` e `scripts`.  
✅ **Conexões (`→`)** indicam **comunicação entre servidores e serviços**.  
✅ **Instâncias de Componentes (`▭+`)** representam **serviços rodando na infraestrutura**.  
✅ **Dispositivos físicos** mostram **hardware que participa da implantação**.  

---