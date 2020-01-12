---
layout: post
title:  "Micro Frontends"
date:   2020-01-01 17:59:38 -0200
categories: jekyll update
---


>Bom desenvolvimento de front-end é difícil. Escalar o desenvolvimento de front-end para que muitas equipes possam trabalhar simultaneamente em um produto grande e complexo é ainda mais difícil. Neste artigo, descreveremos uma tendência recente de dividir monólitos de front-end em muitas partes menores e mais gerenciáveis, e como essa arquitetura pode aumentar a eficácia e a eficiência das equipes que trabalham no código de front-end. Além de falar sobre os vários benefícios e custos, abordaremos algumas das opções de implementação disponíveis e mergulharemos em um aplicativo de exemplo completo que demonstra a técnica.

## CONTEÚDO ##

* [Benefícios](#beneficios)
    * [Atualizações incrementais]()
    * [Bases de código simples e dissociadas]()
    * [Implantação independente]()
    * [Equipes autônomas]()
    * [Em poucas palavras]()
* [O exemplo]()
* [Abordagens de integração]()
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

---

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

## Benefícios ##

Em vez de definir micro frontends em termos de abordagens técnicas específicas ou detalhes de implementação, colocamos ênfase nos atributos que surgem e nos benefícios que eles oferecem.

## Atualizações incrementais ## 

Para muitas organizações, este é o começo de sua jornada de micro frontends. O velho e grande monólito de front-end está sendo retido pela pilha de tecnologia do passado, ou pelo código escrito sob pressão de entrega, e está chegando ao ponto em que uma reescrita total é tentadora. Para evitar os [riscos](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/) de uma reescrita completa, preferimos [estrangular](https://martinfowler.com/bliki/StranglerApplication.html) o aplicativo antigo, peça por peça, e, enquanto isso, continuamos a oferecer novos recursos aos nossos clientes sem ser sobrecarregados pelo monólito.

Isso geralmente leva a uma arquitetura de micro frontends. Uma vez que uma equipe teve a experiência de obter um recurso até a produção, com poucas modificações no velho mundo, outras equipes também vão querer se juntar ao novo mundo. O código existente ainda precisa ser mantido e, em alguns casos, pode fazer sentido continuar adicionando novos recursos, mas agora a opção está disponível.

O fim do jogo aqui é que temos mais liberdade para tomar decisões caso a caso em partes individuais de nosso produto e fazer atualizações incrementais em nossa arquitetura, nossas dependências e nossa experiência do usuário. Se houver uma mudança significativa em nossa estrutura principal, cada micro front-end poderá ser atualizado sempre que fizer sentido, em vez de ser forçado a parar o mundo e atualizar tudo de uma vez. Se quisermos experimentar novas tecnologias ou novos modos de interação, podemos fazê-lo de maneira mais isolada do que antes.

## Bases de código simples e dissociadas

O código fonte de cada micro front-end individual será, por definição, muito menor que o código-fonte de um único front-end monolítico. Essas bases de código menores tendem a ser mais simples e fáceis para os desenvolvedores trabalharem. Em particular, evitamos a complexidade decorrente do acoplamento não intencional e inadequado entre componentes que não devem se conhecer. Ao desenhar linhas mais grossas em torno dos [contextos limitados](https://martinfowler.com/bliki/BoundedContext.html) do aplicativo, dificultamos o surgimento de um acoplamento acidental.



--- 

[Artigo Original](https://martinfowler.com/articles/micro-frontends.html)

