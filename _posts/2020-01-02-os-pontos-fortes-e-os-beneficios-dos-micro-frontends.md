---
layout: post
title:  "Os pontos fortes e os benefícios dos micro frontends"
date:   2020-01-02 17:59:38 -0200
categories: jekyll update
---


![](https://bs-uploads.toptal.io/blackfish-uploads/blog/article/content/cover_image_file/cover_image/58147/1003-Micro_Frontends_Dan_Newsletter-61c0a75f6486f4724af75bc0f88f0a89.png)

A arquitetura de micro-front-end é uma abordagem de design na qual um aplicativo front-end é decomposto em "microapps" individuais e semi-independentes, trabalhando livremente juntos. O conceito de micro-frontend é vagamente inspirado por, e nomeado após, microsserviços.

Os benefícios do padrão de micro-front-end incluem:

1. As arquiteturas de micro-interface podem ser mais simples e, portanto, mais fáceis de raciocinar e gerenciar.
2. As equipes de desenvolvimento independentes podem colaborar em um aplicativo front-end com mais facilidade.
3. Eles podem fornecer um meio para migrar de um aplicativo "antigo", com um aplicativo "novo" sendo executado lado a lado com ele.


Embora os micro frontendos tenham recebido muita atenção ultimamente, até o momento não existe uma implementação dominante única e nenhuma estrutura clara de "melhor" micro-frontend. De fato, existe uma variedade de abordagens, dependendo dos objetivos e requisitos. Veja a bibliografia para algumas das implementações mais conhecidas.

Neste artigo, pularemos grande parte da teoria das micro frontends. Aqui está o que não abordaremos:

- "Fatiar" um aplicativo em microapps
- Problemas de implantação, incluindo como as micro frontends se encaixam em um modelo de CI / CD
- Teste
- Se os microapps devem estar alinhados individualmente com os microsserviços no back-end
- Críticas ao conceito de micro-frontend
- A diferença entre micro frontends e uma arquitetura simples de componentes antigos

Em vez disso, apresentaremos um tutorial de micro-front-end com foco em uma implementação concreta, destacando os problemas importantes na arquitetura de micro-front-end e suas possíveis soluções.

Nossa implementação é chamada Yumcha. O significado literal de "yum cha" em cantonês é "beber chá", mas seu significado cotidiano é "sair para o dim sum". A idéia aqui é que os microapps individuais dentro de um macroapp (como chamaremos de composto, app de nível) são análogas às várias cestas de porções de tamanho reduzido trazidas em um almoço com dim sum.

![](https://bs-uploads.toptal.com/blackfish-uploads/uploaded_file/file/57219/image-1570616238950-e2a18963217427699df3de4d2be7bea5.png)

Às vezes, nos referimos ao Yumcha como uma “estrutura de micro-frontend”. No mundo de hoje, o termo “estrutura” é geralmente usado para se referir a Angular, React, Vue.js ou outras superestruturas semelhantes para aplicativos da web. Não estamos falando de [uma estrutura nesse sentido](https://www.toptal.com/javascript/are-big-front-end-frameworks-bad) . Chamamos Yumcha de uma estrutura apenas por uma questão de conveniência: na verdade, é mais um conjunto de ferramentas e algumas camadas finas para a criação de aplicativos baseados em micro frontend.


## Primeiros passos do tutorial de micro-front-end: marcação para um aplicativo composto

Vamos nos aprofundar pensando em como podemos definir um macroapp e os microapps que o compõem. A marcação sempre esteve no coração da web. Nosso macroapp será, portanto, especificado por nada mais complicado do que esta marcação:

```html
<html>
  <head>
    <script src="/yumcha.js"></script>
  </head>
  <body>
    <h1>Hello, micro-frontend app.</h1>

    <!-- HERE ARE THE MICROAPPS! -->
    <yumcha-portal name="microapp1" src="https://microapp1.example.com"></yumcha-portal>
    <yumcha-portal name="microapp2" src="https://microapp2.example.com"></yumcha-portal>

  </body>
</html>

```

Definir nossa macroapp usando a marcação nos dá acesso total ao poder do HTML e CSS para criar e gerenciar nossos microapps. Por exemplo, um microapp pode sentar-se em cima de outro, ou de lado, ou estar no canto da página, ou em um painel de um acordeão, ou permanecer oculto até que algo aconteça, ou permanecer permanentemente em segundo plano .

Nomeamos o elemento personalizado usado para microapps ```<yumcha-portal>``` porque "portal" é um termo promissor para microapps usado na [proposta de portal](https://wicg.github.io/portals/) , uma tentativa inicial de definir um elemento HTML padrão para uso em micro frontends.
  
  
## Implementando o ```<yumcha-portal>``` elemento personalizado
  
Como devemos implementar ```<yumcha-portal>``` ? Desde que é um elemento personalizado, como um componente da web, é claro! Podemos escolher entre vários concorrentes fortes para escrever e compilar componentes da web de micro-front-end; aqui usaremos o [LitElement](https://lit-element.polymer-project.org/) , a mais recente iteração do Polymer Project. O LitElement suporta o açúcar sintático baseado em TypeScript, que lida com a maior parte do padrão do elemento personalizado para nós. Para ```<yumcha-portal>``` disponibilizar a nossa página, precisamos incluir o código relevante como a ```<script>```, como fizemos acima.
  
Mas o que ```<yumcha-portal>``` realmente faz? Uma primeira aproximação seria apenas criar um ```iframe``` com a fonte especificada:  


```jsx

render() {
    return html`<iframe src=${this.src}></iframe>`;
  }
  
```

... onde ```render``` é o padrão LitElement renderizando o hook, usando seu ```html``` tagged template literal. Essa funcionalidade mínima pode ser quase o suficiente para alguns casos de uso triviais.


## Incorporando Microapps em ```iframe```S

```iframe```s são o elemento HTML que todo mundo adora odiar, mas, na verdade, eles fornecem um comportamento extremamente útil e sólido em sandbox. No entanto, ainda há uma longa lista de problemas a serem observados ao usar ```iframe```s, com impacto potencial no comportamento e na funcionalidade do nosso aplicativo:


- Primeiro, ```iframe```s têm peculiaridades bem conhecidas em termos de tamanho e disposição.
- É claro que o CSS **ficará completamente isolado** do ```iframe```, para melhor ou para o pior.
- O botão "voltar" do navegador funcionará razoavelmente bem, embora **o status atual da navegação ```iframe``` não seja refletido no URL da página** , portanto, não podemos recortar e colar URLs para chegar ao mesmo estado do aplicativo composto, nem um link direto para eles.
- A comunicação com o ```iframe``` exterior, dependendo da configuração do CORS, **pode precisar passar pelo ```postMessage``` protocolo** .
- Acordos terão que ser feitos para **authentication across ```iframe``` boundaries**.
- **Alguns leitores de tela podem tropeçar** nos limites do ```iframe```  ou precisar do ```iframe``` ter um título que possam anunciar ao usuário.


Alguns desses problemas podem ser evitados ou atenuados se você não usar ```iframes```, uma alternativa que discutiremos mais adiante neste artigo.

No lado positivo, o ```iframe``` terá seu próprio, independente ```Content-Security-Policy```(CSP). Além disso, se o microapp apontado ```iframe``` usar um  service worker ou implementar a server-side rendering, tudo funcionará conforme o esperado. Também podemos especificar várias opções de sandbox ```iframe``` para limitar seus recursos, como poder navegar para o quadro superior.

Alguns navegadores enviaram ou planejam enviar um ```loading=lazy``` atributo para ```iframes```, que adia o carregamento abaixo da dobra ```iframes``` até o usuário rolar para perto deles, mas isso não fornece o controle refinado do carregamento lento que queremos.

O verdadeiro problema com ```iframes``` é que o conteúdo do iframe requer várias solicitações de rede para recuperar. O nível superior ```index.html``` é recebido, seus scripts são carregados e seu HTML é analisado - mas o navegador deve iniciar outra solicitação para o ```iframe```HTML, aguardar para recebê-lo, analisar e carregar seus scripts e renderizar o iframeconteúdo. Em muitos casos, o ```iframe```JavaScript ainda precisaria girar, fazer suas próprias chamadas de API e mostrar dados significativos somente depois que essas chamadas de API retornassem e os dados fossem processados para visualização.

Isso provavelmente resultará em atrasos indesejáveis e artefatos de renderização, especialmente quando vários microapps estiverem envolvidos. Se o ```iframe``` aplicativo implementar o SSR, isso ajudará, mas ainda não evitará a necessidade de viagens de ida e volta adicionais.

Portanto, um dos principais desafios que enfrentamos ao projetar a implementação do nosso portal é como lidar com esse problema de ida e volta. Nosso objetivo é que uma única solicitação de rede reduza a página inteira com todos os seus microapps, incluindo qualquer conteúdo que cada um deles possa preencher previamente. A solução para esse problema está no servidor Yumcha.

## O servidor Yumcha

Um elemento-chave da solução de micro front-end apresentada aqui é configurar um servidor dedicado para lidar com a composição de micro aplicativos. Esse servidor solicita proxies aos servidores em que cada microapp está hospedado. Concedido, será necessário algum esforço para configurar e gerenciar este servidor. Algumas abordagens de micro front-end (por exemplo,  [single-spa](https://single-spa.js.org/)) tentam dispensar a necessidade de tais configurações especiais de servidor, em nome da facilidade de implantação e configuração.


No entanto, o custo de configurar esse proxy reverso é mais do que compensado pelos benefícios que obtemos; de fato, existem comportamentos importantes de aplicativos baseados em micro frontend que simplesmente não podemos alcançar sem ele. Existem muitas alternativas comerciais e gratuitas para configurar esse proxy reverso.

O proxy reverso, além de rotear solicitações de microapp para o servidor apropriado, também roteia solicitações de macroapp para um servidor de macroapp. Esse servidor processa o HTML do aplicativo composto de uma maneira especial. Ao receber uma solicitação ```index.html``` do navegador por meio do servidor proxy em um URL como ```http://macroapp.example.com```, ele recupera o arquivo ```index.html``` e o submete a uma transformação simples, mas crucial, antes de devolvê-lo.

Especificamente, o HTML é analisado em busca de ```<yumcha-portal>``` tags, o que pode ser feito facilmente com um dos analisadores de HTML competentes disponíveis no ecossistema Node.js. Usando o ```src``` atributo to ```<yumcha-portal>```, o servidor que executa o microapp é contatado e o mesmo ```index.html``` é recuperado - incluindo o conteúdo renderizado no servidor, se houver. O resultado é inserido na resposta HTML como uma tag ```<script>``` ou ```<template>```, para não ser executado pelo navegador.


![](https://bs-uploads.toptal.com/blackfish-uploads/uploaded_file/file/57220/image-1570616261080-16d12b453e2f6670b9f7b36ba48e63de.png)

As vantagens dessa configuração incluem, principalmente, que, na primeira solicitação da ```index.html``` página composta, o servidor pode recuperar as páginas individuais dos servidores microapp individuais em sua totalidade - incluindo o conteúdo renderizado por SSR, se houver - e entregue uma página única e completa ao navegador, incluindo o conteúdo que pode ser usado para preencher os ```iframes``` com viagens de ida e volta do servidor sem mais (usando o ```srcdoc``` atributo subutilizado ). O servidor proxy também garante que todos os detalhes de onde os microapps estão sendo servidos sejam ocultados por olhares indiscretos. Por fim, simplifica os problemas do CORS, pois todos os pedidos de aplicativos estão sendo feitos na mesma origem.


De volta ao cliente, a ```<yumcha-portal>``` tag é instanciada e localiza o conteúdo em que foi colocada no documento de resposta pelo servidor e, no momento apropriado, renderiza ```iframe``` e atribui o conteúdo ao seu ```srcdoc``` atributo. Se não estivermos usando ```iframes``` (veja abaixo), o conteúdo correspondente a essa ```<yumcha-portal>``` tag será inserido no shadowDOM do elemento personalizado, se estiver usando isso, ou diretamente embutido no documento.

Neste ponto, já temos um aplicativo baseado em micro frontend parcialmente funcional.

Esta é apenas a ponta do iceberg em termos de funcionalidade interessante para o servidor Yumcha. Por exemplo, gostaríamos de adicionar recursos para controlar como as respostas de erro HTTP dos servidores de microapp são tratadas ou como lidar com microapps que respondem muito lentamente - não queremos esperar uma eternidade para servir a página se um microapp não for respondendo! Esses e outros tópicos deixaremos para outro post.

A ```index.html``` lógica de transformação de macroapp da Yumcha pode ser facilmente implementada da maneira lambda sem função de servidor ou como middleware para estruturas de servidor como Express ou Koa.

## Controle Microapp baseado em stub

Voltando ao lado do cliente, há outro aspecto de como implementamos microapps importantes para eficiência, carregamento lento e renderização sem trepidação. Nós poderia gerar a iframetag para cada MicroApp, ou com um ```src``` atributo que faz com que outra rede pedido, ou com o ```srcdoc``` atributo preenchida com o conteúdo povoado para nós pelo servidor. Mas, nos dois casos, o código ```iframe``` será iniciado imediatamente, incluindo o carregamento de todas as suas tags de script e link, inicialização e quaisquer chamadas iniciais da API e processamento de dados relacionados - mesmo que o usuário nunca acesse o microapp em questão.

Nossa solução para esse problema é inicialmente representar microapps na página como pequenos stubs inativados, que podem ser ativados. A ativação pode ser direcionada pela região do microapp que está sendo vista, usando a ```IntersectionObserverAPI``` subutilizada , ou mais comumente por pré-notificações enviadas de fora. Obviamente, também podemos especificar que o microapp seja ativado imediatamente.

De qualquer forma, quando e somente quando o microapp é ativado é ```iframe``` realmente processado e seu código carregado e executado. Em termos de nossa implementação usando LitElement, e assumindo que o status de ativação é representado por uma ```activated``` variável de instância, teríamos algo como:


```jsx
render() {
  if (!this.activated) return html`{this.placeholder}`;
  else return html`
    <iframe srcdoc="${this.content}" @load="${this.markLoaded}"></iframe>`;
}

```

## Comunicação inter-microapp

Embora os microapps que compõem um macroapp sejam, por definição, pouco acoplados, eles ainda precisam se comunicar. Por exemplo, um microapp de navegação precisaria enviar uma notificação de que outro microapp recém selecionado pelo usuário deve ser ativado, e o aplicativo a ser ativado precisa receber essas notificações.

De acordo com nossa mentalidade minimalista, queremos evitar a introdução de muitos mecanismos de transmissão de mensagens. Em vez disso, no espírito dos componentes da web, usaremos eventos DOM. Fornecemos uma API de transmissão trivial que pré-notifica todos os stubs de um evento iminente, aguarda por qualquer um que tenha solicitado a ativação para esse tipo de evento ser ativado e, em seguida, despacha o evento no documento, no qual qualquer microapp pode escutar isto. Dado que todos os nossos ```iframes``` são da mesma origem, podemos acessar ```iframe``` a página e vice-versa para encontrar elementos contra os quais disparar eventos.


## Encaminhamento

Hoje em dia, todos esperamos que a barra de URL nos SPAs represente o estado de exibição do aplicativo, para que possamos recortar, colar, enviar e-mail, texto e vincular a ele para ir diretamente para uma página dentro do aplicativo. Em um aplicativo de micro-interface, no entanto, o estado do aplicativo é na verdade uma combinação de estados, um para cada micro-aplicativo. Como devemos representar e controlar isso?

A solução é codificar o estado de cada microapp em um único URL composto e usar um pequeno roteador de macroapp que sabe como montar esse URL composto e separá-lo. Infelizmente, isso requer lógica específica do Yumcha em cada microapp: para receber mensagens do roteador de macroapp e atualizar o estado do microapp e, inversamente, para aconselhar o roteador de macroapp sobre mudanças nesse estado para que a URL composta possa ser atualizada. Por exemplo, pode-se imaginar um ```YumchaLocationStrategy``` para Angular ou um ```<YumchaRouter>``` elemento para React.

![](https://bs-uploads.toptal.com/blackfish-uploads/uploaded_file/file/57221/image-1570616282764-ede50fa138e04e585295cc0c78567d9e.png)

## O caso não-```iframe``` 

Como mencionado acima, hospedar microapps em ```iframes``` tem algumas desvantagens. Existem duas alternativas: inclua-as diretamente embutidas no HTML da página ou coloque-as no DOM da sombra. Ambas as alternativas refletem um pouco os prós e os contras de ```iframes```, mas às vezes de maneiras diferentes.


Por exemplo, políticas individuais de microapp CSP teriam que ser mescladas de alguma forma. Tecnologias de assistência, como leitores de tela, devem funcionar melhor do que com ```iframes```, supondo que suportem o shadowDOM (o que nem todos ainda). Deve ser simples organizar o registro de service workers de um microapp usando o conceito de "escopo", embora o aplicativo precise garantir que seu service worker seja registrado com o nome do aplicativo, não "/". Nenhum dos problemas de layout associados se ```iframe``` aplica aos métodos  inlined  ou shadow DOM.

No entanto, os aplicativos criados usando estruturas como Angular e React provavelmente ficarão infelizes vivendo em linha ou no DOM sombra. Para aqueles, provavelmente vamos querer usar ```iframes``` .


Os métodos DOM inline e shadow diferem quando se trata de CSS. O CSS será encapsulado de forma limpa no sombra DOM. Se, por algum motivo, desejássemos compartilhar CSS externo com o shadowDOM, teríamos que usar  [constructable stylesheets](https://wicg.github.io/construct-stylesheets/) ou algo semelhante. Com microapps embutidos, todo o CSS seria compartilhado por toda a página.

No final, a implementação da lógica para microapps DOM inline e shadow ```<yumcha-portal>``` é simples. Recuperamos o conteúdo para um determinado microapp de onde ele foi inserido na página pela lógica do servidor como um ```<template>``` elemento HTML , clonamos e anexamos ao que LitElement chama renderRoot, que normalmente é o shadowDOM do elemento, mas também pode ser definido como o próprio elemento ( this) para o caso inline (non-shadowDOM).


Mas espere! O conteúdo exibido pelo servidor microapp é uma página HTML inteira. Não podemos inserir a página HTML para o MicroApp, completo com as tags ```html```, ```head``` e ```body``` , no meio para o macroapp, podemos?

Resolvemos esse problema, aproveitando uma peculiaridade da tag ```template```  na qual o conteúdo do microapp recuperado do servidor microapp está quebrado. Acontece que quando os navegadores modernos encontrar uma tag ```template``` , embora eles não “executem”, eles fazem parse, e ao fazê-lo remover conteúdo inválido, como as tags ```<html>```, ```<head>``` e ```<body>```, preservando seu conteúdo interno. Portanto, as tags `` <script>``  e ```<link>``` no ```<head>```, bem como o conteúdo do ```<body>```, são preservadas. É exatamente isso que queremos para inserir conteúdo microapp em nossa página.

## Arquitetura de micro-front-end: o diabo está nos detalhes

As micro frontend criarão raízes no ecossistema de aplicativos da Web se (a) se tornarem uma melhor abordagem arquitetônica; e (b) podemos descobrir como implementá-las de maneiras que atendam aos inúmeros requisitos práticos da web de hoje.

Em termos da primeira pergunta, ninguém afirma que as micro frontends são a arquitetura certa para todos os casos de uso. Em particular, haveria poucas razões para o desenvolvimento greenfield de uma única equipe adotar micro frontends. Deixarei a questão de que tipos de aplicativos em que tipos de contextos poderiam se beneficiar mais de um padrão de micro-frontend para outros comentaristas.

Em termos de implementação e viabilidade, vimos vários detalhes com os quais se preocupar, incluindo vários nem mencionados neste artigo - principalmente autenticação e segurança, duplicação de código e SEO. No entanto, espero que este artigo estabeleça uma abordagem básica de implementação para micro frontends que, com mais refinamento, possa atender aos requisitos do mundo real.



## Bibliografia

- [Micro Front Ends — Doing It Angular Style — Part 1](https://medium.com/outbrain-engineering/micro-front-ends-doing-it-angular-style-part-1-219c842fd02e)
- [Micro Front Ends — Doing It Angular Style — Part 2](https://medium.com/outbrain-engineering/micro-front-ends-doing-it-angular-style-part-2-1393ced4ceab)
- [Evolving an AngularJS application using microfrontends](https://engineering.contaazul.com/evolving-an-angularjs-application-using-microfrontends-2bbcac9c023a)
- [Micro-Frontends](https://medium.com/@PepsRyuu/micro-frontends-341defa8d1d4)
- [UI microservices — reversing the anti-pattern (micro frontends)](https://medium.com/@kitson.mac/ui-microservices-reversing-the-anti-pattern-375bc22287b0)
- [UI microservices — an anti-pattern?](https://medium.com/@kitson.mac/ui-micro-services-40798d2e3ef4)
- [Page Building using Micro-Frontends](https://medium.com/js-dojo/page-building-using-micro-frontends-c13c157958c8) takes a Yumcha-like approach of reverse proxy and SSIs, which I highly recommend.
- [Micro-frontends resources](https://medium.com/@lucamezzalira/micro-frontends-resources-53b1ec7d512a)
- [Podium](https://podium-lib.io/)
- [I Don’t Understand Micro-Frontends](https://medium.com/@lucamezzalira/i-dont-understand-micro-frontends-88f7304799a9). This is a pretty good overview of types of micro-frontend architectures and use cases.
- [Serverless Micro-frontends using Vue.js, AWS Lambda, and Hypernova](https://medium.com/js-dojo/serverless-micro-frontends-using-vue-js-aws-lambda-and-hypernova-835d6f2b3bc9)
- [Micro Frontends](https://martinfowler.com/articles/micro-frontends.html): A great, comprehensive overview.
  
  

## COMPREENDENDO O BÁSICO

### O que são micro frontends?

As micro frontends são um novo padrão no qual as UIs de aplicativos da Web (front ends) são compostas de fragmentos semi-independentes que podem ser construídos por diferentes equipes, usando diferentes tecnologias. As arquiteturas de micro front-end se parecem com arquiteturas de back-end, nas quais os back-ends são compostos a partir de microsserviços semi-independentes.

### O que é arquitetura de micro-interface?

Uma arquitetura de micro-front-end estabelece a abordagem para os elementos estruturais de uma estrutura de micro-front-end. Ele também define os relacionamentos entre eles, governando como os fragmentos da interface do usuário são montados e se comunicam, a fim de alcançar a experiência ideal do desenvolvedor e do usuário.

### Os microsserviços podem ter interfaces de usuário?

Sim, de certa forma eles podem. Os padrões de micro frontend geralmente adotam a abordagem em que um fragmento do micro frontend, talvez implementado como um componente da web de micro frontend, é emparelhado com um microsserviço para fornecer sua interface do usuário.


### O que define um microsserviço?

Um microsserviço é um elemento de uma arquitetura na qual os aplicativos são estruturados como uma coleção de serviços interoperantes. Se o front-end adotar o padrão de micro front-end, um microsserviço poderá ser emparelhado com um micro front-end.

### Qual é a relação entre micro frontends e componentes da web?

Micro frontends e componentes da web (elementos personalizados) podem estar relacionados de várias maneiras. Os componentes da Web são uma maneira natural baseada em marcação para descrever os microapps que compõem um aplicativo de micro-front-end. E os microapps individuais em um aplicativo de micro frontend podem ser construídos usando componentes da web.


---

Autor: [Bob Myers](https://www.linkedin.com/in/bobmyers/)

[Artigo Original](https://www.toptal.com/front-end/micro-frontends-strengths-benefits)

