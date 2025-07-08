# `favicon.ico`

É um **ícone de site** (site icon) exibido em:

- Guias do navegador
- Barra de endereços
- Favoritos e histórico
- Atalhos na área de trabalho ou tela inicial (em dispositivos móveis)

O nome “favicon” vem de “**favorite icon**”, e o formato `.ico` permite armazenar múltiplos tamanhos e profundidades de cor em um único arquivo.

---

## Onde ele aparece no projeto Angular?

- Localizado por padrão em: `src/favicon.ico`
- Referenciado no `index.html`:

```html
<link rel="icon" type="image/x-icon" href="favicon.ico" />
```

Esse caminho é relativo à pasta `src`, e o Angular CLI já inclui esse ícone automaticamente ao criar o projeto.

---

## Como o Angular lida com o favicon?

- O `favicon.ico` é incluído como **ativo estático** no build final
- Ele é listado na seção `"assets"` do `angular.json`:

```json
"assets": [
  "src/favicon.ico",
  "src/assets"
]
```

Isso garante que o ícone seja copiado para a pasta `dist/` durante o build e esteja disponível para o navegador.

---

## Personalização e substituição

Você pode substituir o ícone padrão do Angular (aquele com o “A” vermelho) por um ícone personalizado:

1. Crie ou obtenha um novo ícone `.ico` (tamanho recomendado: **32x32** ou **48x48** pixels)
2. Substitua o arquivo `src/favicon.ico`
3. Limpe o cache do navegador (Ctrl+F5) para ver a mudança
4. Opcionalmente, use um ícone `.png` e altere o `index.html`:

```html
<link rel="icon" type="image/png" href="assets/favicon.png" />
```

---

## Dicas práticas

- Se o ícone não atualizar, pode ser cache do navegador — experimente abrir em outro navegador ou limpar o cache
- Para melhor compatibilidade com dispositivos móveis, considere usar ícones adicionais (`apple-touch-icon`, `manifest.json`)
- Ferramentas como [favicon.io](https://favicon.io/) ou [realfavicongenerator.net](https://realfavicongenerator.net/) ajudam a criar favicons otimizados

---
