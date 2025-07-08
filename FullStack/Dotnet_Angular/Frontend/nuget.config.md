# `nuget.config`

É um **arquivo XML de configuração** que define como o NuGet deve se comportar em relação a:

- **Fontes de pacotes** (repositórios públicos ou privados)
- **Credenciais de acesso**
- **Pastas de instalação**
- **Políticas de restauração e push**
- **Proxy e rede**

Ele pode existir em **níveis diferentes**: global (usuário), máquina, solução ou projeto — e as configurações são aplicadas em cascata.

---

## Estrutura básica do arquivo

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <add key="NuGet.org" value="https://api.nuget.org/v3/index.json" />
    <add key="MeuRepoPrivado" value="https://meu-repo.com/nuget" />
  </packageSources>

  <packageSourceCredentials>
    <MeuRepoPrivado>
      <add key="Username" value="usuario" />
      <add key="ClearTextPassword" value="senha" />
    </MeuRepoPrivado>
  </packageSourceCredentials>

  <config>
    <add key="globalPackagesFolder" value="C:\MeusPacotes" />
    <add key="repositoryPath" value=".\packages" />
  </config>
</configuration>
```

---

### Principais seções explicadas

- **`packageSources`**: Define os repositórios de onde os pacotes serão baixados.
- **`packageSourceCredentials`**: Armazena credenciais para fontes privadas (não recomendado em texto plano).
- **`config`**:
  - `globalPackagesFolder`: pasta onde os pacotes são armazenados globalmente.
  - `repositoryPath`: pasta local para pacotes em projetos que usam `packages.config`.
- **`bindingRedirects`**: (opcional) controla redirecionamentos de versão de assembly.
- **`disabledPackageSources`**: permite desativar fontes específicas.

---

## Onde ele pode estar?

| Localização                     | Escopo                   |
| ------------------------------- | ------------------------ |
| `%APPDATA%\NuGet\`              | Configuração do usuário  |
| `C:\Program Files\NuGet\Config` | Configuração da máquina  |
| Raiz da solução                 | Configuração por projeto |

Você pode ter múltiplos arquivos `nuget.config`, e o NuGet os lê em ordem de precedência.

---

## Como criar ou editar?

- Manualmente com qualquer editor de texto
- Via CLI: `nuget config -set key=value -configFile caminho`
- Visual Studio: menu **Tools > NuGet Package Manager > Package Sources**

---

## Dicas para seu projeto FullStack

- Se você usa **repositórios privados** (como Azure Artifacts ou GitHub Packages), o `nuget.config` é essencial para autenticação.
- Em ambientes de **CI/CD**, é comum incluir um `nuget.config` na raiz da solução para garantir consistência entre builds.
- Evite armazenar senhas em texto plano — prefira usar variáveis de ambiente ou autenticação via CLI.

---
