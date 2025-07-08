# `HomeComponent`

É um **componente Angular** que representa uma **visualização específica** — neste caso, a página inicial. Ele é composto por quatro arquivos principais:

| Arquivo | Função |
| --- | --- |
| `home.component.ts` | Lógica do componente (classe, propriedades, métodos) |
| `home.component.html` | Template HTML da interface visual |
| `home.component.css` | Estilos específicos do componente |
| `home.component.spec.ts` | Testes unitários com Jasmine/Karma (opcional) |

---

## Como o Angular CLI cria o componente?

Ao executar:

```bash
ng generate component Home
```

A CLI realiza automaticamente:

- Criação da pasta `/src/app/home/`
- Geração dos quatro arquivos mencionados
- Atualização do `AppModule` (`app.module.ts`) com a nova referência
- Registro do seletor `<app-home>` para uso em templates

---

## Estrutura gerada por padrão

### `home.component.ts`

```ts
import { Component } from "@angular/core";

@Component({
  selector: "app-home",
  templateUrl: "./home.component.html",
  styleUrls: ["./home.component.css"],
})
export class HomeComponent {}
```

### `home.component.html`

```html
<p>home works!</p>
```

Esse conteúdo é apenas um placeholder — você pode substituí-lo por qualquer layout desejado.

---

## Ignorando testes com `--skip-tests`

Se você não quiser gerar o arquivo de testes:

```bash
ng generate component Home --skip-tests
```

Isso evita a criação do `home.component.spec.ts`, útil para protótipos ou quando os testes serão adicionados posteriormente.

---

## Simulação com `--dry-run`

Se quiser ver o que o comando faria **sem executar**:

```bash
ng generate component Home --dry-run
```

Isso mostra os arquivos que seriam criados e modificados, sem alterar nada no projeto — ideal para validação prévia.

---

## Como usar o `HomeComponent`?

Depois de criado, você pode renderizá-lo no `AppComponent`:

```html
<app-home></app-home>
```

Ou configurar uma rota no `AppRoutingModule`:

```ts
{ path: '', component: HomeComponent }
```

---

## Dicas para seu projeto FullStack

- Use o `HomeComponent` como ponto de entrada visual e informativo do app
- Adicione elementos como banners, menus, ou cards de navegação
- Combine com `NavMenuComponent` e `FetchDataComponent` para criar uma estrutura de SPA completa

---
