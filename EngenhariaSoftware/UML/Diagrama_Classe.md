# **Diagrama de Classes UML**

Na **Unified Modeling Language (UML)**, um **diagrama de classes** é utilizado para representar a estrutura e o comportamento de um sistema orientado a objetos. Ele define os **atributos**, **métodos** e as relações entre classes, servindo como um **projeto conceitual** antes da implementação.

## **Estrutura de uma Classe UML**

Cada classe é representada como um **retângulo dividido em três compartimentos**:

```
+-----------------------+
|      Carro            |
+-----------------------+
| - marca: String       |
| - modelo: String      |
| - ano: int            |
+-----------------------+
| + ligar(): void       |
| + acelerar(): string  |
| + frear(): void       |
+-----------------------+
```

### **1. Compartimento Superior: Nome da Classe**
   - Contém o **nome da classe**, geralmente centralizado e destacado em **negrito**.
   - No exemplo acima, a classe modelada é **Carro**.

### **2. Compartimento do Meio: Atributos**
   - Lista os **atributos** da classe, que representam seus estados ou características.
   - Sintaxe:
     ```
     [visibilidade] nome: tipo
     ```
   - A **visibilidade** define o nível de acesso ao atributo:
     - `-` **Privado**: Só pode ser acessado dentro da própria classe.
     - `+` **Público**: Pode ser acessado por qualquer classe.
     - `#` **Protegido**: Pode ser acessado pela própria classe e suas subclasses.
   - No exemplo:
     - `- marca: String` (privado, do tipo `String`)
     - `- modelo: String` (privado, do tipo `String`)
     - `- ano: int` (privado, do tipo `int`)

### **3. Compartimento Inferior: Métodos (Operações)**
   - Define os **comportamentos** da classe.
   - Sintaxe:
     ```
     [visibilidade] nome(parâmetros): tipo de retorno
     ```
   - O **tipo de retorno** pode ser:
     - `void`: Indica que o método **não retorna** um valor.
     - Tipo de dado (`String`, `int`, etc.): Indica que o método **retorna** um valor desse tipo.
   - Métodos do exemplo:
     - `+ ligar(): void` (público, sem retorno)
     - `+ acelerar(): string` (público, retorna uma `String`)
     - `+ frear(): void` (público, sem retorno)

---

## **Detalhes Adicionais na UML**

### **Propriedades em UML (`<<property>>`)**
Propriedades em C# podem ser representadas como atributos na UML, usando **estereótipos** (`<< >>`) para diferenciá-las.

```
+-----------------------------+
|      Account                |
+-----------------------------+
| + <<property>> Name: string |
+-----------------------------+
```
- A palavra **"property"** entre **guillemets** (`<< >>`) indica que `Name` é uma **propriedade pública**.
- **Não exibimos variáveis de instância**, pois elas são detalhes de implementação.

### **Construtores na UML (`<<constructor>>`)**
A UML também modela **construtores** como operações, diferenciando-os das demais funções da classe.

```
+------------------------------------------------+
|      Account                                   |
+------------------------------------------------+
| + <<property>> Name: string                    |
+------------------------------------------------+
| + <<constructor>> Account(accountName: string) |
+------------------------------------------------+
```
- O **estereótipo** (`<<constructor>>`) indica que `Account` é um **método especial** para inicialização da classe.
- **Construtores geralmente aparecem antes dos métodos normais**.

---

## **Resumo**
✅ **Cada classe** é representada por um **retângulo com três compartimentos**.  
✅ **Os atributos** possuem **visibilidade, nome e tipo de dado**.  
✅ **Os métodos** possuem **visibilidade, nome, parâmetros (opcional) e tipo de retorno**.  
✅ **Propriedades e construtores** podem ser diferenciados com **estereótipos (`<< >>`)** na UML.  

Um **diagrama de classes UML** fornece uma visão geral da estrutura de uma classe, mas **não exibe detalhes de implementação** (como variáveis internas ou os métodos `get/set` de uma propriedade).

---
