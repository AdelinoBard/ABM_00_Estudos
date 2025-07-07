# Estrutura de uma API Web no ASP.NET

A base de uma Web API no ASP.NET gira em torno de _controllers_, _rotas_ e _modelos_:

## 1. **Controllers (Controladores)**

- São classes que herdam de `ControllerBase` ou `ApiController`.
- Contêm métodos públicos chamados _actions_, que são responsáveis por processar requisições HTTP (GET, POST, PUT, DELETE).
- Cada método representa um endpoint, ou seja, uma URL acessível da API.

## 2. **Routing (Roteamento)**

- Define como as URLs são mapeadas para os métodos nos controladores.
- Pode ser feito via _attribute routing_ (`[Route("api/[controller]")]`) ou via convenções configuradas no `Startup.cs` ou `Program.cs`.
- Permite definir rotas personalizadas e parâmetros dinâmicos na URL.

## 3. **Models (Modelos de Dados)**

- Representam as estruturas de dados que serão recebidas ou retornadas pela API.
- São usados tanto para deserialização dos dados do corpo da requisição quanto para retorno de dados estruturados como JSON ou XML.

## 4. **Middlewares**

- São componentes que interceptam requisições/respostas HTTP durante o pipeline de processamento.
- Usados para autenticação, tratamento de erros, logging, compressão, CORS etc.

---

## Funcionamento da API Web ASP.NET

O ciclo de vida de uma requisição funciona da seguinte forma:

1. **Recebimento da Requisição**

   - O servidor (como o IIS ou Kestrel) recebe uma solicitação HTTP.
   - O ASP.NET identifica a rota e encaminha para o controlador correto.

2. **Execução do Método do Controlador**

   - O controlador processa a requisição usando lógica de negócio.
   - Pode acessar bancos de dados, serviços externos, ou realizar cálculos.

3. **Serialização da Resposta**

   - O resultado é serializado para JSON, XML ou outro formato configurado.
   - É enviado de volta ao cliente como resposta HTTP.

4. **Status Codes**

   - A API responde com códigos como 200 (OK), 201 (Created), 400 (Bad Request), 401 (Unauthorized), entre outros — indicando o sucesso ou falha da operação.

---

## Comunicação e Segurança

- Usa os protocolos HTTP/HTTPS para garantir comunicação universal.
- Autenticação via JWT, OAuth2, ou ASP.NET Identity.
- Controle de acesso pode ser feito com `[Authorize]` e _roles_.

---

## Hospedagem e Servidores

- Pode ser hospedada no IIS, Azure App Service, contêiner Docker ou qualquer servidor compatível com .NET Core.
- O servidor Kestrel é o servidor web interno e eficiente utilizado pelo ASP.NET Core.

---

## Tecnologias Complementares

| Tecnologia       | Função                                        |
| ---------------- | --------------------------------------------- |
| Entity Framework | ORM para acesso a dados                       |
| Swagger/OpenAPI  | Documentação interativa da API                |
| SignalR          | Comunicação em tempo real via WebSocket       |
| MediatR          | Implementação de CQRS e organização de lógica |

---
