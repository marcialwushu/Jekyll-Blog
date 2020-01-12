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
< html  lang = "en"  dir = "ltr" > 
  < cabeça > 
    < meta  charset = "utf-8" > 
    < title > Alimente-me </ title > 
  </ head > 
  < corpo > 
    < h1 > 🍽 Alimente-me </ h1 > 
    <! - # include file = "$ PAGE.html" -> 
  </ body > 
</ html >

```

Servimos esse arquivo usando o Nginx, configurando a $PAGE variável correspondendo ao URL que está sendo solicitado:

```js

servidor {
     escute  8080 ;
    server_name localhost;

    root / usr / share / nginx / html;
    index index.html;
    ssi  on ;

    # Redirecione / para / procure 
    reescrever ^ / $ http: // localhost: 8080 / browse redirect ;

    # Decida qual fragmento HTML inserir com base na 
    localização / navegação da URL {
       set  $ PAGE  'browse' ;
    }
    local / pedido {
       set  $ PAGE  'order' ;
    }
    local / perfil {
       set  $ PAGE  'profile'
    }

    # Todos os locais devem renderizar através do index.html 
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
   "name" : "@ feed-me / container" ,
   "version" : "1.0.0" ,
   "description" : "Um aplicativo Web de entrega de alimentos" ,
   "dependências" : {
     "@ feed-me / browse-restaurants " : " ^ 1.2.3 " ,
     " @ feed-me / order-food " : " ^ 4.5.6 " ,
     " @ feed-me / perfil do usuário " : " ^ 7.8.9 "
  }
}
```

A princípio, isso parece fazer sentido. Ele produz um único pacote Javascript implementável, como é habitual, permitindo a duplicação de dependências comuns de nossos vários aplicativos. No entanto, essa abordagem significa que precisamos recompilar e liberar cada micro front-end para liberar uma alteração em qualquer parte individual do produto. Assim como nos microsserviços, já vimos dores suficientes causadas por um processo de liberação tão lento que recomendamos fortemente contra esse tipo de abordagem para micro frontends.

Depois de todo o trabalho de dividir nosso aplicativo em bases de código discretas que podem ser desenvolvidas e testadas independentemente, não vamos reintroduzir todo esse acoplamento no estágio de lançamento. Deveríamos encontrar uma maneira de integrar nossos micro frontends em tempo de execução, em vez de em tempo de construção.

## Integração em tempo de execução via iframes ##

Uma das abordagens mais simples para compor aplicativos juntos no navegador é o humilde iframe. Por sua natureza, os iframes facilitam a criação de uma página a partir de subpáginas independentes. Eles também oferecem um bom grau de isolamento em termos de estilo e variáveis globais que não interferem entre si.

```html
< html > 
  < head > 
    < title > Alimente-me! </ title > 
  </ head > 
  < body > 
    < h1 > Bem-vindo ao Feed me! </ h1 >

    < iframe  id = "micro-frontend-container" > </ iframe >

    < tipo de script  = "text / javascript" > const microFrontendsByRoute = {
         '/' : 'https://browse.example.com/index.html' ,
         '/ order-food' : 'https: //order.example. com / index.html ' ,
         ' / user-profile ' : ' https://profile.example.com/index.html ' ,
      
      };

      const iframe = documento .getElementById ( 'micro-frontend-container' );
      iframe.src = microFrontendsByRoute [ janela .location.pathname];
    </ script > 
  </ body > 
</ html >

```

Assim como na [opção](https://martinfowler.com/articles/micro-frontends.html#Server-sideTemplateComposition) de inclusão do [servidor](https://martinfowler.com/articles/micro-frontends.html#Server-sideTemplateComposition) , criar uma página com iframes não é uma técnica nova e talvez não pareça tão excitante. Porém, se revisitarmos os principais benefícios das micro-interfaces [listadas anteriormente](https://martinfowler.com/articles/micro-frontends.html#Benefits) , os iframes serão os principais, desde que tenhamos cuidado com o modo como dividimos o aplicativo e estruturamos nossas equipes.

Muitas vezes vemos muita relutância em escolher iframes. Embora parte dessa relutância pareça ser motivada por um pressentimento de que os iframes são um pouco "eca", há algumas boas razões para que as pessoas os evitem. O fácil isolamento mencionado acima tende a torná-los menos flexíveis do que outras opções. Pode ser difícil criar integrações entre diferentes partes do aplicativo, para tornar o roteamento, o histórico e os links diretos mais complicados, além de apresentar alguns desafios extras para tornar sua página totalmente responsiva.


## Integração em tempo de execução via JavaScript ## 

A próxima abordagem que descreveremos é provavelmente a mais flexível e a que vemos equipes adotando com mais frequência. Cada micro frontend é incluído na página usando uma <script>tag e, ao carregar, expõe uma função global como seu ponto de entrada. O aplicativo de contêiner determina então qual micro front-end deve ser montado e chama a função relevante para informar a um micro front-end quando e onde se renderizar.
   

```html

