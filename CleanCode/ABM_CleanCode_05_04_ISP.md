# Princípio da Segregação de Interfaces (ISP) em C#

O Princípio da Segregação de Interfaces (ISP) estabelece que **"Clientes não devem ser forçados a depender de interfaces que não utilizam"**. Em C#, onde as interfaces são explícitas e fortemente tipadas, esse princípio é especialmente relevante para criar designs coesos e mantáveis.

## O Problema das Interfaces "Gordas"

Quando uma interface contém muitos membros, as classes que a implementam são obrigadas a fornecer implementações para todos eles, mesmo quando não são necessários. Isso leva a:

- Código inchado com implementações vazias ou lançando `NotImplementedException`
- Alto acoplamento entre componentes
- Dificuldade de evolução do sistema

## Exemplo Prático em C#

### Implementação Ruim (Violando o ISP)

```csharp
public interface IWorker
{
    void Work();
    void Eat();
    void Sleep();
    void AttendMeeting();
    void Code();
    void Design();
}

public class Programmer : IWorker
{
    public void Work() { /* Trabalhar */ }
    public void Eat() { /* Comer */ }
    public void Sleep() { /* Dormir */ }
    public void AttendMeeting() 
    { 
        // Programador não deveria precisar implementar isso
        throw new NotImplementedException(); 
    }
    public void Code() { /* Programar */ }
    public void Design() 
    { 
        // Não é responsabilidade do programador
        throw new NotImplementedException(); 
    }
}
```

**Problemas:**
- `Programmer` é forçado a implementar métodos irrelevantes
- Interface viola o princípio da responsabilidade única
- Dificulta a criação de novos tipos de trabalhadores

### Implementação Boa (Respeitando o ISP)

```csharp
public interface IBasicActivities
{
    void Work();
    void Eat();
    void Sleep();
}

public interface IDeveloperSkills
{
    void Code();
}

public interface IDesignerSkills
{
    void Design();
}

public interface IMeetingAttendee
{
    void AttendMeeting();
}

public class Programmer : IBasicActivities, IDeveloperSkills
{
    public void Work() { /* Trabalhar */ }
    public void Eat() { /* Comer */ }
    public void Sleep() { /* Dormir */ }
    public void Code() { /* Programar */ }
}

public class Manager : IBasicActivities, IMeetingAttendee
{
    public void Work() { /* Trabalhar */ }
    public void Eat() { /* Comer */ }
    public void Sleep() { /* Dormir */ }
    public void AttendMeeting() { /* Participar de reuniões */ }
}
```

**Melhorias:**
- Interfaces pequenas e focadas
- Classes implementam apenas o que precisam
- Fácil adição de novos comportamentos
- Baixo acoplamento entre componentes

## Aplicação no Mundo Real em C#

### Exemplo com Configurações

**Ruim:**
```csharp
public interface IAppSettings
{
    string DbConnectionString { get; set; }
    int CacheDuration { get; set; }
    string EmailServiceUrl { get; set; }
    bool EnableLogging { get; set; }
    LogLevel LogLevel { get; set; }
    // ... 20 outras propriedades
}

public class DatabaseService
{
    private readonly IAppSettings _settings;
    
    public DatabaseService(IAppSettings settings)
    {
        _settings = settings; // Forçado a depender de tudo, mas só usa DbConnectionString
    }
}
```

**Bom:**
```csharp
public interface IDatabaseSettings
{
    string DbConnectionString { get; set; }
}

public interface ICacheSettings
{
    int CacheDuration { get; set; }
}

public interface IEmailSettings
{
    string EmailServiceUrl { get; set; }
}

public class DatabaseService
{
    private readonly IDatabaseSettings _settings;
    
    public DatabaseService(IDatabaseSettings settings)
    {
        _settings = settings; // Depende apenas do que precisa
    }
}
```

## Benefícios do ISP em C#

1. **Menor acoplamento**: Classes dependem apenas do que realmente usam
2. **Maior coesão**: Interfaces representam responsabilidades bem definidas
3. **Facilidade de teste**: Mocks mais simples de criar
4. **Evolução do sistema**: Novas funcionalidades não exigem mudanças em implementações existentes
5. **Princípio de responsabilidade única**: Suporta e reforça o SRP

## Padrões Relacionados

- **Interface segregation** naturalmente leva ao uso de:
  - Injeção de Dependência
  - Princípio de Composição sobre Herança
  - Design Orientado a Domínio

## Conclusão

Em C#, o ISP nos ensina a:
- Criar interfaces pequenas e específicas
- Evitar "interface god objects"
- Compor comportamentos em vez de herdar de hierarquias complexas
- Manter o sistema flexível e adaptável a mudanças

---