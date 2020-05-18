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



![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.09.08.png)


>1. Abra o aplicativo móvel enquanto estiver conectado
>2. Abra o perfil e marque a guia 'Contato'
>3. Pressione 'ligar' (bellen) para ver um número de telefone ou 'E-mail' para ver o endereço de e-mail


Se você quiser fazer uma análise de um perfil, o [statflux.com](http://statflux.com/) poderá ajudá-lo um pouco. Ele mostra alguns detalhes que você pode encontrar no perfil, mas também fornece informações sobre outros detalhes, como curtidas e comentários comuns.
Também fornece as postagens 'Mais curtidas' e 'Mais comentários'.
Ao olhar para um perfil com muitas postagens e você não sabe qual postagem pode ser interessante para você, o Statflux.com pode ajudá-lo.


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.11.51.png)

>Exemplo de @zuck no Statflux.com

## Ampliando fotos de perfil e baixando fotos de uma conta

O Instagram tem uma foto de perfil cortada (círculo). Mas às vezes você quer ter a foto completa, pois isso fornecerá apenas um pouco mais de detalhes sobre o que está acontecendo na parte de trás da foto ou talvez quem mais está na foto.

Existe uma maneira de recuperar isso do código-fonte, mas o complemento ' [**DownAlbum**](https://chrome.google.com/webstore/detail/downalbum/cgjnhhjpfcdhbhlcmmjppicjmgfkppok?hl=en) ' também faz o truque.
Não apenas pode ajudá-lo com o Instagram, mas também funciona para o Facebook, Pinterest, Twitter, Ask.fm e Weibo. O DownAlbum pode ajudá-lo a ampliar uma imagem de perfil com muita facilidade;

Quando instalado, logo abaixo da foto do perfil, aparecerá um botão 'Baixar foto'. Clique no link e uma nova página será aberta, mostrando a foto maior do perfil que você pode usar para investigar melhor.


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.14.54.png)


>Exemplo de 'DownAlbum'

O 'DownAlbum' oferece uma opção para baixar fotos também. Quando você clica em uma foto, o texto 'Baixar foto' é exibido. Ao clicar nele, uma nova página será exibida, mostrando uma foto um pouco maior. Basta clicar com o botão direito e salvar a foto.

Outra opção é o site ' instasave.io ', digite o nome de usuário do perfil no qual você está interessado e pressione o botão 'baixar' abaixo de cada foto para salvar a foto.

Ambas as opções são apenas um download por um.

Deseja fazer o download de todas as fotos possíveis em um perfil?

Existe um complemento do Google Chrome chamado ' [**Downloader for Instagram + Direct Message**](https://chrome.google.com/webstore/detail/downloader-for-instagram/olkpikmlhoaojbbmmpejnimiglejmboe?hl=en) ', que pode ajudá-lo a baixar fotos em massa.

Quando o complemento estiver instalado, você verá um botão no canto vertical.

Escolha o botão da extrema direita para fazer o download do perfil completo. Certifique-se de carregar a página totalmente para fazer o download de tudo. Como você vê neste exemplo; Zuckerberg tem 141 postagens, mas a ferramenta indica que existem apenas 24. Se você carregar a página completamente, poderá baixar todas as fotos. Você pode personalizar o intervalo.


Além disso: não esqueça a seção 'Marcado' no Instagram! Isso exige que você efetue login, mas às vezes fornece uma ótima visão de outras fotos. A seção "Marcado" pode ser encontrada na biografia, ao lado da seção "Postagens".

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.27.38.png)

>Mostrado à direita: Downloader for Instagram + Direct Message

## Instagram Stories

