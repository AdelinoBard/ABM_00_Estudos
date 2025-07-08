# VS

## solução

Uma solução é basicamente uma coleção de um ou vários projetos.

- Ex.: em nossa abordagem de múltiplos projetos, acabaremos tendo dois projetos (o aplicativo Angular front-end e a API Web ASP.NET Core back-end) em uma única solução.

## Conselhos

- Também é aconselhável escolher uma pasta de nível raiz com um nome curto para evitar possíveis erros e/ou problemas relacionados a nomes de caminho muito longos: o Windows 10 tem um limite de 260 caracteres que pode criar alguns problemas com alguns pacotes npm profundamente aninhados.

- **Portas Fixas**: O motivo para usar portas fixas é que teremos que lidar com alguns recursos do framework (como proxies internos) que exigem endpoints fixos. No caso improvável de essas portas ficarem ocupadas e/ou não puderem ser usadas, sinta-se à vontade para alterá-las: apenas certifique-se de aplicar as mesmas alterações em todo o livro para evitar erros HTTP 404.
