---
layout: post
title:  "Como criar uma arquitetura front-end escalável e sustentável"
date:   2019-12-31 17:59:38 -0200
categories: jekyll update
---


As estruturas e bibliotecas front-end modernas facilitam a criação de [componentes reutilizáveis da interface do usuário](https://kevtiq.co/blog/interfacing-your-ui-components/) . Este é um passo em uma boa direção para criar aplicativos front-end de manutenção. No entanto, em muitos projetos ao longo dos anos, descobri que fabricar componentes reutilizáveis geralmente não é suficiente. Meus projetos se tornaram insustentáveis, à medida que os requisitos mudavam ou novos requisitos surgiam. Levou mais e mais tempo para encontrar o arquivo correto ou depurar algo em muitos arquivos.

Mudança precisava acontecer. Posso melhorar minhas habilidades de pesquisa ou ser mais experiente no uso do Código do Visual Studio. Mas, muitas vezes, não sou o único trabalhando no front-end. Portanto, precisamos configurar nossos projetos de front-end. Precisamos torná-los sustentáveis ​​e escaláveis. Isso significa que podemos aplicar alterações nos recursos atuais, mas também adicionar novos recursos mais rapidamente.

## Localizando uma arquitetura escalável

No desenvolvimento tradicional, temos muitos [padrões arquiteturais](https://en.wikipedia.org/wiki/Software_design_pattern) que podemos seguir. Dois deles ainda populares são o  [domain-driven development (DDD)](https://martinfowler.com/bliki/BoundedContext.html) e a [separation of concerns (SoC)](https://en.wikipedia.org/wiki/Separation_of_concerns) . No desenvolvimento front-end, eles também podem ser de grande valor. Com o DDD, você tenta agrupar recursos semelhantes e separá-los o máximo possível de outros grupos (por exemplo, módulos). Enquanto no SoC, por exemplo, separamos lógicas, visualizações e modelos de dados (por exemplo, usando o padrão de design MVC ou MVVM).

Esperamos que aplicativos modernos de front-end façam cada vez mais trabalhos pesados. Com essa complexidade adicional, os bugs estão se tornando mais frequentes. Precisamos de uma arquitetura confiável, que seja sustentável e escalável. Meu objetivo era, e ainda é, encontrar uma arquitetura front-end que seja independente da estrutura. A arquitetura deve fornecer um desenvolvedor ou uma equipe para criar um front-end escalável. Ao adotar a arquitetura (por exemplo, remover peças), você pode adaptá-la a projetos pequenos e grandes.

![](https://kevtiq.co/static/5c7f0e7136f7083da337533c07a075d1/4c1a3/architecture-high-level.png)

## Preenchendo os detalhes

Nosso objetivo como desenvolvedores de front-end é agregar valor aos nossos usuários, permitindo que eles interajam com o nosso trabalho. Quando o fizerem, o roteamento do aplicativo guiará o usuário para o módulo correto. Cada módulo pode é um domínio separado. A lógica de negócios molda esses domínios. Vários módulos usam essa lógica, como recuperar dados de um serviço de back-end. Essa lógica é colocada na camada de aplicação. Essa é a configuração principal de uma arquitetura front-end escalável.

Ao olhar para uma estrutura de projeto, podemos seguir algo como mostrado abaixo. Todo o código da camada principal está no ```app``` diretório Embora todos os módulos tenham um diretório no ```modules``` diretório Os componentes reutilizáveis da interface do usuário (por exemplo, tabelas) que não dependem da lógica de negócios estão no ```components``` diretório


```
src/
├── assets/
├── components/
├── core/
├── lib/
├── modules/
└── styles/
```

Os diretórios restantes mantêm nossas ```assets``` funções estáticas (por exemplo, imagens) ou auxiliares ```lib```. Elas podem diferir das funções simples do utilitário à lógica complexa de layout automático dos gráficos ou até conter os ganchos de reação genéricos. Finalmente, temos um ```styles``` diretório. Muitos preferem algo parecido ```CSS-in-JS``` ou componentes estilizados . Prefiro uma arquitetura CSS sólida, como o [ITCSS de Harry Roberts](https://csswizardry.com/2018/11/itcss-and-skillshare/) , que segue a mentalidade SoC da arquitetura.

O acima não parece algo especial. Essa é uma abordagem modular padrão para desenvolvimento. Porém, ao ampliar um módulo e a camada principal, a arquitetura brilha. Abaixo, eu ampliei a camada principal e um único módulo. No restante desta postagem do blog, discuto cada um dos diferentes tópicos e as idéias por trás deles. As conexões pontilhadas são conexões opcionais que você pode usar quando quiser uma arquitetura menos complexa. Nesse caso, o pub / sub e os trabalhadores são removidos da arquitetura e os controladores conversam diretamente com as lojas e os clientes da API.

![](https://kevtiq.co/static/18409a5774708c3d4107a316bd76db07/b77c0/architecture-detailed.png)


## A espinha dorsal do aplicativo

A camada principal é a espinha dorsal da arquitetura. O objetivo desta parte do aplicativo é ser escalável e independente da estrutura. Existem algumas partes principais nessa camada: clientes de API, um pub / sub e uma ou mais lojas. Você também pode ter alguns [trabalhadores da Web](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) em execução nesse nível. Lojas vêm em vários tamanhos. À primeira vista, você pode pensar no estado do aplicativo. E você está certo, essa é uma loja. Mas e a pilha de histórico do usuário? Este é, de fato, outro exemplo de loja.

Quando você olha para as lojas sob essa luz, encontra muitas delas. Estado do aplicativo, histórico de navegação, gerenciamento de sessões, caches de API e histórico do criador de logs. Eles devem residir no nível do aplicativo. Isso também significa que eles devem ser configurados aqui. Você pode, por exemplo, fazer o download do [pacote de histórico no npm](https://www.npmjs.com/package/history) e usá-lo no histórico de navegação. Na loja, você pode expandir o pacote adicionando suas funções (por exemplo, uma diferente ```push```). Agora você também pode expô-los ao restante do seu aplicativo.

Por outro lado, temos um ou mais clientes API. Alguns de nossos projetos têm um serviço de back-end dedicado para conversar. Seja um gateway de API no topo de um cluster [Kubernetes](https://kubernetes.io/) com muitos microsserviços ou um único back-end de monólito. Mas, às vezes, precisamos nos conectar a diferentes serviços externos. Cada um desses serviços requer configuração (por exemplo, autenticação). Todas essas configurações e clientes chamados residem na camada principal. Dessa forma, eles podem ser usados ​​por todos os módulos.

![](https://kevtiq.co/static/e2b0787093463e969df68e0a06a6fb6e/59594/architecture-pubsub.png)

As diferentes lojas e clientes da API podem se tornar um problema de consistência. Tente combinar solicitações GraphQL e solicitações REST para mostrar os dados corretos. Usando um pub / sub, podemos generalizar como os controladores interagem com todas as diferentes partes desse nível. Eles publicam eventos de solicitação e assinam eventos de resposta. Isso remonta quantas bibliotecas modernas de gerenciamento de estado funcionam. Outra vantagem dessa abordagem é que você pode alterar uma API do cliente, sem que os módulos saibam.

Tudo isso soa como um exagero para aplicativos menores, e muitas vezes pode ser. Você pode reduzir a complexidade nessa arquitetura. Quando você possui apenas um único cliente de API, pode remover o pub / sub. Nesse caso, você pode 'conversar' com o cliente da API e as diferentes lojas.

Uma estrutura de projeto correspondente para o ```app``` diretório pode ser algo como:


```
.
└── core/
    ├── apis/
    ├── config/
    ├── controllers/
    ├── events/
    ├── lib/
    ├── models/
    ├── stores/
    ├── workers/
    └── index.js
    
```

A maioria dos diretórios dentro da ```app``` pasta deve ser auto-explicativa agora. Os diretórios ```controllers``` e ```models``` compartilham o mesmo objetivo que aqueles dentro de um módulo. O ```lib``` diretório contém todas as funções auxiliares (por exemplo, uma ```createPubSub``` função). Por último, podemos ter eventos agendados (por exemplo, um evento de logoff automático) armazenados no ```events``` diretório.


## módulos, módulos e mais módulos

O que define um módulo e como ele é separado dos componentes complexos da interface do usuário? A palavra-chave aqui é lógica de negócios . Leve tudo para carregar um arquivo. Você pode combinar componentes genéricos como uma zona de arrastar e soltar. Porém, o upload real é diferente para cada aplicativo, guiado por escolhas tecnológicas. Ao combinar o componente da interface do usuário e a ação real para fazer upload de um arquivo, criamos um pequeno módulo contido. No momento em que combinamos componentes com a lógica de negócios, os convertemos em módulos.

O diagrama detalhado da arquitetura já mostra as partes internas de um módulo. A estrutura de um módulo é inspirada nas idéias do MVC e MVVM. Na maioria das vezes, o roteamento do aplicativo aponta para um módulo específico. O roteamento do próprio módulo determina qual página ele carrega, ou seja, uma única página está vinculada a uma única rota. Uma página é o que um usuário vê e compreende dos componentes e controladores da interface do usuário.

Controladores são um termo abrangente para ações e interfaces. Usuários externos acionam ações quando interagem com nossos aplicativos. As interfaces ouvem alterações nos estados, seja no módulo ou em algum outro lugar do aplicativo. Na maioria dos casos, eles são (parcialmente) separados dos componentes da interface do usuário. Mas eles também podem viver no seu componente. Se eles não são necessários em outros componentes, por que separá-los? O contexto de reação com uma função redutora é um ótimo exemplo de um componente combinado. Tudo depende da complexidade do problema que você tenta resolver.

```
.
└── modules/
    └── users/
        ├── components/
        ├── config/
        │   ├── constants.js
        │   ├── routes.js
        │   ├── tables.js
        │   └── forms.js
        ├── controllers/
        ├── models/
        ├── pages/
        ├── queries/
        ├── state/
        └── index.js
        
```

Controladores são na maioria das vezes (pequenas) ações e, portanto, podem vir em diferentes formatos. Eles podem ser simples funções JavaScript (por exemplo, funções utilitárias) ou React Hooks. Mas podemos separá-los dos componentes no ```controllers``` diretório

Como a camada principal, um módulo pode ter seu próprio gerenciamento de estado e definições estáticas, ou seja, constantes. Nesse caso, vamos colocar esse código no ```state```, ```config``` e ```models``` diretórios (ou arquivos). Dependendo de nossos clientes de API, queremos definir e agrupar consultas (por exemplo, GraphQL). Estes devem estar no ```queries``` diretório.


## Compartilhamento entre módulos

Nunca vi um aplicativo no qual pudéssemos desacoplar completamente os módulos. É inevitável que você tenha que compartilhar modelos, controladores e componentes entre os módulos. Mas como os módulos podem interagir entre si?

O ```index.js``` arquivo de um módulo descreve quais componentes, controladores e modelos estão acessíveis para outros componentes. Assim, poderíamos usar uma zona de recebimento de arquivos ou o controlador de upload do módulo de arquivos. Mas, às vezes, temos que escolher o que estamos expondo para outros módulos. Será um controlador ou combinamos o controlador em um componente?

Vejamos o exemplo de um menu suspenso de usuário. Podemos criar uma ação que nos fornece todos os usuários que podemos selecionar entre diferentes módulos. Mas agora precisamos criar um menu suspenso específico em todos os outros módulos. Isso pode não exigir muito esforço para ter um componente suspenso genérico. Mas esse componente pode não funcionar em um formulário. Pode valer a pena o investimento para criar um ```UserDropdown``` componente que possamos usar. Quando algo muda em torno dos usuários, agora mudamos apenas um componente. Às vezes, precisamos escolher o que expor: controladores ou componentes.


## Anatomia do componente da interface do usuário

Ainda falta um último nível de detalhe, e essa é a arquitetura de um componente da interface do usuário. Em um post [anterior](https://kevtiq.co/blog/interfacing-your-ui-components/), eu já descrevi isso. Quando você olha para essa anatomia, verá alguns conceitos que aplicamos em uma escala maior.

![](https://kevtiq.co/static/bc2f240c52ba00eaa381ec6e71cb3f91/0e91d/architecture-component.png)

O front-end é o primeiro ponto de entrada para nossos usuários. Com nossos projetos de front-end crescendo em recursos, também apresentaremos mais bugs. Mas nossos usuários não esperam bugs e novos recursos rapidamente. Isto é impossível. No entanto, usando uma boa arquitetura, podemos apenas tentar conseguir isso o máximo possível.

## Conclusão

No desenvolvimento front-end, geralmente ajustamos nosso projeto à estrutura que usamos. Embora vivamos dentro de um ecossistema quando o fazemos, muitas vezes não é escalável para o futuro. Observando os conceitos existentes, podemos ajustar nossa visão sobre problemas de front-end. Vendo conceitos de front-end para o que são, podemos criar uma arquitetura escalável que funciona para pequenos ou grandes, muitos ou poucos.


---

Autor: [Kevin Pennekamp](https://dev.to/kevtiq)

[Artigo Original](https://kevtiq.co/blog/scalable-front-end-architecture/)


