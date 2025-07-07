# Angular

O Angular é um framework moderno e robusto para desenvolvimento do lado do cliente, projetado para potencializar ao máximo os recursos avançados do HTML, do ECMAScript e dos navegadores atuais. Ele permite criar aplicações web dinâmicas ao vincular de forma eficiente as partes de entrada e saída de uma página HTML a um modelo estruturado, flexível, reutilizável e de fácil testabilidade.

---

## História do Angular

Para compreender o surgimento do Angular, é preciso revisitar uma era em que o desenvolvimento web era amplamente dominado por bibliotecas JavaScript como jQuery e MooTools. Naquele cenário, os primeiros frameworks client-side — como Dojo, Backbone.js e Knockout.js — tentavam conquistar espaço entre os desenvolvedores, ainda que enfrentassem limitações quanto à escalabilidade e à organização do código. Era um tempo em que soluções modernas como React e Vue.js sequer haviam sido concebidas.

Embora o jQuery continue presente em cerca de 74% dos sites, segundo plataformas como BuiltWith e w3Techs, seu papel evoluiu. A preferência dos desenvolvedores migrou para ferramentas mais robustas e completas — e foi nesse contexto que o Angular emergiu como protagonista. Ao oferecer uma arquitetura escalável, suporte a aplicações complexas e integração nativa de recursos avançados como injeção de dependência, roteamento e two-way data binding, o Angular redefiniu os padrões do desenvolvimento front-end moderno.

---

## Início do AngularJS

A história do AngularJS teve início em 2009, quando Miško Hevery — então engenheiro de software no Google — e Adam Abrons — hoje diretor de engenharia na Grand Rounds — embarcaram em um projeto paralelo ambicioso. Juntos, criaram uma ferramenta de desenvolvimento web de ponta a ponta (E2E) que incluía um serviço de armazenamento online em JSON e uma biblioteca client-side para construção de aplicações web baseadas nesse serviço. Para divulgar o projeto, registraram o domínio GetAngular.com.

Na mesma época, Hevery foi designado para trabalhar no projeto Google Feedback, ao lado de dois outros desenvolvedores. Após meses de trabalho, o time acumulou cerca de 17.000 linhas de código em apenas seis meses — o que levou a um cenário cada vez mais complexo, difícil de testar e manter.

Foi então que Hevery propôs um desafio ao seu gerente: reescrever todo o aplicativo usando o GetAngular, sozinho, em apenas duas semanas. Embora tenha demorado três semanas (um pouco além da previsão inicial), o novo código tinha apenas 1.500 linhas, mantendo todas as funcionalidades do anterior com uma arquitetura muito mais enxuta e eficiente.

O resultado impressionou o Google, que abraçou o projeto e lhe deu um novo nome: AngularJS. Nascia assim um dos frameworks mais influentes na história do desenvolvimento web.