< html > 
  < head > 
    < title > Alimente-me! </ title > 
  </ head > 
  < body > 
    < h1 > Bem-vindo ao Feed me! </ h1 >

    <! - Esses scripts não renderizam nada imediatamente -> 
    <! - Em vez disso, anexam funções de ponto de entrada à `janela` -> 
    < script  src = " https://browse.example.com/bundle. js " ></ script > 
    < script  src = "https://order.example.com/bundle.js" ></ script > 
    < script  src = "https://profile.example.com/bundle.js" ></ script >

    < div  id = "micro-frontend-root" > </ div >

    < script  type = "text / javascript" > // Essas funções globais são anexadas à janela pelos scripts acima const microFrontendsByRoute = {
         '/' : window .renderBrowseRestaurants,
         '/ order-food' : window .renderOrderFood,
         '/ user- profile ' : window .renderUserProfile,
      
      
      };
      const renderFunction = microFrontendsByRoute [ window .location.pathname];

      // Tendo determinado a função do ponto de entrada, agora a chamamos, 
      // fornecendo o ID do elemento em que ele deve se renderizar 
      renderFunction ( 'micro-frontend-root' );
    </ script > 
  </ body > 
</ html >

```

O exposto acima é obviamente um exemplo primitivo, mas demonstra a técnica básica. Diferentemente da integração em tempo de compilação, podemos implantar cada um dos bundle.jsarquivos independentemente. E, diferentemente dos iframes, temos total flexibilidade para criar integrações entre nossos micro frontends da maneira que quisermos. Poderíamos estender o código acima de várias maneiras, por exemplo, para baixar apenas cada pacote JavaScript, conforme necessário, ou para transmitir e receber dados ao renderizar um micro front-end.

A flexibilidade dessa abordagem, combinada com a capacidade de implementação independente, a torna a escolha padrão e a que vimos na natureza com mais frequência. Vamos explorá-lo com mais detalhes quando entrarmos no [exemplo completo](https://martinfowler.com/articles/micro-frontends.html#TheExampleInDetail).

## Integração em tempo de execução via Web Components ## 

Uma variação da abordagem anterior é que cada micro frontend defina um elemento customizado em HTML para o contêiner instanciar, em vez de definir uma função global para o contêiner chamar.


```html

< html > 
  < head > 
    < title > Alimente-me! </ title > 
  </ head > 
  < body > 
    < h1 > Bem-vindo ao Feed me! </ h1 >

    <! - Esses scripts não renderizam nada imediatamente -> 
    <! - Em vez disso, cada um define um tipo de elemento personalizado -> 
    < script  src = "https://browse.example.com/bundle.js" ></ script > 
    < script  src = "https://order.example.com/bundle.js" ></ script > 
    < script  src = "https://profile.example.com/bundle.js" ></ script >

    < div  id = "micro-frontend-root" > </ div >

    < script  type = "text / javascript" > // Esses tipos de elementos são definidos pelos scripts acima const webComponentsByRoute = {
         '/' : 'micro-frontend-browse-restaurants' ,
         '/ order-food' : 'micro-frontend -order-food ' ,
         ' / user-profile ' : ' micro-frontend-user-profile ' ,
      
      
      };
      const webComponentType = webComponentsByRoute [ janela .location.pathname];

      // Depois de determinar o tipo de elemento personalizado do componente da Web certo, 
      // agora criamos uma instância e a anexamos ao documento 
      const root = document .getElementById ( 'micro-frontend-root' );
      const webComponent = documento .createElement (webComponentType);
      root.appendChild (webComponent);
    </ script > 
  </ body > 
</ html >

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

A maior parte do restante deste artigo será uma explicação detalhada de apenas uma maneira pela qual nosso aplicativo de exemplo pode ser implementado. Vamos nos concentrar principalmente em como o aplicativo de contêiner e os micro frontends se [ntegram usando JavaScript](https://martinfowler.com/articles/micro-frontends.html#Run-timeIntegrationViaJavascript)pois essa é provavelmente a parte mais interessante e complexa. Você pode ver o resultado final implantado ao vivo em https://demo.microfrontends.com e o código fonte completo pode ser visto no Github .







--- 

[Artigo Original](https://martinfowler.com/articles/micro-frontends.html)

