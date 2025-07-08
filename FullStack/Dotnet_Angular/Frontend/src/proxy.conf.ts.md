# `proxy.conf.ts`

O arquivo `proxy.conf.ts` é uma **variação em TypeScript** da tradicional configuração de proxy usada pelo servidor de desenvolvimento do Angular (`ng serve`). Ele permite **redirecionar chamadas HTTP** feitas pelo frontend para o backend ASP.NET Core — evitando problemas de CORS e facilitando a integração local.

É um **arquivo de configuração de proxy escrito em TypeScript** que define regras para o servidor de desenvolvimento Angular redirecionar chamadas de API para outro servidor — geralmente o backend .NET.

Embora o padrão seja usar `proxy.conf.json` ou `proxy.conf.js`, o uso de `.ts` permite:

- Tipagem estática
- Autocompletar no editor
- Lógica dinâmica com variáveis e funções

---

## Estrutura típica de um `proxy.conf.ts`

```ts
import { ProxyConfigArray } from "webpack-dev-server";

const PROXY_CONFIG: ProxyConfigArray = [
  {
    context: ["/api", "/auth"],
    target: "https://localhost:40443",
    secure: false,
    changeOrigin: true,
    logLevel: "debug",
    pathRewrite: { "^/api": "" },
  },
];

export default PROXY_CONFIG;
```

### Explicando os campos

- `context`: caminhos interceptados pelo proxy (ex: `/api`, `/auth`)
- `target`: URL do backend ASP.NET Core
- `secure`: se `false`, ignora certificados HTTPS inválidos (útil em dev)
- `changeOrigin`: ajusta o cabeçalho `Origin` para combinar com o `target`
- `pathRewrite`: reescreve o caminho da URL antes de enviar ao backend
- `logLevel`: define o nível de log (`info`, `debug`, `warn`, etc.)

---

## Como ativar no Angular

1. Salve o arquivo como `proxy.conf.ts` (ou outro nome) na pasta `src/`
2. Compile para JavaScript (o Angular CLI espera um `.js`)
   - Use `tsc src/proxy.conf.ts` para gerar `proxy.conf.js`
3. No `angular.json`, configure:

```json
"serve": {
  "options": {
    "proxyConfig": "src/proxy.conf.js"
  }
}
```

Ou use diretamente:

```bash
ng serve --proxy-config src/proxy.conf.js
```

---

## Por que usar `.ts` em vez de `.json`?

- Permite lógica condicional (ex: diferentes targets por ambiente)
- Pode importar variáveis de ambiente ou arquivos externos
- Facilita manutenção em projetos complexos

---

## Dicas para seu projeto FullStack

- Use `context: ['/weatherforecast']` para redirecionar chamadas específicas da API ASP.NET
- Combine com `environment.ts` para tornar o `target` dinâmico
- Gere o `.js` automaticamente com um script no `package.json`:

```json
"scripts": {
  "build-proxy": "tsc src/proxy.conf.ts",
  "start": "npm run build-proxy && ng serve --proxy-config src/proxy.conf.js"
}
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