As Histórias do Instagram são vídeos ou fotos curtos do Snapchat. Você pode editar o vídeo / foto com adesivos, texto, cor e GIFs. (Deseja saber mais sobre 'Histórias'? Confira este [artigo](https://buffer.com/library/instagram-stories) para o Buffer da [Ash Read](https://twitter.com/Ashread_) ) Por padrão, as histórias são visíveis por 24 horas, mas você pode 'Destacar' as pessoas que podem vê-las por um longo período de tempo. Esses 'Destaques' podem ser categorizados.

Você pode reconhecer se um perfil tem histórias olhando para a foto do perfil. Se houver um círculo colorido ao redor, isso indica que o perfil possui histórias.

Se você quiser ver essas histórias, precisará fazer login.

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.35.20.png)


>Esquerda: o perfil do @ zuck não tem uma história
>Direita: O perfil do @bbc tem uma história


Às vezes, os perfis têm essas histórias destacadas categorizadas. Você verá essas histórias logo abaixo da biografia.

Clique em uma categoria para ver as histórias.

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.36.12.png)

>Abaixo da biografia, você encontrará os destaques categorizados

## Procurando Histórias

A pesquisa de histórias só é possível se as histórias forem marcadas com um local ou hashtag.

O site oferece a você a oportunidade de pesquisar as histórias; se você pesquisar uma hashtag ou local na barra de pesquisa na parte superior do site, verá uma foto redonda com o círculo colorido ao redor. Clique na foto para ver as histórias que correspondem a essa tag ou local específico.


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.37.07.png)

>Resultados da pesquisa no Instagram

A pesquisa de histórias é um pouco mais fácil, eu acho, ao usar o addon do Google Chrome ' Downloader for Instagram '.

Quando instalado, no canto superior direito, você verá um pequeno ícone com as cores do Instagram.

Clique no logotipo para abrir uma nova página onde você verá o menu como visto na captura de tela; agora você terá a opção de ver as histórias de seus amigos, os principais vídeos ao vivo, os locais e fazer algumas pesquisas.

Procurei a hashtag 'Amsterdã' e selecionei a com a bandeirinha no final.


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.40.00.png)

>Resultados da pesquisa com 'Downloader for Instagram'

Quando eu clicar no resultado, você não verá as Histórias imediatamente. Clique no pequeno ícone de olho roxo e você verá as histórias imediatamente.

Usando as setas (tecla esquerda e direita), você pode alternar entre as histórias.

O usuário que enviou a história é mostrado à esquerda (na captura de tela borrada em azul).

E muito útil; O Downloader para Instagram oferece novamente (no canto superior esquerdo) a oportunidade de baixar apenas uma ou todas as histórias conectadas à hashtag.


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.42.19.png)


>Faça o download das histórias usando os botões no canto superior direito

## Pesquisando palavras-chave

Se você não está procurando hashtags, mas apenas palavras usadas em geral, o Instagram pode não ser o melhor lugar para pesquisar, como você pode ver na imagem abaixo, à esquerda.

O Google ou qualquer outro mecanismo de pesquisa pode ser uma solução melhor. Para o Google, use o operador:

Inurl: instagram.com/p/ “keyword” (substitua 'keyword' por qualquer palavra-chave que você gosta). No exemplo que escolho para 'hora do jantar'.


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.46.10.png)


>Esquerda: pesquisando palavras-chave no Instagram
>Direita: pesquisando palavras-chave no Google


Agora você vê que um dos resultados inclui as palavras 'hora do jantar'. O horário do jantar não é usado como hashtag. Portanto, se você tivesse pesquisado essas palavras-chave na barra de pesquisa do Instagram, não teria encontrado esta postagem.

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.47.14.png)

>Resultado de pesquisa do Google

## Procurando por hashtags

Quando você selecionar um resultado, neste caso, uma hashtag, verifique não apenas as primeiras fotos. Essas serão as fotos 'Top' (mais populares) e nem sempre fornecerão o que você está procurando. Em vez disso, role para baixo para ver 'Mais recentes'.

Para pesquisar especificamente hashtags, use o símbolo #. (por exemplo, #osint)

