---
layout: post
title:  "Noções básicas sobre ITMS-90809: Depreciação da API do UIWebView"
date:   2019-12-21 17:59:38 -0200
categories: jekyll update
---

Recentemente, a Apple lançou um novo aviso de envio de aplicativo informando que eles estão obsoletos formalmente no UIWebView. Queríamos que a comunidade do Ionic soubesse do que se trata esse aviso e como a equipe do Ionic planeja abordá-lo.

>Atualização 25/11/2019: A equipe do Cordova [lançou o Cordova iOS 5.1.0](https://cordova.apache.org/announcements/2019/11/25/cordova-ios-release-5.1.0.html) , que desativa o UIWebview no momento da compilação. Para usá-lo, verifique se você possui um plug-in WKWebView instalado e adicione ```<preference name="WKWebViewOnly" value="true" />``` ao seu ```config.xml``` arquivo. Detalhes completos abaixo.

**Conclusão:** a Apple ainda está aceitando envios de aplicativos iOS baseados em Ionic que contêm referências ao UIWebView. Para atender ao novo requisito, basta atualizar para a versão mais recente do Capacitor. Se você estiver usando o Cordova, veja abaixo.

## O que é isso?

Um [WebView](https://ionicframework.com/docs/building/webview) é um navegador da Web incorporado que aplicativos nativos podem usar para exibir conteúdo da Web. Usados por tempos de execução nativos como [Cordova](https://cordova.apache.org/) e [Capacitor](https://capacitor.ionicframework.com/) , eles fazem parte do molho secreto que os desenvolvedores Ionic usam para empacotar aplicativos baseados na Web em aplicativos móveis nativos que podem acessar recursos de hardware nativos, como a câmera ou o Bluetooth.

A Apple anunciou anteriormente a descontinuação do [UIWebView](https://developer.apple.com/documentation/uikit/uiwebview) em junho de 2018. A partir do iOS 12, eles começaram a alertar os desenvolvedores sobre a migração para o WKWebView, o sucessor do UIWebView.

Esta notificação recente colocou-a em primeiro plano. Para referência, veja a mensagem que você verá se fizer upload de um aplicativo binário na App Store:

Identificamos um ou mais problemas com uma entrega recente para seu aplicativo, [Nome do aplicativo e número da versão]. Sua entrega foi bem-sucedida, mas você pode corrigir os seguintes problemas na sua próxima entrega:

*ITMS-90809: Uso preterido da API - a Apple deixará de aceitar envios de aplicativos que usam APIs UIWebView. Consulte <https://developer.apple.com/documentation/uikit/uiwebview> para obter mais informações.*

Depois de corrigir os problemas, você pode usar o Xcode ou o Application Loader para carregar um novo binário no App Store Connect.

## Qual é o problema?

Ao criar um aplicativo Ionic, você pode escolher entre Cordova ou Capacitor para implantar uma versão móvel nativa. Embora as versões mais recentes sejam usadas ```WKWebView``` automaticamente, o Cordova ainda usa as APIs do UIWebView ou contém referências a elas (o Capacitor foi atualizado para remover essas referências - veja abaixo).

Após o envio do aplicativo, a Apple pesquisa o código do aplicativo pela string "UIWebView" e gera um aviso de envio, se encontrado. Portanto, cordova-iosserá necessária uma versão futura da (biblioteca iOS do Cordova) para garantir que todas as referências às APIs do UIWebView sejam removidas.

## Isso me impedirá de lançar um aplicativo iOS baseado em Ionic?

Atualmente, não, pois isso é apenas um aviso , não um erro. Os avisos não resultarão em rejeições da App Store. As APIs do UIWebView ainda são suportadas na próxima versão do iOS 13 e no macOS Catalina, mas ainda estão desaparecendo em versões futuras .

Em algum momento no futuro, os aplicativos iOS poderão ser impedidos de serem lançados na App Store quando a Apple decidir impor aplicativos de bloqueio que usam o UIWebView.


## O que a Ionic está fazendo sobre isso?

Pedimos à Apple a data oficial em que eles deixarão de aceitar envios de aplicativos que incluem APIs UIWebView, mas ainda não recebemos resposta. Atualizaremos este blog quando soubermos mais informações.

## Usando Cordova?

Em 25 de novembro de 2019, a equipe do Cordova lançou o Cordova iOS 5.1.0 , que desabilita o UIWebview em tempo de compilação. Eles estavam discutindo anteriormente um plano para avançar.

Atualizar:

- Verifique se você possui um plug-in WKWebView instalado: o [oficial Apache ou o Ionic](https://github.com/ionic-team/cordova-plugin-ionic-webview) . Todos os aplicativos iniciais Ionic incluem automaticamente ```cordova-plugin-ionic-webview```.
- Adicione ```<preference name="WKWebViewOnly" value="true" />``` ao seu arquivo ```config.xml``` .
- Execute ```cordova prepare ios``` para aplicar as alterações.

Para recapitular:

- 5.1.0 possui um sinalizador de tempo de compilação condicional que desativa o UIWebView. Essa é uma correção inicial para impedir que o aviso da Apple seja acionado.
- 6.0.0 removerá a totalidade do UIWebView. Esta é uma mudança inédita, com mais alterações necessárias, e será lançada nos próximos meses.

## Usando Capacitor?

Com esse aviso de descontinuação, agora é o momento perfeito para considerar a migração para o [Capacitor](https://capacitor.ionicframework.com/) , sucessor espiritual da Ionic para Cordova, que permite que aplicativos modernos da Web sejam executados em todas as principais plataformas com facilidade.

Em 4 de setembro de 2019, a equipe Ionic lançou uma nova versão do Capacitor (aqui está o [changelog v1.2.0](https://github.com/ionic-team/capacitor/blob/master/CHANGELOG.md#120-2019-09-04) ) que [removeu as referências ao UIWebView](https://github.com/ionic-team/capacitor/pull/1925) . Para [atualizar seu aplicativo](https://capacitor.ionicframework.com/docs/basics/workflow#5-updating-capacitor) , basta executar os seguintes comandos para atualizar a biblioteca iOS do Capacitor:

```
npm update @capacitor/cli
npm update @capacitor/core
npm update @capacitor/ios
npx cap sync
```

Observe que, se você estiver [usando plug-ins Cordova](https://capacitor.ionicframework.com/docs/cordova/using-cordova-plugins) em seu projeto Capacitor, precisará garantir que eles sejam atualizados eventualmente.

Os clientes que usam plug-ins Ionic Native Enterprise Edition, incluindo o popular [plug-in InAppBrowser, também](https://ionicframework.com/docs/enterprise/inappbrowser) podem atualizar agora. Se sua equipe conta com um plug-in nativo específico, entre em [contato conosco para obter assistência](https://ionicframework.com/enterprise/contact) . Se você estiver em um [plano do Ionic Native Enterprise](https://ionicframework.com/docs/enterprise) , entre em [contato com o Suporte do Ionic](https://ionic.zendesk.com/hc/en-us/requests/new) se tiver alguma dúvida.

---

Autor: [Matt Netkow](https://twitter.com/dotNetkow)

[Artigo Original](https://ionicframework.com/blog/understanding-itms-90809-uiwebview-api-deprecation/)
