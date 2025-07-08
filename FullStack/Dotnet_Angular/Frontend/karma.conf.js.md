# `karma.conf.js`

**Karma** é uma ferramenta de execução de testes para JavaScript, criada pelo time do Angular. Ele permite que os testes sejam executados em navegadores reais (como Chrome, Firefox, etc.) e fornece relatórios detalhados sobre os resultados.

---

## Função do `karma.conf.js`

Esse arquivo:

- Define **quais arquivos serão testados**
- Configura **quais navegadores serão usados**
- Estabelece **quais frameworks e bibliotecas de teste** serão carregados
- Controla **plugins, preprocessadores e relatórios**
- Permite personalizar o comportamento do Karma para diferentes ambientes (dev, CI, etc.)

---

## Estrutura típica do `karma.conf.js`

```js
module.exports = function (config) {
  config.set({
    basePath: "",
    frameworks: ["jasmine", "@angular-devkit/build-angular"],
    plugins: [
      require("karma-jasmine"),
      require("karma-chrome-launcher"),
      require("karma-coverage"),
      require("karma-jasmine-html-reporter"),
      require("@angular-devkit/build-angular/plugins/karma"),
    ],
    client: {
      clearContext: false, // mantém os resultados visíveis no navegador
    },
    coverageReporter: {
      dir: require("path").join(__dirname, "./coverage/nome-do-projeto"),
      subdir: ".",
      reporters: [{ type: "html" }, { type: "text-summary" }],
    },
    reporters: ["progress", "kjhtml"],
    browsers: ["Chrome"],
    singleRun: false,
    restartOnFileChange: true,
  });
};
```

---

### Principais seções explicadas

- **`frameworks`**: Define os frameworks de teste. `jasmine` é o padrão, e `@angular-devkit/build-angular` integra o Karma com o Angular.
- **`plugins`**: Lista os plugins usados, como o `karma-jasmine` (framework), `karma-chrome-launcher` (navegador), e `karma-coverage` (relatórios de cobertura).
- **`coverageReporter`**: Gera relatórios de cobertura de código — útil para saber o quanto do seu código está sendo testado.
- **`reporters`**: Define como os resultados dos testes serão exibidos. `progress` mostra no terminal, `kjhtml` mostra no navegador.
- **`browsers`**: Lista os navegadores que serão usados para rodar os testes. Pode incluir `Chrome`, `Firefox`, `Edge`, etc.
- **`singleRun`**: Se `true`, executa os testes uma vez e encerra (ideal para CI). Se `false`, mantém o Karma em modo observador.
- **`restartOnFileChange`**: Reexecuta os testes automaticamente ao modificar arquivos.

---

## Por que isso importa?

- Garante que os testes sejam executados de forma consistente em diferentes ambientes
- Permite integração com ferramentas de CI/CD
- Ajuda a manter a qualidade do código com testes automatizados
- Facilita a depuração de falhas em navegadores reais

---

## Dicas para seu projeto FullStack

- Você pode personalizar o `karma.conf.js` para rodar testes em múltiplos navegadores simultaneamente
- Combine com o `tsconfig.spec.json` para configurar o TypeScript nos testes
- Use `karma-coverage` para gerar relatórios e identificar partes não testadas do código

---
