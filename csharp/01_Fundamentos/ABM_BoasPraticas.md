# Boas Práticas de Programação: Legibilidade e Organização do Código

## 1. Introdução

A legibilidade do código é fundamental para facilitar a compreensão, manutenção e expansão do software.

Use indentação, linhas em branco e comentários.

---

## 2. Indentação

### 2.1 Definição

Indentação é o espaçamento à esquerda do código, usado para indicar a estrutura hierárquica do programa. Pode ser feita com **tabulações** ou **espaços**.

### 2.2 Exemplo em C#

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("ABM");
        Console.WriteLine("Lógica de Programação em C#");
    }
}
```

### 2.3 Boas Práticas

- **Consistência:** Mantenha o mesmo número de espaços ou tabulações em cada nível.
- **Evite misturar espaços e tabulações:** Isso pode causar inconsistências.
- **Siga as convenções da linguagem:** Por exemplo, Python exige indentação para definir blocos.

---

## 3. Linhas em Branco

### 3.1 Definição

Linhas em branco são espaços vazios entre linhas de código, usados para separar blocos lógicos e melhorar a organização.

### 3.2 Exemplo em C#

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("ABM");

        Console.WriteLine("Lógica de Programação em C#");
    }
}
```

### 3.3 Boas Práticas

- **Separe funções e métodos:** Use linhas em branco para distinguir partes do código.
- **Evite excesso:** Muitas linhas em branco podem tornar o código disperso.

---

## 4. Comentários

### 4.1 Tipos de Comentários

1. **Linha única:** `// Comentário em C#`
2. **Bloco:** `/* Comentário de várias linhas */`
3. **Documentação (XML/Javadoc):** Inclui informações como objetivo, autor e data.

### 4.2 Boas Práticas

- **Explique o "porquê":** Foque na intenção, não no funcionamento do código.
- **Mantenha-os atualizados:** Comentários desatualizados podem confundir.
- **Evite redundâncias:** Não comente o que o código já torna óbvio.

### 4.3 Exemplos em Diversas Linguagens

#### HTML

```html
<!-- Comentário em HTML -->
<p>Parágrafo</p>
```

#### CSS

```css
/* Comentário em CSS */
p {
  color: red;
}
```

#### JavaScript

```javascript
// Comentário de linha
/* Comentário
   de bloco */
```

#### Python

```python
# Comentário em Python
print("Olá, mundo!")
```

#### SQL (MySQL)

```sql
-- Comentário em SQL
SELECT * FROM users;
```

---

## 5. Conceitos Relacionados

### 5.1 Nomenclatura

- Use nomes descritivos para variáveis e funções.
- Siga convenções como `camelCase` ou `snake_case`.

### 5.2 Modularização

- Divida o código em funções e classes menores.
- Organize em módulos para reutilização.

### 5.3 Documentação Externa

- **READMEs:** Explique o propósito do projeto.
- **APIs:** Use ferramentas como Swagger para documentação.

### 5.4 Ferramentas de Formatação

- **Prettier, ESLint, Black:** Automatize a formatação.
- **Integre ao IDE:** Configure para aplicar regras automaticamente.

### 5.5 Revisão de Código

- **Code Reviews:** Avalie a legibilidade e boas práticas.
- **Pair Programming:** Colabore para melhorar a qualidade.

---
