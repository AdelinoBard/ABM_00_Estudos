# `FetchDataComponent`

É um **componente Angular dedicado à exibição de dados** — neste caso, os dados da previsão do tempo vindos da API ASP.NET Core. Ele foi criado para **separar responsabilidades** e tornar o `AppComponent` mais limpo e focado apenas na estrutura e navegação da aplicação.

---

## Estrutura do `fetch-data.component.ts`

```ts
import { HttpClient } from "@angular/common/http";
import { Component } from "@angular/core";
import { environment } from "../../environments/environment";

@Component({
  selector: "app-fetch-data",
  templateUrl: "./fetch-data.component.html",
  styleUrls: ["./fetch-data.component.css"],
})
export class FetchDataComponent {
  public forecasts?: WeatherForecast[];

  constructor(http: HttpClient) {
    http
      .get<WeatherForecast[]>(environment.baseUrl + "api/weatherforecast")
      .subscribe(
        (result) => {
          this.forecasts = result;
        },
        (error) => console.error(error)
      );
  }
}

interface WeatherForecast {
  date: string;
  temperatureC: number;
  temperatureF: number;
  summary: string;
}
```

### Explicando cada parte

- **`HttpClient`**: serviço Angular usado para fazer requisições HTTP à API.
- **`environment.baseUrl`**: variável que muda conforme o ambiente (`development`, `production`) e evita hardcoding de URLs.
- **`WeatherForecast`**: interface que define o formato dos dados esperados da API.
- **`subscribe()`**: método que escuta a resposta da API e atualiza a propriedade `forecasts`.

---

## Template HTML (`fetch-data.component.html`)

Você pode exibir os dados com uma tabela simples:

```html
<h2>Previsão do Tempo</h2>
<table *ngIf="forecasts">
  <thead>
    <tr>
      <th>Data</th>
      <th>Temp. (°C)</th>
      <th>Temp. (°F)</th>
      <th>Resumo</th>
    </tr>
  </thead>
  <tbody>
    <tr *ngFor="let forecast of forecasts">
      <td>{{ forecast.date }}</td>
      <td>{{ forecast.temperatureC }}</td>
      <td>{{ forecast.temperatureF }}</td>
      <td>{{ forecast.summary }}</td>
    </tr>
  </tbody>
</table>
```

---

## Por que mover para um componente dedicado?

- **Separação de responsabilidades**: cada componente cuida de uma parte da aplicação.
- **Reutilização**: o `FetchDataComponent` pode ser usado em outras rotas ou módulos.
- **Testabilidade**: facilita escrever testes unitários e de integração.
- **Escalabilidade**: permite que o projeto cresça de forma organizada.

---

## Dicas para seu projeto FullStack

- Use o `AppRoutingModule` para criar rotas que levem ao `FetchDataComponent`.
- Adicione o `NavMenuComponent` ao `AppComponent` para permitir navegação entre componentes.
- Crie serviços Angular (`WeatherService`) para encapsular chamadas HTTP e manter o componente mais limpo.

---
