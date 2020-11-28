---
layout: post
title:  "I-Tier - Desmontando o Monolito"
date:   2020-03-12 17:59:38 -0200
categories: jekyll update
---

Nós [completamos recentemente](https://engineering.groupon.com/2013/node-js/geekon-i-tier/) um projeto de um ano para migrar o tráfego na web US Groupon a partir de uma aplicação monolítica Ruby on Rails para uma nova pilha Node.js com resultados substanciais.

Todo o frontend da web do Groupon nos EUA tem sido uma única base de código Rails desde seu início. A base de código do front-end cresceu rapidamente, o que dificultou a manutenção e desafiou o envio de novos recursos. Como solução para esse monólito gigantesco, decidimos redesenhar o frontend dividindo-o em peças pequenas, independentes e mais gerenciáveis. No centro deste projeto, reconstruímos cada seção principal do site como um aplicativo Node.js independente. Também reconstruímos a infraestrutura para fazer todos os aplicativos independentes funcionarem juntos. O resultado foi o nível de interação (I-Tier).

Alguns dos destaques desta grande migração de arquitetura incluem o seguinte:

- Os carregamentos de páginas são significativamente mais rápidos em todo o site
- Nossas equipes de desenvolvimento podem desenvolver e enviar recursos mais rapidamente e com menos dependências de outras equipes
- Podemos eliminar implementações redundantes dos mesmos recursos em diferentes países onde o Groupon está disponível

Esta postagem é a primeira de uma série sobre como reformulamos o site e os grandes benefícios que estamos vendo que serão essenciais para impulsionar os negócios da Groupon. Leia a história completa.

## Um pouco de história

O Groupon começou como uma única página da web que mostrava uma oferta por dia para pessoas em Chicago. Um exemplo de negócio típico pode ser algo como um desconto em um restaurante local ou um ingresso para um evento local. Cada negócio tinha um “ponto de inflexão” - o número mínimo de pessoas que precisavam comprar o negócio para que fosse válido. Se um número suficiente de pessoas comprasse o negócio chegando ao ponto de inflexão, todos teriam o desconto. Caso contrário, ninguém conseguiu o desconto.

O site foi originalmente construído como um aplicativo Ruby on Rails. Rails foi uma ótima escolha no começo, pois foi uma das maneiras mais fáceis para a pequena equipe de desenvolvimento que tínhamos de colocar nosso site em funcionamento rapidamente. Também foi fácil implementar novos recursos no Rails; isso foi um grande trunfo para nós no início, pois o conjunto de recursos estava em constante evolução.

A arquitetura original do Rails era muito simples:

![](https://engineering.groupon.com/wp-content/blogs.dir/3/files/2013/10/arch.png)

No entanto, rapidamente superamos a capacidade de servir todo o nosso tráfego por meio de um único aplicativo Rails apontando para um único cluster de banco de dados. Adicionamos mais servidores front-end e réplicas de banco de dados e colocamos tudo atrás de um CDN, mas isso só funcionou até que as gravações do banco de dados se tornassem um gargalo. O processamento de pedidos causou várias gravações no banco de dados; como resultado, decidimos mover esse código de nosso aplicativo Rails para um novo serviço com seu próprio cluster de banco de dados.

Continuamos seguindo este padrão de quebrar a funcionalidade de back-end existente em novos serviços, mas o resto do site (visualizações, controladores, ativos, etc) permaneceu parte do aplicativo Rails original:

![](https://engineering.groupon.com/wp-content/blogs.dir/3/files/2013/10/arch2.png)

Essa mudança na arquitetura nos deu tempo, mas sabíamos que seria apenas temporária. A base de código ainda era gerenciável para a pequena equipe de desenvolvimento que tínhamos na época e nos permitiu evitar que o site falhasse durante o pico de tráfego.

## Tornar-se global

Nessa época, o Groupon começou a se expandir internacionalmente. Em um curto período, deixamos de operar apenas nos EUA para expandir nossas operações em 48 países diferentes. Ao longo do caminho, também adquirimos várias empresas internacionais, como a CityDeal . Cada aquisição veio com sua própria pilha de software pré-existente.

A arquitetura CityDeal era semelhante à arquitetura Groupon, mas era uma implementação totalmente separada construída por uma equipe diferente. Como resultado, houve diferenças no design e na tecnologia - Java em vez de Ruby, Apache em vez de nginx, PostgreSQL em vez de MySQL.

![](https://engineering.groupon.com/wp-content/blogs.dir/3/files/2013/10/arch3b.png)

Como vemos nas empresas de rápido crescimento, tivemos que escolher entre desacelerar para integrar as diferentes pilhas ou manter os dois sistemas, sabendo que estávamos assumindo uma dívida técnica que teríamos que pagar mais tarde. Tomamos uma decisão intencional de manter as implementações nos EUA e na Europa separadas no início em troca de um crescimento mais rápido do negócio. E à medida que mais aquisições se seguiram, mais complexidade foi adicionada à arquitetura.

## Móvel

Também construímos clientes móveis para iPhone, iPad, Android e Windows Mobile; definitivamente não queríamos construir um aplicativo móvel diferente para cada país onde a Groupon operava. Em vez disso, decidimos construir uma camada de API no topo de cada uma de nossas plataformas de software de back-end; nossos clientes móveis conectados a qualquer terminal de API que corresponda ao país do usuário:

![](https://engineering.groupon.com/files/2013/10/arch4.png)

Isso funcionou bem para nossa equipe móvel. Eles conseguiram construir um único aplicativo móvel que funcionou em todos os nossos países.

Mas ainda havia um problema. Sempre que criamos um novo produto ou recurso, primeiro o criamos para a web e, posteriormente, criamos uma API para que o recurso pudesse ser implementado no celular. Estávamos repetindo nossos esforços.

Agora que quase metade do nosso negócio é móvel nos Estados Unidos, precisamos desenvolver uma mentalidade de dispositivos móveis primeiro. Conseqüentemente, queremos uma arquitetura em que um único back-end possa atender clientes móveis e da Web com o mínimo de esforço de desenvolvimento.

## Monolitos múltiplos

À medida que o Groupon continuou a evoluir e novos produtos foram lançados, a base de código do frontend Ruby ficou maior. Havia muitos desenvolvedores trabalhando na mesma base de código. Chegou ao ponto em que era difícil para os desenvolvedores executar o aplicativo localmente. As suítes de teste ficaram lentas e os testes instáveis ​​se tornaram um problema real. E, como era uma única base de código, o aplicativo inteiro precisava ser implantado de uma vez. Quando um problema de produção exigia uma reversão, as alterações de todos seriam revertidas, em vez de apenas o recurso quebrado. Resumindo, tínhamos todos os problemas de uma base de código monolítica que havia crescido muito.

Mas tivemos esse problema várias vezes. Não apenas tivemos que lidar com a base de código dos EUA, mas tivemos muitos dos mesmos problemas com a base de código europeia. Precisávamos redesenhar totalmente o front-end.

## Reescreva tudo!

Reconstruir todo o front-end é um empreendimento arriscado. Leva muito tempo envolvendo muitas pessoas diferentes e há uma chance real de você não chegar a nada melhor do que o antigo sistema. Ou pior - demora muito e você desiste no meio do caminho sem nenhum resultado para mostrar o esforço.

Mas tivemos grande sucesso no passado, reestruturando peças menores de nossa infraestrutura. Por exemplo, nosso site para celular e nosso site voltado para o comerciante foram reconstruídos com ótimos resultados. Essa experiência nos deu um bom ponto de partida e a partir dela traçamos objetivos claros para este projeto.

## Meta 1: Unificar nossos front-ends

Com várias pilhas de software implementando os mesmos recursos em diferentes países, não fomos capazes de nos mover tão rápido quanto desejávamos. Precisávamos eliminar a redundância em nossa pilha de software.

## Meta 2: colocar o celular no mesmo nível da web

Como quase metade de nossos negócios nos EUA é móvel, não podíamos nos dar ao luxo de construir uma versão para web e outra para celular. Precisávamos de uma arquitetura onde a web fosse apenas mais um cliente usando as mesmas APIs que nossos aplicativos móveis.

## Meta 3: tornar o site mais rápido

Nosso site estava mais lento do que queríamos. Na pressa de lidar com o crescimento do site, o front-end dos EUA acumulou dívidas de tecnologia, o que tornou sua otimização um desafio. Queríamos uma solução que não exigisse tanto código para atender a uma solicitação. Queríamos algo simples .

## Meta 4: deixe as equipes se moverem independentemente

Quando o Groupon foi lançado, o site era realmente simples. Mas, desde então, adicionamos muitas novas linhas de produtos com equipes de desenvolvimento com suporte localizadas em todo o mundo. Queríamos que cada equipe pudesse construir e implantar seus recursos de forma independente e rápida. Precisávamos quebrar a interdependência existente entre as equipes de produto porque tudo estava em uma única base de código.

## Aproximação

Primeiro, decidimos dividir cada recurso principal do site em um aplicativo da web separado:

![](https://engineering.groupon.com/wp-content/blogs.dir/3/files/2013/10/arch52.png)

Construímos uma estrutura de aplicativo da web em Node.js que incluía recursos comuns necessários a cada aplicativo para tornar mais fácil para nossas equipes construir esses aplicativos da web individuais.

## Barra lateral: Por que Node.js?

Antes de construir nossa nova camada de front-end, avaliamos várias pilhas de software diferentes para ver qual seria a mais adequada para nós.

Estávamos procurando uma solução para um problema muito específico - lidar com eficiência com muitas solicitações HTTP recebidas, fazer solicitações de API paralelas para atender a cada uma dessas solicitações HTTP e renderizar os resultados em HTML. Também queríamos algo que pudéssemos monitorar, implantar e oferecer suporte com segurança.

Escrevemos protótipos usando várias pilhas de software e os testamos. Publicaremos um acompanhamento mais detalhado com os detalhes, mas no geral descobrimos que o Node.js é uma boa opção para esse problema muito específico.

## Abordagem, continuação ...

Em seguida, adicionamos uma camada de roteamento na parte superior que encaminha os usuários ao aplicativo apropriado com base na página que eles estavam visitando:

![](https://engineering.groupon.com/wp-content/blogs.dir/3/files/2013/10/arch6.png)

Construímos o serviço de roteamento Groupon (que chamamos de Grout) como um módulo nginx. Isso nos permite fazer muitas coisas interessantes, como conduzir testes A / B entre diferentes implementações do mesmo aplicativo em servidores diferentes.

E para fazer com que todos esses aplicativos da web independentes funcionem perfeitamente juntos, construímos serviços separados para compartilhar layouts e estilo, mantendo a configuração compartilhada e gerenciando tratamentos de teste A / B. Publicaremos mais detalhes sobre esses serviços no futuro.

Tudo isso fica na frente de nossa API e nada na camada de front-end pode se comunicar diretamente com um banco de dados ou serviço de back-end. Isso nos permite construir uma única camada de API federada que atende aos nossos aplicativos da web e móveis:

![](https://engineering.groupon.com/wp-content/blogs.dir/3/files/2013/10/arch7a.png)

Estamos trabalhando na unificação de nossos sistemas de back-end, mas, no curto prazo, ainda precisamos oferecer suporte a nossos back-ends dos EUA e da Europa. Portanto, projetamos nosso front-end para funcionar nos dois back-ends ao mesmo tempo:

![](https://engineering.groupon.com/wp-content/blogs.dir/3/files/2013/10/arch9b.png)

## Resultados

Acabamos de migrar nosso front-end dos EUA de Ruby para nossa nova infraestrutura Node.js. O antigo front-end monolítico foi dividido em aproximadamente 20 aplicativos da web separados, cada um dos quais uma reescrita limpa. No momento, estamos atendendo a 50 mil rpm desses servidores em um dia normal, mas esperamos múltiplos desse tráfego durante a temporada de férias. E esse número aumentará muito à medida que migrarmos pelo tráfego de nossos outros 48 países.

Estes são os benefícios que vimos até agora:

- Os carregamentos de páginas são mais rápidos em toda a linha - normalmente em 50%. Parte disso se deve a mudanças na tecnologia e parte porque tivemos a chance de reescrever todas as nossas páginas da web para ficarem muito mais finas. E ainda esperamos obter ganhos significativos aqui à medida que implementamos mudanças adicionais.
- Estamos atendendo à mesma quantidade de tráfego com menos hardware em comparação com a pilha antiga.
- As equipes podem implementar mudanças em seus aplicativos de forma independente.
- Conseguimos fazer alterações de design e recursos em todo o site muito mais rapidamente do que conseguiríamos com nossa arquitetura antiga.


No geral, essa migração tornou possível para nossas equipes de desenvolvimento enviar páginas mais rapidamente com menos interdependências e removeu algumas das limitações de desempenho de nossa plataforma antiga. Mas temos muitas outras melhorias planejadas para o futuro e publicaremos detalhes em breve.


---

Autor: [Adam Geitgey](https://engineering.groupon.com/author/ageitgey/)

[Artigo Original](https://engineering.groupon.com/2013/misc/i-tier-dismantling-the-monoliths/)
