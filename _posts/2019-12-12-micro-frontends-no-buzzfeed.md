---
layout: post
title:  "Micro Frontends no BuzzFeed"
date:   2019-12-12 17:59:38 -0200
categories: jekyll update
---

A definição do que constitui um "micro Frontend" talvez ainda não tenha chegado a um consenso. O [smart folks at DAZN](https://medium.com/dazn-tech/orchestrating-micro-frontends-a5d2674cbf33) considera uma série de páginas completas gerenciadas por um orquestrador do lado do cliente. Outras abordagens, como o OpenComponents , compõem páginas únicas de vários micro frontends.


O caso de uso do BuzzFeed se encaixa em algum lugar entre os dois. Eu não diria que temos uma arquitetura de micro frontend; no entanto, nós os alavancamos em algumas partes da página. Consideramos algo como um micro front-end se a API retornar html totalmente renderizado (e ativos), mas não um elemento ```<html>``` ou ```<body>```.

Temos três micro frontends: o componente do cabeçalho, o conteúdo da postagem e nossas incorporações interativas. Cada um deles adotou a abordagem de micro front-end porque apresentava problemas de negócios reais e distintos.

## Micro Frontend # 1: O cabeçalho

Por quê? Distribuição de componentes

![](https://miro.medium.com/max/1600/0*dOnfRQsyxQq4SkX0)

Este é o cabeçalho do buzzfeed.com. Ele possui uma leve camada de configuração e uma quantidade razoável de código por trás dele: certamente o suficiente para merecer uma abstração em vez de duplicá-la em todos os nossos serviços.


Originalmente, fizemos essa abstração e a extraímos em um pacote npm, cujos serviços importaram como parte de seu processo de criação. Isso nos permitiu remover a duplicação e fazer com que o serviço agrupasse o cabeçalho como parte de seu próprio processo de compilação (o que significa que poderíamos deduplicar facilmente códigos e bibliotecas comuns).


Com apenas dois ou três serviços, essa técnica funciona muito bem, mas temos mais de dez serviços de renderização no buzzfeed.com. Isso significava que toda vez que desejávamos fazer uma alteração no cabeçalho, tínhamos que fazer as seguintes alterações mais de 10 vezes:



1. Atualize o código no cabeçalho
2. Fazer uma solicitação pull
3. Mesclar e publicar para npm
4. Atualize o serviço package.json
5. Fazer uma solicitação pull
6. Mesclar e implantar o serviço


Isso tornou-se extremamente demorado e levou as equipes a evitar alterações no cabeçalho por causa disso. Claro, existem maneiras pelas quais poderíamos ter aprimorado esse fluxo de trabalho (por exemplo, usando sempre solto e apenas reconstruindo o serviço, automatizando a atualização e a criação de PRs de serviço), mas ainda assim parecia a abordagem errada. Ao mudar para um padrão de micro front-end, agora podemos distribuir o cabeçalho instantaneamente para todos os serviços e o fluxo de trabalho para atualizá-lo em todo o site buzzfeed.com agora:

1. Atualize o código no cabeçalho
2. Fazer uma solicitação pull
3. Implantar o cabeçalho

## Micro Frontend # 2: Publicar conteúdo (ou como chamamos: The Subbuzzes)

Por quê? Para manter um contrato com o CMS

Temos alguns "destinos" diferentes (por exemplo, BuzzFeed e BuzzFeed News) para o nosso conteúdo, mas cada um deles é alimentado por um único CMS. Cada destino é seu próprio serviço (ou vários serviços) que se conecta às nossas APIs de conteúdo. Isso significa que temos a capacidade de renderizar o mesmo conteúdo em vários destinos; no entanto, na prática, escolhemos não.


![](https://miro.medium.com/max/1600/0*UZyp02pqT1yv_xOX)

O mesmo conteúdo renderizado em três destinos diferentes do BuzzFeed.

Isso também significa que precisamos manter um contrato entre as APIs de CMS / Conteúdo e os serviços de renderização. Para ilustrar isso, é mais fácil focar em um exemplo.

Quando um editor deseja adicionar uma imagem à página, ele seleciona a imagem "sub-buzz" no CMS e a carrega. Eles então têm a opção de adicionar extensões a essa imagem. Uma dessas extensões é a capacidade de marcar a imagem como mostrando o Conteúdo Gráfico. A intenção de adicionar esta extensão é que a imagem fique embaçada e o usuário tenha que optar por vê-la (isso é particularmente importante no conteúdo de notícias confidenciais). No entanto, na medida em que o CMS se importa, tudo isso significa um valor booleano armazenado em uma imagem. Como o CMS depende dos serviços de renderização para adicionar uma sobreposição desfocada, acabamos com um acoplamento implícito entre os dois. Se um destino falhasse no suporte a esse recurso, os usuários seriam expostos ao conteúdo gráfico e teríamos falhado em manter as intenções dos editores.

Então, o que isso tem a ver com o Micro Frontends?

Poderíamos optar por abstrair esses modelos de sub-buzz em um pacote npm e compartilhá-los entre os destinos; no entanto, quando alteramos o suporte para algo no CMS, precisamos dos serviços de renderização para poder refletir isso imediatamente. O CMS é implantado em um estado sem versão e as APIs de conteúdo apenas expõem os principais números de versão. Acoplá-los a pacotes npm usando o semver e implantados por meio de um pacote dificultaria a permanência em sincronia. Movendo as sub-vibrações atrás de uma API HTTP, podemos atualizar o contrato de rendering-cms em todos os destinos imediatamente e garantir que cada destino ofereça suporte aos recursos mais recentes do CMS.

## Micro Frontend nº 3: incorporações (plataforma de formato Buzz)

Por quê? Independência da plataforma

Talvez o caso de uso mais claro para o Micro Frontends: o Embed. Hospedamos uma tonelada de incorporações (Instagram, Twitter etc.), incluindo incorporações de terceiros. Chamamos esses BFPs de Buzz Format Platform, que podem ser desde uma inscrição em um boletim informativo até um formato de questionário altamente reutilizável ou um formato sob medida para apoiar uma história de investigação.

O ponto de entrada para uma incorporação geralmente é um iframe ou um elemento de script, portanto, não é realmente qualificado como o Micro Frontends. Rompemos esse molde (sempre que possível), processando-os no servidor e incluindo o DOM retornado diretamente na página. Fazemos isso para que possamos processar as incorporações em formatos distribuídos (como nosso BuzzFeed Mobile App ou Facebook Instant Articles), além de expor o conteúdo aos rastreadores de mecanismos de pesquisa.

O BFP oferece independência da plataforma e dá aos engenheiros a sensação de trabalhar em um pequeno componente sem ter que considerar o ecossistema mais amplo do BuzzFeed. Esse sentimento é o que sempre tentamos obter ao criar ambientes de desenvolvedor e o Micro Frontends certamente oferece essa oportunidade.

## Os trade-offs

Uma arquitetura de micro front-end pode oferecer uma ótima experiência para o desenvolvedor e muita flexibilidade, mas elas não são de graça. Você as troca contra:

**Recursos maiores do lado do cliente ou orquestração mais difícil**

Compomos nossas micro frontends no navegador, o que significa que não há um processo de compilação singular que pode otimizar e desduplicar dependências compartilhadas. Para conseguir isso no nível do navegador, você precisa dividir todas as dependências por código e certificar-se de usar as mesmas versões - ou criar em uma camada de orquestração.

**Maior risco ao liberar atualizações**

Assim como somos capazes de distribuir novas alterações instantaneamente em muitos serviços, também podemos distribuir bugs e erros. Esses erros também aparecem no tempo de execução, e não no tempo de compilação ou no IC. Usamos esse risco elevado como uma oportunidade para nos concentrarmos mais em testes e garantir que o contrato de componentes seja mantido.

Também houve críticas de que as micro interfaces tornam mais difícil ter um UX coeso, mas isso não é algo que experimentamos. Todos esses micro frontend herdam padrões de design e componentes menores por meio de pacotes compartilhados.

No geral, o padrão de micro front-end funcionou bem para o BuzzFeed Tech nesses casos de uso e foi bem testado nos últimos um a dois anos. 

Definitivamente, existe um ponto de inflexão em que ter muito mais deles exigiria mais trabalho para compensar a primeira troca, mas achamos que ainda não estamos lá e não esperamos estar lá tão cedo - abstraindo componentes para compartilhamento pacotes funcionam bem para a maioria dos nossos casos. Onde isso não acontece, é bom ter outro padrão arquitetural para alcançar.

>...

A BuzzFeed Tech está contratando. Se você estiver interessado em navegar pelas aberturas, acesse buzzfeed.com/jobs . Temos papéis em Los Angeles, Minneapolis, Londres e Nova York!

Você também pode descobrir algumas das novidades que estamos lançando no BuzzFeed Tech seguindo nosso twitter, @buzzfeedexp !

---

[BuzzFeed](https://tech.buzzfeed.com/micro-frontends-at-buzzfeed-b8754b31d178)
