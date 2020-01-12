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





--- 

[Artigo Original](https://martinfowler.com/articles/micro-frontends.html)

