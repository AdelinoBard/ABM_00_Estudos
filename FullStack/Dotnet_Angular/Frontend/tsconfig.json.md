# `tsconfig.json`

O `tsconfig.json` é o **arquivo de configuração central do compilador TypeScript (TSC)** em projetos Angular — e é essencial para garantir que o código TypeScript seja corretamente transpilado para JavaScript.

É um **arquivo JSON** que define como o TypeScript deve **compilar o projeto**. Ele informa ao compilador:

- Quais arquivos incluir ou excluir
- Quais opções de compilação aplicar
- Quais bibliotecas e tipos usar
- Como lidar com módulos, decoradores, JSX, entre outros

Sua presença indica que o diretório é a **raiz de um projeto TypeScript**.

---

## Estrutura típica do `tsconfig.json`

```json
{
  "compilerOptions": {
    "target": "es2020",
    "module": "es2020",
    "moduleResolution": "node",
    "strict": true,
    "sourceMap": true,
    "experimentalDecorators": true,
    "skipLibCheck": true,
    "outDir": "./dist/out-tsc",
    "typeRoots": ["node_modules/@types"]
  },
  "include": ["src/**/*.ts"],
  "exclude": ["node_modules", "**/*.spec.ts"]
}
```

---

### Principais propriedades explicadas

### `compilerOptions`

Define como o TypeScript deve compilar o código:

- `target`: versão do JavaScript gerado (`es5`, `es6`, `es2020`, etc.)
- `module`: tipo de módulo usado (`commonjs`, `es2020`, etc.)
- `strict`: ativa todas as verificações de tipo estritas
- `sourceMap`: gera arquivos `.map` para depuração
- `experimentalDecorators`: habilita suporte a decoradores (usado no Angular)
- `skipLibCheck`: ignora verificação de tipos em arquivos `.d.ts`
- `outDir`: pasta de saída dos arquivos compilados
- `typeRoots`: onde buscar definições de tipo

### `include` e `exclude`

Controlam quais arquivos serão **compilados** ou **ignorados**:

- `include`: arquivos e pastas que devem ser compilados
- `exclude`: arquivos que devem ser ignorados (ex: testes, dependências)

---

## Por que isso importa?

- Garante que o projeto seja compilado corretamente
- Evita erros de tipagem e inconsistência
- Permite otimizações de build e integração com ferramentas como Webpack, Angular CLI e Visual Studio
- Facilita manutenção e escalabilidade do código

---

## Relação com arquivos especializados

Em projetos Angular, o `tsconfig.json` é **estendido** por arquivos como:

- `tsconfig.app.json`: para a aplicação principal
- `tsconfig.spec.json`: para testes unitários
- `tsconfig.server.json`: para renderização no servidor (Angular Universal)

Esses arquivos usam `"extends": "./tsconfig.json"` para herdar configurações e sobrescrever apenas o necessário.

---

## Recursos adicionais

Você pode explorar todas as opções disponíveis na [documentação oficial do TypeScript](https://www.typescriptlang.org/tsconfig/) ou na [referência do Angular](https://angular.io/config/tsconfig).

---
