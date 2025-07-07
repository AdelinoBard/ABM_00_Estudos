# OpenAPI (Swagger)

**OpenAPI Specification (OAS)** é uma especificação independente de linguagem para **descrever e documentar APIs REST**. Ela permite que tanto humanos quanto máquinas compreendam os recursos de uma API sem precisar acessar o código-fonte.

## Principais objetivos

- Documentar APIs de forma padronizada
- Permitir geração automática de clientes, servidores e testes
- Facilitar integração entre sistemas desacoplados

---

## Evolução do Swagger para OpenAPI

- Swagger surgiu em 2010 como uma ferramenta para documentar APIs REST.
- Em 2016, foi renomeado oficialmente para **OpenAPI Specification** e passou a ser mantido pela OpenAPI Initiative, sob a Linux Foundation.
- Swagger continua existindo como um conjunto de ferramentas que implementam e trabalham com a especificação OpenAPI.

---

## Ferramentas Swagger baseadas em OpenAPI

Essas ferramentas ajudam a criar, visualizar e consumir APIs:

| Ferramenta | Função |
| --- | --- |
| **Swagger Editor** | Editor online para escrever definições OpenAPI |
| **Swagger UI** | Interface interativa para visualizar e testar endpoints da API |
| **Swagger Codegen** | Gera código cliente e servidor a partir da especificação |
| **Swashbuckle.AspNetCore** | Pacote NuGet para integrar Swagger em projetos ASP.NET Core |

---

## Como funciona no Visual Studio com .NET

Ao criar um projeto ASP.NET Core com suporte a OpenAPI habilitado:

- O Visual Studio inclui automaticamente o pacote **Swashbuckle.AspNetCore**.
- O Swagger UI é configurado no `Program.cs` e está disponível apenas em ambiente de desenvolvimento.
- O endpoint padrão é algo como: `https://localhost:40443/swagger`.

### Componentes do Swashbuckle

- `SwaggerGen`: Gera o documento Swagger a partir dos controladores e modelos.
- `Swagger`: Middleware que expõe o documento como JSON.
- `SwaggerUI`: Interface visual para explorar a API.

---

## Benefícios em projetos FullStack

Quando você usa Angular no frontend e .NET no backend, o OpenAPI oferece:

- Documentação clara para o frontend consumir a API
- Geração automática de clientes Angular com ferramentas como `NSwag`
- Facilidade para testar e validar endpoints durante o desenvolvimento
- Controle sobre exposição pública da documentação (evitando riscos de segurança)

---
