# `styles.css`

É um **arquivo CSS localizado em `src/styles.css`** que define **estilos aplicáveis a toda a aplicação Angular**. Diferente dos estilos encapsulados por componente, os estilos definidos aqui são **globais** e afetam qualquer elemento que corresponda aos seletores definidos.

---

## Estrutura típica

```css
/* Estilo global para parágrafos */
p {
  font-family: "Segoe UI", sans-serif;
  color: #333;
  line-height: 1.6;
}

/* Estilo para botões */
button {
  background-color: #0078d4;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
}
```

Você pode incluir regras CSS diretamente ou importar outros arquivos:

```css
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");
@import "./assets/css/custom-theme.css";
```

---

## Como o Angular usa esse arquivo?

- O Angular CLI injeta automaticamente o `styles.css` no build final
- Ele é referenciado no `angular.json`:

```json
"styles": [
  "src/styles.css"
]
```

- Durante o build, os estilos são **empacotados e inseridos no `<head>` do `index.html`** como um `<style>` embutido ou como arquivo externo, dependendo da configuração

---

## Diferença entre estilos globais e por componente

| Tipo de estilo | Escopo de aplicação       | Arquivo típico    |
| -------------- | ------------------------- | ----------------- |
| Global         | Toda a aplicação          | `styles.css`      |
| Por componente | Apenas no componente alvo | `*.component.css` |

Estilos globais são úteis para:

- Tipografia padrão
- Cores e temas
- Layout base
- Reset de estilos (`normalize.css` ou `reset.css`)

---

## Dicas para seu projeto FullStack

- Use o `styles.css` para definir estilos universais que não dependem de lógica de componente
- Evite sobrescrever estilos de componentes diretamente — prefira usar classes utilitárias
- Para organização, crie subpastas como `src/assets/css/` e importe arquivos no `styles.css`
- Teste estilos com ferramentas como DevTools para garantir que estão sendo aplicados corretamente

---
