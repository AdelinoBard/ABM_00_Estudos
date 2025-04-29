# Princípio da Responsabilidade Única (SRP - Single Responsibility Principle)  

Como Robert C. Martin afirma em *Código Limpo*, **"Uma classe deve ter apenas um motivo para mudar"**. É comum a tentação de sobrecarregar uma classe com múltiplas responsabilidades, como tentar caber tudo em uma única mala em uma viagem. O problema é que isso **quebra a coesão** da classe e introduz múltiplos pontos de modificação. Minimizar as alterações em uma classe é crucial, pois mudanças em uma funcionalidade podem impactar inesperadamente outros módulos dependentes.

## **Ruim (Violando o SRP):**
```csharp
public class UserSettings  
{
    private User _user;

    public UserSettings(User user)  
    {
        _user = user;
    }

    public void ChangeSettings(Settings newSettings)  
    {
        if (VerifyCredentials())  
        {
            // Lógica para alterar configurações...
        }
    }

    private bool VerifyCredentials()  
    {
        // Lógica de autenticação...
    }
}
```
**Problemas:**  
- `UserSettings` gerencia **configurações do usuário** e **autenticação** (duas responsabilidades).  
- Se a lógica de autenticação mudar, a classe precisará ser modificada, mesmo que não haja alterações nas configurações.  

## **Bom (Respeitando o SRP):**
```csharp
public class UserAuthenticator  
{
    private User _user;

    public UserAuthenticator(User user)  
    {
        _user = user;
    }

    public bool VerifyCredentials()  
    {
        // Lógica de autenticação isolada...
    }
}

public class UserSettings  
{
    private User _user;
    private UserAuthenticator _authenticator;

    public UserSettings(User user)  
    {
        _user = user;
        _authenticator = new UserAuthenticator(user);
    }

    public void ChangeSettings(Settings newSettings)  
    {
        if (_authenticator.VerifyCredentials())  
        {
            // Lógica específica para alterar configurações...
        }
    }
}
```
**Melhorias:**  
- `UserAuthenticator` lida **apenas com autenticação**.  
- `UserSettings` foca **apenas em configurações**, delegando autenticação para outra classe.  
- **Menos acoplamento**: Mudanças na autenticação não afetam `UserSettings`.  

## Princípios Aplicados:  
- **SRP**: Cada classe tem uma única responsabilidade.  
- **Separação de preocupações**: Autenticação e configurações são lógicas independentes.  
- **Facilidade de manutenção**: Modificações são localizadas e previsíveis.  

---