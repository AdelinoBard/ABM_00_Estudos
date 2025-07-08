# `index.html`

É a **página HTML principal** que o navegador carrega quando você acessa o aplicativo Angular. Ela serve como **container inicial** para o app e é onde o Angular **injeta dinamicamente** os componentes e scripts compilados.

---

## Estrutura típica do `index.html`

```html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
    <meta charset="utf-8" />
    <title>Meu App Angular</title>
    <base href="/" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="icon" type="image/x-icon" href="favicon.ico" />
  </head>
  <body>
    <app-root></app-root>
  </body>
</html>
```

### Destaques

- **`<base href="/">`**: define a base para rotas relativas — essencial para o roteamento Angular funcionar corretamente.
- **`<app-root>`**: é o seletor do componente raiz (`AppComponent`) — o Angular substitui essa tag pelo conteúdo renderizado.
- **`<link rel="icon">`**: define o favicon exibido na aba do navegador.
- Nenhuma tag `<script>` ou `<link>` adicional é necessária — a Angular CLI injeta automaticamente os arquivos compilados (`main.js`, `styles.css`, etc.) durante o build.

---

## Como o Angular usa o `index.html`

1. O navegador carrega o `index.html`.
2. O Angular localiza o seletor `<app-root>` e injeta o conteúdo do `AppComponent`.
3. Os arquivos JavaScript e CSS gerados pelo build são adicionados automaticamente.
4. A aplicação é inicializada com base no `main.ts`, que faz o bootstrap do módulo principal (`AppModule`).

---

## Por que isso importa?

- Centraliza a estrutura inicial do app
- Permite configurar metadados, favicon, fontes e estilos globais
- Serve como base para múltiplos ambientes (produção, homologação, etc.)
- Pode ser personalizado para SEO, acessibilidade e performance

---

## Dicas para seu projeto FullStack

- Evite adicionar scripts manualmente — use o `angular.json` para incluir bibliotecas externas
- Para múltiplos ambientes, você pode criar versões alternativas como `index.stg.html` e configurar no `angular.json`
- Mantenha o HTML enxuto e limpo — o Angular cuida da renderização dinâmica

---
