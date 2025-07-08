# Estrutura Geral do Projeto Angular

Ao criar um projeto Angular, a CLI (Command Line Interface) gera uma **estrutura de diretórios e arquivos** que organiza o código, configurações e recursos. Em um modelo multiprojeto, como o seu, o front-end fica em uma pasta separada (ex: `/healthcheck.client/`), e o backend em outra (ex: `/healthcheck.server/`).

---

## Pasta `/src/`: o coração do front-end

Contém os **arquivos de código-fonte e recursos estáticos**:

| Subpasta/Arquivo | Função                                                 |
| ---------------- | ------------------------------------------------------ |
| `app/`           | Componentes, módulos e lógica da aplicação             |
| `assets/`        | Imagens, fontes e arquivos estáticos                   |
| `environments/`  | Configurações específicas por ambiente (`dev`, `prod`) |
| `favicon.ico`    | Ícone exibido na aba do navegador                      |
| `index.html`     | Página HTML principal, onde o Angular injeta o app     |
| `main.ts`        | Ponto de entrada da aplicação Angular                  |
| `polyfills.ts`   | Compatibilidade com navegadores antigos                |
| `styles.css`     | Estilos globais da aplicação                           |
| `test.ts`        | Arquivo de configuração para testes unitários          |

---

## Arquivos Raiz do Espaço de Trabalho Angular

Esses arquivos ficam na raiz do projeto Angular e controlam o comportamento da aplicação e do ambiente de desenvolvimento:

| Arquivo | Função |
| --- | --- |
| `angular.json` | Configurações da CLI Angular (build, serve, test, lint, etc.) |
| `package.json` | Lista de dependências npm e scripts de automação |
| `package-lock.json` | Versões exatas dos pacotes instalados |
| `tsconfig.json` | Configuração base do compilador TypeScript |
| `tsconfig.app.json` | Configuração TypeScript específica da aplicação |
| `tsconfig.spec.json` | Configuração TypeScript para testes |
| `.editorconfig` | Regras de formatação de código para o editor |
| `.gitignore` | Arquivos e pastas ignorados pelo Git |
| `README.md` | Documentação introdutória do projeto |
| `proxy.conf.js/json` | Redirecionamento de chamadas HTTP para o backend ASP.NET Core |

---

## Como o Visual Studio lida com isso?

- O Visual Studio 2022 **executa comandos da CLI Angular em segundo plano** ao criar o projeto.
- A pasta `/node_modules/` é **oculta por padrão** no Solution Explorer, mas pode ser exibida clicando em “Mostrar Todos os Arquivos”.
- Os comandos como `ng build`, `ng serve`, `ng test` podem ser executados via terminal ou scripts definidos no `package.json`.

---

## Dicas para seu projeto FullStack

- Mantenha o front-end e o back-end **bem separados**, mas com comunicação fluida via proxy (`proxy.conf.js`)
- Use o `angular.json` para configurar múltiplos ambientes e otimizações de build
- Documente bem o `README.md` para facilitar onboarding de novos desenvolvedores
- Utilize `tsconfig.*.json` para modularizar a compilação por contexto (app, testes, server)

---
