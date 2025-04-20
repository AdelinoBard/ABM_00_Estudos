# **SOLID**

## **Resumo Mnemônico**  
🔹 **S**RP: 1 classe = 1 tarefa.  
🔹 **O**CP: Estenda sem modificar.  
🔹 **L**SP: Herança sem surpresas.  
🔹 **I**SP: Interfaces enxutas.  
🔹 **D**IP: Inverta dependências.  

---

### **1. SRP (Single Responsibility Principle)**  
📌 *"Uma classe deve ter apenas **um motivo** para mudar."*  
- Cada classe deve resolver **um único problema**.  
- Exemplo: Separar lógica de negócio (regras) de acesso a dados (repositórios).  

**C#**:  
```csharp
// Ruim: Uma classe com múltiplas responsabilidades
class UsuarioService {
    void Cadastrar() { /*...*/ }
    void EnviarEmail() { /*...*/ } // Deveria estar em outra classe
}

// Bom: Classes especializadas
class UsuarioService { void Cadastrar() { /*...*/ } }
class EmailService { void EnviarEmail() { /*...*/ } }
```

---

### **2. OCP (Open/Closed Principle)**  
📌 *"Entidades devem estar **abertas para extensão**, mas **fechadas para modificação**."*  
- Use **herança**, **interfaces** ou **padrões como Strategy** para estender comportamentos.  

**C#**:  
```csharp
interface IForma { double CalcularArea(); }
class Retangulo : IForma { /*...*/ }  // Nova forma? Só implementar a interface.
class Circulo : IForma { /*...*/ }     // Sem modificar código existente.
```

---

### **3. LSP (Liskov Substitution Principle)**  
📌 *"Subtipo deve ser **substituível** por seu tipo base sem quebrar o sistema."*  
- Herança deve manter **consistência comportamental**.  
- Exemplo: Se `Pato` herda de `Ave`, deve poder voar (senão viola LSP).  

**C#**:  
```csharp
// Ruim: Quadrado herda de Retângulo e quebra o comportamento (setWidth altera height)
class Retangulo { virtual int Width { get; set; } virtual int Height { get; set; } }
class Quadrado : Retangulo { override int Width { set { base.Width = base.Height = value; } } } // Viola LSP!

// Bom: Interfaces separadas
interface IForma { int Area { get; } }
class Retangulo : IForma { /*...*/ }
class Quadrado : IForma { /*...*/ }
```

---

### **4. ISP (Interface Segregation Principle)**  
📌 *"Clientes não devem depender de interfaces que **não usam**."*  
- Prefira **interfaces pequenas e específicas** a "interfaces gordas".  

**C#**:  
```csharp
// Ruim: Interface monolítica
interface IFuncionario {
    void Trabalhar();
    void Gerenciar(); // Nem todos funcionários gerenciam!
}

// Bom: Interfaces segregadas
interface ITrabalhador { void Trabalhar(); }
interface IGerente : ITrabalhador { void Gerenciar(); }
```

---

### **5. DIP (Dependency Inversion Principle)**  
📌 *"Dependa de **abstrações**, não de implementações concretas."*  
- Módulos de alto nível não devem depender diretamente de detalhes.  

**C#**:  
```csharp
// Ruim: Classe depende de concreto
class PedidoService {
    private SqlDatabase _db;  // Acoplamento forte!
}

// Bom: Depende de abstração (interface)
class PedidoService {
    private IDatabase _db;  // Injetado via DI (ex: Entity Framework, Dapper)
    public PedidoService(IDatabase db) { _db = db; }
}
```

---