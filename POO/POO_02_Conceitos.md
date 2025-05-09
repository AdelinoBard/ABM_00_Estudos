# Conceitos de Programação Orientada a Objetos (POO)

## 1. Introdução à POO

- **O que é POO?**  
  Paradigma de programação que organiza o código em "objetos", representando entidades do mundo real, para facilitar a modelagem de sistemas complexos.

- **Vantagens da POO:**
  - Reuso de código
  - Manutenção mais fácil
  - Abstração de problemas
  - Organização clara

## 2. Fundamentos da POO

### Classes e Objetos

- **Classe:**  
  Modelo ou "molde" que define atributos (dados) e métodos (comportamentos) comuns a um tipo de objeto.  
  Exemplo: Classe `Carro` pode ter atributos como `cor` e `modelo`, e métodos como `acelerar()`.

- **Objeto:**  
  Instância concreta de uma classe, com valores específicos para seus atributos.  
  Exemplo: Um objeto `meuCarro` da classe `Carro` com `cor = "vermelho"`.

### Atributos e Métodos

- **Atributos:**  
  Variáveis que armazenam o estado do objeto (ex: `velocidade`, `nome`).
- **Métodos:**  
  Funções que definem o comportamento do objeto (ex: `calcularTotal()`, `salvarDados()`).

### Construtores e Destrutores

- **Construtor:**  
  Método especial chamado automaticamente ao criar um objeto, usado para inicializar atributos.
- **Destrutor:**  
  Método especial chamado quando um objeto é destruído, usado para liberar recursos (ex: fechar arquivos).

## 3. Pilares da POO

### Encapsulamento

- **Definição:**  
  Protege os dados internos de um objeto, expondo apenas o necessário via métodos públicos.
- **Modificadores de Acesso:**
  - `public`: Acessível por qualquer classe.
  - `private`: Acessível apenas dentro da própria classe.
  - `protected`: Acessível pela classe e suas subclasses.

### Herança

- **Definição:**  
  Permite que uma classe (subclasse) herde atributos e métodos de outra classe (superclasse), promovendo reuso.  
  Exemplo: Classe `Cachorro` herda de `Animal`.
- **Tipos:**
  - Herança simples (uma superclasse).
  - Herança múltipla (várias superclasses, em algumas linguagens).

### Polimorfismo

- **Definição:**  
  Capacidade de um objeto responder de formas diferentes a uma mesma mensagem, dependendo do contexto.
- **Exemplos:**
  - Sobrecarga: Métodos com mesmo nome e parâmetros diferentes.
  - Sobrescrita: Redefinição de um método herdado em uma subclasse.

### Abstração

- **Definição:**  
  Foco nos aspectos essenciais de um objeto, ignorando detalhes irrelevantes.
- **Implementação:**
  - Classes abstratas: Não podem ser instanciadas, apenas herdadas.
  - Interfaces: Contratos que definem métodos obrigatórios (sem implementação).

## 4. Conceitos Avançados

### Relacionamentos entre Objetos

- **Associação:**  
  Objetos se comunicam sem dependência direta (ex: `Aluno` usa `Biblioteca`).
- **Agregação:**  
  Relação "tem-um" onde um objeto contém outro, mas ambos podem existir separadamente (ex: `Departamento` tem `Funcionários`).
- **Composição:**  
  Relação mais forte onde um objeto é parte de outro e não existe sem ele (ex: `Casa` tem `Paredes`).

### Coleções e Genéricos

- **Coleções:**  
  Estruturas para armazenar grupos de objetos (ex: listas, dicionários).
- **Genéricos:**  
  Permitem criar classes e métodos que funcionam com qualquer tipo de dado (ex: `List<T>`).

### Tratamento de Exceções

- **Exceções:**  
  Erros que ocorrem durante a execução do programa.
- **Tratamento:**  
  Blocos `try-catch` para lidar com exceções de forma controlada.

## 5. Testes e Qualidade de Código

### Tipos de Testes

- **Testes Unitários:**  
  Verificam unidades individuais de código (ex: uma função).
- **Testes de Integração:**  
  Garantem que diferentes módulos funcionem juntos.
- **Testes Funcionais:**  
  Validam se o sistema atende aos requisitos.
- **Testes de Regressão:**  
  Garantem que novas alterações não quebrem funcionalidades existentes.

### Boas Práticas

- **Refatoração:**  
  Melhorar a estrutura do código sem alterar seu comportamento.
- **Debugging:**  
  Identificar e corrigir erros no código.
- **Documentação:**  
  Comentar o código e manter documentação atualizada.

## 6. Ferramentas e Técnicas

- **LINQ:**  
  Linguagem integrada para consultas em coleções (ex: filtrar dados).
- **Delegados e Eventos:**  
  Mecanismos para criar callbacks e notificações.
- **Namespaces:**  
  Organizam classes em grupos lógicos para evitar conflitos de nomes.

---
