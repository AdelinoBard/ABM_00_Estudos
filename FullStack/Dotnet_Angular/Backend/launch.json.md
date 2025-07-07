# `launch.json`

É um arquivo de configuração localizado em `.vscode/launch.json` que define **como o VS Code deve iniciar e depurar sua aplicação**. Ele permite configurar diferentes navegadores, URLs, e diretórios de origem para facilitar o processo de debugging.

---

## Estrutura típica no seu projeto

O arquivo contém configurações para os navegadores Edge e Chrome, por exemplo:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "edge",
      "request": "launch",
      "name": "localhost (Edge)",
      "url": "https://localhost:4200",
      "webRoot": "${workspaceFolder}"
    },
    {
      "type": "chrome",
      "request": "launch",
      "name": "localhost (Chrome)",
      "url": "https://localhost:4200",
      "webRoot": "${workspaceFolder}"
    }
  ]
}
```

---

### Explicando cada campo

- `"type"`: Define o tipo de depurador. Pode ser `"chrome"` ou `"edge"`.
- `"request"`: `"launch"` indica que o VS Code deve iniciar o navegador.
- `"name"`: Nome da configuração que aparece na lista de perfis de depuração.
- `"url"`: URL que será aberta no navegador ao iniciar a depuração (geralmente o Angular roda em `https://localhost:4200`).
- `"webRoot"`: Diretório raiz dos arquivos do frontend. `${workspaceFolder}` aponta para a pasta principal do projeto.

---

## Dicas importantes

- **Use apenas os blocos de navegador que você tem instalado**. Se você mantiver configurações para navegadores ausentes, o projeto pode falhar ao iniciar.
- Você pode alternar entre Chrome e Edge diretamente no menu de depuração do VS Code.
- Se estiver usando HTTPS (`https://localhost:4200`), certifique-se de que os certificados estejam corretamente configurados no Angular.

---

## Integração com Backend .NET

O `launch.json` cuida do frontend. Para o backend .NET, o Visual Studio usa o `launchSettings.json`, que define como o servidor Kestrel ou IIS Express será iniciado. Ambos os arquivos trabalham juntos para permitir depuração simultânea do frontend e backend.

---