> Para conferir essa história contada pelo próprio criador, veja o discurso de Miško Hevery na ng-conf 2014: [Assista aqui](https://www.youtube.com/watch?v=r1A1VR0ibIQ)

---

## AngularJS – Primeiros Passos e Sucesso

A primeira versão estável do AngularJS apareceu no GitHub em outubro de 2010, com o codinome curioso "dragon-breath". Já a versão 1.0.0, chamada "temporal domination", foi lançada em junho de 2012 e rapidamente se tornou um fenômeno nas comunidades de desenvolvimento web.

Mas por que o AngularJS chamou tanta atenção? Ele trouxe várias novidades que facilitaram muito a vida dos desenvolvedores. Vamos conhecer algumas:

- **Injeção de dependência**  
  Esse nome pode parecer complicado, mas a ideia é simples: em vez de o desenvolvedor ter que organizar tudo sozinho, o AngularJS ajuda a montar os pedaços do sistema automaticamente. Isso deixa o código mais limpo e fácil de testar.

- **Diretivas**  
  As diretivas permitem criar “comandos personalizados” no HTML, que podem adicionar comportamentos especiais a elementos da página. É como dar superpoderes ao seu código HTML, tornando tudo mais dinâmico e reutilizável.

- **Ligação de dados bidirecional (Two-way Data Binding)**  
  Uma das grandes mágicas do AngularJS: sempre que os dados mudam no sistema, a tela muda junto. E se algo mudar na tela, os dados se atualizam também — tudo automaticamente!

- **Aplicações de Página Única (SPA)**  
  Com o AngularJS, você não precisa recarregar a página toda a cada clique. Ele permite criar sites rápidos e fluídos, parecidos com aplicativos de celular. Essa abordagem virou tendência e inspirou frameworks como React e Vue.js.

- **Cache amigável**  
  Como o AngularJS trabalha no navegador (lado do cliente), os sites criados com ele podem ser armazenados em cache com facilidade. Isso ajuda o site a abrir mais rápido e até funcionar melhor em redes lentas.

---

## Angular 2 – Um Novo Começo

Em 14 de setembro de 2016, nasceu o **Angular 2**, uma versão completamente reformulada do antigo AngularJS. Mas não foi apenas uma atualização: foi uma **reescrita total**, inspirada nas novas regras da linguagem JavaScript (ES2015). Assim como quando o ASP.NET foi reinventado como ASP.NET Core, o Angular 2 surgiu para acompanhar os tempos modernos — com um jeito completamente diferente de pensar e criar aplicações web.

A mudança foi tão profunda que os códigos escritos no AngularJS antigo quase não podiam ser reaproveitados. Mesmo mantendo um nome parecido, o Angular 2 era, na prática, **um framework novo**, mais moderno e preparado para os desafios das aplicações atuais.

### O que o Angular 2 trouxe de novo?

- **Arquitetura baseada em componentes**  
  Agora, cada parte da aplicação pode ser separada em "blocos" chamados **componentes**. Isso facilita organizar, testar e reaproveitar o código — como se estivéssemos montando um quebra-cabeça.

- **Injeção de dependência turbinada**  
  O sistema que ajuda a montar as partes da aplicação foi melhorado. O desenvolvedor não precisa se preocupar em conectar tudo manualmente — o Angular cuida disso por trás dos bastidores.

- **Pensamento modular e moderno**  
  A estrutura do Angular 2 permite dividir a aplicação em partes menores e mais fáceis de entender e manter.

- **Controle de versão semântico (SemVer)**  
  O Angular 2 começou a usar uma forma inteligente de marcar suas versões:

  - X: mudança grande e incompatível
  - Y: melhorias que não quebram o código
  - Z: correções pequenas  
    Isso ajuda quem desenvolve a entender o que mudou entre versões rapidamente.

- **TypeScript como base**  
  O Angular 2 adotou o **TypeScript**, uma linguagem desenvolvida pela Microsoft que melhora o JavaScript, adicionando recursos para facilitar o desenvolvimento, como tipos de dados e organização por classes. Mas calma: quem sabe só JavaScript pode aprender aos poucos, e o Angular ajuda bastante com isso!

- **Renderização no servidor (SSR)**  
  Com o **Angular Universal**, agora é possível “pré-montar” a página no servidor antes de enviar para o navegador. Isso faz o site abrir mais rápido — ótimo para melhorar a experiência do usuário.

- **Ferramentas para apps mobile**  
  O **Angular Mobile Toolkit** trouxe recursos para desenvolver aplicativos móveis com ótimo desempenho.

- **Interface de linha de comando (CLI)**  
  Quer criar um componente ou uma nova rota? Com poucos comandos no terminal, a **CLI do Angular** já faz tudo para você — economizando tempo e evitando erros.

---

## Angular 4 – Mais leve, mais rápido e mais organizado

Em 23 de março de 2017, o Google lançou o **Angular 4**, que foi uma continuação direta do Angular 2. E você deve estar se perguntando: “Cadê o Angular 3?” Pois é, essa versão foi **pulada de propósito**! Como partes do framework estavam em versões diferentes (por exemplo, o Angular Router já estava na versão 3), o time resolveu sincronizar tudo direto na versão 4 para evitar confusão e padronizar os números de versão.

### O que mudou no Angular 4?

A maior parte do framework continuava parecida com a do Angular 2, mas vieram **várias melhorias que deixaram tudo mais eficiente e amigável para desenvolvedores**, mesmo iniciantes. Dá uma olhada:

- **Compilação antecipada (AOT – Ahead of Time)**  
  No Angular 4, os arquivos da sua aplicação são _compilados antes_ de serem enviados para o navegador. Isso deixa o site mais rápido ao carregar e ajuda a detectar erros antes mesmo de executar. É como revisar um texto antes de imprimir — muito mais seguro!

- **Animações separadas em pacote próprio**  
  As animações passaram a fazer parte de um pacote específico: `@angular/animations`. Isso permite que projetos que não usam efeitos visuais fiquem mais leves e rápidos, já que não carregam essa parte.

- **Validação de e-mail simplificada**  
  O Angular 4 trouxe um novo validador de formulários que facilita a verificação de e-mails válidos — ótimo para quem está criando formulários de login ou contato.

- **Novo acesso aos parâmetros de URL com `paramMap`**  
  Agora ficou mais fácil trabalhar com links que contêm parâmetros, como `www.site.com/produto?id=10`. O `paramMap` ajuda a ler esses dados com mais clareza e simplicidade.

- **Suporte melhorado à internacionalização (i18n)**  
  O Angular 4 deu um passo importante para quem precisa criar versões do site em vários idiomas, tornando o processo mais fácil e flexível.

---

## Angular 5 – Melhorias para um desenvolvimento mais ágil e moderno

Em 1º de novembro de 2017, o Google lançou o **Angular 5**, trazendo várias melhorias focadas em **desempenho**, **organização** e **experiência do desenvolvedor**. E se você está começando a aprender Angular, fique tranquilo: essa versão tornou o processo de criar aplicações web mais rápido, seguro e intuitivo.

Vamos ver o que ficou mais legal nessa versão?

### Nova API para fazer chamadas HTTP

Se você quiser que sua aplicação converse com um servidor (por exemplo, para buscar dados ou enviar informações), vai usar algo chamado "API HTTP". O Angular 5 trouxe uma versão nova e muito melhor disso:

- Antes, usava-se o pacote `@angular/http`, que foi **descontinuado**.
- Agora, tudo é feito com `@angular/common/http`, que oferece:
  - Suporte melhor para trabalhar com arquivos JSON.
  - **Interceptadores**, que permitem modificar ou observar requisições antes que sejam enviadas.
  - **Objetos imutáveis**, que tornam o código mais seguro e confiável.

Essa mudança deixou o processo de comunicação com servidores mais **poderoso e organizado** para qualquer aplicativo.

### Transferência de Estado entre Servidor e Cliente

Para deixar o carregamento da página ainda mais rápido, o Angular 5 introduziu uma **API de Transferência de Estado**. Com ela, é possível:

- Armazenar informações do servidor antes de enviá-las ao navegador.
- Fazer com que o navegador carregue dados prontos, sem precisar refazer tudo do zero.

Isso ajuda muito em aplicativos que usam **renderização no servidor**, especialmente aqueles com conteúdo dinâmico.

### Mais controle sobre o que acontece durante a navegação

O Angular 5 trouxe vários **eventos novos no sistema de rotas**, que são como “avisos” para os desenvolvedores saberem exatamente o que está acontecendo durante a troca de páginas ou carregamento de dados. Alguns desses eventos incluem:

- `ActivationStart` e `ActivationEnd` – para saber quando uma rota começa e termina.
- `GuardsCheckStart` e `GuardsCheckEnd` – ajudam a controlar permissões antes de entrar em uma página.
- `ResolveStart` e `ResolveEnd` – mostram quando dados estão sendo carregados antes de exibir o conteúdo.

Esses eventos ajudam a criar aplicações mais **inteligentes, seguras e responsivas**.

---

## Angular 6 – Evolução com mais consistência

Em abril de 2018, o Google lançou o **Angular 6**. Essa versão não trouxe grandes mudanças visuais ou revolucionárias, mas foi essencial para deixar o framework mais **organizado, rápido e fácil de manter**. Pense nela como aquela atualização que arruma a casa e prepara tudo para as novidades futuras.

### Mais organização com ferramentas e compatibilidade

A principal proposta do Angular 6 foi **padronizar a estrutura do framework** e de suas ferramentas, facilitando a vida dos desenvolvedores. Algumas das melhorias mais importantes foram:

- **Novo sistema de dependências com `ng add`**  
  Agora ficou mais fácil instalar novos recursos em um projeto Angular. Com o comando `ng add`, o próprio Angular baixa o que for necessário, configura tudo automaticamente e já deixa pronto para uso — quase como instalar um aplicativo no celular com um clique!

- **Atualizações na CLI (Interface de Linha de Comando)**  
  A ferramenta usada para criar projetos e comandos do Angular (a famosa CLI) ficou mais inteligente e ganhou **novos comandos**, tornando o processo de desenvolvimento mais rápido e intuitivo.

- **Compatibilidade com o RxJS 6**  
  O RxJS é uma biblioteca usada para lidar com eventos e dados que mudam com o tempo (como cliques, respostas de API etc.). A versão 6 trouxe melhorias na forma de **registrar e organizar códigos reativos**, deixando tudo mais limpo e fácil de entender.

- **Angular Material mais integrado**  
  O suporte ao **Angular Material** ficou melhor. Esse é um conjunto de componentes prontos que seguem o estilo visual do Google (Material Design) — ótimo para criar interfaces bonitas com pouco esforço.

- **Introdução ao Ivy (novidade futura)**  
  A equipe do Angular apresentou o **Ivy**, um novo sistema de renderização (a forma como os componentes são mostrados na tela). Ele não foi ativado ainda, mas é a base para versões futuras que deixariam os aplicativos ainda mais rápidos e leves.

---

## Angular 7 – Mais rápido, mais amigável e com boas novidades

Em outubro de 2018, chegou o **Angular 7**, trazendo melhorias em várias áreas do framework — como o código principal, os componentes visuais (Angular Material) e as ferramentas de desenvolvimento (CLI). Foi uma atualização importante, focada em deixar a experiência mais prática e agradável para quem desenvolve aplicações web com Angular.

### Atualizações simplificadas

Atualizar projetos Angular antigos para versões novas costumava ser trabalhoso... mas isso mudou! O Angular 7 veio com:

- **Guia interativo de atualização**: disponível em [update.angular.io](https://update.angular.io), esse guia mostra passo a passo o que precisa ser feito (com comandos e sugestões) para atualizar seu projeto com segurança.
- **Novo comando na CLI (`ng update`)**: com um simples comando no terminal, você pode atualizar automaticamente as dependências e configurações do projeto.

### Dicas ao usar comandos (Prompts da CLI)

Agora, ao criar um novo projeto com `ng new` ou adicionar pacotes com `ng add`, a ferramenta faz perguntas úteis — como se você quer usar roteamento ou SCSS — e já configura tudo pra você. Isso ajuda muito quem está começando, evitando erros e tornando o processo mais intuitivo.

### Novidades no Angular Material e CDK

O Angular 7 melhorou a biblioteca visual do framework e trouxe recursos muito úteis para interfaces:

- **Rolagem virtual**: ideal para listas enormes. Somente os itens visíveis são carregados, deixando o app mais leve e rápido.
- **Arrastar e soltar (drag & drop)**: agora você pode criar interfaces interativas com movimentos personalizados sem complicação.
- **Listas suspensas (dropdowns)** mais eficientes e fáceis de configurar.

### Compatibilidade com ferramentas parceiras

O Angular 7 reforçou o suporte a projetos que ajudam a trabalhar com Angular:

- **Angular Console**: interface gráfica para criar e gerenciar projetos Angular.
- **AngularFire**: pacote oficial para conectar o Angular com o Firebase.
- **NativeScript**: para criar apps nativos Android/iOS com Angular.
- **StackBlitz**: um editor online onde você pode programar e testar projetos Angular direto do navegador!

### Suporte às últimas versões de ferramentas

O Angular 7 passou a funcionar com novas versões de ferramentas usadas no dia a dia:

- **TypeScript 3.1**
- **RxJS 6.3**
- **Node.js 10**

Mesmo assim, versões anteriores ainda funcionam para quem precisa manter projetos antigos.

### Angular Language Service – ajuda direto no código

Essa ferramenta mostra sugestões, erros e dicas enquanto você escreve o código HTML dos seus componentes. É como ter um assistente ao seu lado, corrigindo e completando tudo em tempo real — antes ela só funcionava em editores como VS Code, mas passou a funcionar também no StackBlitz.

---

## Angular 8 – Preparando terreno para o futuro

Lançado em 29 de maio de 2019, o **Angular 8** chegou com foco em melhorias internas e ferramentas que tornaram o desenvolvimento web ainda mais poderoso. Uma das principais novidades foi a chegada opcional do **Ivy**, uma nova forma de transformar os componentes do Angular em código JavaScript que o navegador entende.

### O que é Ivy?

Imagine o Ivy como um novo “motor” para o Angular — mais rápido, leve e esperto. Ele não mudou a forma como escrevemos o código, mas mudou a forma como o Angular entende e usa esse código nos bastidores. No Angular 8, ainda era opcional, ativado colocando `"enableIvy": true` no arquivo `tsconfig.json`. Mais tarde, ele se tornaria o padrão.

### Outras melhorias importantes

- **Bazel – construção automática de apps**  
  O Angular 8 passou a suportar o **Bazel**, uma ferramenta que ajuda a automatizar tarefas como construir e testar o projeto. Ideal para quem trabalha em equipes grandes ou com sistemas mais complexos que precisam de rapidez e organização.

- **Roteamento com nova sintaxe**  
  Agora ficou mais moderno declarar rotas (caminhos do site) com a função `import()`. Isso permite carregar partes da aplicação só quando o usuário realmente precisa — deixando tudo mais rápido.

- **Service workers com mais controle**  
  Os **service workers** são pequenos scripts que funcionam nos bastidores, ajudando a deixar os apps mais rápidos e até funcionarem offline. Com Angular 8, é possível controlar melhor quando e como eles são ativados. Também ficou mais fácil ignorar esses scripts em certas situações usando o cabeçalho `ngsw-bypass`.

- **API do espaço de trabalho**  
  Agora é mais simples ajustar configurações do projeto com uma **API que lê e modifica o arquivo `angular.json`**, sem precisar mexer diretamente no código. Bem prático!

### Limpeza na casa

O Angular 8 também deu uma "faxina": removeu ferramentas antigas e pacotes que já estavam obsoletos, como o antigo `@angular/http`, que foi substituído há algumas versões por `@angular/common/http`.

---

## Angular 9 – Um grande salto em performance

Lançado em fevereiro de 2020, o **Angular 9** foi uma versão marcante que trouxe **melhor desempenho, pacotes menores** e uma nova tecnologia que trabalharia nos bastidores de todos os projetos: o tão aguardado **Ivy**.

Apesar de ter ficado pouco tempo como a versão mais recente (apenas 4 meses antes do Angular 10), o Angular 9 foi essencial para deixar o framework mais rápido, leve e fácil de manter — especialmente para quem está começando a desenvolver aplicações web.

### O que há de novo?

- **Pacotes JavaScript menores e mais rápidos**  
  Um dos maiores problemas das versões anteriores do Angular eram os arquivos muito grandes que os navegadores precisavam baixar. O Angular 9 trouxe uma solução: pacotes mais compactos, que carregam mais rápido e melhoram a experiência do usuário.

- **Ivy se torna padrão**  
  O **Ivy** é o “motor” que transforma componentes Angular em código JavaScript entendível pelos navegadores. Ele já estava disponível como opção no Angular 8, mas agora virou **o padrão**! Com ele, os projetos passaram a ficar menores e mais rápidos, sem que os desenvolvedores precisassem mudar a forma de programar.

- **Ligações sem seletor (sem selector)**  
  Essa funcionalidade, que antes estava ausente no Ivy, voltou com tudo. Ela permite que certos componentes sejam vinculados de forma mais flexível dentro do código.

- **Internacionalização (i18n)**  
  Agora ficou mais fácil preparar um aplicativo para funcionar em vários idiomas! Com a ajuda de comandos da **Angular CLI** e o novo atributo `i18n`, o framework gera automaticamente os arquivos necessários para tradutores.
  - Curiosidade: `i18n` é uma abreviação de **internationalization** — há 18 letras entre o “i” e o “n”. Assim como `l10n` representa **localization**. Divertido, né?

### Por que o Ivy é tão importante?

Para quem está começando, o Ivy pode parecer invisível — ele atua nos bastidores. Mas o impacto é enorme:

- Traduz o que você escreve nos componentes para ações que alteram a página.
- Usa menos instruções e gera menos código JavaScript.
- Faz com que o app fique mais leve, rápido e fácil de manter.

O Angular 9 foi como uma atualização de motor de carro: o visual continua parecido, mas por dentro tudo ficou mais eficiente.

---

## Angular 10 – Mais ajustes, mais leveza e mais controle

Lançado em 24 de junho de 2020, o **Angular 10** chegou poucos meses depois do Angular 9. O motivo? A equipe quis **retomar o ritmo de lançamentos** e ajustar o calendário, já que a versão anterior saiu com algum atraso. Apesar de parecer uma atualização rápida, essa versão trouxe várias correções e melhorias que tornaram o framework ainda mais estável e confiável.

### Mais de 2.000 correções

Sim, o Angular 10 focou muito em limpar e melhorar o que já existia. Foram mais de **2.000 ajustes e correções** de bugs! Isso significa menos erros e uma experiência melhor para quem desenvolve e para quem usa as aplicações.

### Principais novidades para iniciantes

- **Atualização para o TypeScript 3.9**  
  TypeScript é a linguagem usada com Angular, e nessa versão ela ficou ainda mais poderosa e inteligente. Algumas versões antigas deixaram de funcionar, mas tudo isso para garantir que o projeto esteja sempre alinhado com as melhores práticas.

- **Novo seletor de intervalo de datas** no Angular Material  
  O Angular Material — um conjunto de componentes visuais para criar interfaces bonitas — ganhou um **seletor de datas com intervalo**, perfeito para formulários como reservas, calendários e agendamentos.

- **Avisos ao usar CommonJS**  
  Se você estiver usando pacotes com formato **CommonJS**, agora o Angular dá um aviso. Por quê? Porque esse tipo de importação pode deixar o aplicativo mais **pesado e lento**. A ideia é incentivar formas mais modernas e eficientes de importar recursos.

- **Modo de projeto mais rigoroso (strict mode)**  
  Ao criar um projeto novo, você pode ativar um modo chamado **strict**, que aplica regras mais detalhadas no código. Pode parecer desafiador no começo, mas isso ajuda a encontrar erros mais cedo e deixar o aplicativo mais rápido e leve — graças ao famoso **tree-shaking**, que remove código desnecessário.

> Quer saber o que é tree-shaking? É como se o Angular balançasse uma árvore cheia de código e derrubasse tudo que não estivesse sendo usado. Isso deixa o projeto menor e mais rápido! Você pode entender melhor [neste guia](https://developer.mozilla.org/en-US/docs/Glossary/Tree_shaking).

---

## Angular 11 – Mais agilidade, testes modernos e melhorias importantes

Lançado em **11 de novembro de 2020**, o **Angular 11** veio com várias melhorias que tornaram o desenvolvimento web ainda mais rápido, organizado e seguro. Mesmo sem mudanças gigantescas, essa versão trouxe atualizações que ajudam bastante quem está criando aplicações com Angular — incluindo quem está começando agora!

### Testes mais robustos com _Component Test Harness_

Criar bons testes para o seu código é essencial, e o Angular 11 trouxe uma nova forma de fazer isso com o **Component Test Harness**. Em vez de depender da estrutura interna do HTML (DOM), seus testes passam a usar uma "camada intermediária" que simula o comportamento do componente.

Isso ajuda os testes a continuarem funcionando mesmo que o código mude por dentro — ótimo para evitar que pequenos ajustes quebrem funcionalidades.

### Atualizações rápidas com _Hot Module Replacement (HMR)_

O **HMR** permite que o navegador atualize partes do seu aplicativo sem recarregar a página inteira.  
No Angular 11, ficou muito mais fácil usar essa funcionalidade! Basta ativar com o comando:

```bash
ng serve --hmr
```

Assim, você vê as mudanças do seu código quase instantaneamente enquanto desenvolve.

### Suporte ao TypeScript 4.0

O **TypeScript** é a linguagem que roda por trás do Angular, e a nova versão (4.0) trouxe mais rapidez na hora de compilar os projetos, além de facilitar a detecção de erros.

- Atenção: versões anteriores como 3.9 não são mais compatíveis.

### Nova ferramenta de análise: migração de TSLint para ESLint

Antes, o Angular usava o **TSLint** para verificar o estilo e a qualidade do código. Agora, passou a usar o **ESLint**, uma ferramenta mais moderna e com mais recursos.  
O Angular 11 oferece um **passo a passo simples** com a **CLI** para fazer essa troca de forma segura.

### Adeus ao Internet Explorer 9 e 10

A equipe do Angular decidiu encerrar o suporte para navegadores antigos como o **IE 9 e 10**, além do **IE Mobile**.

- Isso ajuda a simplificar o desenvolvimento e aproveitar melhor as tecnologias modernas.

### Outras melhorias úteis

- **Visualização atualizada do Language Service**: ajuda a escrever HTML com dicas de código, sugestões e verificação de erros em tempo real.
- **Service Worker mais eficiente**: melhor controle sobre como e quando os dados são armazenados para funcionar offline.
- **Carregamento lento para saídas nomeadas**: o app só carrega certas partes quando realmente precisa, o que torna tudo mais rápido.
- **Pipes mais seguros**: os tipos usados em operações como formatação de texto, datas e valores ficaram mais bem definidos.
- **Suporte à numeração ISO de semanas**: útil para mostrar corretamente semanas do ano em calendários e datas.

---

## Angular 12 – Mais rápido, mais seguro e mais organizado

O **Angular 12** foi lançado em **12 de maio de 2021**, trazendo melhorias importantes para deixar o desenvolvimento de aplicativos web mais **rápido, seguro e bem estruturado** — mesmo para quem está dando os primeiros passos com o Angular.

### Adeus ao View Engine, olá Ivy

Até então, o Angular usava o **View Engine**, um sistema antigo para transformar componentes em código que o navegador consegue entender. No Angular 12, esse sistema foi **finalmente aposentado** e substituído pelo **Ivy**, uma tecnologia muito mais moderna e eficiente que já vinha sendo adotada desde versões anteriores.

Com o Ivy, os projetos são compilados mais rapidamente e geram menos código — isso significa aplicativos **mais leves e ágeis**!

### Novidades que facilitam a vida do desenvolvedor

- **🔍 Operador de coalescência nula (`??`) nos templates**  
  Esse operador permite mostrar um valor alternativo se algo estiver "vazio" ou indefinido. Exemplo:

  ```html
  {{ usuario.nome ?? 'Visitante' }}
  ```

  Assim, se o nome não estiver disponível, aparece "Visitante".

- **Estilos com Sass direto no componente**  
  Agora você pode escrever **Sass** (uma linguagem de estilo com recursos extras) direto dentro dos componentes Angular. Isso ajuda a organizar melhor os estilos e deixar o visual do app mais bonito e personalizado.

- **Fim do suporte ao IE11 (Internet Explorer)**  
  O Angular 12 avisou que não seria mais compatível com o Internet Explorer 11 na próxima versão. Como esse navegador é bem antigo e quase não usado hoje em dia, essa decisão ajuda os desenvolvedores a focarem em tecnologias mais modernas.

- **Melhorias na comunicação HTTP**  
  A biblioteca do Angular para fazer chamadas HTTP ficou mais clara e prática:
  - Nomes mais fáceis de entender, como `HttpStatusCode.OK`.
  - Novas funções para lidar com parâmetros e informações das requisições com mais facilidade.

### Modo estrito ativado por padrão

O **modo estrito** agora vem ativado automaticamente ao criar novos projetos. Isso significa que:

- O Angular e o TypeScript vão fazer **verificações extras** no seu código.
- Você será alertado sobre possíveis erros ou comportamentos estranhos **logo no início**.
- O aplicativo fica **mais leve**, porque o Angular consegue eliminar partes do código que não estão sendo usadas (**tree-shaking**).

Embora o modo estrito pareça exigir mais atenção, ele ajuda muito quem está aprendendo — mostrando onde melhorar e incentivando boas práticas desde o começo.

---

## Angular 13 – Mais limpo, moderno e eficiente

Lançado em **3 de novembro de 2021**, o **Angular 13** trouxe atualizações importantes que tornaram o framework mais rápido, fácil de manter e alinhado com as tecnologias modernas da web. Se você está começando agora, esta versão dá passos firmes para simplificar a vida dos desenvolvedores — e isso é ótimo!

### O que mudou de forma prática?

- **Fim do View Engine: tudo é Ivy agora!**  
  O Angular passou a usar apenas o **Ivy**, seu sistema de renderização mais novo e inteligente. O mecanismo antigo, chamado View Engine, foi completamente retirado.  
  Isso significa **menos código**, **mais velocidade** e **melhor organização** no projeto. E como o Ivy já era usado desde a versão 9, essa transição ficou bem tranquila.

- **Fim do suporte ao Internet Explorer 11**  
  Com o fim do View Engine, o Angular também deixou de funcionar no **IE11** (aquele navegador bem antigo). Isso libera os desenvolvedores para usar recursos mais modernos sem se preocupar com compatibilidade retrógrada.

- **Novo formato de pacotes (APF)**  
  Os pacotes criados com Angular agora seguem um padrão mais moderno (`ES2020`) e têm suporte oficial para **exports no Node.js**, o que ajuda a organizar e distribuir bibliotecas de forma mais prática.

### Facilidades para quem está desenvolvendo

- **FormControlStatus**  
  Um novo tipo no Angular que ajuda a saber em que estado está um campo de formulário — por exemplo, se está válido, inválido, tocado, sujo, etc.  
  Isso facilita o tratamento de formulários e melhora a experiência do usuário.

- **Nova API de Componentes**  
  Agora é possível criar componentes com **menos código repetitivo**. A ideia é tornar o desenvolvimento mais direto, sem complicações desnecessárias.

- **Cache de compilação ativado por padrão**  
  O Angular passou a guardar partes da compilação para **acelerar os tempos de construção** dos projetos. Isso faz diferença no dia a dia, principalmente quando você está testando ou fazendo ajustes.

- **RxJS atualizado para a versão 7.4**  
  O Angular 13 trouxe uma atualização da biblioteca **RxJS**, usada para trabalhar com dados que mudam com o tempo (como eventos de cliques, respostas de APIs, etc). A nova versão é mais rápida e eficiente.

- **Testes mais leves com TestBed**  
  A ferramenta usada para testes no Angular agora consome **menos memória** e executa tudo **mais rapidamente** — ótimo para quem quer aprender a testar seus componentes sem complicações.

---

## Angular 14 – Mais simples, mais seguro e mais inteligente

Lançado em **2 de junho de 2022**, o **Angular 14** veio cheio de melhorias pensadas para facilitar a vida de quem desenvolve aplicações — especialmente quem está aprendendo! As principais novidades se concentraram na **segurança do código**, na **interface de linha de comando (CLI)** e em formas mais simples de criar componentes e formulários.

### Formulários mais seguros com _Typed Angular Forms_

Antes, ao trabalhar com formulários no Angular, o desenvolvedor podia acabar passando dados errados sem perceber — como enviar um número onde era esperado um texto, por exemplo.

O Angular 14 trouxe a ideia de **tipagem estrita nos formulários**, ou seja:

- O Angular passa a entender melhor os **tipos de dados** que cada campo precisa.
- O desenvolvedor recebe **alertas e sugestões** ao escrever o código.
- Os formulários ficam **mais seguros e fáceis de manter**.

Isso significa menos erros e mais controle sobre o que está sendo enviado no seu app!

### Componentes independentes (_Standalone Components_)

Antes, para criar qualquer componente Angular, era preciso “registrá-lo” dentro de um módulo (`@NgModule`). Mas o Angular 14 trouxe uma forma mais direta:

- Agora você pode **criar componentes que funcionam por conta própria**, usando apenas o `@Component` com suas importações.
- Menos código repetitivo e mais **liberdade na organização** do projeto.

Para quem está começando, isso facilita bastante e deixa tudo menos complicado!

### Limpeza de mensagens de erro (Tree-Shakable Errors)

No processo de criação de uma versão final do app, o Angular tenta “enxugar” ao máximo o código — o que chamamos de **tree-shaking**.

Com essa novidade:

- **Mensagens de erro visíveis** para o desenvolvedor são removidas do código da versão final.
- O app continua funcionando perfeitamente, mas fica **mais leve** e rápido para o usuário.

Isso ajuda a manter o desempenho sem perder os alertas úteis durante o desenvolvimento.

---

## Angular 15 – Mais claro, mais estável e com recursos prontos para usar

Lançado em **16 de novembro de 2022**, o **Angular 15** marcou um momento importante na evolução do framework. Ele reuniu e **aperfeiçoou várias melhorias** das versões anteriores, tornando o desenvolvimento com Angular ainda mais simples e confiável para todo tipo de projeto — especialmente para quem está aprendendo!

### Componentes autônomos com superpoderes

Nas versões anteriores, os **componentes autônomos** surgiram como uma forma de criar componentes **sem depender de módulos** (`NgModule`). Agora, no Angular 15, esse recurso está mais completo:

- Já é possível usar componentes autônomos com **HttpClient**, **Angular Elements**, **roteamento**, entre outros.
- Isso significa menos configuração e mais rapidez ao criar partes da aplicação.

Para quem está começando, esse modelo facilita bastante a organização do código!

### Imagens mais otimizadas com `NgOptimizedImage`

Imagens são essenciais em qualquer site — mas se não forem bem tratadas, podem deixar tudo lento.  
O Angular 15 trouxe o `NgOptimizedImage`, um recurso que ajuda a:

- Carregar imagens de forma **mais eficiente e rápida**.
- Evitar que elas fiquem distorcidas ou demorem para aparecer.
- Melhorar o desempenho geral do aplicativo.

Tudo isso com apenas algumas configurações simples direto no código!

### Composição de diretivas com `Directive Composition API`

Se você já aprendeu sobre **diretivas** (elementos que mudam o comportamento do HTML), o Angular 15 trouxe uma forma de **combinar várias diretivas** em uma só. Isso deixa o código:

- **Mais limpo**
- **Mais reutilizável**
- **Mais fácil de entender**

É uma forma prática de aplicar múltiplos comportamentos sem complicações.

### Mensagens de erro mais explicativas

Sabe quando algo dá errado e aparece uma mensagem difícil de entender no console do navegador?  
O Angular 15 resolveu isso! Agora:

- Os **rastreamentos de erros** estão mais claros e detalhados.
- Fica **mais fácil descobrir o que deu errado** e onde ajustar o código.

---

## Angular 16 – Uma grande evolução no desenvolvimento com Angular

Lançado em **3 de maio de 2023**, o **Angular 16** foi considerado por muitos o **maior avanço desde o início do Angular**! Essa versão trouxe várias melhorias internas e novos recursos que deixaram o desenvolvimento web mais inteligente, rápido e moderno — ótimo para quem está aprendendo ou já usando o framework.

### **Angular Signals** – Reatividade ficou mais clara

Com **Signals**, o Angular trouxe uma nova forma de criar valores que mudam dinamicamente (dados reativos), como listas, contadores ou resultados de buscas. Agora:

- Você pode **controlar melhor quando e como os dados mudam**.
- É fácil enxergar **as dependências** entre esses dados.

Ideal para criar interfaces mais rápidas e organizadas — sem precisar aprender outras bibliotecas reativas separadas.

---

### **Hidratação inteligente** – economia e velocidade

Quando um site é carregado no navegador, o Angular normalmente reconstrói toda a página. Com a **hidratação não destrutiva**, ele passa a:

- **Atualizar apenas o que mudou**, sem recriar tudo.
- Economizar **largura de banda**.
- Tornar o app mais **rápido e estável**.

Isso é essencial para projetos que usam **renderização no servidor**, onde partes da página já vêm prontas do backend.

---

### **Testes simplificados com Jest e Web Test Runner**

Testar o código ficou mais fácil! O Angular 16 passou a suportar ferramentas como:

- **Jest**: roda os testes sem precisar abrir um navegador.
- **Web Test Runner**: permite testar componentes diretamente no terminal.

Essas ferramentas são mais rápidas e mais fáceis de usar do que o antigo **Karma**, tornando os testes menos complicados para quem está começando.

---

### **Tags de fechamento automático** – mais clareza no HTML

Agora, você pode escrever componentes com **tags mais enxutas**, como:

```html
<meu-componente />
```

Antes, era necessário escrever:

```html
<meu-componente></meu-componente>
```

Isso melhora a **legibilidade do código** e deixa tudo mais limpo e simples.

---

### **Componentes MDC** – visuais modernos com Material Design v3

O Angular 16 trouxe novos **componentes visuais baseados no Material Design**, criados em parceria com o Google. Eles seguem as últimas tendências de interface, com:

- Estilo atualizado.
- Melhor acessibilidade.
- Comportamentos mais amigáveis em dispositivos móveis e desktops.

Ideal para criar interfaces bonitas sem esforço!

---

## Angular 17 – A versão mais rápida e moderna até agora

Lançado em **8 de novembro de 2023**, o **Angular 17** é a versão mais recente e traz melhorias incríveis que deixam as aplicações web mais rápidas, inteligentes e fáceis de desenvolver. Mesmo quem está aprendendo agora pode aproveitar esses novos recursos para criar experiências modernas sem complicações.

---

### **Visualizações diferíveis** – carregue apenas o necessário

Você já entrou em um site que demora a carregar porque tenta mostrar tudo de uma vez? Com as **visualizações diferíveis**, o Angular 17 permite que partes do conteúdo só sejam carregadas **quando realmente forem necessárias**, como:

- Componentes que só aparecem após uma interação.
- Seções que estão mais abaixo na página.

Isso deixa a aplicação **mais rápida e eficiente**, principalmente em dispositivos móveis.

---

### **Fluxo de controle integrado** – nova forma de organizar o conteúdo

O Angular 17 trouxe uma **nova sintaxe nos templates HTML**, facilitando a criação de estruturas como:

- Condições (`if/else`)
- Loops (`for`)
- Carregamento de conteúdo sob demanda

Agora tudo fica **mais claro, direto e fácil de escrever**, sem precisar criar várias diretivas complicadas.

---

### **Desempenho turbinado**

Essa versão ficou até **90% mais rápida** em comparação com anteriores! Isso significa que:

- O tempo de carregamento dos sites é menor.
- O navegador processa as ações com mais fluidez.
- O usuário sente tudo mais leve e ágil.

Ótimo para melhorar a experiência, especialmente em aplicações que usam muitas interações.

---

### **API de transições** – animações suaves entre páginas

Mudar de uma tela para outra sem "trancos" é essencial em aplicativos modernos. Com a **API de transições**, você pode:

- Criar **animações entre componentes e páginas**
- Deixar seu app com **visual mais profissional e fluido**
- Manter o controle de **quando e como os elementos aparecem**

Isso ajuda a encantar o usuário e tornar a navegação mais natural.

---

## Angular 18 – Mais leve, inteligente e moderno

Lançado em **22 de maio de 2024**, o **Angular 18** trouxe recursos que tornam as aplicações web ainda mais rápidas, organizadas e fáceis de manter. Mesmo para quem está aprendendo, essa versão oferece melhorias que ajudam a criar experiências modernas com mais eficiência e menos esforço.

### Zoneless (sem Zone.js)

O **Zone.js** era uma tecnologia usada para detectar mudanças no aplicativo e atualizar a tela automaticamente. Agora, o Angular está testando o **modo sem Zone.js** — conhecido como _Zoneless_ — que faz isso de forma mais direta e leve.

Resultado: menos consumo de recursos e mais desempenho.

---

### Views diferíveis e controle de fluxo com `@defer`, `@if` e `@for`

Essas novidades facilitam muito a criação de interfaces dinâmicas. Agora você pode usar comandos simples como:

- `@if` → mostra algo só se uma condição for verdadeira.
- `@for` → repete um item com base em uma lista.
- `@defer` → carrega partes da tela **somente quando necessário** (ótimo para deixar o app mais rápido!).

Isso ajuda a organizar o código e melhora a performance, já que nem tudo precisa ser exibido de uma vez.

---

### Melhorias no SSR (renderização no servidor)

O **SSR** permite que partes do site já cheguem prontas do servidor, acelerando o carregamento. Agora, com **event replay**, o Angular consegue **registrar e repetir interações que aconteceram antes do JavaScript carregar**, como cliques e preenchimento de campos.

Isso garante uma navegação fluida, mesmo quando o carregamento do JavaScript está em segundo plano.

---

### Material 3 estável

O **Material 3**, que é o conjunto mais moderno de componentes visuais criado pelo Google, agora está pronto para ser usado com toda segurança e estabilidade. Com ele, seus projetos ganham:

- Interface mais bonita e acessível.
- Comportamento mais fluido.
- Estilo visual atualizado e consistente com as tendências atuais.

---

## Angular 19 – Carregamento inteligente, reatividade avançada e desenvolvimento mais fluido

Lançado em **19 de novembro de 2024**, o **Angular 19** trouxe melhorias importantes que deixam os aplicativos web mais rápidos, dinâmicos e fáceis de criar. Mesmo quem está iniciando pode aproveitar essas novidades sem dificuldade!

### Carregamento inteligente com **hydration incremental**

Se você já ouviu falar em _SSR_ (Server Side Rendering), é o processo de montar partes do site diretamente no servidor — o que acelera o carregamento inicial. O Angular 19 introduziu o **hydration incremental**, que:

- Carrega apenas os componentes que realmente precisam ser atualizados.
- Evita reconstruir a página inteira.
- Deixa tudo **mais rápido e eficiente**, especialmente em dispositivos móveis.

É como acender as luzes só nos cômodos onde há pessoas — prático e econômico!

---

### Controle de como o conteúdo é exibido com **modo de renderização por rota**

Agora o desenvolvedor pode escolher, **para cada página ou rota**, como ela deve ser carregada:

- No navegador do usuário (client).
- No servidor (server).
- Ou pré-renderizada com antecedência (prerender).

Isso dá muito mais flexibilidade e controle sobre o desempenho do app!

---

### Reatividade conectada com **Linked Signals**

Os **Signals** foram uma grande novidade do Angular 16 — uma forma moderna de lidar com dados que mudam com frequência, como listas ou formulários.

O Angular 19 trouxe os **Linked Signals**, que permitem criar **relações entre diferentes valores reativos**.

Ideal para quando você quer atualizar um dado automaticamente com base em outro.

---

### Interações preservadas com **event replay** (agora padrão)

Antes, em aplicativos com SSR, podia acontecer do usuário clicar em algo antes do JavaScript terminar de carregar — e essa ação se perdia.  
Com o **event replay**, essas interações são **registradas e executadas depois**, sem precisar recarregar ou perder dados.

Isso garante uma experiência mais suave e confiável para o usuário.

---

### Atualizações instantâneas com **Hot Module Replacement (HMR)**

Durante o desenvolvimento, o HMR permite:

- Alterar estilos ou layouts.
- Ver mudanças **na hora**, sem recarregar a página.

É ótimo para quem está ajustando visual ou comportamento do app e quer agilidade na hora de testar.

---

## Angular 20 – Reativo, mais leve e fácil de testar

Lançado em **28 de maio de 2025**, o **Angular 20** veio para **refinar** ainda mais tudo o que já vinha sendo construído nas versões anteriores. A ideia é tornar o desenvolvimento com Angular ainda mais **rápido, acessível e seguro** – ótimo tanto para quem está aprendendo quanto para quem já programa há algum tempo.

---

### **Signals API agora é estável**

Os **Signals** são uma forma moderna de lidar com dados que mudam ao longo do tempo — como cliques, formulários, listas dinâmicas etc.

Com a Signals API agora **estável e aprimorada**, você pode:

- Criar componentes que atualizam automaticamente com base nos dados.
- Controlar melhor o desempenho da sua aplicação.
- Escrever menos código para fazer mais.

Mesmo quem nunca programou com reatividade vai achar essa abordagem mais clara e intuitiva.

---

### **Zoneless em modo de testes (Developer Preview)**

Tradicionalmente, o Angular usava uma ferramenta chamada `Zone.js` para detectar mudanças no aplicativo. O Angular 20 está testando o **Zoneless**, que faz esse trabalho de forma **mais leve e rápida**, sem depender dessa biblioteca.

Isso promete deixar os aplicativos mais eficientes e com menos consumo de recursos — embora ainda esteja em fase de testes.

---

### **Melhorias no motor gráfico (Ivy), renderização no servidor (SSR) e acessibilidade**

O Angular 20 também melhorou:

- **Ivy**: o sistema que transforma o seu código em algo que o navegador entende, agora ainda mais rápido.
- **SSR (Server-Side Rendering)**: exibe páginas prontas vindas do servidor para carregar mais rápido.
- **Acessibilidade**: seus componentes podem ser mais facilmente usados por pessoas com deficiência ou por leitores de tela.

Isso deixa o seu app mais inclusivo e com melhor desempenho.

---

### **CLI mais inteligente + pacotes menores**

A **CLI** (linha de comando) do Angular está mais poderosa e fácil de usar:

- Comandos mais simples.
- Menos dependências desnecessárias.
- Projetos iniciais mais limpos e compactos.

Ótimo para quem está começando e quer um projeto leve desde o início.

---

### **Segurança e testes com Jest, Vitest e Web Test Runner**

Testar o seu app é fundamental — e agora ficou bem mais fácil:

- Suporte direto para ferramentas populares como **Jest**, **Vitest** e **Web Test Runner**.
- Mais velocidade na hora de rodar testes.
- Melhor organização de erros e mensagens.

Assim você consegue identificar problemas logo no início do desenvolvimento, sem dor de cabeça.

---
