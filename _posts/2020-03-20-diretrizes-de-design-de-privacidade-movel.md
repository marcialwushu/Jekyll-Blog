---
layout: post
title:  "Diretrizes de design de privacidade para desenvolvimento de aplicativos móveis"
date:   2020-03-20 17:59:38 -0200
categories: jekyll update
---

## Índice

- [Introdução]()
- [Definições]()
- [Transparência, escolha e controle - colocando o usuário em primeiro lugar]()
- [Retenção de dados e segurança]()
- [Educação]()
- [Redes sociais e mídia social]()
- [Publicidade móvel]()
- [Localização]()
- [Crianças e adolescentes]()
- [Responsabilidade e fiscalização]()


## Introdução

### Background

O surgimento de plataformas móveis abertas e a convergência de celular e a ‘web’ criaram um celular vibrante e dinâmico ecossistema que permite aos indivíduos moldar e apresentar ricos
identidades pessoais online, conecte-se com comunidades de seus escolha e envolva-se com aplicativos e serviços inovadores.

Muito disso depende do acesso em tempo real e uso de pessoal informações que muitas vezes são transferidas globalmente entre aplicativos, dispositivos e empresas.

Embora essas habilidades sirvam como um capacitador poderoso para inovações modelos de negócios e personalização de aplicativos e serviços, eles também podem fornecer um veículo para programas maliciosos ou
acesso sub-reptício às informações pessoais de um usuário. Até aplicativos que acessam e usam informações pessoais de forma legítima pode deixar de atender às expectativas de privacidade dos usuários e prejudicar sua
confiança e confiança nas organizações e no ecossistema móvel mais amplo. Os problemas ocorrem quando os usuários não recebem informações claras e transparentes aviso de acesso de um aplicativo e uso de seu pessoal
informações, ou quando não têm a oportunidade de expressar escolha significativa e controle sobre o uso de suas informações para fins secundários e além do necessário para a operação de
um aplicativo ou serviço.

A GSMA publicou recentemente um conjunto de privacidade móvel universal princípios que descrevem a maneira como os consumidores de celular a privacidade pode ser respeitada e protegida. Essas diretrizes buscam articular esses princípios em termos funcionais para aplicativos móveis Projeto.

### Escopo

Essas diretrizes aplicam princípios de design de privacidade a aplicativos e seus serviços relacionados projetados para dispositivos móveis. Eles são destinados para se aplicar a todas as partes na aplicação ou cadeia de entrega de serviço que são responsáveis por coletar e processar as informações pessoais de um usuário informações - desenvolvedores, fabricantes de dispositivos, plataformas e sistema operacional empresas, operadoras móveis, anunciantes e empresas de análise.

### Objetivo

Aplicativos e seus serviços relacionados devem criar boa privacidade experiências e geram confiança e segurança. Chave para perceber estes objetivos é uma estrutura robusta e eficaz para a proteção de privacidade, baseada nos princípios de transparência, escolha e controle.

Essas diretrizes adotam uma abordagem de privacidade desde o design e são destinadas para ajudar a garantir que os aplicativos móveis sejam desenvolvidos de forma que respeitar e proteger a privacidade dos usuários e de seus em formação. Privacidade por Design também significa reconhecer que os usuários têm interesses de privacidade (expectativas, necessidades, desejos e preocupações) que deve ser abordado de forma proativa desde o início e não como um reflexão posterior ou um "complemento". As diretrizes encorajam o
desenvolvimento, entrega e operação de aplicativos móveis que coloque os usuários em primeiro lugar e ajude-os a compreender (no mínimo):

- quais informações pessoais um aplicativo móvel pode acessar, coletar e usar
- para que as informações serão usadas, e por que, e
- como os usuários podem exercer a escolha e o controle sobre esse uso.

Exemplos são fornecidos com cada diretriz e algumas casos de uso são apresentados em um anexo separado.

## Definições

**Consentimento ativo**: significa que o usuário tem uma oportunidade clara de concordar com um uso específico e notificado de suas informações pessoais. O consentimento ativo se aplicaria ao uso secundário não óbvio de um informações pessoais do usuário e/ou aplicativos que tenham implicações adicionais de privacidade para os usuários, como uma solicitação de aplicativo a localização de um usuário onde tais dados não são necessários para o funcionamento da aplicação. O consentimento ativo deve ser capturado em
uma forma de o consentimento não ser a opção padrão.

**Aplicativo**: onde usamos o termo 'Aplicativo' ou 'Aplicativo', nós pretendem ter um escopo amplo; pode incluir um aplicativo nativo, um aplicativo ou script em execução em um tempo de execução específico, ou um widget ou script em execução em um ambiente de navegador.

**Dados de localização**: informações que identificam a localização geográfica de o dispositivo de um usuário, que pode incluir Cell ID, GPS, Wifi ou outro menos informações granulares, como vila ou cidade.

**Informações pessoais**: Existem muitas definições legais de pessoal informações, mas em seus termos mais simples, significa informações que se relacionam a um indivíduo e que você pode usar para identificá-lo, contatar ou localize-os.

As informações pessoais podem incluir:

- dados coletados diretamente de um usuário por meio de um usuário do aplicativo interface (nome, endereço, data de nascimento)
- dados que são coletados indiretamente, como número de telefone celular, IMEI ou UDID
- dados coletados sobre o comportamento de um usuário, como dados de localização, dados de navegação na web ou os aplicativos usados que estão vinculados a um único perfil
- dados gerados pelo usuário, como listas de contatos, vídeos e fotos, mensagens, e-mails, notas e registros de chamadas.

Para ser identificado, um indivíduo não precisa ser conhecido pelo nome - um usuário podem ser identificados mesmo quando suas informações estão associadas apenas a um identificador exclusivo, como um identificador de dispositivo exclusivo.

Existem categorias de informações que podem ser consideradas "sensíveis" e que pode precisar de segurança adicional. Isso pode, por exemplo, incluem credenciais de logon, registro e detalhes financeiros e informações sobre a saúde de uma pessoa, por exemplo.

**Privacidade**: privacidade é um conceito dinâmico que pode significar diferentes coisas para pessoas diferentes. Para efeitos destas diretrizes, privacidade é definida como a capacidade dos indivíduos de saber como seus informações pessoais serão coletadas, compartilhadas e usadas, e para exercer escolha e controle sobre seu uso.

**Usuário**: o usuário final de aplicativos e serviços relacionados.





