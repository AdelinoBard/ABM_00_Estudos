# `package.json`

O `package.json` arquivo é o arquivo de configuração do **Node Package Manager (npm)**. Ele basicamente contém uma lista de pacotes npm que o desenvolvedor deseja restaurar antes do projeto começa.

É um **arquivo de configuração JSON** que descreve o projeto e gerencia:

- Dependências e versões
- Scripts de automação
- Metadados (nome, versão, autor, etc.)
- Configurações específicas para ferramentas como ESLint, Babel, Jest, etc.

---

## Estrutura típica

```json
{
  "name": "meu-projeto-angular",
  "version": "1.0.0",
  "scripts": {
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test"
  },
  "dependencies": {
    "@angular/core": "^15.0.0",
    "rxjs": "^7.5.0"
  },
  "devDependencies": {
    "karma": "~6.4.0",
    "typescript": "~4.8.4"
  }
}
```

---

### Principais seções explicadas

| Seção | Função |
| --- | --- |
| `name` e `version` | Identificam o projeto |
| `scripts` | Automatizam tarefas (build, test, lint, etc.) |
| `dependencies` | Pacotes necessários em tempo de execução |
| `devDependencies` | Pacotes usados apenas em desenvolvimento (testes, compiladores, etc.) |
| `config` | Valores personalizados acessíveis via scripts |
| `engines` | Define versões mínimas de Node/npm |

---

## Prefixos de versão

- `^1.2.3`: aceita atualizações **menores e patches** (exclui `2.0.0`)
- `~1.2.3`: aceita apenas **patches** (exclui `1.3.0`)
- Sem prefixo: trava na versão exata

Esses prefixos ajudam a controlar o comportamento de atualização automática dos pacotes.

Para uma lista extensa de comandos e prefixos _npmJS_ disponíveis, é aconselhável verificar o site oficial da Documentação do _npmJS_ em <https://docs.npmjs.com/files/package.json>.

---

## Por que ele é importante?

- Garante que todos os desenvolvedores usem as **mesmas dependências**
- Permite **automatizar tarefas** com scripts personalizados
- Facilita a integração com ferramentas de CI/CD
- É essencial para o funcionamento do `npm install`, que gera a pasta `/node_modules`

---

## Dicas para seu projeto FullStack

- Mantenha o `package.json` **versionado no Git**
- Combine com `package-lock.json` para garantir reprodutibilidade
- Use scripts como `npm run lint` ou `npm run test` para facilitar o dia a dia
- Evite instalar pacotes sem salvar no `package.json` (`npm install pacote --save` ou `--save-dev`)

---
