---
layout: post
title:  "Pesquisando no Instagram"
date:   2020-02-21 17:59:38 -0200
categories: jekyll update
---


![](https://osintcurio.files.wordpress.com/2019/07/katka-pavlickova-vsntw97ujja-unsplash-1.jpg)


Recentemente, apresentei na 'Dutch Osint Conference 2019' (este ano um evento fechado, mas espero que o próximo ano seja aberto a todos!) Sobre como pesquisar no Instagram. Eu queria compartilhar com você a apresentação que dei para que você também pudesse fazer pesquisas básicas no Instagram.

Pode parecer uma 'leitura longa', mas há muitas fotos na história, então não deixe que o tamanho do blog o assuste. E também confira a parte 2 !


## Antes de começarmos…

Embora não seja necessário ter uma conta do Instagram para fazer algum OSINT no Instagram, ela pode ser útil sempre que você quiser seguir determinadas hashtags ou perfis.

É possível criar uma conta pelo aplicativo móvel, mas você também pode usar o site para criar um perfil. Você pode usar seu email ou sua conta do Facebook para criar uma conta.

Para a maior parte do que estou mostrando, você não precisará fazer login. Se precisar fazer login, mostrarei este pequeno botão azul 'Log In' no canto superior esquerdo da captura de tela.

## Barra de pesquisa

Basta visitar qualquer perfil aleatório do Instagram para encontrar a barra de pesquisa no topo. Você não precisa fazer logon para isso.

Por exemplo, Instagram.com/search fornecerá um perfil privado, mas você verá a barra de pesquisa na parte superior.


![](https://osintcurio.files.wordpress.com/2019/07/picture1-1.png)

>instagram.com/search


## Procurando pessoas

Procurar pessoas no Instagram pode não ser tão eficiente quanto parece.

Por exemplo, ao procurar 'Mark Zuckerberg', recebo um perfil aleatório antes do real 'Mark Zuckerberg'. O Google ou qualquer outro mecanismo de pesquisa pode ser uma fonte melhor para usar. Use o Google Dorks como 'site: Instagram.com "mark zuckerberg".


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-19.55.59.png)

>Esquerda: resultados da pesquisa no Instagram
>Direita: resultados da pesquisa no Google

Também existem muitos sites que oferecem a possibilidade de pesquisar conteúdo no Instagram. [**O Picdeer.com**](http://picdeer.com/) é um dos muitos que oferecem a opção de procurar usuários.

Isso facilita um pouco, pois as hashtags e os usuários não estão misturados nos resultados da pesquisa, como o Instagram.com está mostrando. Agora você verá uma lista de hashtags no lado esquerdo e usuários no lado direito.

Novamente, existem muitos outros sites como esse; [**pictame.com**](https://pictame.com/) , [**sometag.com**](https://sometag.com/) são um dos muitos.


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-19.57.08.png)

>Resultados da pesquisa em Picdeer.com

Se você está procurando um certo tipo de usuário, digamos pessoas que pertencem a um grupo ou seguem uma religião, pode ser interessante procurar o que as pessoas afirmam em sua biografia. O [**Searchmy.bio**](https://searchmy.bio/) ajuda você a fazer exatamente isso. Esse mecanismo de pesquisa pesquisará apenas na seção bio dos perfis de usuário.

Você pode classificar 'mais seguidores' ou 'mais relevantes', escolher um mínimo ou máximo de seguidores em seus resultados e optar por incluir também hashtags.


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-19.59.51.png)

>Searchmy.bio

Quando você encontrar um perfil de seu interesse, existem alguns complementos úteis que você pode usar.

Começando com ' [**Helpertools for Instagram**](https://chrome.google.com/webstore/detail/helper-tools-for-instagra/hcdbfckhdcpepllecbkaaojfgipnpbpb) ', um complemento do Google Chrome.

No exemplo abaixo, usei o perfil de Mark Zuckerberg, [@zuck](http://instagram.com/zuck) . O 'Helptools for Instagram' é parcialmente gratuito. Ainda não usei a versão paga. Existem algumas opções que são realmente legais; você pode comparar dois perfis entre si. Esses perfis precisam ser abertos para que a ferramenta funcione sua mágica. Dependendo da quantidade de seguidores / seguidores, às vezes pode demorar um pouco. Isso ocorre porque o Helpertools colocou uma 'pausa' para impedir que o Instagram detecte a ferramenta.

Mas minha opção favorita é uma pequena opção que pode não chamar sua atenção a princípio; 'Conta de negócios'.

No caso de Marcas, é marcado como 'falso', o que significa que ele não tem um.

Ter uma 'conta comercial' é algo diferente de uma conta 'verificada'. Alterar seu perfil para "comercial" é uma configuração que você pode alterar pessoalmente. O Instagram não verifica nenhuma informação.

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.02.26.png)

>Resultados de 'Helpertools for Instagram'

Portanto, a conta Marcas não é uma conta comercial. Então, queremos olhar para uma conta que seja.

Vamos dar uma olhada em uma conta de uma loja de queijos local na Holanda; dê uma olhada no perfil; você pode ver algum detalhe de contato? Não!

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.05.22.png)

>Nenhum detalhe de contato é mostrado

Vamos verificar o Helpertools para ver se é uma conta comercial…

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.06.02.png)


Sim, ele é!

Podemos até ver em qual categoria eles colocaram seu perfil. Mas espere, tem mais!

Para ver mais informações, agora você precisa criar um perfil ou fazer logon no seu perfil. Em um telefone celular (ou bom emulador) com conexão à Internet.

Então, saiba que sabemos que é um perfil de negócios, podemos procurar mais informações.

Então, agora abrimos o aplicativo móvel e estamos conectados. (Eu usei um aplicativo Android).

Visitando o perfil da loja de queijos, você verá alguns botões abaixo da biografia. Um deles é 'Contato'. Se clicar em 'Contato', um pop-up aparecerá e mostrará todos os detalhes de contato vinculados ao perfil (que são preenchidos pelo proprietário). Então agora vemos um endereço de e-mail que não era visível antes!

Mas espere, há outro botão 'Ligar' (Bellen), e isso mostrará o número de telefone!

Portanto, passando de zero para detalhes de contato, agora temos um endereço de e-mail e número de telefone.

Lembrar; ao apenas olhar o perfil pelo site, teríamos perdido essa informação!






