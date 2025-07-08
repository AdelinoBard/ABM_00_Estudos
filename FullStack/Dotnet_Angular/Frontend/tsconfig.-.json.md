# `tsconfig.*.json`

Os arquivos `tsconfig.*.json` são fundamentais para modular e especializar a configuração do compilador TypeScript em projetos Angular — especialmente em ambientes FullStack. Eles permitem que diferentes partes do projeto (aplicação, testes, servidor) tenham configurações específicas, herdando e sobrescrevendo o que está definido no `tsconfig.json` raiz.

---

## Visão Geral dos Arquivos `tsconfig.*.json`

| Arquivo | Finalidade principal |
| --- | --- |
| `tsconfig.json` | Base genérica para todo o workspace Angular |
| `tsconfig.app.json` | Configuração específica da aplicação Angular (arquivos de produção) |
| `tsconfig.spec.json` | Configuração para testes unitários com Jasmine/Karma |
| `tsconfig.server.json` | Configuração para renderização do lado servidor (Angular Universal) |

Todos esses arquivos usam a propriedade `"extends"` para herdar do `tsconfig.json` principal e sobrescrever apenas o necessário.

---

## Estrutura típica de cada arquivo

### `tsconfig.app.json`

```json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "outDir": "./out-tsc/app",
    "types": []
  },
  "files": ["src/main.ts"],
  "include": ["src/**/*.ts"],
  "exclude": ["src/test.ts", "src/**/*.spec.ts"]
}
```

- Foca na **compilação da aplicação principal**
- Exclui arquivos de teste
- Define saída (`outDir`) e arquivos de entrada (`main.ts`)

### `tsconfig.spec.json`

```json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "outDir": "./out-tsc/spec",
    "types": ["jasmine", "node"]
  },
  "files": ["src/test.ts"],
  "include": ["src/**/*.spec.ts", "src/**/*.d.ts"]
}
```

- Foca em **testes unitários**
- Inclui arquivos `.spec.ts`
- Adiciona tipos específicos para Jasmine e Node

### `tsconfig.server.json`

```json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "outDir": "./out-tsc/server",
    "types": []
  },
  "angularCompilerOptions": {
    "entryModule": "./src/app/app.server.module#AppServerModule"
  }
}
```

- Usado em projetos com **Angular Universal**
- Define o módulo de entrada para renderização no servidor

---

## Por que isso importa?

- **Modularidade**: cada parte do projeto tem sua própria configuração
- **Reutilização**: evita duplicação ao herdar do `tsconfig.json`
- **Testes isolados**: configurações específicas para testes evitam conflitos
- **Performance**: compilações mais rápidas e otimizadas por contexto

---

## Dicas para seu projeto FullStack

- Mantenha o `tsconfig.json` raiz enxuto e genérico
- Use os arquivos especializados para ajustar caminhos, tipos e exclusões
- Combine com `angular.json` para vincular corretamente cada `tsconfig.*.json` ao seu respectivo builder (`build`, `test`, `server`)
- Se estiver usando Angular Universal, o `tsconfig.server.json` é obrigatório

---
