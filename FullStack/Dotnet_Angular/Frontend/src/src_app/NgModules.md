# O que são NgModules?

**NgModules** (Angular Modules) são **classes decoradas com `@NgModule`** que agrupam e organizam funcionalidades relacionadas — como componentes, diretivas, pipes e serviços — em blocos reutilizáveis e coesos.

Eles definem o **contexto de compilação** e **injeção de dependência** para os elementos que pertencem ao módulo.

---

## Estrutura básica de um NgModule

```ts
import { NgModule } from "@angular/core";
import { BrowserModule } from "@angular/platform-browser";
import { AppComponent } from "./app.component";

@NgModule({
  declarations: [AppComponent], // Componentes, diretivas e pipes pertencentes ao módulo
  imports: [BrowserModule], // Outros módulos que este módulo depende
  providers: [], // Serviços disponíveis via injeção de dependência
  bootstrap: [AppComponent], // Componente raiz que será inicializado
})
export class AppModule {}
```

---

## Tipos de NgModules

| Tipo | Finalidade |
| --- | --- |
| **Módulo raiz** | Inicializa a aplicação (`AppModule`) |
| **Módulo de recurso** | Agrupa funcionalidades específicas (ex: `UserModule`, `ProductModule`) |
| **Módulo compartilhado** | Contém componentes e pipes reutilizáveis (`SharedModule`) |
| **Módulo de serviço** | Fornece serviços utilitários (`CoreModule`, `HttpClientModule`) |
| **Módulo de roteamento** | Define rotas (`AppRoutingModule`, `FeatureRoutingModule`) |

---

## Ciclo de inicialização

1. O arquivo `main.ts` chama `platformBrowserDynamic().bootstrapModule(AppModule)`
2. O Angular carrega o `AppModule`
3. O `AppModule` inicializa o `AppComponent`
4. O `AppComponent` renderiza o restante da aplicação

---

## Principais propriedades do `@NgModule`

| Propriedade | Função |
| --- | --- |
| `declarations` | Componentes, diretivas e pipes que pertencem ao módulo |
| `imports` | Outros módulos que fornecem funcionalidades necessárias |
| `exports` | Elementos que podem ser usados por outros módulos |
| `providers` | Serviços disponíveis para injeção de dependência |
| `bootstrap` | Componente(s) que iniciam a aplicação (apenas no módulo raiz) |

---

## Dicas para seu projeto FullStack

- Crie **módulos de recurso** para separar funcionalidades (ex: `DashboardModule`, `AuthModule`)
- Use `SharedModule` para componentes reutilizáveis como botões, tabelas, etc.
- Utilize `CoreModule` para serviços globais como autenticação e interceptadores
- Configure `AppRoutingModule` para gerenciar rotas de forma centralizada

---
