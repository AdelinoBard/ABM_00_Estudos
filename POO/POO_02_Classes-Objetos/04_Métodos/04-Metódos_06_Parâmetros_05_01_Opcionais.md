# Métodos: Parâmetros

## **5.1. Parâmetros Opcionais**

Em C#, podemos definir **valores padrão** para parâmetros, tornando-os **opcionais**. Isso significa que, ao chamar um método, não precisamos fornecer valores para todos os parâmetros, pois alguns podem assumir um valor predefinido.

## **O que são Parâmetros Opcionais?**

Parâmetros opcionais permitem que um método tenha valores padrão em alguns de seus argumentos. Se esses argumentos não forem fornecidos na chamada do método, o valor padrão será utilizado automaticamente.

### **Exemplo básico**

```csharp
void ConfigurarTema(string tema, bool modoEscuro = true)
{
    Console.WriteLine($"Tema: {tema}, Modo Escuro: {modoEscuro}");
}
```

Neste exemplo:

- **`tema`** é obrigatório – deve ser informado ao chamar o método.
- **`modoEscuro`** é opcional – se não for informado, assumirá `true` como padrão.

### **Chamadas válidas**

```csharp
ConfigurarTema("Azul");        // Usa modoEscuro = true (padrão)
// Saída: Tema: Azul, Modo Escuro: True

ConfigurarTema("Verde", false); // Sobrescreve o valor padrão
// Saída: Tema: Verde, Modo Escuro: False
```

## **Regras dos Parâmetros Opcionais**

Ao usar parâmetros opcionais, algumas regras precisam ser seguidas:

- **Os parâmetros opcionais devem estar à direita dos obrigatórios.**

```csharp
void Exemplo(string obrigatorio, int opcional = 0) // Válido
```

- **Não podemos definir um parâmetro obrigatório após um opcional.**

```csharp
void Exemplo(int opcional = 0, string obrigatorio) // Inválido - erro de compilação
```

- **Os valores padrão devem ser constantes.**

```csharp
void Salvar(string nome, bool backup = true) // Válido
```

- **Não podemos definir um valor padrão com variáveis ou expressões dinâmicas.**

```csharp
void Salvar(string nome, bool backup = DateTime.Now.Hour > 18) // Inválido
```

## **Aplicação em Métodos Matemáticos**

Imagine que queremos calcular a potência de um número. Podemos definir o expoente como um parâmetro opcional.

```csharp
int Potencia(int baseValor, int expoente = 2)
{
    int resultado = 1;
    for (int i = 0; i < expoente; i++)
    {
        resultado *= baseValor;
    }
    return resultado;
}
```

Agora podemos chamar o método de duas formas:

```csharp
Console.WriteLine(Potencia(5));       // Usa expoente = 2 (padrão)
// Saída: 25

Console.WriteLine(Potencia(3, 3));    // Define expoente como 3
// Saída: 27
```

## **Parâmetros Opcionais vs Sobrecarga**

Se não quisermos usar parâmetros opcionais, podemos usar **sobrecarga** (definir várias versões de um mesmo método):

### **Exemplo com Sobrecarga**

```csharp
// Versão completa
void Configurar(string tema, bool modoEscuro)
{
    Console.WriteLine($"Tema: {tema}, Modo Escuro: {modoEscuro}");
}

// Versão simplificada
void Configurar(string tema)
{
    Configurar(tema, true); // Chama a primeira versão com valor padrão
}
```

| **Parâmetros Opcionais** | **Sobrecarga de Métodos**               |
| ------------------------ | --------------------------------------- |
| Código mais compacto     | Mais declarações de métodos             |
| Fácil de entender        | Útil quando a lógica muda por parâmetro |

## **Quando Usar Parâmetros Opcionais?**

- **Casos recomendados:**

  - Métodos com **poucas variações** de argumentos.
  - Quando **valores padrão** fazem sentido no contexto.
  - **Código mais limpo**, evitando múltiplas versões de um mesmo método.

- **Cuidados ao usar parâmetros opcionais:**

  - **Evite muitos parâmetros opcionais** – pode tornar o método difícil de entender.
  - **Prefira sobrecarga** se a lógica muda significativamente.

---
