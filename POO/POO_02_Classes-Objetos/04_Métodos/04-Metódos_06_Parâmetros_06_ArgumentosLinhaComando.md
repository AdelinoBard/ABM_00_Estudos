# Métodos: Parâmetros

## **6. Argumentos de Linha de Comando**

Em muitos aplicativos, é possível fornecer **argumentos de linha de comando** ao executá-los. Esses argumentos permitem passar informações externas para o programa sem necessidade de interação direta.

### **Como funciona?**

O método `Main` pode receber um array de strings (`string[] args`) contendo os argumentos fornecidos na execução do programa.

```csharp
class Programa
{
    static void Main(string[] args)
    {
        Console.WriteLine($"Número de argumentos: {args.Length}");

        foreach (string arg in args)
        {
            Console.WriteLine($"Argumento: {arg}");
        }
    }
}
```

### **Executando com argumentos**

Se esse programa for compilado e executado no terminal com o seguinte comando:

```bash
Programa.exe "Primeiro" "Segundo" "Terceiro"
```

A saída será:

```bash
Número de argumentos: 3
Argumento: Primeiro
Argumento: Segundo
Argumento: Terceiro
```

### **Regras e Observações**

- Os argumentos são separados por **espaços**, não por vírgulas.
- O número de argumentos pode ser verificado com `args.Length`.
- Caso nenhum argumento seja passado, `args` será um array vazio (`args.Length == 0`).

### **Exemplo de uso**

Argumentos de linha de comando são úteis para:

- Passar **nomes de arquivos** ao programa.
- Configurar opções de execução (exemplo: **modo escuro ativado**).
- Automatizar **tarefas sem necessidade de entrada manual**.

```csharp
static void ConfigurarModo(string[] args)
{
    bool modoEscuro = args.Length > 0 && args[0] == "dark";
    Console.WriteLine($"Modo Escuro: {modoEscuro}");
}
```

Com a execução:

```bash
Programa.exe dark
```

Saída:

```bash
Modo Escuro: True
```
