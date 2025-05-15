## **Tipos de Métodos**

### **a) Métodos com Retorno (`return`)**

Retornam um valor após sua execução.

```csharp
public string ObterNomeCompleto(string nome, string sobrenome)
{
    return $"{nome} {sobrenome}";
}
```

### **b) Métodos sem Retorno (`void`)**

Executam uma ação sem retornar um valor.

```csharp
public void ExibirMensagem(string mensagem)
{
    Console.WriteLine(mensagem);
}
```

### **c) Métodos Estáticos (`static`)**

Pertencem à classe (não a uma instância). Podem ser chamados sem criar um objeto.

```csharp
public static double ConverterParaDolar(double valorEmReal)
{
    return valorEmReal * 5.0; // Taxa de câmbio fictícia
}
```

### **d) Métodos com Parâmetros Opcionais**

Podem ter valores padrão, tornando os argumentos opcionais.

```csharp
public void Configurar(string tema, bool darkMode = true)
{
    Console.WriteLine($"Tema: {tema}, Modo Escuro: {darkMode}");
}
```
