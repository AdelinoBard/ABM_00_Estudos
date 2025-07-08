# `AppComponent`

O `AppComponent` é o **componente raiz** de qualquer aplicação Angular — o primeiro a ser carregado e o ponto de partida da árvore de componentes. Ele é essencial para o funcionamento do app e serve como a base sobre a qual todos os outros componentes são montados.

---

## Estrutura do `AppComponent`

A convenção Angular define que o `AppComponent` deve estar na pasta `/src/app/`, e ele é composto por quatro arquivos principais:

| Arquivo | Função |
| --- | --- |
| `app.component.ts` | Lógica do componente (classe, propriedades, métodos, ciclo de vida) |
| `app.component.html` | Template HTML que define a interface visual |
| `app.component.css` | Estilos específicos do componente |
| `app.component.spec.ts` | Testes unitários com Jasmine/Karma |

---

## Detalhamento dos arquivos

### `app.component.ts`

```ts
import { Component } from "@angular/core";

@Component({
  selector: "app-root",
  templateUrl: "./app.component.html",
  styleUrls: ["./app.component.css"],
})
export class AppComponent {
  title = "MeuAppAngular";
}
```

- O **decorador `@Component`** define metadados como o seletor (`app-root`), o template e os estilos.
- A classe `AppComponent` contém a lógica do componente, como propriedades e métodos.

### `app.component.html`

```html
<h1>{{ title }}</h1>
<router-outlet></router-outlet>
```

- Usa **interpolação** (`{{ title }}`) para exibir dados da classe.
- O `<router-outlet>` é um ponto de injeção para componentes de rotas.

### `app.component.css`

```css
h1 {
  color: #0078d4;
  font-family: "Segoe UI", sans-serif;
}
```

- Define estilos **encapsulados** para o componente.
- Não afeta outros componentes, graças ao encapsulamento de estilo do Angular.

### `app.component.spec.ts`

```ts
import { TestBed } from "@angular/core/testing";
import { AppComponent } from "./app.component";

describe("AppComponent", () => {
  it("deve criar o componente", () => {
    const fixture = TestBed.createComponent(AppComponent);
    const app = fixture.componentInstance;
    expect(app).toBeTruthy();
  });
});
```

- Usa **Jasmine** para definir testes.
- Executado com o **Karma Test Runner**.

---

## Papel do `AppComponent` na inicialização

- É referenciado no `index.html` via `<app-root></app-root>`
- É declarado no `AppModule` (`app.module.ts`) dentro de `declarations` e `bootstrap`
- Serve como **raiz da árvore de componentes**, que pode crescer com rotas e subcomponentes

---

## Boas práticas

- Mantenha o `AppComponent` enxuto — ele deve apenas **orquestrar** a aplicação
- Evite colocar lógica de negócio nele — use serviços e componentes filhos
- Use o `router-outlet` para renderizar visualizações com base nas rotas

---
