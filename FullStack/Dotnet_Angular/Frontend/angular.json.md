# `angular.json`

O papel mais importante dentro do ambiente de trabalho é reproduzido pelo `angular.json` arquivo, criado pela CLI na raiz do espaço de trabalho. Este é o arquivo de configuração do espaço de trabalho e contém padrões de configuração para todo o espaço de trabalho e específicos do projeto para todas as ferramentas de compilação e desenvolvimento fornecidas pela CLI Angular.

## Visão Geral do `angular.json`

Esse arquivo é gerado automaticamente pela Angular CLI e fica na **raiz do workspace**. Ele define:

- Configurações **globais** do espaço de trabalho
- Configurações **específicas** de cada projeto (aplicações ou bibliotecas)
- Padrões para **build, serve, test, lint, e deploy**
- Regras para **schematics**, **CLI**, e **cache**

---

## Estrutura Principal

```json
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "version": 1,
  "newProjectRoot": "projects",
  "projects": {
    "nome-do-projeto": {
      "projectType": "application",
      "schematics": {},
      "root": "",
      "sourceRoot": "src",
      "prefix": "app",
      "architect": { ... }
    }
  },
  "cli": { ... },
  "schematics": { ... }
}
```

- `$schema`: Define o caminho para o schema JSON que valida a estrutura do arquivo.
- `version`: Versão do schema de configuração. Pode mudar conforme a versão da CLI.
- `newProjectRoot`: Define onde novos projetos serão criados. Mesmo que a pasta `projects` não exista, ela será usada como destino padrão.
- `projects`: Contém todos os projetos do workspace. Cada projeto tem suas próprias configurações de build, serve, test, etc.

---

## Bloco `architect`

Dentro de cada projeto, o bloco `architect` define os comandos que a CLI pode executar:

```json
"architect": {
  "build": {
    "builder": "@angular-devkit/build-angular:browser",
    "options": {
      "outputPath": "dist/nome-do-projeto",
      "index": "src/index.html",
      "main": "src/main.ts",
      "polyfills": "src/polyfills.ts",
      "tsConfig": "tsconfig.app.json",
      "assets": ["src/favicon.ico", "src/assets"],
      "styles": ["src/styles.css"],
      "scripts": []
    }
  },
  "serve": { ... },
  "test": { ... },
  "lint": { ... },
  "e2e": { ... }
}
```

Cada comando (`build`, `serve`, `test`, etc.) tem seu próprio `builder` e conjunto de `options`.

---

## Regras de Herança

O `angular.json` segue uma **hierarquia de configuração**:

1. **Workspace (nível global)**: configurações padrão
2. **Projeto (nível local)**: sobrescreve o global
3. **Linha de comando**: sobrescreve tudo

Isso permite flexibilidade e personalização sem perder consistência.

---

## Evolução com Angular 8+

Antes do Angular 8, alterações só podiam ser feitas manualmente. Agora, com a **Workspace API**, é possível modificar o `angular.json` programaticamente, o que facilita automações e integrações com ferramentas externas.

Você pode conferir mais sobre isso na [documentação oficial da Angular CLI](https://angular.dev/reference/configs/workspace-config).

---

## Dicas para seu projeto FullStack

- Use o `angular.json` para configurar caminhos personalizados, múltiplos ambientes, e otimizações de build
- Combine com o `tsconfig.json` e `package.json` para controle total do frontend
- Evite editar manualmente sem entender a estrutura — erros podem quebrar a CLI

---
