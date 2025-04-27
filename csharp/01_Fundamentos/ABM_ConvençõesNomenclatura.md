# Convenções de Nomenclatura em Programação

## 1. Introdução

As convenções de nomenclatura são essenciais para manter o código legível, consistente e de fácil manutenção.

---

## 2. Padrões Principais de Nomenclatura

### 2.1 Camel Case

- **Formato:** `primeiraPalavraMinúsculaSegundaPalavraMaiúscula`
- **Exemplo:** `nomeCompleto`, `idadeUsuario`
- **Aplicações:**
  - Nomes de variáveis locais
  - Parâmetros de métodos
  - Nomes de campos privados (em algumas linguagens)
  - Nomes de métodos (em linguagens como JavaScript)

### 2.2 Pascal Case

- **Formato:** `PrimeiraPalavraMaiúsculaSegundaPalavraMaiúscula`
- **Exemplo:** `NomeCompleto`, `ClienteService`
- **Aplicações:**
  - Nomes de classes e interfaces
  - Namespaces/pacotes
  - Métodos públicos
  - Propriedades
  - Enums e constantes (em algumas linguagens)

### 2.3 Snake Case

- **Formato:** `palavras_separadas_por_underscore`
- **Exemplo:** `nome_completo`, `tabela_clientes`
- **Aplicações:**
  - Nomes de variáveis em Python, Ruby
  - Nomes de banco de dados e colunas SQL
  - Constantes em muitas linguagens (ex: `MAX_CONNECTIONS`)

### 2.4 Kebab Case

- **Formato:** `palavras-separadas-por-hifens`
- **Exemplo:** `nome-completo`, `arquivo-config`
- **Aplicações:**
  - URLs e rotas web
  - Nomes de arquivos e diretórios
  - IDs em HTML/CSS

### 2.5 Prefixos e Sufixos Especiais

- **Hungarian Notation:** `strNome` (tipo + nome)
- **Underscore prefixado:** `_campoPrivado` (campos privados em C#)
- **Sufixo "Async":** `GetDataAsync()` (métodos assíncronos)

---

## 3. Aplicações por Tipo de Elemento

### 3.1 Classes e Interfaces

- **Padrão:** Pascal Case
- **Exemplos:**
  - `ClienteRepository`
  - `ILoggerService`
- **Boas práticas:**
  - Use substantivos ou frases substantivadas
  - Evite prefixos como "C" ou "I" (exceto para interfaces em algumas linguagens)

### 3.2 Métodos e Funções

- **Padrão:** Pascal Case (C#, Java) ou Camel Case (JavaScript, Python)
- **Exemplos:**
  - `CalcularTotal()` (Pascal)
  - `formatarData()` (Camel)
- **Boas práticas:**
  - Use verbos ou frases verbais
  - Seja específico (`ProcessarPagamento` em vez de `Processar`)

### 3.3 Variáveis e Parâmetros

- **Padrão:** Camel Case
- **Exemplos:**
  - `quantidadeItens`
  - `usuarioLogado`
- **Boas práticas:**
  - Evite abreviações obscuras (`usr` em vez de `usuario`)
  - Seja descritivo (`totalVendas` em vez de `tv`)

### 3.4 Constantes

- **Padrão:** Snake Case (geralmente maiúsculas) ou Pascal Case
- **Exemplos:**
  - `MAX_TENTATIVAS`
  - `DiasDaSemana` (enum)
- **Boas práticas:**
  - Use apenas para valores verdadeiramente constantes
  - Documente o significado quando não for óbvio

### 3.5 Propriedades

- **Padrão:** Pascal Case
- **Exemplos:**
  - `NomeCompleto`
  - `IsAtivo`
- **Boas práticas:**
  - Para booleanos, prefira prefixos como "Is", "Has" ou "Can"
  - Evite propriedades que executam lógica complexa

---

## 4. Linguagens Específicas

### 4.1 C#/.NET

- Classes: `PascalCase`
- Métodos: `PascalCase`
- Parâmetros/Variáveis: `camelCase`
- Campos privados: `_camelCase` (prefixo underscore)
- Constantes: `PascalCase` ou `UPPER_CASE`

### 4.2 Java

- Classes: `PascalCase`
- Métodos: `camelCase`
- Constantes: `UPPER_SNAKE_CASE`
- Pacotes: `lowercase.sem.underscores`

### 4.3 JavaScript

- Classes: `PascalCase`
- Funções/Variáveis: `camelCase`
- Constantes: `UPPER_SNAKE_CASE`
- Arquivos: `kebab-case` (para componentes React)

### 4.4 Python

- Classes: `PascalCase`
- Funções/Variáveis: `snake_case`
- Constantes: `UPPER_SNAKE_CASE`
- Métodos privados: `_prefixo_underscore`

### 4.5 SQL

- Tabelas/Colunas: `snake_case`
- Constraints: `UPPER_SNAKE_CASE`
- Stored Procedures: `sp_NomeAcao` (SQL Server)

---

## 5. Boas Práticas Gerais

1. **Consistência:** Mantenha o mesmo padrão em todo o projeto
2. **Clareza:** Prefira nomes longos e descritivos a abreviações
3. **Contexto:** Nomes devem refletir o domínio do problema
4. **Evite:**
   - Nomes genéricos (`data`, `info`, `processar`)
   - Notações redundantes (`ClienteClass`)
   - Palavras reservadas da linguagem como nomes
5. **Refatoração:** Renomeie elementos quando o significado mudar

---

## 6. Ferramentas Úteis

1. **Linters:** ESLint, Pylint, StyleCop
2. **Extensões de IDE:** ReSharper, SonarLint
3. **Dicionários:** Mantenha um glossário de termos do projeto
4. **Code Reviews:** Inclua verificação de nomenclatura no processo

---