Além disso; Existem muitos sites para ajudá-lo a procurar por hashtags usadas no Instagram. Sites como [pictame.com](http://pictame.com/) e [hashatit.com](http://hashatit.com/) são apenas alguns deles.

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.44.18.png)

>Pesquisa de hashtags no Instagram, role para baixo até 'Mais recentes'

## Seguindo hashtags

Quando você encontrar uma hashtag específica e quiser manter-se atualizado, faça login e pressione 'Seguir' para seguir as postagens conectadas a essa hashtag específica.

Para seguir uma hashtag, você precisa fazer login.

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.48.48.png)

>Como seguir uma hashtag no Instagram

## Baixar hashtags

O download de hashtags é muito fácil ao usar o complemento do Google Chrome ' [Downloader for Instagram](https://chrome.google.com/webstore/detail/downloader-for-instagram/olkpikmlhoaojbbmmpejnimiglejmboe?hl=en)' .

Carregue a página da maneira que desejar e use o complemento para baixar as postagens vinculadas à hashtag.

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.50.06.png)

>Faça o download das postagens marcadas com uma hashtag usando 'Downloader for Instagram'


## Procurando por locais

A pesquisa de locais pode ser feita através da barra de pesquisa na parte superior do site. Você pode reconhecer um local pelo ícone 'soltar'.

Selecione um local para ver quais histórias são postadas nesse local e quais outras postagens são desse local.

Atenção: você não precisa estar fisicamente nesse local. Você pode escolher qualquer local que desejar. Então, uma foto minha, em frente à Estação Central de Amsterdã, pode ter a localização da Time Square New York, só porque eu disse ao Instagram que a foto foi tirada lá. Se você deseja adicionar um local à sua foto, precisará conceder ao Instagram permissão para seus dados de localização.


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.55.55.png)


>Pesquise resultados de locais no Instagram

Não tem certeza se o local que você está procurando está no Instagram? Ou você pode não ter a ortografia correta;
Confira Instagram.com/explore/locations/

Uma lista de países é mostrada abaixo. Selecione o país de interesse e selecione a cidade em que está interessado.


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-20.58.12.png)


>Filtre o país e a cidade para ver quais locais existem em uma cidade específica


## Procurando postagens mais antigas marcadas para um local

Um entusiasta do OSINT compartilhou comigo este vídeo sobre como encontrar postagens no Instagram de um local, dentro de um determinado período de tempo. Devo dizer que é bastante complexo, mas, embora o vídeo tenha sido publicado em 2017, ainda funciona parcialmente em 2019!

Confira o vídeo aqui: <https://youtu.be/FYnfKghpJBw>

E o script Python aqui: <https://repl.it/repls/FormalYellowgreenLinux>

No vídeo, um som matemático é explicado sobre como calcular a data em que você está interessado. Quando você tiver uma data, poderá pesquisar o local em que está interessado.


Dê uma olhada no URL, no final você vai adicionar; ' ? Max_id = ' seguido do número que você calculou
POR EXEMPLO <https://www.instagram.com/explore/locations/3001373/times-square-new-york-city/?max_id=1817012758118400>

Role para baixo até a seção 'Mais recentes' para ver as postagens mais antigas.


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-11-at-21.05.12.png)


>A foto à esquerda é de 27 de agosto de 2011, mas é mostrada como o primeiro resultado na seção 'Mais recente'


## É isso aí!

Esses foram alguns métodos básicos para pesquisar no Instagram. É claro que existem cerca de um milhão de maneiras, métodos, sites, complementos e scripts que você poderia usar para facilitar a pesquisa no Instagram. Se o seu método ou truque favorito não for mencionado no blog acima, fique à vontade para deixar um comentário abaixo! Desta forma, todos nós podemos aprender🙂

Pronto para mais ?! Confira a parte 2 de como pesquisar no Instagram!

---

Author: [TECHNISETTE](https://osintcurio.us/author/technisette/)

[Artigo Original](https://osintcurio.us/2019/07/16/searching-instagram/)









