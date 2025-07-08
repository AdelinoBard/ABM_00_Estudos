# `proxy.conf.js`

É um **arquivo de configuração de proxy** usado pelo servidor de desenvolvimento Angular (`ng serve`) para **redirecionar chamadas HTTP** feitas pelo frontend para o backend ASP.NET Core — especialmente útil quando ambos rodam em portas diferentes.

---

## Estrutura recomendada para múltiplos endpoints

```js
const PROXY_CONFIG = [
  {
    context: ["/api"],
    target: "https://localhost:40443",
    secure: false,
    changeOrigin: true,
    logLevel: "debug",
  },
];

module.exports = PROXY_CONFIG;
```

### Explicando os campos

- `context`: define o prefixo das rotas que serão interceptadas (ex: `/api`)
- `target`: URL do backend ASP.NET Core
- `secure`: se `false`, ignora certificados HTTPS inválidos (útil em dev)
- `changeOrigin`: ajusta o cabeçalho `Origin` para combinar com o `target`
- `logLevel`: define o nível de log (`debug`, `info`, etc.)

---

## Integração com o Angular

### 1. **Atualize o `app.component.ts`**

```ts
http
  .get<WeatherForecast[]>("/api/weatherforecast")
  .subscribe((result) => (this.forecasts = result));
```

### 2. **Configure o proxy no `angular.json`**

```json
"serve": {
  "options": {
    "proxyConfig": "src/proxy.conf.js"
  }
}
```

Ou use diretamente no terminal:

```bash
ng serve --proxy-config src/proxy.conf.js
```

---

## Ajuste no ASP.NET Core

No `WeatherForecastController.cs`, altere a rota:

```csharp
[Route("api/[controller]")]
```

Isso garante que o endpoint `/api/weatherforecast` seja reconhecido corretamente.

---

## Benefícios da abordagem com prefixo `/api`

- Evita erros de CORS durante o desenvolvimento
- Permite usar URLs relativas no Angular (`/api/...`)
- Cria uma regra genérica que cobre todos os endpoints da API
- Facilita a manutenção e escalabilidade do projeto

---

## E em produção?

Se Angular e ASP.NET Core forem hospedados **em domínios diferentes**, o proxy do Angular **não estará disponível**. Nesse caso:

- Configure o **base URL da API** no Angular via `environment.ts`
- Use **interceptadores HTTP** para adicionar o prefixo automaticamente
- Garanta que o backend esteja configurado para aceitar **CORS**

---

## Dica extra: usando `environment.ts`

```ts
export const environment = {
  production: false,
  apiUrl: "https://localhost:40443/api",
};
```

E no serviço Angular:

```ts
this.http.get(`${environment.apiUrl}/weatherforecast`);
```

---

## `proxy`

Um **proxy** é como um intermediário digital entre você e a internet. Em vez de seu dispositivo se conectar diretamente a um site ou serviço online, ele envia a solicitação para o servidor proxy, que então repassa essa solicitação ao destino final e devolve a resposta para você. Isso pode parecer simples, mas tem implicações poderosas:

### Para que serve um proxy?

- **Privacidade**: oculta seu endereço IP real, dificultando rastreamento
- **Segurança**: pode bloquear sites maliciosos e filtrar conteúdo indesejado
- **Acesso a conteúdos restritos**: permite acessar sites bloqueados por região
- **Controle de rede**: usado por empresas e escolas para limitar o que pode ser acessado
- **Cache**: armazena páginas acessadas com frequência para acelerar o carregamento

### Tipos de proxy

| Tipo | Características |
| --- | --- |
| **Transparente** | Revela seu IP real e se identifica como proxy — usado para filtragem de conteúdo |
| **Anônimo** | Oculta seu IP, mas se identifica como proxy |
| **Alto anonimato** | Não revela que é um proxy e oculta completamente seu IP |

### Proxy vs VPN

Embora ambos ocultem seu IP, a **VPN** cria um túnel criptografado para todo o tráfego do dispositivo, enquanto o **proxy** atua apenas em nível de aplicativo e **não criptografa** os dados.

---
