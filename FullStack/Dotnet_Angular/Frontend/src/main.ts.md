# `main.ts`

É o **arquivo de entrada principal** da aplicação Angular. Ele:

- Inicializa o Angular no navegador
- Faz o **bootstrap** do módulo raiz (`AppModule`)
- Define se o app será executado em modo de produção ou desenvolvimento
- Pode usar o compilador **JIT (Just-In-Time)** ou **AOT (Ahead-Of-Time)**

---

## Estrutura típica do `main.ts`

```ts
import { enableProdMode } from "@angular/core";
import { platformBrowserDynamic } from "@angular/platform-browser-dynamic";

import { AppModule } from "./app/app.module";
import { environment } from "./environments/environment";

if (environment.production) {
  enableProdMode(); // Desativa verificações e logs para melhorar performance
}

platformBrowserDynamic()
  .bootstrapModule(AppModule)
  .catch((err) => console.error(err));
```

---

### Explicando cada parte

- **`enableProdMode()`**: ativa o modo de produção, removendo verificações extras e melhorando a performance
- **`platformBrowserDynamic()`**: cria a plataforma Angular para execução no navegador
- **`.bootstrapModule(AppModule)`**: inicializa o módulo raiz da aplicação
- **`catch(err => ...)`**: captura erros de inicialização

---

## JIT vs AOT

| Compilador | Quando ocorre a compilação | Vantagens | Como ativar |
| --- | --- | --- | --- |
| **JIT** | No navegador, em tempo de execução | Mais flexível para desenvolvimento | Padrão no `ng serve` |
| **AOT** | Durante o build, antes da execução | Mais rápido e seguro em produção | `ng build --aot` ou `ng serve --aot` |

Você pode usar AOT **sem alterar o `main.ts`**, apenas adicionando o sinalizador `--aot` nos comandos da CLI.

---

## Relação com outros arquivos

- O `main.ts` importa o `AppModule`, que por sua vez importa o `AppComponent`
- O `AppComponent` tem o seletor `app-root`, que é renderizado dentro do `index.html`
- Esse fluxo conecta o TypeScript ao HTML e inicia a renderização da aplicação

---

## Dicas para seu projeto FullStack

- Mantenha o `main.ts` simples e limpo — ele deve apenas **inicializar** o app
- Use `enableProdMode()` corretamente para evitar logs desnecessários em produção
- Combine com `angular.json` para configurar o uso de AOT por padrão

---
