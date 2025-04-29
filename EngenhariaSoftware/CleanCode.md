# **Clean Code**: Princípios para Escrever Código Limpo e Legível

Código limpo é aquele que é **fácil de entender, manter e expandir**. Ele é escrito pensando não apenas em sua funcionalidade, mas também na pessoa que o lerá ou trabalhará nele no futuro (incluindo você mesmo!).

## **Princípios Gerais de Código Limpo**

1. **Nomes Significativos**  
   Use nomes descritivos e claros para variáveis, métodos e classes.

2. **Métodos Pequenos**  
   Mantenha métodos curtos e focados em uma única tarefa.

3. **Evitar Duplicação** (DRY - _Don't Repeat Yourself_)  
   Evite repetir o mesmo código em diferentes partes do programa.

4. **Comentários Úteis**  
   Use comentários para explicar o "porquê" do código, e não o "como".

5. **Formatação Consistente**  
   Utilize uma formatação consistente para facilitar a leitura e a manutenção.

6. **Tratamento de Erros**  
   Trate erros de forma clara e compreensível, utilizando exceções.

7. **Testes Automatizados**  
   Escreva testes para garantir que o código funcione como esperado e para simplificar futuras alterações.

8. **Simplicidade**  
   Mantenha o código simples e evite complexidade desnecessária.

## **Princípios de Design**

1. **Princípio da Responsabilidade Única** (_Single Responsibility Principle_)  
   Cada classe ou método deve ter uma única responsabilidade ou função.

2. **Princípio da Separação de Preocupações**  
   Separe as diferentes responsabilidades do código em módulos distintos.

3. **Princípio da Inversão de Dependência** (_Dependency Inversion Principle_)  
   Dependa de abstrações, não de implementações concretas.

4. **Princípio da Substituição de Liskov** (_Liskov Substitution Principle_)  
   Subclasses devem ser substituíveis por suas classes base sem alterar o comportamento do programa.

5. **Princípio da Abertura e Fechamento** (_Open/Closed Principle_)  
   O código deve ser aberto para extensão, mas fechado para modificação.

6. **Princípio da Interface Segregada** (_Interface Segregation Principle_)  
   Prefira interfaces pequenas e específicas em vez de grandes e abrangentes.

7. **Princípio da Inversão de Controle** (_Inversion of Control_)  
   Inverta o controle do fluxo do programa, usando padrões como injeção de dependência.

8. **Princípio da Lei de Demeter**  
   Cada módulo deve conhecer o mínimo possível de outros módulos para reduzir o acoplamento.

## **Boas Práticas**

1. **Princípio KISS (Keep It Simple, Stupid)**  
   Mantenha o código simples e fácil de entender.

2. **Princípio YAGNI (You Aren't Gonna Need It)**  
   Não adicione funcionalidades que não são necessárias no momento.

3. **Princípio SOLID**  
   Um conjunto de cinco princípios de design orientado a objetos que ajudam a tornar o código mais flexível e compreensível:
   - **Single Responsibility Principle (SRP)**:
     - Uma classe deve ter apenas uma razão para mudar, ou seja, deve ter uma única responsabilidade.
   - **Open/Closed Principle (OCP)**:
     - Entidades de software (classes, módulos, funções, etc.) devem estar abertas para extensão, mas fechadas para modificação.
   - **Liskov Substitution Principle (LSP)**:
     - Objetos de uma classe base devem poder ser substituídos por objetos de uma classe derivada sem alterar o funcionamento do programa.
   - **Interface Segregation Principle (ISP)**:
     - Muitas interfaces específicas são melhores do que uma interface única e generalista.
   - **Dependency Inversion Principle (DIP)**:
     - Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações.

---
