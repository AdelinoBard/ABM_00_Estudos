# Métodos: Parâmetros

## **8. Sobrecarga de Métodos (Overloading)**

A **sobrecarga de métodos** permite declarar vários métodos com o mesmo nome, mas com diferentes **listas de parâmetros** (quantidade, tipo ou ordem). Isso possibilita chamar o mesmo método de diferentes maneiras, sem precisar criar nomes distintos para funções semelhantes.

## **O que é Sobrecarga de Métodos?**

- Um método pode ser sobrecarregado se tiver **assinaturas diferentes**, ou seja, variações no número e tipo dos parâmetros.
- **O tipo de retorno não diferencia sobrecargas**, apenas os parâmetros.
- A sobrecarga é útil para tornar o código mais intuitivo e reutilizável.

### **Exemplo Simples**

Vamos definir um método `ExibirMensagem` que pode ser chamado com ou sem um argumento.

```csharp
void ExibirMensagem()
{
    Console.WriteLine("Mensagem padrão.");
}

void ExibirMensagem(string texto)
{
    Console.WriteLine(texto);
}

// Uso:
ExibirMensagem();               // Saída: Mensagem padrão.
ExibirMensagem("Olá, mundo!");  // Saída: Olá, mundo!
```

Aqui, o mesmo método `ExibirMensagem` pode ser chamado de forma genérica (sem parâmetros) ou personalizado (com um texto).

## **Como o Compilador Escolhe Qual Método Chamar?**

Quando um método sobrecarregado é chamado, o **compilador C#** determina automaticamente qual versão do método usar, com base nos **argumentos fornecidos**.

```csharp
int Somar(int a, int b) // Versão com 2 inteiros
{
    return a + b;
}

double Somar(double a, double b) // Versão com 2 doubles
{
    return a + b;
}

// Uso:
Console.WriteLine(Somar(3, 5));    // Saída: 8  (chama a versão com int)
Console.WriteLine(Somar(3.5, 2.1));// Saída: 5.6 (chama a versão com double)
```

O compilador identifica os tipos de argumentos e escolhe a versão apropriada do método.

## **Aplicação Prática: Cálculo de Áreas**

A sobrecarga é útil quando precisamos calcular áreas de diferentes formas geométricas usando um único nome de método.

```csharp
double CalcularArea(double lado) // Quadrado
{
    return lado * lado;
}

double CalcularArea(double largura, double altura) // Retângulo
{
    return largura * altura;
}

// Uso:
Console.WriteLine(CalcularArea(4));       // Saída: 16 (quadrado)
Console.WriteLine(CalcularArea(4, 3));    // Saída: 12 (retângulo)
```

Agora, podemos calcular a área de um quadrado ou retângulo usando o mesmo nome de método, sem precisar criar nomes diferentes.

## **Regras Importantes**

Para usar a sobrecarga corretamente, devemos seguir algumas regras:

1. **Os métodos devem ter assinaturas diferentes** (diferentes tipos ou número de parâmetros).
2. **O tipo de retorno não diferencia sobrecargas**, apenas os parâmetros.
3. **A ordem dos argumentos também importa** — métodos com a mesma quantidade de parâmetros, mas em ordem diferente, são considerados distintos.

### **Exemplo**

```csharp
void Teste(int a, double b) { /* ... */ }
void Teste(double a, int b) { /* ... */ }
```

Aqui, os métodos `Teste` são distintos porque a ordem dos parâmetros é diferente.

## **Erros Comuns na Sobrecarga**

Atenção aos erros que podem ocorrer ao tentar sobrecarregar métodos:

- **Erro: Tipos de retorno diferentes, mas mesma assinatura**

```csharp
int Somar(int a, int b) { return a + b; }
double Somar(int a, int b) { return a + b; } // Erro! Assinatura idêntica.
```

O compilador não consegue distinguir métodos apenas pelo tipo de retorno.

- **Erro: Sobrecarga sem propósito claro** Definir vários métodos sobrecarregados sem relação pode confundir os desenvolvedores. A sobrecarga deve **manter um propósito lógico**.

---
