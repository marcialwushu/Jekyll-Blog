---
layout: post
title:  "PHP 8.0 Data de Release e status do JIT no PHP"
date:   2018-11-11 02:25:31 -0200
categories: jekyll update
---

O PHP continua sendo a linguagem mais popular do lado do servidor para criar sites. Com uma participação de mercado estimada em 80%, a linguagem de programação de vinte e poucos anos está em toda parte. O PHP evoluiu, e as próximas principais etapas são o PHP 8.0.0 e a compilação JIT (just in time). Vamos dar uma olhada nisso.

A última grande versão do PHP foi 7.0.0. Esta versão foi um marco importante com desempenho significativamente aprimorado e menor uso de memória. Desde a versão 7.0, houve dois lançamentos adicionando recursos e adicionando recursos: 7.1 em 2016 e 7.2 em 2017. 

Mas, assim como ocorre com os estados de versionamento semântico, não pode haver alterações significativas nas versões principais com o patch de versão semântica (major.minor.patch). A próxima versão secundária, PHP 7.3, está prevista para ser lançada no final de 2018. A próxima versão secundária, PHP 7.3, está prevista para ser lançada no final de 2018.

O lançamento do PHP 8.0 ainda não está agendado, mas como é um grande salto, levará alguns anos. A partir de agora, também não há detalhes dos recursos, mas estima-se que a programação esteja a anos de distância. Algumas especulações definem o lançamento do PHP 8.0.0 em setembro de 2021:


[![](https://res.cloudinary.com/marcialwushu/image/upload/v1541913040/PDF/php8.png)](https://twitter.com/Crell/status/931427244760846336?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E931427244760846336&ref_url=https%3A%2F%2Freact-etc.net%2Fentry%2Fphp-8-0-0-release-date-and-jit-status)

## Estado de Just In Time (JIT) em PHP

A compilação just in time é uma maneira de otimizar o código de execução. É um método popular usado pela Java Virtual Machine (JVM), bem como a popular V8 JavaScript VM do Google. Por enquanto ambos usam o JIT, mesmo não sendo uma bala de prata.

Inicialmente, o desenvolvimento do PHP antes da evolução atual (PHP 7.x) se concentrava em melhorar o desempenho do PHP usando um JIT. Esse esforço resultou em melhorias substanciais nos benchmarks, mas provou fornecer pequenas melhorias em aplicações do mundo real, como WordPress ou Joomla.

Depois que o trabalho foi feito para o PHP 7.0 e fornecendo melhorias significativas, as melhorias no desempenho nas versões 7.1 e 7.2 foram bastante modestas. É por isso que a [equipe está trabalhando na implementação do JIT](https://react-etc.net/entry/php-8-to-ship-with-a-jit-compiler) novamente. [Existem alguns resultados encorajadores](https://mobile.twitter.com/dr4goonis/status/806817526097346560), mas a partir de agora não há uma análise profunda sobre o projeto PHP JIT.

Como o PHP é um software de código aberto, os desenvolvedores podem baixar e compilar o código-fonte. No entanto, muitas pessoas evitam a possibilidade de compilar software por conta própria. Felizmente, há uma imagem do Docker disponível que permite aos desenvolvedores experimentarem as compilações mais recentes do PHP JIT com facilidade:


>Este código é um ajudante para testar o php com suporte a jit experimental. Ele foi escrito como um projeto de estimação inspirado no tweet que mostra 54% de melhoria no desempenho. 
>- [Imagem do Docker do PHP com suporte experimental ao JIT](https://github.com/mente/php-docker-jit)

Tanto o JIT quanto o 8.0.0 aparecem no futuro do PHP, mas ambos são recursos significativos que permanecem no futuro. E, especialmente para o JIT, os processos de vida curta do PHP não são ideais para a implementação do JIT - isso é comparado a processos em execução contínua como o Node.js ou o Java.

---

Original Written by Jorgé on Monday January 8, 2018

[ARTIGO ORIGINAL](https://react-etc.net/entry/php-8-0-0-release-date-and-jit-status)
