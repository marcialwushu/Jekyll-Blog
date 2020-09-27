---
layout: post
title:  "Usando microsserviços em .Net Core e container Docker"
date:   2020-03-06 17:59:38 -0200
categories: jekyll update
---

## Introdução

Durante este artigo, aprenderemos como trabalhar com os padrões de arquitetura de microsserviço e contêineres Docker usando a plataforma .NET Core 3 para construir um sistema distribuído.

## Arquitetura monolítica vs arquitetura de microsserviços

Antes de falar sobre microsserviços, precisamos entender a diferença entre a abordagem de aplicativo tradicional e a abordagem de aplicativo de microsserviços.

![](https://miro.medium.com/max/700/1*6iFbmAd5ME5eHjEMqGdHHA.png)

>https://martinfowler.com/articles/microservices.html

Qualquer aplicativo é construído como uma coleção de serviços que podem ser desenvolvidos, testados, com versões, implantados e escalados.

Para aplicativos monolíticos, Escalas é feito clonando o aplicativo em vários servidores - VMs.

Mas, para microsserviços, o dimensionamento é feito pela implantação de cada um de forma independente com várias instâncias em servidores - VMs.

![](https://miro.medium.com/max/700/1*poYG_SVBsal_bdfG0RvAGA.png)

>Arquitetura monolítica vs arquitetura de microsserviços

Ao desenvolver um aplicativo do lado do servidor, você pode iniciá-lo com uma arquitetura modular hexagonal ou em camadas que consiste em diferentes tipos de componentes ou camadas:

- **Camada de apresentação** - camada de IU, pode ser um aplicativo da web, móvel ou desktop.
- **Camada de serviços** - responsável por lidar com solicitações HTTP e responder com HTML ou JSON/XML (para APIs de serviços da web).
- **Camada de lógica de negócios** - a lógica de negócios do aplicativo.
- **Camada de acesso ao banco de dados** - objetos de acesso aos dados responsáveis pelo acesso ao banco de dados.

Apesar de ter uma arquitetura logicamente modular, o aplicativo é empacotado e implantado como um monólito.

Os aplicativos monolíticos são mais de um único pacote completo, tendo todos os componentes e serviços necessários relacionados encapsulados em um pacote.

Mas, para microsserviços, a ideia é simples, consiste em dividir seu aplicativo em um conjunto de serviços menores e interconectados em vez de construir um único aplicativo monolítico. Cada microsserviço é um pequeno aplicativo que possui sua própria arquitetura hexagonal consistindo em lógica de negócios junto com vários adaptadores. Alguns microsserviços exporiam um REST, RPC ou API baseada em mensagem e a maioria dos serviços consomem APIs fornecidas por outros serviços. Outros microsserviços podem implementar uma IU da web.


Os microsserviços são implantados independentemente com seu próprio banco de dados por serviço, portanto, o subjacente.

## Arquitetura e padrões de microsserviços

Uma coisa sobre microsserviços é que existem diferentes coisas que você pode usar, essas tecnologias para microsserviços ou não, mas se escolhermos construir e arquitetar um microsserviço, existem muitos padrões, a maioria deles relacionados ou provenientes de um design orientado por domínio. Vou falar sobre alguns deles depois.

![](https://miro.medium.com/max/700/1*iwABO73Wp7MdG9JfjqsFuQ.png)

>Padrões e tecnologias de estilo de arquitetura de microsserviços

## Estilo de arquitetura de microsserviços

![](https://miro.medium.com/max/700/1*m4Q4ojNKiqKREv4DKiqJmg.png)

>Estilo de arquitetura de microsserviços

Os desenvolvedores consideram os microsserviços como um estilo de arquitetura que promove o desenvolvimento de aplicativos complexos como um conjunto de pequenos serviços baseados em recursos de negócios e vários subsistemas independentes na forma de serviços autônomos .

A imagem a seguir mostra o estilo de arquitetura de microsserviços.

>Existem vários componentes em uma arquitetura de microsserviços além dos próprios microsserviços.

Começamos com um cliente que interage com um servidor usando uma autenticação usando o **provedor de identidade** que gerencia as informações de identidade e fornece serviços de autenticação em uma rede distribuída. Para garantir essa interação, precisamos de um ponto de entrada do cliente que é o **API Gateway** . É um único ponto de contato do cliente que, por sua vez, retorna respostas de microsserviços subjacentes e às vezes uma resposta agregada de vários microsserviços, em nosso esquema, temos quatro serviços que usam o **Gerenciamento** que mantém os nós para o serviço. E para manter o controle de serviços e endereços de serviço e endpoints, usamos o **Service Discovery**.


Temos **CDN** que é uma rede de distribuição de conteúdo para servir recursos estáticos. Por exemplo, páginas e conteúdo da web em uma rede distribuída e o **Conteúdo Estático** são recursos estáticos como páginas e conteúdo da web.

Falaremos mais detalhadamente sobre o API Gateway:

![](https://miro.medium.com/max/700/1*dfH4NJ1D8w5zY3U3DRNrPw.png)

>Gateway API

Um gateway de API está localizado entre os clientes e os serviços. Ele atua como um proxy reverso, roteando solicitações de clientes para serviços. Ele também pode executar várias tarefas multifuncionais, como autenticação, encerramento de SSL e limitação de taxa. Se você não implantar um gateway, os clientes deverão enviar solicitações diretamente aos serviços de front-end.

Isso cria um acoplamento entre o cliente e o servidor. O cliente deve saber como cada serviço foi dividido. isso torna a manutenção do cliente mais difícil e os serviços de refatoração.

Agora, precisamos implantar nossos serviços no contêiner, para fazer isso, usaremos o Docker.

## Container Docker

![](https://miro.medium.com/max/700/1*qamIVeRVa8gc9Efzt6swFQ.png)


Docker é uma ferramenta que facilita a criação, implantação e execução de aplicativos usando uma abordagem de contêiner.

Esses contêineres são leves e levam menos tempo para inicializar do que os servidores tradicionais. Esses contêineres também aumentam o desempenho e reduzem custos, ao mesmo tempo em que fornecem gerenciamento adequado de recursos. Outra vantagem do Docker é que não é mais necessário pré-alocar RAM para cada container.

### Microsserviço usando ASP.NET Core

E antes de começarmos a modelar nossa arquitetura de microsserviços usando as estratégias e técnicas deste curso, precisamos de um problema para resolver, e é aqui que entra este estudo de caso. E nosso estudo de caso é baseado em agendamento de consultas médicas.

#### Ambiente de Pré-requisitos

- Visual Studio 2019 ou 2017 tem suporte integrado para Docker
- O Windows 10 é necessário para a instalação do Docker.
- SDK do .NET Core
- Docker para Windows
- Ferramentas Docker

#### Criando uma solução de aplicativo Asp.NET Core 3

Comecei com essa solução antiga, o aplicativo N-Layered e inclui APIs da Web. E precisamos mudar isso para microsserviços.

GitHub: https://github.com/didourebai/Plateforme.AlloTabib-Before

![](https://miro.medium.com/max/700/1*qMmzM4mOnoxxH74E1IXUJQ.png)

>Arquitetura monolítica em camadas N

Este aplicativo possui esta estrutura:

- Camada de serviço: inclui todas as APIs usadas e integra a estrutura swagger.

![](https://miro.medium.com/max/700/1*fdrpi31RW8k4IDphUuJfgQ.png)

>APIs da Web e Swagger

![](https://miro.medium.com/max/700/1*C8LXlio4_XPdc9COqxtWbA.png)

>API de conta de usuário

- Camada de aplicativo e domínio: esta é a camada de negócios.
- Duas aplicações web: usando MVC 4 e AngularJS.
- A camada de infraestrutura é a camada de acesso ao banco de dados.

Criamos uma nova solução em branco para incluir todos os projetos de API que são nossos serviços:

![](https://miro.medium.com/max/700/1*Q3qGdjW3fwjJxzHW_5gCPQ.png)

>Visual Studio 2019

![](https://miro.medium.com/max/700/1*MxvFDiZJX7TpjKezeTGw7w.png)

>API com Docker habilitado

Ou se pudermos usar o Docker com um orquestrador Kubernetes, ele está pronto para o aplicativo da Web principal:

![](https://miro.medium.com/max/700/1*aCDByTsVUKm1ptJUsPBjOQ.png)

>Docker e Kubernetes

![](https://miro.medium.com/max/700/1*c-c2XBxUm5mCfz9w6PehIQ.png)

>API

### Envie imagens do Docker para o Azure Container Registry

![](https://miro.medium.com/max/700/1*HW1PI2e2bGAT-qRndsjQXA.png)

## HTTP Client Factory

Para garantir um aplicativo em nuvem resiliente, precisamos implementar uma comunicação resiliente com os aposentados.
Para implementar isso, usamos a melhor biblioteca para novas tentativas e o sql breaker é o Poly, um código aberto. Portanto, você pode manipular ou implementar HttpClient em sua aplicação com Http Factory em .net Core.


## Orquestradores no Azure

Podemos usar o Kubernetes com Docker ou Service Fabric se nossos microsserviços forem baseados em processos simples e forem mais usados ​​para serviços com estado.


![](https://miro.medium.com/max/700/1*Q-w8sjfEaAtRgAELmt7jfw.png)

>Orquestradores no Azure


## Conclusão

Este artigo foi uma visão geral sobre microsserviços com Docker, microsserviços permitem evoluir, implantar e dimensionar partes do aplicativo de forma independente, mas não podemos usar essa arquitetura para aplicativos pequenos porque é dedicada a desafios de software distribuído e para aplicativos escalonáveis e em evolução de longo prazo.

---

Autor: [Rebai Hamida](https://medium.com/@didourebai?source=follow_footer--------------------------follow_footer-----------)

[Artigo Original](https://medium.com/@didourebai/using-microservices-in-net-core-and-docker-container-c202785dd295)



