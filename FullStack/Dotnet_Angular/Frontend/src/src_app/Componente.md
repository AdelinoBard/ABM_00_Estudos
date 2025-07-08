# Componente

Para criar um componente Angular chamado **Modelo** via Angular CLI, basta abrir o terminal na raiz do seu projeto Angular e digitar o seguinte comando:

```bash
ng generate component Modelo
```

Ou, de forma abreviada:

```bash
ng g c Modelo
```

---

## Explicação do comando

| Parte             | Significado                                         |
| ----------------- | --------------------------------------------------- |
| `ng`              | Chama a Angular CLI                                 |
| `generate` (`g`)  | Instrui a CLI a gerar um artefato                   |
| `component` (`c`) | Indica que você quer criar um **componente**        |
| `Modelo`          | Nome do componente (será convertido para lowercase) |

---

## O que será gerado

Esse comando criará uma pasta chamada `modelo` dentro de `/src/app/` com os seguintes arquivos:

```plaintext
/src/app/modelo/
├── modelo.component.ts       → lógica do componente
├── modelo.component.html     → template HTML da interface
├── modelo.component.css      → estilos do componente
├── modelo.component.spec.ts  → testes unitários (usando Jasmine/Karma)
```

Além disso, o Angular CLI irá:

- Importar o `ModeloComponent` no `AppModule`
- Adicionar `ModeloComponent` à lista de `declarations` do módulo

---

## Dicas

- Para **ignorar a criação dos testes**:

  ```bash
  ng g c Modelo --skip-tests
  ```

- Para **simular a geração sem fazer alterações**:

  ```bash
  ng g c Modelo --dry-run
  ```

- Para gerar o componente em uma **subpasta específica**:

  ```bash
  ng g c features/modelo
  ```

---
