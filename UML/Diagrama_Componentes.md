# **Diagrama de Componentes UML**

O **Diagrama de Componentes** é uma representação visual da **organização e dos relacionamentos entre os componentes de software**. Ele é essencial para **arquiteturas de sistemas maiores**, pois ajuda a visualizar **módulos, bibliotecas, executáveis e dependências**.

Em **.NET/C#**, os diagramas de componentes são especialmente úteis para:
- **Compreender a estrutura de assemblies** e como eles se relacionam.
- **Organizar a arquitetura de projetos** dentro de uma solução.
- **Visualizar dependências** entre **módulos e bibliotecas**.

---

## **Elementos Principais do Diagrama de Componentes**

### **1. Componente (`▭`)**
   - Representa um **módulo de software**, como **bibliotecas (`DLLs`), serviços, APIs ou executáveis (`EXEs`)**.
   - Desenhado como um **retângulo com um pequeno ícone de componente** (`▭+`).
   - Exemplo:  
     ```
     ▭+ API de Pagamentos
     ```

### **2. Interface (`◌`)**
   - Indica **um conjunto de operações** que um componente disponibiliza para outros.
   - Representada por um **círculo pequeno** (`◌`).
   - Exemplo:
     ```
     ◌ Autenticação
     ```

### **3. Conector de Dependência (`⇢`)**
   - Mostra **relações entre componentes** (quem depende de quem).
   - **Seta tracejada** (`---→`), indicando **uso de um serviço ou biblioteca**.
   - Exemplo:
     ```
     API de Pagamentos ---→ Banco de Dados
     ```

### **4. Artefato (`📄`)**
   - Representa um **arquivo físico**, como um **executável (`EXE`), um assembly (`DLL`) ou um script**.
   - Indicado por um **retângulo com um símbolo de documento** (`📄`).
   - Exemplo:
     ```
     📄 Pagamentos.dll
     ```

---

## **Exemplo de Diagrama de Componentes UML**

Vamos modelar um **sistema de e-commerce**, onde uma API de pagamentos depende de um banco de dados e se comunica com um sistema de autenticação:

```
    ▭+ Sistema de Pagamento
         |
         v
      ◌ Autenticação
         |
         v
     📄 Pagamentos.dll
         |
         v
    ---→ Banco de Dados
```

Neste exemplo:
- **O sistema de pagamento** usa uma **interface de autenticação** (`◌`).
- **O sistema depende do assembly `Pagamentos.dll`** (`📄`).
- **O sistema se conecta ao banco de dados**, indicado pela **seta tracejada**.

---

## **Resumo**
✅ **Componentes (`▭+`)** representam **módulos de software**.  
✅ **Interfaces (`◌`)** indicam **funcionalidades disponíveis** para outros módulos.  
✅ **Conectores de dependência (`⇢`)** mostram **relações entre componentes**.  
✅ **Artefatos (`📄`)** representam **arquivos físicos como `DLLs` ou `EXEs`**.  

---