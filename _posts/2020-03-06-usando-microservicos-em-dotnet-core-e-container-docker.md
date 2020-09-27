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

Começamos com um cliente que interage com um servidor usando uma autenticação usando o provedor de identidade que gerencia as informações de identidade e fornece serviços de autenticação em uma rede distribuída. Para garantir essa interação, precisamos de um ponto de entrada do cliente que é o API Gateway . É um único ponto de contato do cliente que, por sua vez, retorna respostas de microsserviços subjacentes e às vezes uma resposta agregada de vários microsserviços, em nosso esquema, temos quatro serviços que usam o Gerenciamento que mantém os nós para o serviço. E para manter o controle de serviços e endereços de serviço e endpoints, usamos o Service Discovery.




