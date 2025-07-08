# `aspnetcore-https.js`

O arquivo `aspnetcore-https.js` é um **script auxiliar gerado pelo Visual Studio** em projetos que integram ASP.NET Core com frameworks JavaScript como Angular ou React. Ele tem um papel bem específico: **configurar o ambiente de desenvolvimento para usar HTTPS**, aproveitando os certificados gerados pelo ASP.NET Core.

---

## O que é o `aspnetcore-https.js`?

É um **script Node.js** que:

- Localiza o **certificado HTTPS gerado pelo comando `dotnet dev-certs`**
- Exporta esse certificado em formato `.pem` e `.key`
- Permite que o frontend (Angular) use HTTPS localmente, evitando problemas de segurança e pop-ups de autorização

---

## Onde ele aparece?

- Criado automaticamente pelo Visual Studio na pasta `ClientApp` (ou raiz do frontend)
- Usado como parte do script `prestart` no `package.json`:

```json
"scripts": {
  "prestart": "node aspnetcore-https",
  "start": "ng serve"
}
```

Esse `prestart` é o responsável por acionar o pop-up de autorização HTTPS, por exemplo — ele executa o script antes de iniciar o servidor Angular.

---

## Estrutura simplificada do script

```js
const fs = require("fs");
const spawn = require("child_process").spawn;
const path = require("path");

const baseFolder = process.env.APPDATA
  ? `${process.env.APPDATA}/ASP.NET/https`
  : `${process.env.HOME}/.aspnet/https`;

const certificateName = process.env.npm_package_name || "nome-do-app";

const certFilePath = path.join(baseFolder, `${certificateName}.pem`);
const keyFilePath = path.join(baseFolder, `${certificateName}.key`);

if (!fs.existsSync(certFilePath) || !fs.existsSync(keyFilePath)) {
  spawn(
    "dotnet",
    [
      "dev-certs",
      "https",
      "--export-path",
      certFilePath,
      "--format",
      "Pem",
      "--no-password",
    ],
    { stdio: "inherit" }
  ).on("exit", (code) => process.exit(code));
}
```

---

## Por que isso é útil?

- Garante que o frontend possa se comunicar com o backend via HTTPS durante o desenvolvimento
- Evita erros de CORS e Mixed Content em navegadores modernos
- Facilita testes com APIs protegidas por HTTPS

---

## Observações importantes

- Esse script **não é um pacote NPM**, então não tente instalar com `npm install aspnetcore-https`
- Ele é **gerado localmente** e geralmente **excluído do controle de versão**
- Se estiver ausente, você pode copiar de outro projeto ou criar manualmente com base no exemplo acima

---
