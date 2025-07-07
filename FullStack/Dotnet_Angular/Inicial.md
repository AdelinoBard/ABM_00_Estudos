# Configuracoes Iniciais - DotNET + Angular

---

## Pré-Requisitos

Antes de colocar a mão na massa, é fundamental garantir que seu ambiente de desenvolvimento esteja configurado corretamente:

### .NET CLI

- Verifique se o .NET CLI está instalado:

```bash
dotnet --version
```

- Se o comando não funcionar, adicione `C:\Program Files\dotnet\` à variável de ambiente `PATH`.

### Node.js + Angular CLI

- Instale o Node.js usando o gerenciador de versões [`nvm-windows`](https://github.com/coreybutler/nvm-windows/releases) (recomendado).

- Após instalar o Node.js, instale o Angular CLI:

```bash
npm install -g @angular/cli@17.0.3
```

- Confirme se o Angular CLI está funcionando:

```bash
ng version
```

---

## Criando o Projeto FullStack

### Etapa 1: Criar os projetos no Visual Studio 2022

O Visual Studio oferece duas abordagens:

| Opção              | Descrição                                           |
| ------------------ | --------------------------------------------------- |
| Template Autônomo  | Angular e ASP.NET Core em projetos separados.       |
| Template Integrado | Estrutura simplificada, introduzida na versão 17.8. |

Ambos geram código compatível com a versão do Angular instalada.

### Etapa 2: Nomeando e Organizando

- Escolha uma pasta raiz com nome curto para evitar erros de caminho longo no Windows.

---

## Configurando o Projeto

### Inicialização Múltipla

- No **Solution Explorer**, clique com o botão direito na solução.
- Selecione “Configurar projetos de inicialização”.
- Marque **"Vários projetos de inicialização"** e defina ambos como **"Iniciar"**.
- Coloque o projeto ASP.NET acima do Angular (ordem de execução).

---

## Executando e Depurando

Ao iniciar o projeto com F5 ou pelo botão de "Start":

1. **ASP.NET Core Server**: Inicia Kestrel ou IIS Express.
2. **Angular Live Dev Server**: Usa `ng serve` na porta 4200.
3. **Navegador**: Conecta ao Angular na porta 4200 e este encaminha chamadas de API para o ASP.NET na porta 40443.

> O Angular Dev Server é usado **somente em desenvolvimento**.

---

## Estrutura dos Projetos

### Backend ASP.NET

- Pasta `Dependencies`: Pacotes e referências.
- Pasta `Controllers`: Exemplo com `WeatherForecastController`.
- Arquivos principais:
  - `Program.cs`
  - `appsettings.json`

> O projeto ASP.NET é apenas uma API, então não há `Views` ou `Pages`.

### Frontend Angular

- Criado com Angular CLI.
- Arquitetura moderna com módulos, componentes, serviços etc.
- Comunicação com API via **HttpClient**.

---
