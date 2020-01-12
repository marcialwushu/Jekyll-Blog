---
layout: post
title:  "Micro Frontends"
date:   2020-01-01 17:59:38 -0200
categories: jekyll update
---


>Bom desenvolvimento de front-end é difícil. Escalar o desenvolvimento de front-end para que muitas equipes possam trabalhar simultaneamente em um produto grande e complexo é ainda mais difícil. Neste artigo, descreveremos uma tendência recente de dividir monólitos de front-end em muitas partes menores e mais gerenciáveis, e como essa arquitetura pode aumentar a eficácia e a eficiência das equipes que trabalham no código de front-end. Além de falar sobre os vários benefícios e custos, abordaremos algumas das opções de implementação disponíveis e mergulharemos em um aplicativo de exemplo completo que demonstra a técnica.

## CONTEÚDO

- [Benefícios]()
    - [Atualizações incrementais]()
    - [Bases de código simples e dissociadas]()
    - [Implantação independente]()
    - [Equipes autônomas]()
    - [Em poucas palavras]()
- [O exemplo]()
- [Abordagens de integração]()
    - [Composição do modelo do lado do servidor]()
    - [Integração em tempo de compilação]()
    - [Integração em tempo de execução via iframes]()
    - [Integração em tempo de execução via JavaScript]()
    - [Integração em tempo de execução via Web Components]()
- [Styling]()
- [Bibliotecas de componentes compartilhados]()
- [Comunicação entre aplicativos]()
- [Comunicação de back-end]()
- [Teste]()
- [O exemplo em detalhes]()
    - [O recipiente]()
    - [As micro frontends]()
    - [Comunicação entre aplicativos via roteamento]()
    - [Conteúdo comum]()
    - [A infraestrutura]()
- [Desvantagens]()
    - [Tamanho da carga útil]()
    - [Diferenças de ambiente]()
    - [Complexidade operacional e de governança]()
- [Conclusão]()

---

Nos últimos anos, os microsserviços explodiram em popularidade, com muitas organizações usando esse estilo arquitetural para evitar as limitações de backends grandes e monolíticos. Embora tenha sido escrito muito sobre esse estilo de criação de software do lado do servidor, muitas empresas continuam lutando com bases de código de front-end monolíticas.

Talvez você queira criar um aplicativo da Web progressivo ou responsivo, mas não consegue encontrar um lugar fácil para começar a integrar esses recursos ao código existente. Talvez você queira começar a usar novos recursos da linguagem JavaScript (ou uma das inúmeras linguagens que podem ser compiladas para JavaScript), mas não pode ajustar as ferramentas de compilação necessárias no processo de compilação existente. Ou talvez você queira apenas escalar seu desenvolvimento para que várias equipes possam trabalhar em um único produto simultaneamente, mas o acoplamento e a complexidade no monólito existente significam que todos estão pisando nos dedos uns dos outros. Todos esses são problemas reais que podem afetar negativamente sua capacidade de fornecer com eficiência experiências de alta qualidade aos seus clientes.


