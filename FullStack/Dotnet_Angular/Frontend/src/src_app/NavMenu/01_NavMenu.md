# `NavMenuComponent`

O `NavMenuComponent` é o **componente de navegação principal** da sua aplicação Angular — responsável por permitir que o usuário transite entre diferentes visualizações como Home, FetchData, Modelo, etc.

---

## O que o comando CLI faz?

Ao executar:

```bash
ng generate component NavMenu --skip-tests
```

A Angular CLI irá:

- Criar a pasta `/src/app/nav-menu/`
- Gerar os arquivos:
  - `nav-menu.component.ts` → lógica do componente
  - `nav-menu.component.html` → estrutura visual
  - `nav-menu.component.css` → estilos
- Atualizar o `AppModule` (`app.module.ts`) com a referência ao novo componente

---

## Estrutura básica do `NavMenuComponent`

### `nav-menu.component.ts`

```ts
import { Component } from "@angular/core";

@Component({
  selector: "app-nav-menu",
  templateUrl: "./nav-menu.component.html",
  styleUrls: ["./nav-menu.component.css"],
})
export class NavMenuComponent {}
```

### `nav-menu.component.html`

```html
<nav>
  <ul>
    <li><a routerLink="/home" routerLinkActive="active">Home</a></li>
    <li><a routerLink="/fetch-data" routerLinkActive="active">Previsão</a></li>
    <li><a routerLink="/modelo" routerLinkActive="active">Modelo</a></li>
  </ul>
</nav>
```

### `nav-menu.component.css`

```css
nav {
  background-color: #0078d4;
  padding: 10px;
  border-radius: 4px;
}

nav ul {
  list-style: none;
  display: flex;
  gap: 20px;
  margin: 0;
  padding: 0;
}

nav a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}

nav a.active {
  text-decoration: underline;
}
```

---

## Como integrar ao `AppComponent`

No `app.component.html`, substitua o conteúdo por:

```html
<app-nav-menu></app-nav-menu> <router-outlet></router-outlet>
```

Isso garante que o menu fique visível em todas as páginas e que o conteúdo seja renderizado abaixo dele.

---

## Por que isso importa?

- Cria uma **experiência de navegação fluida**
- Permite que o Angular **renderize componentes dinamicamente** com base na rota
- Facilita a expansão do app com novas páginas e funcionalidades

---

## Dicas para seu projeto FullStack

- Use `routerLinkActive="active"` para destacar a rota atual
- Combine com `AppRoutingModule` para definir as rotas corretamente
- Estilize o menu com responsividade usando `@media` queries ou Angular Material

---
