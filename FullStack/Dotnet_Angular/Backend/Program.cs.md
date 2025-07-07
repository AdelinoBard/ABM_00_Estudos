# `Program.cs`

O arquivo `Program.cs` é o **ponto de entrada principal** de uma aplicação ASP.NET Core, e nas versões mais recentes do .NET (como .NET 6, 7 e 8), ele passou por uma grande simplificação graças ao uso de **top-level statements**.

---

## O que é o `Program.cs`?

É o arquivo responsável por:

- Criar e configurar o **host** da aplicação
- Registrar **serviços** (como controllers, Swagger, autenticação, etc.)
- Definir o **pipeline de middleware** que processa requisições HTTP
- Iniciar a aplicação com `app.Run()`

---

## Estrutura moderna do `Program.cs`

Em um modelo padrão, por exemplo, ele segue esta lógica:

```csharp
var builder = WebApplication.CreateBuilder(args);

// 1 Registrar serviços
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// 2 Configurar middleware
app.UseDefaultFiles();
app.UseStaticFiles();

if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();
app.UseAuthorization();

// 3 Mapear rotas
app.MapControllers();
app.MapFallbackToFile("/index.html");

// 4 Executar aplicação
app.Run();
```

---

### Explicando cada parte

#### 1. `WebApplication.CreateBuilder(args)`

Cria o **builder** que configura o host, lê o `appsettings.json`, define o ambiente e prepara os serviços.

#### 2. `builder.Services`

Aqui você registra os **serviços** que serão injetados via Dependency Injection. Exemplo:

- `AddControllers()` → para APIs REST
- `AddSwaggerGen()` → para documentação interativa
- `AddDbContext()` → para banco de dados (se necessário)

#### 3. `app.Use...`

Define o **pipeline de middleware**, ou seja, os componentes que interceptam e processam requisições HTTP. A ordem importa!

- `UseStaticFiles()` → serve arquivos estáticos (como Angular)
- `UseSwagger()` → habilita Swagger em ambiente de desenvolvimento
- `UseHttpsRedirection()` → força HTTPS
- `UseAuthorization()` → aplica políticas de acesso

#### 4. `app.MapControllers()` e `app.MapFallbackToFile("/index.html")`

- `MapControllers()` → conecta os endpoints da API
- `MapFallbackToFile()` → redireciona rotas não reconhecidas para o `index.html` do Angular (essencial para SPA)

---

## Relação com Angular

O `Program.cs` é configurado para **servir o frontend Angular** como arquivos estáticos e **expor a API .NET** via controllers. A linha `MapFallbackToFile("/index.html")` garante que o Angular possa lidar com rotas client-side.

---

## Program.cs - Evolução Histórica

O arquivo `Program.cs` é o ponto de entrada de toda aplicação ASP.NET Core, introduzido desde a versão 1.0. Sua função principal é **construir e configurar o host** responsável por gerenciar o ciclo de vida da aplicação.

> **Principal função**: criar um construtor - um objeto de fábrica usado para configurar e construir a interface que hospedará nossa aplicação web ASP.NET Core.

O `Program.cs` evoluiu para ser mais **expressivo** e **fácil de usar**, mas mantendo sua essência:

1. **Configurar o host** (serviços, logging, configuração).
2. **Inicializar o servidor web** (Kestrel, IIS).
3. **Definir o pipeline de requisições** (middlewares, endpoints).

Para aprofundar, consulte a documentação oficial: [ASP.NET Core Fundamentals](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/)

### **Mudanças nas Versões:**

- **ASP.NET Core 1.0 - 2.2**:

  - o construtor era chamado de `WebHostBuilder` e a interface de hospedagem era conhecida como `IWebHost`; especializado em aplicações web.
  - eles se tornaram `HostBuilder` e `IHost`, respectivamente a partir do ASP.NET Core 3.0+.

