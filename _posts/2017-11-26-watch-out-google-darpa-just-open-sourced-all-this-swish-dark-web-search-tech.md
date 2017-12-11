---
layout: post
title:  "Cuidado Google, DARPA libera todo o codigo fonte de tecnologia de motor de busca na Dark Web"
date:   2017-11-26 20:50:31 -0200
categories: jekyll update
---

![](https://blogs-images.forbes.com/thomasbrewster/files/2015/04/DIG1-e1429287668368-1940x1091.png)


O Google parece ser uma força indomável. Mas, com o lançamento de hoje do braço de pesquisa militar dos Estados Unidos das suas tecnologias de pesquisa do Memex e da pesquisa competitiva da Europa no gigante Mountain View, pode ser um momento propício para os empresários da tecnológia começarem a criar um assassino do Google.


As tecnologias de busca Memex da DARPA têm grande interesse devido à sua aplicação mainstream inicial: descobrir as operações de tráfico de pessoas que ocorrem na "dark web", o termo "catch-all" para as várias redes de internet que a maioria das pessoas nunca usam, como Tor, Freenet e I2P. E um número significativo de agências de aplicação da lei perguntaram sobre o uso da tecnologia. Mas Memex promete ser perturbador em ambos os mundos criminais e empresariais.


Christopher White, que lidera a equipe dos parceiros da Memex, que inclui membros do Tor Project, um punhado de universidades de prestígio, da NASA e empresas privadas focadas na pesquisa, diz a FORBES que o projeto é tão ambicioso em seu escopo, quer agitar um indústria de pesquisa sólida controlada por um punhado de empresas: Google, Microsoft e Yahoo.


![](https://blogs-images.forbes.com/thomasbrewster/files/2015/04/DIG2-1940x1285.jpg)

Colocando essas ideias grandiosas em ação, a DARPA abrirá hoje diversos componentes da Memex, permitindo que outros tomem as tecnologias e as adaptem para seu próprio uso. Como é visível pela lista de tecnologias abaixo, existe uma ótima possibilidade para pesquisas altamente personalizadas, seja para agentes que tentam derrubar pedófilos ou a próxima Silk Road, ou qualquer pessoa que queira uma experiência web menos genérica. Aqui está um olhar exclusivo sobre quem está ajudando a DARPA a construir o Memex e o que eles estão disponibilizando no [Open Catalogue](https://opencatalog.darpa.mil/) hoje:


>[Uncharted Software](https://uncharted.software/), [University of Southern California](https://www.usc.edu/) e [Next Century Corporation](https://nextcentury.com/)

Esses três produziram as interfaces front-end, chamadas TellFinder e DIG, que atualmente são usadas pelos parceiros da aplicação da lei da Memex. "Eles são muito bons em fazer as coisas parecerem lindas e brilhantes. Processar e exibir informações é realmente difícil e bastante subjetivo ", diz White.


![](https://blogs-images.forbes.com/thomasbrewster/files/2015/04/ApertureTiles_3_DrillDownDetails.jpg)

# ArrayFire

A tecnologia [ArrayFire](https://arrayfire.com/) é uma biblioteca de software projetada para suportar computação acelerada, turbo-boosting de buscas na web com [GPUs](http://www.nvidia.com/object/what-is-gpu-computing.html). "Algumas linhas de código no ArrayFire podem substituir dezenas de linhas de código de computação paralela, economizando tempo valioso dos usuários e reduzindo os custos de desenvolvimento", diz o relatório da tecnologia.


# Universidade Carnegie Mellon

A [CMU](https://www.cmu.edu/index.html) está construindo várias peças do quebra-cabeça Memex, mas o TJBatchExtractor é o que está sendo aberto hoje. Permite que um usuário extraia dados, como um nome, organização ou local, de anúncios publicitários. Foi aprovado na aplicação anti-tráfico humano que já está sendo utilizada pelas agências de aplicação da lei.


# Diffeo

O [Diffeo's](https://diffeo.com/) Dossier Stack aprende o que um usuário quer ao pesquisar na Internet. "Em vez de confiar no ranking do Google para dizer o que é importante, você pode dizer:" Eu quero o Thomas que está no Reino Unido e não os EUA, então não me envie nada que tenha informações orientadas para os EUA ", explica White.


# Hyperion Gray

Conforme apresentado em [um artigo recente da FORBES sobre o Memex](https://www.forbes.com/sites/thomasbrewster/2015/04/10/darpa-memex-search-going-open-source-check-it-out/)
, os rastreadores do [Hyperion Gray's](http://www.hyperiongray.com/) são projetados para replicar a interação humana com os sites. "Pense neles como web crawlers com esteróides", diz White. O seu componente AutoLogin leva as credenciais de autenticação convertidas no sistema para rastrear em áreas protegidas por senha de sites, enquanto o Formasaurus faz o mesmo, mas para formulários da web, determinando o que acontece quando os campos são preenchidos. As ferramentas Frontera, SourcePin e Splash facilitam o usuário médio para organizar e visualizar o tipo de conteúdo que eles desejam em seus resultados. Seu código HG Profiler procura correspondências de dados em diferentes páginas onde não há hiperlink tornando-o óbvio. O Hyperion Gray também criou o Scrapy-Dockerhub, que permite a reembalagem fácil dos rastreadores nos [Docker containers](https://www.forbes.com/sites/benkepes/2015/03/05/aiming-to-leverage-dockers-growth-red-hat-launches-its-own-container-specific-os/#53827b399238)
, permitindo "melhor e fácil rastreamento na web", observa White.


# [IST Research](http://istresearch.com/) e [Parse.ly](https://www.parse.ly/)

Essas duas empresas criaram infra-estrutura "para rastreamento web escalável em tempo real em sistemas distribuídos que usa um tipo de arquitetura de filas e permite a transmissão", explica White. "Essas ferramentas [Scrapy Cluster, pykafka e steamparse] são grandes componentes de infra-estrutura para que você possa construir uma arquitetura de web crawling muito escalável e em tempo real".

# Laboratório Jet Propulsion

Esta [organização baseada na NASA](https://www.jpl.nasa.gov/) criou uma série de blocos de construção da Memex, quatro dos quais - ImageCat, FacetSpace, LegisGATE e ImageSpace - são aplicativos criados em projetos [Apache Software Foundation](https://www.apache.org/)
 que permitem aos usuários analisar e manipular um grande número de imagens e massas de texto. "Pense neles como utilitários que podem ser úteis por conta própria, mas também podem ser componentes de um sistema de software", diz White. O JPL também criou um sistema de análise de vídeo e imagem chamado SMQTK para classificar esse tipo de conteúdo visual com base na relevância, tornando mais fácil para o usuário conectar arquivos ao tópico que eles importam. O Memex Explorer traz todas essas ferramentas juntas sob uma interface comum.


# [MIT Lincoln Laboratory](https://www.ll.mit.edu/)

Três das contribuições do MIT - Text.jl, MITIE, Topic - são ferramentas de processamento de linguagem natural. Eles permitem que o usuário, por exemplo, procure por onde duas organizações são mencionadas em documentos diferentes, ou para pedir descrições concisas de um documento ou uma página da web.


# Universidade de Nova York

A NYU, em colaboração com o JPL e o Continuum Analytics, criou uma interface chamada Topic, que permite ao usuário interagir com "rastreadores focados"(focused crawlers), que constantemente atualizam índices para produzir o que é relevante para o usuário, sempre "reduzindo a coisa que estão rastreando" , observa White. "Nós temos alguns destes diferentes tipos de crawlers, pois não é claro para cada domínio qual é a estratégia de crawling correta.


# [Qadium](https://qadium.com/)

Esta empresa de São Francisco apresentou um punhado de utilitários que permitem a "data marshalling", uma forma de organizar dados para que possa ser inspecionado de diferentes maneiras.


# [Sotera Defense Solutions](http://www.soteradefense.com/)

Esta empresa contrata do governo criou o devidamente chamado DataWake. Ele coleta todos os links que o usuário não clicou, mas poderia, e talvez deveria, ter. Este "wake" inclui os dados por trás desses links.


# SRI International

A [SRI](https://www.sri.com/) está trabalhando ao lado do [Projeto Tor](https://www.torproject.org)
, da Marinha dos EUA e de alguns dos criadores originais do Tor, o navegador anônimo que criptografa o tráfego e acompanha os usuários através de vários servidores para proteger suas identidades. A SRI desenvolveu um "dark crawler" chamado The Hidden Service Forum Spider, que agarra o conteúdo dos Serviços Oculto - esses sites hospedados em nós Tor e são usados ​​principalmente para serviços privados, sejam eles mercados de drogas ou fóruns de direitos humanos para aqueles que vivem sob regimes repressivos . O HSProbe, entretanto, procura por domínios de Serviços ocultos. A equipe da Memex está interessada em aprender mais sobre os cantos mais escuros da web, em parte para ajudar a aplicação da lei a limpá-la de conteúdos ilegais, mas também para obter uma melhor compreensão de quão grande são as partes não mapeadas da internet.


A DARPA está financiando o Tor Project, que é um dos adeptos mais ativos da privacidade no mundo tecnológico, e o US Naval Research Laboratory para testar as ferramentas Memex. A DARPA informou que o Memex não tem o intuito de destruir as proteções de privacidade oferecidas pelo Tor, mesmo que quisesse ajudar a descobrir as identidades dos criminosos. "Nenhum deles [Tor, a Marinha, parceiros Memex] quer que a exploração infantil e a pornografia infantil sejam acessíveis, especialmente no Tor. Estamos financiando esses grupos para testar ", diz White.


# Universidade de Stanford

DeepDive de [Stanford](https://www.stanford.edu/) transforma texto e multimídia em "bases de conhecimento", criando conexões entre relacionamentos das diferentes pessoas ou grupos que estão sendo pesquisados. "É tecnologia de aprendizado de máquina para inferir padrões, relacionamentos de trabalho ... encontrar links em uma quantidade muito grande de documentos", acrescenta White.


---

Thomas Fox-Brewster , Forbes Staff

I cover crime, privacy and security in digital and physical form

[README](https://www.forbes.com/sites/thomasbrewster/2015/04/17/darpa-nasa-and-partners-show-off-memex/#1bffc787378d)

