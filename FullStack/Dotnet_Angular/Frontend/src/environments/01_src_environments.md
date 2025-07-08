# Pasta `/src/environments/`

É o local onde ficam os **arquivos de configuração de ambiente** do Angular. Cada arquivo representa um conjunto de variáveis que serão usadas dependendo do tipo de build:

| Arquivo                      | Finalidade                        |
| ---------------------------- | --------------------------------- |
| `environment.ts`             | Configuração padrão (produção)    |
| `environment.development.ts` | Configuração para desenvolvimento |
| `environment.staging.ts`     | (Opcional) staging ou homologação |

Esses arquivos são substituídos automaticamente durante o build, graças à configuração de `fileReplacements` no `angular.json`.

---

## Como o Angular escolhe o ambiente?

No `angular.json`, você verá algo assim:

```json
"configurations": {
  "production": {
    "fileReplacements": [
      {
        "replace": "src/environments/environment.ts",
        "with": "src/environments/environment.prod.ts"
      }
    ]
  },
  "development": {
    "fileReplacements": [
      {
        "replace": "src/environments/environment.ts",
        "with": "src/environments/environment.development.ts"
      }
    ]
  }
}
```

Isso significa que ao rodar:

```bash
ng build --configuration development
```

O Angular irá **substituir** o `environment.ts` pelo `environment.development.ts`.

---

## Implementando a propriedade `baseUrl`

Você pode definir variáveis como `baseUrl` para apontar para diferentes endpoints da API:

### `environment.development.ts`

```ts
export const environment = {
  production: false,
  baseUrl: "/",
};
```

Usa o proxy Angular para redirecionar chamadas locais.

### `environment.ts` (produção)

```ts
export const environment = {
  production: true,
  baseUrl: "https://localhost:40443/",
};
```

Aponta diretamente para o backend ASP.NET Core.

---

## Como usar no código Angular?

Importe o ambiente no seu serviço ou componente:

```ts
import { environment } from "../environments/environment";

this.http.get(`${environment.baseUrl}weatherforecast`);
```

Isso garante que a URL usada será automaticamente ajustada conforme o ambiente de build.

---

## Dicas práticas

- Use `baseUrl` para evitar hardcoding de URLs
- Crie arquivos como `environment.staging.ts` se precisar de mais ambientes
- Combine com `proxy.conf.js` para facilitar o desenvolvimento local
- Mantenha os arquivos versionados e bem documentados

---
