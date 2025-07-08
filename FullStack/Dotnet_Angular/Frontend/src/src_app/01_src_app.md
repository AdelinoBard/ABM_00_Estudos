# Pasta `/src/app/`

A pasta `/src/app/` é o **núcleo lógico** da aplicação Angular — é onde vive todo o código TypeScript que define a estrutura, comportamento e aparência do frontend.

É o **repositório principal do código-fonte Angular**, contendo:

- Componentes
- Módulos
- Serviços
- Modelos (interfaces/classes)
- Estilos específicos
- Arquivos de teste (`.spec.ts`)
- Configurações de rotas

Tudo que o Angular precisa para renderizar, interagir e se comunicar com o backend está aqui.

---

## Estrutura típica da pasta `/src/app/`

```plaintext
/src/app/
├── app.component.ts         # Componente raiz
├── app.component.html       # Template HTML do componente raiz
├── app.component.css        # Estilos do componente raiz
├── app.component.spec.ts    # Testes unitários do componente raiz
├── app.module.ts            # Módulo raiz da aplicação
├── app.routes.ts            # Configuração de rotas (separada)
├── core/                    # Serviços e funcionalidades globais
├── shared/                  # Componentes reutilizáveis e utilitários
├── features/                # Funcionalidades específicas do negócio
└── models/                  # Interfaces e classes de dados
```

---

### Principais arquivos explicados

| Arquivo | Função |
| --- | --- |
| `app.component.ts` | Define o componente raiz (`<app-root>`) da aplicação |
| `app.module.ts` | Declara e importa todos os módulos e componentes necessários |
| `app.routes.ts` | Define as rotas da aplicação (caso não esteja embutido no módulo) |
| `app.component.html` | Template HTML do componente raiz |
| `app.component.css` | Estilos específicos do componente raiz |
| `app.component.spec.ts` | Testes unitários para o componente raiz |

---

## Subpastas recomendadas

- `core/`: Contém serviços globais, interceptadores, guards, e configurações que não são específicas de uma funcionalidade.
- `shared/`: Componentes, pipes, diretivas e utilitários reutilizáveis em várias partes da aplicação.
- `features/` ou `pages/`: Funcionalidades específicas do negócio, organizadas por domínio (ex: `users/`, `products/`, `dashboard/`).
- `models/`: Interfaces e classes que representam os dados manipulados pela aplicação (ex: `User`, `Product`, `WeatherForecast`).

---

## Por que essa estrutura importa?

- Facilita a escalabilidade e manutenção do projeto
- Organiza testes e lógica por contexto
- Permite modularizar o código e aplicar lazy loading
- Melhora a colaboração entre desenvolvedores

---

## Dicas para seu projeto FullStack

- Use `services` para comunicação com o backend ASP.NET Core via `HttpClient`
- Organize os componentes por funcionalidade, não por tipo técnico
- Utilize `guards` e `interceptors` no `core/` para segurança e tratamento de erros
- Mantenha os modelos sincronizados com os DTOs do backend

---
