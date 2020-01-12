---
layout: post
title:  "Micro Frontends"
date:   2020-01-01 17:59:38 -0200
categories: jekyll update
---


*Bom desenvolvimento de front-end é difícil. Escalar o desenvolvimento de front-end para que muitas equipes possam trabalhar simultaneamente em um produto grande e complexo é ainda mais difícil. Neste artigo, descreveremos uma tendência recente de dividir monólitos de front-end em muitas partes menores e mais gerenciáveis, e como essa arquitetura pode aumentar a eficácia e a eficiência das equipes que trabalham no código de front-end. Além de falar sobre os vários benefícios e custos, abordaremos algumas das opções de implementação disponíveis e mergulharemos em um aplicativo de exemplo completo que demonstra a técnica*.

## CONTEÚDO ##

* [Benefícios](#beneficios)
    * [Atualizações incrementais](#atualizações-incrementais)
    * [Bases de código simples e dissociadas](#bases-de-código-simples-e-dissociadas)
    * [Implantação independente](#implantação-independente)
    * [Equipes autônomas](#equipes-autônomas)
    * [Em poucas palavras](#em-poucas-palavras)
* [O exemplo](#o-exemplo)
* [Abordagens de integração](#abordagens-de-integração)
    * [Composição do modelo do lado do servidor]()
    * [Integração em tempo de compilação]()
    * [Integração em tempo de execução via iframes]()
    * [Integração em tempo de execução via JavaScript]()
    * [Integração em tempo de execução via Web Components]()
* [Styling]()
* [Bibliotecas de componentes compartilhados]()
* [Comunicação entre aplicativos]()
* [Comunicação de back-end]()
* [Teste]()
* [O exemplo em detalhes]()
    * [O recipiente]()
    * [As micro frontends]()
    * [Comunicação entre aplicativos via roteamento]()
    * [Conteúdo comum]()
    * [A infraestrutura]()
* [Desvantagens]()
    * [Tamanho da carga útil]()
    * [Diferenças de ambiente]()
    * [Complexidade operacional e de governança]()
* [Conclusão]()



Nos últimos anos, os [microsserviços](https://martinfowler.com/articles/microservices.html) explodiram em popularidade, com muitas organizações usando esse estilo arquitetural para evitar as limitações de backends grandes e monolíticos. Embora tenha sido escrito muito sobre esse estilo de criação de software do lado do servidor, muitas empresas continuam lutando com bases de código de front-end monolíticas.

Talvez você queira criar um aplicativo da Web progressivo ou responsivo, mas não consegue encontrar um lugar fácil para começar a integrar esses recursos ao código existente. Talvez você queira começar a usar novos recursos da linguagem JavaScript (ou uma das inúmeras linguagens que podem ser compiladas para JavaScript), mas não pode ajustar as ferramentas de compilação necessárias no processo de compilação existente. Ou talvez você queira apenas escalar seu desenvolvimento para que várias equipes possam trabalhar em um único produto simultaneamente, mas o acoplamento e a complexidade no monólito existente significam que todos estão pisando nos dedos uns dos outros. Todos esses são problemas reais que podem afetar negativamente sua capacidade de fornecer com eficiência experiências de alta qualidade aos seus clientes.

>"Um estilo arquitetônico em que aplicativos frontend entregues independentemente são compostos em um todo maior"

Na edição de novembro de 2016 do radar da tecnologia ThoughtWorks, listamos os [micro frontends](https://www.thoughtworks.com/radar/techniques/micro-frontends) como uma técnica que as organizações deveriam avaliar. Posteriormente, promovemos a versão de avaliação e, finalmente, a Adopt, o que significa que a vemos como uma abordagem comprovada que você deve usar quando fizer sentido.

![](https://martinfowler.com/articles/micro-frontends/radar.png)

>Figura 1: Micro frontends apareceram no radar técnico várias vezes.

Alguns dos principais benefícios que vimos de micro frontends são:

- bases de código menores, mais coesas e sustentáveis
- organizações mais escaláveis com equipes autônomas e dissociadas
- a capacidade de atualizar, atualizar ou mesmo reescrever partes do front-end de maneira mais incremental do que era possível anteriormente

Não é por acaso que essas vantagens de destaque são algumas das mesmas que os microsserviços podem oferecer.

Obviamente, não há almoços grátis quando se trata de arquitetura de software - tudo tem um custo. Algumas implementações de micro frontend podem levar à duplicação de dependências, aumentando o número de bytes que nossos usuários devem baixar. Além disso, o aumento dramático na autonomia da equipe pode causar fragmentação na maneira como suas equipes trabalham. No entanto, acreditamos que esses riscos podem ser gerenciados e que os benefícios dos micro frontends geralmente superam os custos.

## Beneficios ##

Em vez de definir micro frontends em termos de abordagens técnicas específicas ou detalhes de implementação, colocamos ênfase nos atributos que surgem e nos benefícios que eles oferecem.

## Atualizações incrementais ## 

Para muitas organizações, este é o começo de sua jornada de micro frontends. O velho e grande monólito de front-end está sendo retido pela pilha de tecnologia do passado, ou pelo código escrito sob pressão de entrega, e está chegando ao ponto em que uma reescrita total é tentadora. Para evitar os [riscos](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/) de uma reescrita completa, preferimos [estrangular](https://martinfowler.com/bliki/StranglerApplication.html) o aplicativo antigo, peça por peça, e, enquanto isso, continuamos a oferecer novos recursos aos nossos clientes sem ser sobrecarregados pelo monólito.

Isso geralmente leva a uma arquitetura de micro frontends. Uma vez que uma equipe teve a experiência de obter um recurso até a produção, com poucas modificações no velho mundo, outras equipes também vão querer se juntar ao novo mundo. O código existente ainda precisa ser mantido e, em alguns casos, pode fazer sentido continuar adicionando novos recursos, mas agora a opção está disponível.

O fim do jogo aqui é que temos mais liberdade para tomar decisões caso a caso em partes individuais de nosso produto e fazer atualizações incrementais em nossa arquitetura, nossas dependências e nossa experiência do usuário. Se houver uma mudança significativa em nossa estrutura principal, cada micro front-end poderá ser atualizado sempre que fizer sentido, em vez de ser forçado a parar o mundo e atualizar tudo de uma vez. Se quisermos experimentar novas tecnologias ou novos modos de interação, podemos fazê-lo de maneira mais isolada do que antes.

## Bases de código simples e dissociadas ##

O código fonte de cada micro front-end individual será, por definição, muito menor que o código-fonte de um único front-end monolítico. Essas bases de código menores tendem a ser mais simples e fáceis para os desenvolvedores trabalharem. Em particular, evitamos a complexidade decorrente do acoplamento não intencional e inadequado entre componentes que não devem se conhecer. Ao desenhar linhas mais grossas em torno dos [contextos limitados](https://martinfowler.com/bliki/BoundedContext.html) do aplicativo, dificultamos o surgimento de um acoplamento acidental.

Obviamente, uma única decisão arquitetônica de alto nível (por exemplo, "vamos fazer micro frontends") não substitui um bom código limpo antiquado. Não estamos tentando nos isentar de pensar em nosso código e de colocar esforço em sua qualidade. Em vez disso, estamos tentando nos preparar para cair no [poço do sucesso](https://blog.codinghorror.com/falling-into-the-pit-of-success/) , tomando decisões ruins com dificuldade e boas decisões com facilidade. Por exemplo, o compartilhamento de modelos de domínio em contextos limitados se torna mais difícil, portanto é menos provável que os desenvolvedores o façam. Da mesma forma, as micro frontends incentivam você a ser explícito e deliberado sobre como os dados e eventos fluem entre diferentes partes do aplicativo, o que é algo que deveríamos estar fazendo de qualquer maneira!

## Implantação independente ##

Assim como nos microsserviços, a implantação independente de micro frontends é essencial. Isso reduz o escopo de qualquer implantação, o que reduz o risco associado. Independentemente de como ou onde seu código de front-end esteja hospedado, cada micro front-end deve ter seu próprio pipeline de entrega contínua, que cria, testa e implementa todo o caminho até a produção. Deveríamos ser capazes de implantar cada micro front-end com muito pouca atenção ao estado atual de outras bases de código ou pipelines. Não importa se o monólito antigo está em um ciclo fixo, manual e trimestral de liberação, ou se a equipe ao lado colocou um recurso incompleto ou incompleto em seu ramo mestre. Se um determinado micro front-end estiver pronto para a produção, ele poderá fazê-lo,

![](https://martinfowler.com/articles/micro-frontends/deployment.png)

>Figura 2: Cada micro front-end é implantado na produção independentemente

## Equipes autônomas ##

Como um benefício de ordem superior da dissociação de nossas bases de código e de nossos ciclos de lançamento, percorremos um longo caminho no sentido de termos equipes totalmente independentes, que podem possuir uma seção de um produto desde a concepção até a produção e além. As equipes podem ter a propriedade total de tudo o que precisam para agregar valor aos clientes, o que lhes permite agir de forma rápida e eficaz. Para que isso funcione, nossas equipes precisam ser formadas em torno de partes verticais da funcionalidade do negócio, e não em torno de recursos técnicos. Uma maneira fácil de fazer isso é criar o produto com base no que os usuários finais verão, para que cada micro front-end encapsule uma única página do aplicativo e pertença de ponta a ponta por uma única equipe. Isso traz maior coesão das equipes

![](https://martinfowler.com/articles/micro-frontends/horizontal.png)

>Figura 3: Cada aplicativo deve pertencer a uma única equipe

## Em poucas palavras

Em resumo, as micro frontends são divididas em coisas grandes e assustadoras em pedaços menores e mais gerenciáveis, e depois explicitadas sobre as dependências entre elas. Nossas escolhas de tecnologia, nossas bases de código, nossas equipes e nossos processos de lançamento devem poder operar e evoluir independentemente um do outro, sem coordenação excessiva.

---

## O exemplo ## 

Imagine um site em que os clientes possam pedir comida para entrega. Na superfície, é um conceito bastante simples, mas há uma quantidade surpreendente de detalhes, se você quiser fazê-lo bem:

- Deve haver uma página de destino em que os clientes possam navegar e pesquisar restaurantes. Os restaurantes devem ser pesquisáveis e filtráveis por qualquer número de atributos, incluindo preço, culinária ou o que um cliente solicitou anteriormente
- Cada restaurante precisa de sua própria página, que mostra seus itens de menu e permite que o cliente escolha o que deseja comer, com descontos, ofertas de refeições e solicitações especiais
- Os clientes devem ter uma página de perfil onde possam ver seu histórico de pedidos, acompanhar a entrega e personalizar suas opções de pagamento

![](https://martinfowler.com/articles/micro-frontends/wireframe.png)

>Figura 4: Um site de entrega de alimentos pode ter várias páginas razoavelmente complexas

Há complexidade suficiente em cada página que justificamos facilmente uma equipe dedicada para cada uma delas, e cada uma dessas equipes deve poder trabalhar em sua página independentemente de todas as outras equipes. Eles devem ser capazes de desenvolver, testar, implantar e manter seu código sem se preocupar com conflitos ou coordenação com outras equipes. Nossos clientes, no entanto, ainda devem ver um site único e integrado.

No restante deste artigo, usaremos esse aplicativo de exemplo sempre que precisarmos de códigos ou cenários de exemplo.

---


## Abordagens de integração ##

Dada a definição bastante flexível acima, existem muitas abordagens que poderiam razoavelmente ser chamadas de micro frontends. Nesta seção, mostraremos alguns exemplos e discutiremos suas vantagens e desvantagens. Existe uma arquitetura bastante natural que surge em todas as abordagens - geralmente há um micro front-end para cada página no aplicativo e existe um único **aplicativo de contêiner**, que:

- renderiza elementos comuns da página, como cabeçalhos e rodapés
- aborda preocupações transversais como autenticação e navegação
- reúne os vários micro frontends na página e informa a cada micro front quando e onde se renderizar

![](https://martinfowler.com/articles/micro-frontends/composition.png)

>Figura 5: Geralmente, você pode derivar sua arquitetura da estrutura visual da página

## Composição do modelo do lado do servidor ##

Começamos com uma abordagem decididamente não inovadora para o desenvolvimento de front-end - renderizando HTML no servidor a partir de vários modelos ou fragmentos. Temos um index.htmlque contém todos os elementos comuns da página e, em seguida, usa inclusões do servidor para conectar conteúdo específico da página a partir de arquivos HTML fragmentados:

```html
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>Feed me</title>
  </head>
  <body>
    <h1>🍽 Feed me</h1>
    <!--# include file="$PAGE.html" -->
  </body>
</html>

```

Servimos esse arquivo usando o Nginx, configurando a $PAGE variável correspondendo ao URL que está sendo solicitado:

```js

server {
    listen 8080;
    server_name localhost;

    root /usr/share/nginx/html;
    index index.html;
    ssi on;

    # Redirect / to /browse
    rewrite ^/$ http://localhost:8080/browse redirect;

    # Decide which HTML fragment to insert based on the URL
    location /browse {
      set $PAGE 'browse';
    }
    location /order {
      set $PAGE 'order';
    }
    location /profile {
      set $PAGE 'profile'
    }

    # All locations should render through index.html
    error_page 404 /index.html;
}

```

Essa é uma composição bastante padrão do lado do servidor. A razão pela qual podemos justificadamente chamar essas micro frontends é que dividimos nosso código de forma que cada peça represente um conceito de domínio independente que possa ser entregue por uma equipe independente. O que não é mostrado aqui é como esses vários arquivos HTML acabam no servidor da Web, mas a suposição é que cada um deles possui seu próprio pipeline de implantação, o que nos permite implantar alterações em uma página sem afetar ou pensar em outra página.

Para uma independência ainda maior, pode haver um servidor separado responsável por renderizar e atender a cada micro front-end, com um servidor na frente que faz solicitações aos outros. Com o cache cuidadoso das respostas, isso pode ser feito sem afetar a latência.

![](https://martinfowler.com/articles/micro-frontends/ssi.png)

>Figura 6: Cada um desses servidores pode ser construído e implantado de forma independente

Este exemplo mostra como as micro frontends não são necessariamente uma nova técnica e não precisam ser complicadas. Desde que tenhamos cuidado com o modo como nossas decisões de design afetam a autonomia de nossas bases de código e nossas equipes, podemos obter muitos dos mesmos benefícios, independentemente da nossa pilha de tecnologias.

## Integração em tempo de compilação ##

Uma abordagem que vemos às vezes é publicar cada micro frontend como um pacote e fazer com que o aplicativo de contêiner inclua todos eles como dependências da biblioteca. Veja como o contêiner package.jsonpode procurar nosso aplicativo de exemplo:


```json
{
  "name": "@feed-me/container",
  "version": "1.0.0",
  "description": "A food delivery web app",
  "dependencies": {
    "@feed-me/browse-restaurants": "^1.2.3",
    "@feed-me/order-food": "^4.5.6",
    "@feed-me/user-profile": "^7.8.9"
  }
}

```

A princípio, isso parece fazer sentido. Ele produz um único pacote Javascript implementável, como é habitual, permitindo a duplicação de dependências comuns de nossos vários aplicativos. No entanto, essa abordagem significa que precisamos recompilar e liberar cada micro front-end para liberar uma alteração em qualquer parte individual do produto. Assim como nos microsserviços, já vimos dores suficientes causadas por um processo de liberação tão lento que recomendamos fortemente contra esse tipo de abordagem para micro frontends.

Depois de todo o trabalho de dividir nosso aplicativo em bases de código discretas que podem ser desenvolvidas e testadas independentemente, não vamos reintroduzir todo esse acoplamento no estágio de lançamento. Deveríamos encontrar uma maneira de integrar nossos micro frontends em tempo de execução, em vez de em tempo de construção.

## Integração em tempo de execução via iframes ##

Uma das abordagens mais simples para compor aplicativos juntos no navegador é o humilde iframe. Por sua natureza, os iframes facilitam a criação de uma página a partir de subpáginas independentes. Eles também oferecem um bom grau de isolamento em termos de estilo e variáveis globais que não interferem entre si.

```html
<html>
  <head>
    <title>Feed me!</title>
  </head>
  <body>
    <h1>Welcome to Feed me!</h1>

    <iframe id="micro-frontend-container"></iframe>

    <script type="text/javascript">
      const microFrontendsByRoute = {
        '/': 'https://browse.example.com/index.html',
        '/order-food': 'https://order.example.com/index.html',
        '/user-profile': 'https://profile.example.com/index.html',
      };

      const iframe = document.getElementById('micro-frontend-container');
      iframe.src = microFrontendsByRoute[window.location.pathname];
    </script>
  </body>
</html>

```

Assim como na [opção](https://martinfowler.com/articles/micro-frontends.html#Server-sideTemplateComposition) de inclusão do [servidor](https://martinfowler.com/articles/micro-frontends.html#Server-sideTemplateComposition) , criar uma página com iframes não é uma técnica nova e talvez não pareça tão excitante. Porém, se revisitarmos os principais benefícios das micro-interfaces [listadas anteriormente](https://martinfowler.com/articles/micro-frontends.html#Benefits) , os iframes serão os principais, desde que tenhamos cuidado com o modo como dividimos o aplicativo e estruturamos nossas equipes.

Muitas vezes vemos muita relutância em escolher iframes. Embora parte dessa relutância pareça ser motivada por um pressentimento de que os iframes são um pouco "eca", há algumas boas razões para que as pessoas os evitem. O fácil isolamento mencionado acima tende a torná-los menos flexíveis do que outras opções. Pode ser difícil criar integrações entre diferentes partes do aplicativo, para tornar o roteamento, o histórico e os links diretos mais complicados, além de apresentar alguns desafios extras para tornar sua página totalmente responsiva.


## Integração em tempo de execução via JavaScript ## 

A próxima abordagem que descreveremos é provavelmente a mais flexível e a que vemos equipes adotando com mais frequência. Cada micro frontend é incluído na página usando uma <script>tag e, ao carregar, expõe uma função global como seu ponto de entrada. O aplicativo de contêiner determina então qual micro front-end deve ser montado e chama a função relevante para informar a um micro front-end quando e onde se renderizar.
   

```html

<html>
  <head>
    <title>Feed me!</title>
  </head>
  <body>
    <h1>Welcome to Feed me!</h1>

    <!-- These scripts don't render anything immediately -->
    <!-- Instead they attach entry-point functions to `window` -->
    <script src="https://browse.example.com/bundle.js"></script>
    <script src="https://order.example.com/bundle.js"></script>
    <script src="https://profile.example.com/bundle.js"></script>

    <div id="micro-frontend-root"></div>

    <script type="text/javascript">
      // These global functions are attached to window by the above scripts
      const microFrontendsByRoute = {
        '/': window.renderBrowseRestaurants,
        '/order-food': window.renderOrderFood,
        '/user-profile': window.renderUserProfile,
      };
      const renderFunction = microFrontendsByRoute[window.location.pathname];

      // Having determined the entry-point function, we now call it,
      // giving it the ID of the element where it should render itself
      renderFunction('micro-frontend-root');
    </script>
  </body>
</html>
```

O exposto acima é obviamente um exemplo primitivo, mas demonstra a técnica básica. Diferentemente da integração em tempo de compilação, podemos implantar cada um dos bundle.jsarquivos independentemente. E, diferentemente dos iframes, temos total flexibilidade para criar integrações entre nossos micro frontends da maneira que quisermos. Poderíamos estender o código acima de várias maneiras, por exemplo, para baixar apenas cada pacote JavaScript, conforme necessário, ou para transmitir e receber dados ao renderizar um micro front-end.

A flexibilidade dessa abordagem, combinada com a capacidade de implementação independente, a torna a escolha padrão e a que vimos na natureza com mais frequência. Vamos explorá-lo com mais detalhes quando entrarmos no [exemplo completo](https://martinfowler.com/articles/micro-frontends.html#TheExampleInDetail).

## Integração em tempo de execução via Web Components ## 

Uma variação da abordagem anterior é que cada micro frontend defina um elemento customizado em HTML para o contêiner instanciar, em vez de definir uma função global para o contêiner chamar.


```html

<html>
  <head>
    <title>Feed me!</title>
  </head>
  <body>
    <h1>Welcome to Feed me!</h1>

    <!-- These scripts don't render anything immediately -->
    <!-- Instead they each define a custom element type -->
    <script src="https://browse.example.com/bundle.js"></script>
    <script src="https://order.example.com/bundle.js"></script>
    <script src="https://profile.example.com/bundle.js"></script>

    <div id="micro-frontend-root"></div>

    <script type="text/javascript">
      // These element types are defined by the above scripts
      const webComponentsByRoute = {
        '/': 'micro-frontend-browse-restaurants',
        '/order-food': 'micro-frontend-order-food',
        '/user-profile': 'micro-frontend-user-profile',
      };
      const webComponentType = webComponentsByRoute[window.location.pathname];

      // Having determined the right web component custom element type,
      // we now create an instance of it and attach it to the document
      const root = document.getElementById('micro-frontend-root');
      const webComponent = document.createElement(webComponentType);
      root.appendChild(webComponent);
    </script>
  </body>
</html>

```

O resultado final aqui é bastante semelhante ao exemplo anterior, a principal diferença é que você está optando por fazer as coisas 'da maneira dos componentes da web'. Se você gosta da especificação do componente da web e gosta da ideia de usar os recursos que o navegador fornece, essa é uma boa opção. Se você preferir definir sua própria interface entre o aplicativo de contêiner e os micro frontends, poderá preferir o exemplo anterior.

---

## Styling ## 

O CSS como linguagem é inerentemente global, herdador e em cascata, tradicionalmente sem sistema de módulos, espaço para nome ou encapsulamento. Alguns desses recursos existem agora, mas muitas vezes falta suporte ao navegador. Em um cenário de micro frontends, muitos desses problemas são exacerbados. Por exemplo, se o micro front-end de uma equipe tem uma folha de estilo que diz h2 { color: black; }, e outra diz h2 { color: blue; }, e ambos os seletores estão anexados à mesma página, alguém ficará desapontado! Esse não é um problema novo, mas é agravado pelo fato de que esses seletores foram escritos por equipes diferentes em momentos diferentes, e o código provavelmente está dividido em repositórios separados, dificultando a descoberta.

Ao longo dos anos, muitas abordagens foram inventadas para tornar o CSS mais gerenciável. Alguns optam por usar uma convenção de nomenclatura estrita, como o [BEM](http://getbem.com/) , para garantir que os seletores sejam aplicados apenas quando pretendidos. Outros, preferindo não confiar apenas na disciplina do desenvolvedor, usam um pré-processador como o [SASS](https://sass-lang.com/) , cujo aninhamento de seletor pode ser usado como uma forma de namespacing. Uma abordagem mais nova é aplicar todos os estilos de maneira programática com [módulos CSS](https://github.com/css-modules/css-modules) ou uma das várias bibliotecas [CSS-in-JS](https://mxstbr.com/thoughts/css-in-js/) , o que garante que os estilos sejam aplicados diretamente apenas nos locais pretendidos pelo desenvolvedor. Ou, para uma abordagem mais baseada em plataforma, o [shadow DOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM) também oferece isolamento de estilo.

A abordagem que você escolhe não importa muito, desde que você encontre uma maneira de garantir que os desenvolvedores possam escrever seus estilos independentemente um do outro e tenha confiança de que seu código se comportará de maneira previsível quando composto em um único aplicativo.

---

## Bibliotecas de componentes compartilhados ##

Mencionamos acima que a consistência visual entre os micro frontends é importante, e uma abordagem para isso é desenvolver uma biblioteca de componentes de interface do usuário reutilizáveis ​​e compartilhados. Em geral, acreditamos que essa é uma boa ideia, embora seja difícil fazer bem. Os principais benefícios da criação dessa biblioteca são esforços reduzidos através da reutilização de código e consistência visual. Além disso, sua biblioteca de componentes pode servir como um guia de estilo vivo e pode ser um ótimo ponto de colaboração entre desenvolvedores e designers.


Uma das coisas mais fáceis de errar é criar muitos desses componentes, muito cedo. É tentador criar um [Framework Foundation](https://martinfowler.com/bliki/FoundationFramework.html) , com todos os recursos visuais comuns que serão necessários em todos os aplicativos. No entanto, a experiência nos diz que é difícil, se não impossível, adivinhar quais devem ser as APIs dos componentes antes de você usá-las no mundo real, o que resulta em muitas mudanças no início da vida de um componente. Por esse motivo, preferimos permitir que as equipes criem seus próprios componentes dentro de suas bases de código conforme necessário, mesmo que isso cause alguma duplicação inicialmente. Permita que os padrões surjam naturalmente e, depois que a API do componente se tornar óbvia, você poderá [coletar](https://martinfowler.com/bliki/HarvestedFramework.html) o código duplicado em uma biblioteca compartilhada e tenha certeza de que você tem algo comprovado.

Os candidatos mais óbvios para o compartilhamento são primitivas visuais "burras", como ícones, rótulos e botões. Também podemos compartilhar componentes mais complexos que podem conter uma quantidade significativa de lógica da interface do usuário, como um campo de pesquisa suspenso com preenchimento automático. Ou uma tabela classificável, filtrável e paginada. No entanto, tenha cuidado para garantir que seus componentes compartilhados contenham apenas lógica da interface do usuário e nenhuma lógica comercial ou de domínio. Quando a lógica do domínio é colocada em uma biblioteca compartilhada, ela cria um alto grau de acoplamento entre aplicativos e aumenta a dificuldade da mudança. Portanto, por exemplo, você geralmente não deve tentar compartilhar umProductTable, que conteria todos os tipos de suposições sobre o que exatamente é um "produto" e como deve se comportar. Essa modelagem de domínio e lógica de negócios pertence ao código do aplicativo das micro frontends, e não a uma biblioteca compartilhada.

Como em qualquer biblioteca interna compartilhada, existem algumas questões complicadas sobre sua propriedade e governança. Um modelo é dizer que, como um ativo compartilhado, "todos" são os proprietários, embora na prática isso geralmente signifique que ninguém é o proprietário. Ele pode rapidamente se tornar uma mistura de códigos inconsistentes, sem convenções claras ou visão técnica. No outro extremo, se o desenvolvimento da biblioteca compartilhada for completamente centralizado, haverá uma grande desconexão entre as pessoas que criam os componentes e as pessoas que os consomem. Os melhores modelos que vimos são aqueles em que qualquer pessoa pode contribuir com a biblioteca, mas há um custodiante(uma pessoa ou uma equipe) responsável por garantir a qualidade, consistência e validade dessas contribuições. O trabalho de manter a biblioteca compartilhada exige fortes habilidades técnicas, mas também as habilidades necessárias para cultivar a colaboração entre muitas equipes.


---

## Comunicação entre aplicativos ##

Uma das perguntas mais comuns sobre micro frontends é como deixá-los conversar entre si. Em geral, recomendamos que eles se comuniquem o menos possível, pois muitas vezes reintroduz o tipo de acoplamento inadequado que procuramos evitar em primeiro lugar.

Dito isto, é geralmente necessário algum nível de comunicação entre aplicativos. [Eventos personalizados](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Creating_and_triggering_events) permitem que os micro frontends se comuniquem indiretamente, o que é uma boa maneira de minimizar o acoplamento direto, apesar de dificultar a determinação e a execução do contrato existente entre os micro frontends. Como alternativa, o modelo React de passar retornos de chamada e dados para baixo (nesse caso, para baixo do aplicativo de contêiner para os micro frontends) também é uma boa solução que torna o contrato mais explícito. Uma terceira alternativa é usar a barra de endereço como um mecanismo de comunicação, que exploraremos com mais [detalhes posteriormente](https://martinfowler.com/articles/micro-frontends.html#Cross-applicationCommunicationViaRouting) .

>Se você estiver usando o redux, a abordagem usual é ter um único armazenamento compartilhado global para todo o aplicativo. No entanto, se cada micro frontend deve ser seu próprio aplicativo independente, faz sentido que cada um tenha seu próprio repositório redux. Os documentos do redux até mencionam ["isolar um aplicativo Redux como um componente em um aplicativo maior"](https://redux.js.org/faq/store-setup#can-or-should-i-create-multiple-stores-can-i-import-my-store-directly-and-use-it-in-components-myself) como um motivo válido para ter vários repositórios.


Qualquer que seja a abordagem que escolhermos, queremos que nossos micro frontends se comuniquem enviando mensagens ou eventos entre si e evitem ter qualquer estado compartilhado. Assim como o compartilhamento de um banco de dados entre microsserviços, assim que compartilhamos nossas estruturas de dados e modelos de domínio, criamos enormes quantidades de acoplamento e torna-se extremamente difícil fazer alterações.

Assim como no estilo, existem várias abordagens diferentes que podem funcionar bem aqui. O mais importante é pensar bastante sobre que tipo de acoplamento você está apresentando e como manterá esse contrato ao longo do tempo. Assim como na integração entre microsserviços, você não poderá fazer alterações significativas em suas integrações sem ter um processo de atualização coordenada em diferentes aplicativos e equipes.

Você também deve pensar em como verificará automaticamente se a integração não quebra. O teste funcional é uma abordagem, mas preferimos limitar o número de testes funcionais que escrevemos devido ao custo de implementá-los e mantê-los. Como alternativa, você pode implementar algum tipo de [contrato orientado ao consumidor](https://martinfowler.com/articles/consumerDrivenContracts.html) , para que cada micro front-end possa especificar o que é necessário para outros micro front-end, sem a necessidade de realmente integrar e executar todos eles em um navegador juntos.

---

## Comunicação de back-end ##

Se tivermos equipes separadas trabalhando independentemente em aplicativos de front-end, e o desenvolvimento de back-end? Acreditamos firmemente no valor das equipes de pilha completa, que possuem o desenvolvimento de seus aplicativos desde o código visual até o desenvolvimento da API e o código do banco de dados e da infraestrutura. Um padrão que ajuda aqui é o padrão [BFF](https://samnewman.io/patterns/architectural/bff/) , em que cada aplicativo de front-end possui um back-end correspondente cujo objetivo é apenas atender às necessidades desse front-end. Embora o padrão BFF possa originalmente significar back-end dedicados para cada canal de front-end (Web, celular, etc.), ele pode ser facilmente estendido para significar um back-end para cada micro front-end.

Há muitas variáveis a serem consideradas aqui. O BFF pode ser independente com sua própria lógica de negócios e banco de dados, ou pode ser apenas um agregador de serviços de recebimento de dados. Se houver serviços a jusante, pode ou não fazer sentido que a equipe que possui o micro frontend e seu melhor amigo também possua alguns desses serviços. Se o micro frontend tiver apenas uma API com a qual converse e essa API for razoavelmente estável, poderá não haver muito valor na criação de um BFF. O princípio norteador aqui é que a equipe que constrói um micro front-end específico não deve esperar que outras equipes construam coisas para eles. Portanto, se todos os novos recursos adicionados a um micro front-end também exigirem alterações no back-end, esse é um argumento forte para um BFF, de propriedade da mesma equipe.


![](https://martinfowler.com/articles/micro-frontends/bff.png)

>Figura 7: Existem várias maneiras diferentes de estruturar seus relacionamentos de front-end / back-end

Outra pergunta comum é: como o usuário de um aplicativo de micro frontend deve ser autenticado e autorizado com o servidor? Obviamente, nossos clientes devem ter que se autenticar apenas uma vez; portanto, o auth geralmente se enquadra na categoria de preocupações transversais que devem pertencer ao aplicativo de contêineres. O contêiner provavelmente possui algum tipo de formulário de login, através do qual obtemos algum tipo de token. Esse token pertenceria ao contêiner e pode ser injetado em cada micro front-end na inicialização. Por fim, o micro front-end pode enviar o token com qualquer solicitação feita ao servidor, e o servidor pode fazer qualquer validação necessária.


---

## Teste ## 

Não vemos muita diferença entre front-end monolíticos e micr-front-end quando se trata de testes. Em geral, quaisquer estratégias que você esteja usando para testar um front end monolítico podem ser reproduzidas em cada micro front end individual. Ou seja, cada micro front-end deve ter seu próprio conjunto abrangente de testes automatizados que garantam a qualidade e a correção do código.


A lacuna óbvia seria então o teste de integração dos vários micro frontends com o aplicativo de contêiner. Isso pode ser feito usando sua ferramenta preferida de ferramenta funcional / de ponta a ponta (como Selenium ou Cypress), mas não leve as coisas muito longe; testes funcionais devem abranger apenas aspectos que não podem ser testados em um nível inferior da [pirâmide de testes](https://martinfowler.com/bliki/TestPyramid.html) . Com isso queremos dizer, use testes de unidade para cobrir sua lógica de negócios de baixo nível e lógica de renderização e, em seguida, use testes funcionais apenas para validar se a página foi montada corretamente. Por exemplo, você pode carregar o aplicativo totalmente integrado em uma URL específica e afirmar que o título codificado do micro frontend relevante está presente na página.

Se houver jornadas de usuário que abranjam micro frontends, você poderá usar testes funcionais para cobri-los, mas mantenha os testes funcionais focados na validação da integração dos frontends, e não na lógica de negócios interna de cada micro frontend, que já deveria ter foi coberto por testes de unidade. [Como mencionado acima](#comunicação-entre-aplicativos), os contratos orientados ao consumidor podem ajudar a especificar diretamente as interações que ocorrem entre os micro frontends sem a escassez de ambientes de integração e testes funcionais.

---

## O exemplo em detalhes ##

A maior parte do restante deste artigo será uma explicação detalhada de apenas uma maneira pela qual nosso aplicativo de exemplo pode ser implementado. Vamos nos concentrar principalmente em como o aplicativo de contêiner e os micro frontends se [ntegram usando JavaScript](https://martinfowler.com/articles/micro-frontends.html#Run-timeIntegrationViaJavascript)pois essa é provavelmente a parte mais interessante e complexa. Você pode ver o resultado final implantado ao vivo em https://demo.microfrontends.com e o código fonte completo pode ser visto no [Github](https://github.com/micro-frontends-demo) .


![](https://martinfowler.com/articles/micro-frontends/screenshot-browse.png)


>Figura 8: A página de destino 'browse' do aplicativo de demonstração completo de micro frontends

A demonstração é toda criada usando o React.js, portanto, vale a pena ressaltar que o React não tem monopólio sobre essa arquitetura. Os micro frontends podem ser implementados com muitas ferramentas ou estruturas diferentes. Escolhemos o React aqui por causa de sua popularidade e por causa de nossa própria familiaridade com ele.


## O recipiente ##

Começaremos com o contêiner , pois é o ponto de entrada para nossos clientes. Vamos ver o que podemos aprender sobre isso package.json:

```js
{
  "name": "@micro-frontends-demo/container",
  "description": "Entry point and container for a micro frontends demo",
  "scripts": {
    "start": "PORT=3000 react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test"
  },
  "dependencies": {
    "react": "^16.4.0",
    "react-dom": "^16.4.0",
    "react-router-dom": "^4.2.2",
    "react-scripts": "^2.1.8"
  },
  "devDependencies": {
    "enzyme": "^3.3.0",
    "enzyme-adapter-react-16": "^1.1.1",
    "jest-enzyme": "^6.0.2",
    "react-app-rewire-micro-frontends": "^0.0.1",
    "react-app-rewired": "^2.1.1"
  },
  "config-overrides-path": "node_modules/react-app-rewire-micro-frontends"
}
```

A partir das dependências reacte react-scripts, podemos concluir que é um aplicativo React.js criado com [create-react-app](https://facebook.github.io/create-react-app/). Mais interessante é o que não existe: qualquer menção aos micro frontends que vamos compor juntos para formar nosso aplicativo final. Se os especificássemos aqui como dependências da biblioteca, estaríamos seguindo o caminho da integração em tempo de construção, que conforme mencionado anteriormente tende a causar acoplamentos problemáticos em nossos ciclos de lançamento.

>Na versão 1 react-scripts, era possível ter vários aplicativos coexistindo em uma única página sem conflitos, mas a versão 2 usa alguns recursos do webpack que causam erros quando dois ou mais aplicativos tentam renderizar-se na mesma página. Por esse motivo, ```react-app-rewired``` substituímos algumas das configurações internas do webpack ```react-scripts```. Isso corrige esses erros e permite que continuemos confiando no react-scripts o gerenciamento de nossas ferramentas de criação.

Para ver como selecionamos e exibimos um micro front-end, vejamos App.js. Usamos o [React Router](https://reacttraining.com/react-router/) para combinar o URL atual com uma lista predefinida de rotas e renderizar um componente correspondente:

```jsx
<Switch>
  <Route exact path="/" component={Browse} />
  <Route exact path="/restaurant/:id" component={Restaurant} />
  <Route exact path="/random" render={Random} />
</Switch>
```

O Random componente não é tão interessante - apenas redireciona a página para um URL de restaurante selecionado aleatoriamente. Os componentes Browsee Restaurantsão assim:

```jsx
const Browse = ({ history }) => (
  <MicroFrontend history={history} name="Browse" host={browseHost} />
);
const Restaurant = ({ history }) => (
  <MicroFrontend history={history} name="Restaurant" host={restaurantHost} />
);
```

Nos dois casos, renderizamos um MicroFrontendcomponente. Além do objeto de histórico (que se tornará importante posteriormente), especificamos o nome exclusivo do aplicativo e o host do qual o pacote configurável pode ser baixado. Esse URL orientado à configuração será semelhante http://localhost:3001ao executado localmente ou https://browse.demo.microfrontends.comem produção.

Depois de selecionar um micro front-end App.js, agora o renderizamos MicroFrontend.js, que é apenas outro componente do React:

```jsx
class MicroFrontend extends React.Component {
  render() {
    return <main id={`${this.props.name}-container`} />;
  }
}

```

>|Esta não é a classe inteira, veremos mais métodos em breve.

Ao renderizar, tudo o que fazemos é colocar um elemento de contêiner na página, com um ID exclusivo para o micro frontend. É aqui que diremos ao nosso micro frontend para se render. Usamos o React's componentDidMount como o gatilho para baixar e montar o micro frontend:


>componentDidMount é um método de ciclo de vida dos componentes React, chamado pela estrutura logo após uma instância do nosso componente ter sido 'montada' no DOM pela primeira vez.


>classe MicroFrontend…

```jsx
componentDidMount() {
    const { name, host } = this.props;
    const scriptId = `micro-frontend-script-${name}`;

    if (document.getElementById(scriptId)) {
      this.renderMicroFrontend();
      return;
    }

    fetch(`${host}/asset-manifest.json`)
      .then(res => res.json())
      .then(manifest => {
        const script = document.createElement('script');
        script.id = scriptId;
        script.src = `${host}${manifest['main.js']}`;
        script.onload = this.renderMicroFrontend;
        document.head.appendChild(script);
      });
  }
  
  ```
  
Primeiro, verificamos se o script relevante, que possui um ID exclusivo, já foi baixado; nesse caso, podemos processá-lo imediatamente. Caso contrário, buscamos o asset-manifest.jsonarquivo no host apropriado, a fim de procurar a URL completa do ativo principal do script. Depois de definir o URL do script, resta apenas anexá-lo ao documento, com um onloadmanipulador que renderiza o micro frontend:


>Temos que buscar a URL do script em um arquivo de manifesto de ativos, porque react-scriptsgera arquivos JavaScript compilados que possuem hashes em seus nomes de arquivo para facilitar o cache.

>class MicroFrontend…

```jsx
  renderMicroFrontend = () => {
    const { name, history } = this.props;

    window[`render${name}`](`${name}-container`, history);
    // E.g.: window.renderBrowse('browse-container', history);
  };
  
```


No código acima, estamos chamando uma função global chamada algo como window.renderBrowse, que foi colocada lá pelo script que acabamos de baixar. Passamos o ID do <main> elemento em que o micro frontend deve renderizar-se, e um history objeto, que explicaremos em breve. **A assinatura desta função global é o principal contrato entre a aplicação do contêiner e as micro frontends**. É aqui que qualquer comunicação ou integração deve acontecer, mantendo-o bastante leve facilita a manutenção e a adição de novas micro front-ends no futuro. Sempre que desejamos fazer algo que exija uma alteração nesse código, devemos pensar muito sobre o que isso significa para o acoplamento de nossas bases de código e a manutenção do contrato.

Há uma peça final, que está lidando com a limpeza. Quando nosso MicroFrontendcomponente desmonta (é removido do DOM), também queremos desmontar o micro frontend relevante. Há uma função global correspondente definida por cada micro front-end para esse fim, que chamamos de método de ciclo de vida React apropriado:


>class MicroFrontend…


```jsx

  componentWillUnmount() {
    const { name } = this.props;

    window[`unmount${name}`](`${name}-container`);
  }
  
 ```
 
 Em termos de conteúdo próprio, tudo o que o contêiner processa diretamente é o cabeçalho de nível superior e a barra de navegação do site, pois são constantes em todas as páginas. O CSS para esses elementos foi escrito com cuidado para garantir que somente estilize elementos dentro do cabeçalho, portanto, não deve entrar em conflito com nenhum código de estilo dentro dos micro frontends.

E esse é o fim do aplicativo de contêiner! É bastante rudimentar, mas isso nos dá um shell que pode baixar dinamicamente nossos micro frontends em tempo de execução e colá-los em algo coeso em uma única página. Esses micro frontends podem ser implantados independentemente até a produção, sem nunca fazer alterações em nenhum outro micro frontend ou no próprio contêiner.

## Os micro frontends ##

O lugar lógico para continuar essa história é com a função de renderização global à qual continuamos nos referindo. A página inicial do nosso aplicativo é uma lista filtrável de restaurantes, cujo ponto de entrada fica assim:

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import registerServiceWorker from './registerServiceWorker';

window.renderBrowse = (containerId, history) => {
  ReactDOM.render(<App history={history} />, document.getElementById(containerId));
  registerServiceWorker();
};

window.unmountBrowse = containerId => {
  ReactDOM.unmountComponentAtNode(document.getElementById(containerId));
};

```

Normalmente, nos aplicativos React.js, a chamada para ReactDOM.renderestaria no escopo de nível superior, o que significa que, assim que esse arquivo de script é carregado, ele começa imediatamente a renderização em um elemento DOM codificado. Para esse aplicativo, precisamos poder controlar quando e onde a renderização ocorre, portanto, envolvemos-o em uma função que recebe o ID do elemento DOM como parâmetro e anexamos essa função ao windowobjeto global . Também podemos ver a função de desmontagem correspondente usada para limpeza.

Enquanto já vimos como essa função é chamada quando o micro frontend é integrado a todo o aplicativo de contêiner, um dos maiores critérios de sucesso aqui é que podemos desenvolver e executar os micro frontend independentemente. Portanto, cada micro front-end também possui index.htmlum script embutido para renderizar o aplicativo em um modo "independente", fora do contêiner:

```html

<html lang="en">
  <head>
    <title>Restaurant order</title>
  </head>
  <body>
    <main id="container"></main>
    <script type="text/javascript">
      window.onload = () => {
        window.renderRestaurant('container');
      };
    </script>
  </body>
</html>

```

![](https://martinfowler.com/articles/micro-frontends/screenshot-order.png)

>Figura 9: Cada micro front-end pode ser executado como um aplicativo independente fora do contêiner.

A partir deste momento, os micro frontends são na maioria simples aplicativos antigos do React. O aplicativo ['browse'](https://github.com/micro-frontends-demo/browse) busca a lista de restaurantes no back-end, fornece <input> elementos para pesquisar e filtrar os restaurantes e renderiza os <Link>elementos do React Router , que navegam para um restaurante específico. Nesse ponto, passaríamos para o segundo micro frontend ['order'](https://github.com/micro-frontends-demo/restaurant-order) , que renderiza um único restaurante com seu menu.
   
![](https://martinfowler.com/articles/micro-frontends/demo-architecture.png)


>Figura 10: Essas micro front-ends interagem apenas através de alterações de rota, não diretamente

A última coisa que vale a pena mencionar sobre os nossos micro frontends é que ambos usam styled-componentspara todo o seu estilo. Essa biblioteca CSS-in-JS facilita a associação de estilos a componentes específicos; portanto, garantimos que os estilos de um micro frontend não vazarão e afetarão o contêiner ou outro micro frontend.

## Comunicação entre aplicativos via roteamento ## 

Nós mencionamos anteriormente que a comunicação entre aplicativos devem ser mantidos a um mínimo. Neste exemplo, o único requisito que temos é que a página de navegação precise informar à página do restaurante qual restaurante carregar. Aqui veremos como podemos usar o roteamento do lado do cliente para resolver esse problema.

Todos os três aplicativos React envolvidos aqui estão usando o React Router para roteamento declarativo, mas foram inicializados de duas maneiras ligeiramente diferentes. Para o aplicativo de contêiner, criamos um <BrowserRouter>, que internamente instanciará um historyobjeto. Este é o mesmo historyobjeto que abordamos anteriormente. Usamos esse objeto para manipular o histórico do lado do cliente e também podemos usá-lo para vincular vários roteadores do React. Dentro de nossas micro frontends, inicializamos o roteador assim:
   
```jsx
<Router history={this.props.history}>

```

Nesse caso, em vez de permitir que o React Router instancie outro objeto de histórico, fornecemos a instância que foi passada pelo aplicativo de contêiner. Todas as <Router>instâncias agora estão conectadas, portanto, as alterações de rota acionadas em qualquer uma delas serão refletidas em todas elas. Isso nos fornece uma maneira fácil de passar "parâmetros" de um micro front-end para outro, via URL. Por exemplo, no micro frontend de navegação, temos um link como este:
   
```jsx
<Link to={`/restaurant/${restaurant.id}`}>

```

Quando esse link é clicado, a rota será atualizada no contêiner, que exibirá a nova URL e determinará que o micro frontend do restaurante deve ser montado e renderizado. A lógica de roteamento desse micro frontend extrairá o ID do restaurante da URL e renderizará as informações corretas.

Esperamos que este exemplo de fluxo mostre a flexibilidade e o poder da URL humilde. Além de ser útil para compartilhar e marcar, nessa arquitetura específica, pode ser uma maneira útil de comunicar a intenção entre micro frontends. O uso do URL da página para esse fim marca muitas caixas:

- Sua estrutura é um padrão aberto e bem definido
- É globalmente acessível a qualquer código na página
- Seu tamanho limitado incentiva o envio de apenas uma pequena quantidade de dados
- É voltado para o usuário, o que incentiva uma estrutura que modela fielmente o domínio
- É declarativo, não imperativo. Ou seja, "é aqui que estamos", em vez de "por favor, faça isso"
- Obriga os micro frontends a se comunicarem indiretamente e a não conhecerem ou dependerem um do outro

Ao usar o roteamento como nosso modo de comunicação entre micro frontends, as rotas que escolhemos constituem um contrato . Nesse caso, definimos a ideia de que um restaurante pode ser visualizado /restaurant/:restaurantIde não podemos mudar esse caminho sem atualizar todos os aplicativos que fazem referência a ele. Dada a importância deste contrato, deveríamos ter testes automatizados que verificam se o contrato está sendo cumprido.

## Conteúdo comum ##

Embora desejemos que nossas equipes e nossos micro front-ends sejam o mais independentes possível, há algumas coisas que devem ser comuns. Escrevemos anteriormente sobre como as [bibliotecas de componentes compartilhados](https://martinfowler.com/articles/micro-frontends.html#SharedComponentLibraries) podem ajudar com a consistência entre micro frontends, mas para esta pequena demonstração, uma biblioteca de componentes seria um exagero. Então, em vez disso, temos um pequeno [repositório de conteúdo comum](https://github.com/micro-frontends-demo/content) , incluindo imagens, dados JSON e CSS, que são veiculados pela rede para todas as micro frontends.

Há outra coisa que podemos optar por compartilhar entre os micro frontends: dependências da biblioteca. Como descreveremos em breve , a duplicação de dependências é uma desvantagem comum dos micro frontends. Mesmo que o compartilhamento dessas dependências entre aplicativos tenha seu próprio conjunto de dificuldades, vale a pena falar sobre esse aplicativo de demonstração sobre como isso pode ser feito.

O primeiro passo é escolher quais dependências compartilhar. Uma análise rápida do nosso código compilado mostrou que cerca de 50% dos pacotes foram contribuídos por reacte react-dom. Além de seu tamanho, essas duas bibliotecas são nossas dependências mais básicas, portanto sabemos que todos os micro frontends podem se beneficiar da sua extração. Por fim, são bibliotecas estáveis ​​e maduras, que geralmente introduzem alterações significativas em duas versões principais; portanto, os esforços de atualização entre aplicativos não devem ser muito difíceis.

Quanto à extração real, tudo o que precisamos fazer é marcar as bibliotecas como [externas](https://webpack.js.org/configuration/externals/) em nossa configuração do webpack, o que podemos fazer com uma religação semelhante à descrita anteriormente .

```jsx
module.exports = (config, env) => {
  config.externals = {
    react: 'React',
    'react-dom': 'ReactDOM'
  }
  return config;
};

```

Em seguida, adicionamos algumas scripttags a cada index.html arquivo, para buscar as duas bibliotecas do nosso servidor de conteúdo compartilhado.

```html
<body>
  <noscript>
    You need to enable JavaScript to run this app.
  </noscript>
  <div id="root"></div>
  <script src="%REACT_APP_CONTENT_HOST%/react.prod-16.8.6.min.js"></script>
  <script src="%REACT_APP_CONTENT_HOST%/react-dom.prod-16.8.6.min.js"></script>
</body>

```

Compartilhar código entre equipes é sempre uma coisa complicada de se fazer bem. Precisamos garantir que apenas compartilhemos coisas que realmente queremos que sejam comuns e que desejemos mudar em vários lugares ao mesmo tempo. No entanto, se tivermos cuidado com o que compartilhamos e o que não compartilhamos, há benefícios reais a serem obtidos.

## A infraestrutura ##

O aplicativo está hospedado na AWS, com infraestrutura principal (buckets S3, distribuições do CloudFront, domínios, certificados etc.), provisionados de uma só vez usando um [repositório centralizado](https://github.com/micro-frontends-demo/infra) do código Terraform. Cada micro frontend possui seu próprio repositório de origem com seu próprio pipeline de implantação contínua no [Travis CI](https://travis-ci.org/micro-frontends-demo/) , que cria, testa e implanta seus ativos estáticos nesses buckets S3. Isso equilibra a conveniência do gerenciamento centralizado da infraestrutura com a flexibilidade da implantação independente.

Observe que cada micro front-end (e o contêiner) recebe seu próprio balde. Isso significa que ele tem livre domínio sobre o que está lá, e não precisamos nos preocupar com colisões de nomes de objetos ou regras conflitantes de gerenciamento de acesso de outra equipe ou aplicativo.

---

## Desvantagens ##

No início deste artigo, mencionamos que existem compensações com micro frontends, assim como em qualquer arquitetura. Os benefícios que mencionamos têm um custo, que abordaremos aqui.

## Tamanho da carga útil ##

Pacotes configuráveis ​​JavaScript criados de forma independente podem causar duplicação de dependências comuns, aumentando o número de bytes que precisamos enviar pela rede para nossos usuários finais. Por exemplo, se todo micro front-end incluir sua própria cópia do React, forçaremos nossos clientes a baixar o React n vezes. Existe uma [relação direta](https://developers.google.com/web/fundamentals/performance/why-performance-matters/) entre o desempenho da página e o engajamento / conversão do usuário, e grande parte do mundo roda na infraestrutura da Internet muito mais lentamente do que aquelas em cidades altamente desenvolvidas, por isso temos muitos motivos para nos preocupar com o tamanho dos downloads.

Este problema não é fácil de resolver. Existe uma tensão inerente entre nosso desejo de permitir que as equipes compilem seus aplicativos de forma independente, para que possam trabalhar autonomamente, e nosso desejo de criar nossos aplicativos de forma que possam compartilhar dependências comuns. Uma abordagem é externalizar dependências comuns de nossos pacotes compilados, como descrevemos para o aplicativo de demonstração. No entanto, assim que seguimos esse caminho, reintroduzimos algum acoplamento em tempo de compilação para nossas micro frontends. Agora, existe um contrato implícito entre eles que diz: "todos devemos usar essas versões exatas dessas dependências". Se houver uma mudança de dependência em uma dependência, podemos acabar precisando de um grande esforço de atualização coordenada e de um evento único de liberação de etapa de bloqueio. Isso é tudo o que estávamos tentando evitar com micro frontends!

Essa tensão inerente é difícil, mas nem todas são más notícias. Primeiro, mesmo se optarmos por não fazer nada sobre dependências duplicadas, é possível que cada página individual ainda seja carregada mais rapidamente do que se tivéssemos construído um único frontend monolítico. O motivo é que, ao compilar cada página de forma independente, implementamos efetivamente nossa própria forma de divisão de código. Nos monólitos clássicos, quando qualquer página do aplicativo é carregada, geralmente fazemos o download do código-fonte e das dependências de todas as páginas de uma só vez. Ao criar de forma independente, qualquer carregamento de página único fará o download apenas da origem e das dependências dessa página. Isso pode resultar em carregamentos iniciais de página mais rápidos, mas navegação subseqüente mais lenta, pois os usuários são forçados a baixar novamente as mesmas dependências em cada página. Se formos disciplinados a não inchar nossos micro frontends com dependências desnecessárias, ou se soubermos que os usuários geralmente mantêm apenas uma ou duas páginas no aplicativo, é possível que consigamos uma redeganho em termos de desempenho, mesmo com dependências duplicadas.

Existem muitos "may's" e "possivelmente's" no parágrafo anterior, o que destaca o fato de que cada aplicativo sempre terá suas próprias características de desempenho únicas. Se você deseja saber com certeza quais serão os impactos no desempenho de uma alteração específica, não há substituto para a realização de medições no mundo real, de preferência na produção. Vimos equipes agonizando com alguns kilobytes extras de JavaScript, apenas para baixar muitos megabytes de imagens de alta resolução ou executar consultas caras em um banco de dados muito lento. Portanto, embora seja importante considerar os impactos no desempenho de todas as decisões de arquitetura, certifique-se de saber onde estão os gargalos reais.

## Diferenças de ambiente ##

Deveríamos ser capazes de desenvolver um único micro front-end sem precisar pensar em todos os outros micro front-end sendo desenvolvidos por outras equipes. Podemos até executar nosso micro front-end em modo “autônomo”, em uma página em branco, em vez de dentro do aplicativo de contêiner que o abrigará na produção. Isso pode tornar o desenvolvimento muito mais simples, especialmente quando o contêiner real é uma base de código herdada e complexa, o que geralmente acontece quando estamos usando micro frontends para fazer uma migração gradual do velho mundo para o novo. No entanto, há riscos associados ao desenvolvimento em um ambiente bastante diferente da produção. Se nosso contêiner em tempo de desenvolvimento se comportar de forma diferente do contêiner de produção, podemos descobrir que nosso micro front-end está quebrado, ou se comporta de maneira diferente quando implantamos na produção. Particularmente preocupantes são os estilos globais que podem ser trazidos pelo contêiner ou por outros micro frontends.

A solução aqui não é tão diferente de qualquer outra situação em que precisamos nos preocupar com diferenças ambientais. Se estamos desenvolvendo localmente em um ambiente que não é de produção semelhante, precisamos garantir que vamos integrar regularmente e implantar nosso micro frontend para ambientes que são como a produção, e nós devemos fazer o teste (manual e automático) nesses ambientes detectar problemas de integração o mais cedo possível. Isso não resolverá completamente o problema, mas, em última análise, é outra desvantagem que devemos considerar: o aumento da produtividade de um ambiente de desenvolvimento simplificado vale o risco de problemas de integração? A resposta vai depender do projeto!


## Complexidade operacional e de governança ##

A desvantagem final é uma paralela direta aos microsserviços. Como uma arquitetura mais distribuída, os micro frontends inevitavelmente levarão a ter mais coisas para gerenciar - mais repositórios, mais ferramentas, mais compilar / implantar pipelines, mais servidores, mais domínios etc. Então, antes de adotar essa arquitetura, existem algumas perguntas a serem feitas. deve considerar:

- Você possui automação suficiente para provisionar e gerenciar de maneira viável a infraestrutura adicional necessária?
- Seus processos de desenvolvimento, teste e release de front-end serão dimensionados para muitos aplicativos?
- Você se sente confortável com as decisões sobre práticas de desenvolvimento de ferramentas e ferramentas cada vez mais descentralizadas e menos controláveis?
- Como você garantirá um nível mínimo de qualidade, consistência ou governança em suas muitas bases de código de front-end independentes?

Provavelmente poderíamos preencher outro artigo inteiro discutindo esses tópicos. O ponto principal que queremos destacar é que, quando você escolhe micro frontends, por definição, está optando por criar muitas coisas pequenas em vez de uma coisa grande. Você deve considerar se possui a maturidade técnica e organizacional necessária para adotar essa abordagem sem criar o caos.


---

## Conclusão ##

À medida que as bases de código de front-end continuam a ficar mais complexas ao longo dos anos, vemos uma necessidade crescente de arquiteturas mais escaláveis. Precisamos ser capazes de traçar limites claros que estabeleçam os níveis certos de acoplamento e coesão entre entidades técnicas e de domínio. Deveríamos poder escalar a entrega de software em equipes independentes e autônomas.

Embora longe da única abordagem, vimos muitos casos do mundo real em que as micro front-ends oferecem esses benefícios, e conseguimos aplicar a técnica gradualmente ao longo do tempo nas bases de código herdadas e também nas novas. Se os micro frontends são a abordagem certa para você e sua organização ou não, podemos apenas esperar que isso faça parte de uma tendência contínua em que a arquitetura e a engenharia de frontend sejam tratadas com a seriedade que sabemos que merece.





--- 

Autor: [Cam Jackson](https://camjackson.net/)

[Artigo Original](https://martinfowler.com/articles/micro-frontends.html)

