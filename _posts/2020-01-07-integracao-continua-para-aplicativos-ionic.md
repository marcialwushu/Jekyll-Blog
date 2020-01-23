---
layout: post
title:  "Integração Contínua para Aplicativos Ionic"
date:   2020-01-07 17:59:38 -0200
categories: jekyll update
---

![](https://d2mn9dr0jv4622.cloudfront.net/wp-content/uploads/2017/12/06165310/continuous-integration-for-ionic-apps1.png)


### Ionic Framework

>O [Ionic](http://ionicframework.com/) é um SDK de código aberto completo para o desenvolvimento de aplicativos móveis híbridos. Construído sobre AngularJS e Apache Cordova, o Ionic fornece ferramentas e serviços para o desenvolvimento de aplicativos móveis híbridos usando tecnologias da Web como CSS, HTML5 e Sass. Os aplicativos podem ser criados com essas tecnologias da Web e depois distribuídos por lojas de aplicativos nativas para serem instaladas nos dispositivos usando o Cordova. - [Fonte](https://en.wikipedia.org/wiki/Ionic_(mobile_app_framework))

Neste post, mostraremos como configurar a integração contínua para compilações Ionic em apenas alguns cliques usando o Nevercode .

**Vamos começar!**

## Primeiros passos

Primeiro, crie uma conta gratuita no Nevercode. Tudo o que você precisa para começar é um navegador da Web e nenhum software adicional. O Nevercode detecta e configura seus projetos Ionic automaticamente.

Na primeira vez que você fizer login no Nevercode, você verá um painel vazio.

![](https://d2mn9dr0jv4622.cloudfront.net/wp-content/uploads/2017/12/13140346/empty_dashboard1.png)

Comece clicando em " **adicionar novo aplicativo** ".

Digite o URL do seu repositório Git e selecione um tipo de autenticação. Se você se inscrever via **Bitbucket** ou **Github** usando OAuth, poderá simplesmente selecionar o repositório via UI.

### Caso contrário, você tem três opções para autenticação:

- repositório público
- usuário e senha
- Chave SSH

## Selecione Configuração

Na próxima etapa, você precisa selecionar a ramificação no menu suspenso. (Observe que você pode alterar a ramificação posteriormente.) O Nevercode clonará o repositório, procurará projetos a partir dele e procurará as configurações. Todas essas ações podem ser monitoradas ao mesmo tempo a partir do seu navegador, através da janela de registro ao vivo, como mostrado abaixo.

![](https://d2mn9dr0jv4622.cloudfront.net/wp-content/uploads/2017/12/13140336/ionic_configuration.png)

>Selecionando configuração

Quando a verificação for concluída, você verá três opções:

- **Projeto** : diretório em que seu arquivo de configuração Ionic está ```config.xml``` armazenado
- **Configurações** : escolha se deseja criar a versão de depuração ou lançamento do seu aplicativo
- **Construir para plataformas** : escolha se você deseja criar seu aplicativo apenas para Android ou iOS ou para ambas as plataformas.

Agora clique em ' **Salvar e iniciar a compilação** ', o
Nevercode executará automaticamente a primeira compilação do seu projeto Ionic. **Feito!**

## Configurações avançadas

As configurações avançadas do Nevercode permitem ajustar a construção do seu aplicativo Ionic.

### Gerenciamento de Dependências

Geralmente, os aplicativos iônicos dependem de módulos de nó adicionais. O Nevercode instala automaticamente as dependências listadas no ```package.json``` arquivo do seu projeto npm installimediatamente após a clonagem do seu repositório para construção.

### Cache de Dependência

O cache de dependência permite acelerar as compilações armazenando as dependências do projeto. Se ativado, o pacote com dependências em cache será configurado antes de cada compilação.

### Assinatura de código

Por padrão, a assinatura de código é desativada para que você possa testar o Nevercode sem problemas com perfis de aprovisionamento e certificados de assinatura. Mas quando chega a hora de implantar aplicativos ou instalar em dispositivos reais de teste, recebemos orientações simples sobre como assinar [binários Android](https://developer.nevercode.io/docs/signing-android-binaries-in-cordova) e [iOS](https://developer.nevercode.io/docs/code-signing).

## Testando Aplicações Ionic

![](https://d2mn9dr0jv4622.cloudfront.net/wp-content/uploads/2017/12/06084150/testing-ionic-applications.png)

Aplicativos ionic podem ser testados através de etapas de teste personalizadas. Usando scripts personalizados, você pode configurar e executar qualquer estrutura de teste de sua escolha como parte das construções do seu projeto. Desde que os resultados do teste sejam relatados no formato **xUnit XML** e direcionados para a pasta especificada por nossa variável de ambiente, o Nevercode os analisará, levará em consideração ao definir o status da sua compilação e exibirá na guia testes da visualização de compilação .

Infelizmente, o ecossistema híbrido não possui padrões bem definidos de como os testes são gravados, onde são colocados na estrutura do projeto, qual estrutura de teste eles usam ou como são executados. Dadas essas infinitas possibilidades, qualquer tentativa de automação completa provavelmente acabaria curta e deixaria muitos usuários frustrados. Felizmente, configurar testes personalizados com o Nevercode é bastante fácil.


### Configurando testes personalizados

A primeira etapa da configuração é garantir que todas as suas dependências de teste estejam disponíveis na caixa de proteção de compilação. Estamos incluindo Jasmine, Karma-CLI, Transferidor, Chrome e Firefox prontos para uso.


- A maneira mais natural de instalar outros componentes de teste é através de um [script post-clone personalizado](https://developer.nevercode.io/docs/custom-build-steps) , que você já pode estar usando para instalar as outras dependências do cross-platform app’s.
- Em seguida, configure o executor de teste de sua escolha para gerar seus resultados no **formato xUnit** no local especificado pela ```$NEVERCODE_XUNIT_RESULTS_DIR``` variável de ambiente.
- Por fim, inclua um [post-build script](https://developer.nevercode.io/docs/custom-build-steps) com os comandos necessários para executar seus testes automaticamente.

Com essas etapas simples, seus testes personalizados serão executados durante a próxima compilação bem-sucedida. O Nevercode mostrará os resultados dos **testes na guia Testes** da tela de informações da compilação e os levará em consideração ao determinar o status final da compilação. Para uma explicação detalhada sobre o teste de aplicativos híbridos, consulte nosso [guia](https://developer.nevercode.io/docs/testing-hybrid-applications) dedicado .

![](https://d2mn9dr0jv4622.cloudfront.net/wp-content/uploads/2017/12/13140340/ionic_tests.png)

>Resultados de teste de aplicações iônicas

## Distribuição de Compilação

A distribuição de compilação é parte integrante do ciclo de vida do desenvolvimento de aplicativos. O Nevercode suporta a publicação de seus artefatos de construção em vários canais de distribuição, como:

- Google Play, iTunes Connect
- HockeyApp, Crashlytics, TestFairy, Relution
- Slack, HipChat, E-mail

Vamos dar uma olhada no exemplo de publicação no [Google Play](https://developer.nevercode.io/docs/google-play) . Primeiro, navegue até as configurações do projeto e selecione Publicação, depois Google Play na lista exibida. A única coisa que você precisa fazer agora para publicar automaticamente no Google Play é fornecer suas credenciais como um arquivo JSON, selecionar uma faixa e salvar.

**É isso aí!**


![](https://d2mn9dr0jv4622.cloudfront.net/wp-content/uploads/2017/12/13142604/publishing.png)

**Nota**: para automatizar totalmente seu processo de integração contínua, você pode configurar diferentes fluxos de trabalho para cada ramo, descrevendo como o seu projeto deve ser construído, testado e publicado.

## Conclusão

O Ionic é uma ótima opção para o desenvolvimento de aplicativos móveis - há muitas boas razões para usá-lo em seu próximo projeto, como:

- Cross-Platform (Web, iOS, Android)
- Uma base de código
- Tecnologias da Web (HTML, CSS, JS)
- Código aberto e gratuito
- Disponibilidade de plugins (por exemplo, plugins Cordova)
- Ótimos componentes de interface do usuário padrão

Combinando o Ionic com integração e entrega contínuas, é onde realmente começa a brilhar e fornecer grande valor comercial e maior produtividade. A beleza do Nevercode é que é muito simples de configurar e não requer uma força especial de engenheiros do DevOps, como Jenkins.

---

[NEVERCODE.IO](https://nevercode.io/blog/continuous-integration-for-ionic-apps/)

