# Pasta `/src/assets/`

É uma **pasta dedicada a arquivos estáticos** que devem ser incluídos no build final da aplicação Angular **sem serem processados ou transpilados**. Tudo que estiver dentro dela será copiado “como está” para a pasta de saída (`/dist/`) quando o projeto for compilado.

---

## Estrutura típica

```plaintext
/src/
├── assets/
│   ├── images/
│   ├── icons/
│   ├── fonts/
│   └── docs/
```

Você pode organizar os arquivos por tipo ou por funcionalidade — por exemplo, imagens de produtos, ícones de navegação, fontes personalizadas, PDFs, etc.

---

## Como o Angular lida com essa pasta?

- O Angular CLI já está configurado para **copiar automaticamente** os arquivos da pasta `assets` para o build final.
- Essa configuração está no `angular.json`:

```json
"assets": [
  "src/favicon.ico",
  "src/assets"
]
```

- No build, os arquivos são copiados para `dist/[nome-do-projeto]/assets/`

---

## Como referenciar arquivos da pasta `assets`?

Você pode usar caminhos relativos no HTML ou nos componentes Angular:

```html
<img src="assets/images/logo.png" alt="Logo" />
```

Ou com binding:

```html
<img [src]="'assets/images/' + nomeDoArquivo" />
```

---

## Boas práticas

- Evite colocar arquivos grandes ou desnecessários — eles aumentam o tempo de build e o tamanho do bundle
- Use nomes de arquivos sem espaços ou caracteres especiais para evitar problemas de carregamento
- Para bibliotecas externas (como fontes ou ícones), você pode importar diretamente no `styles.css` ou copiar para `assets` se necessário
- Se quiser usar subpastas fora de `assets`, você pode configurar isso no `angular.json` com `glob`, `input` e `output`

---

## E se estiver usando Angular 18+?

A partir do Angular 18, há suporte para uma pasta `public/` como alternativa à `assets/`. Mas você ainda pode usar `src/assets/` normalmente, desde que esteja declarada corretamente no `angular.json`.

---