- **ASP.NET Core 3.0+**:
  - Introduziu o **Host Genérico** (`HostBuilder` e `IHost`), permitindo suporte não apenas a aplicações web, mas também a microsserviços (gRPC), workers (BackgroundService) e outros tipos de aplicações.

---

## **O que é um Host?**

Em um aplicativo web, o host deve implementar a interface `IHost`, que expõe um conjunto de recursos e serviços relacionados à web que serão usados ​​para lidar com as solicitações HTTP.

O **host** é o **contexto de execução** da aplicação, responsável por:

1. **Inicialização**: Configura serviços, middlewares e dependências.
2. **Gerenciamento de Ciclo de Vida**: Controla inicialização, execução e encerramento.
3. **Integração com o Servidor Web**: Garante que o servidor esteja pronto para processar requisições.

A afirmação anterior pode levar à suposição de que o host e o servidor web são a mesma coisa. No entanto, é muito importante entender que não são, pois atendem a propósitos muito diferentes. Simplificando, o host é responsável pela inicialização e pelo gerenciamento do ciclo de vida do aplicativo, enquanto o servidor é responsável por aceitar solicitações HTTP. Parte da responsabilidade do host inclui garantir que os serviços do aplicativo e o servidor estejam disponíveis e configurados corretamente.

Podemos pensar no host como um _wrapper_ em torno do servidor: o host é configurado para usar um servidor específico, enquanto o servidor não tem conhecimento de seu host.

Para mais informações sobre a interface `IHost`, bem como toda a inicialização da pilha ASP.NET Core, confira o seguinte guia: <https://docs.microsoft.com/en-us/aspnet/core/fundamentals/>.

### **Diferença entre Host e Servidor Web**

| **Host (`IHost`)** | **Servidor (ex: Kestrel, IIS)** |
| --- | --- |
| Gerencia a aplicação (DI, Config, Logging). | Processa requisições HTTP. |
| Configura middlewares e pipeline de requisições. | Escuta e responde a chamadas HTTP. |
| Pode executar serviços em segundo plano. | Não conhece o host. |

**Analogia**:  
O host é como um **diretor de orquestra**, enquanto o servidor é um **músico** que segue suas instruções.

---

## **O Novo Modelo (ASP.NET Core 6.0+)**

A partir do .NET 6, a Microsoft simplificou o modelo de inicialização com `WebApplicationBuilder` e `WebApplication`, reduzindo a complexidade sem perder a flexibilidade.

A abordagem de _host genérico_ ainda pode ser usada, mas a maneira recomendado de configurar uma aplicação web com as versões mais recentes do .NET envolve o uso do novo modelo de hospedagem que mencionamos brevemente há pouco. A nova abordagem se baseia em uma nova classe `WebApplicationBuilder` com uma implementação integrada de `IHostBuilder` e `IHost`: essa pequena, porém eficaz, melhoria torna a lógica geral de `Program.cs` muito mais simples para novos desenvolvedores entenderem, sem alterar a abordagem subjacente baseada em host.

### **Comparação: Antigo vs. Novo**

#### **Antigo (Genérico)**

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var host = Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            })
            .Build();

        host.Run();
    }
}
```

#### **Novo (Simplificado)**

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () => "Hello World!");
app.Run();
```

### **Vantagens do Novo Modelo:**

- Menos boilerplate.
- Configuração mais intuitiva.
- Compatível com Minimal APIs.
- Mantém a mesma infraestrutura subjacente (`IHost`/`IHostBuilder`).

---

## Startup.cs foi removido?

Sim! A partir do .NET 6, o `Startup.cs` foi **fundido** com o `Program.cs`, tornando o código mais direto e fácil de entender. Toda a configuração de serviços e middleware agora acontece em um único lugar.

Para obter informações adicionais sobre essa alteração, confira as notas de desenvolvimento da Migração para o ASP.NET Core no .NET 6 por David Fowler (Engenheiro Distinto da Equipe ASP.NET) no seguinte URL: <https://gist.github.com/davidfowl/0e0372c3c1d895c3ce195ba983b1e03d>

---
