# `proxy.conf.js`

É um **arquivo de configuração de proxy** usado pelo servidor de desenvolvimento do Angular (`ng serve`) para **redirecionar requisições HTTP** feitas pelo frontend para o backend ASP.NET Core — especialmente útil quando ambos rodam em portas diferentes.

---

## Por que usar?

- Evita erros de **CORS (Cross-Origin Resource Sharing)** durante o desenvolvimento
- Permite usar **URLs relativas** no Angular (`/weatherforecast`) sem precisar colocar `https://localhost:40443`
- Facilita o **debug** e a **integração local** entre frontend e backend

---

## Estrutura explicada

```js
const PROXY_CONFIG = [
  {
    context: ["/weatherforecast"], // Caminhos que serão interceptados
    target: "https://localhost:40443", // URL do backend ASP.NET Core
    secure: false, // Ignora certificados HTTPS inválidos (útil em dev)
  },
];

module.exports = PROXY_CONFIG;
```

- `context`: Define os **endpoints** que devem ser redirecionados. Pode ser um array com múltiplos caminhos, como `["/api", "/auth"]`.
- `target`: É a **URL do backend** — geralmente o endereço local do ASP.NET Core, incluindo a porta HTTPS definida no `launchSettings.json`.
- `secure`: Se `false`, permite que o proxy aceite certificados HTTPS **autoassinados**, comuns em ambientes de desenvolvimento.

---

## Como ativar no Angular

No `angular.json`, dentro da configuração de `serve`, adicione:

```json
"options": {
  "proxyConfig": "src/proxy.conf.js"
}
```

Ou use diretamente no terminal:

```bash
ng serve --proxy-config src/proxy.conf.js
```

---

## Boas práticas

- Use caminhos genéricos como `"/api"` para cobrir múltiplos endpoints
- Nunca use `secure: false` em produção
- Mantenha o `proxy.conf.js` fora do controle de versão se ele contiver URLs sensíveis
- Teste se o proxy está funcionando com `console.log` ou ferramentas como o navegador e Postman

---

## Dica para seu projeto FullStack

Se sua API ASP.NET Core estiver escutando em múltiplas portas (HTTP e HTTPS), certifique-se de usar a **porta HTTPS correta** no `target`. Você pode verificar isso no `launchSettings.json` do backend:

```json
"applicationUrl": "https://localhost:40443;http://localhost:50443"
```

---
