---
layout: post
title:  "Pesquisando no Instagram - parte 2"
date:   2020-02-22 17:59:38 -0200
categories: jekyll update
---

![](https://osintcurio.files.wordpress.com/2019/07/photo-1516251193007-45ef944ab0c6.jpeg?w=1650&h=768&crop=1)


## Procurando detalhes de contato da conta comercial sem ferramentas

Na primeira parte, falamos sobre a recuperação de detalhes de contato das contas comerciais do Instagram com a ajuda do addon Chrome [Helper Tools for Instagram](https://chrome.google.com/webstore/detail/helper-tools-for-instagra/hcdbfckhdcpepllecbkaaojfgipnpbpb) . Esse complemento ainda pode ajudá-lo a determinar se uma conta é uma conta 'comercial' ou não. Onde, no primeiro blog, destacamos que você precisará de um telefone celular para visualizar os detalhes de contato, temos uma solução melhor para você agora!

Os detalhes de contato também podem ser visualizados quando conectado ao site! [@Sector035](http://twitter.com/sector035) encontrou uma maneira [como](https://twitter.com/Sector035/status/1153309691151302662) :

- Certifique-se de fazer login na sua conta do Instagram (pesquisa) em um navegador da web
- Visite a conta em que está interessado e verifique se é uma conta comercial. Você pode verificar usando as [Ferramentas auxiliares](https://chrome.google.com/webstore/detail/helper-tools-for-instagra/hcdbfckhdcpepllecbkaaojfgipnpbpb) , mas também pode tentar a sua sorte, continuando os próximos passos.
- Agora precisamos recuperar o ID do usuário do Instagram. Você pode fazer isso clicando com o botão direito do mouse em algum lugar da página de interesse onde não há contato (por exemplo, no lado direito ou esquerdo) e selecione 'Exibir fonte da página' (ou use Ctrl + U, isso funciona na maioria dos navegadores).
- Pesquise, usando Ctrl + F, a profilePage_ (o número atrás de 'profilePage_' é o número que você precisa copiar.)

![](https://osintcurio.files.wordpress.com/2019/09/screenshot-2019-09-10-at-09.52.38.png?w=1024)

>Exemplo de um ID de usuário da página do Instagram da Starbucks

- Agora abra uma nova guia e cole o seguinte URL. Substitua " ID " pelo número de identificação encontrado na sua página de interesse.
- https://i.instagram.com/api/v1/users/ID/info/ (por exemplo, <https://i.instagram.com/api/v1/users/1034466/info> )

Agora você poderá ver as informações que a conta comercial preencheu!

Se observarmos o exemplo usado da Starbucks, seu resultado será semelhante a este:

![](https://osintcurio.files.wordpress.com/2019/09/screenshot-2019-09-10-at-09.54.39.png)


>Você verá que o 'is_business' está definido como TRUE e poderá ver o endereço de e-mail e o número de telefone

Também há muitas outras coisas interessantes a serem reunidas aqui ao lado dos detalhes de contato! Como o 'instagram_location_id', por exemplo. Se você copiar esse número e colocá-lo atrás de 'facebook.com' (facebook.com/22092443056), ele fornecerá a conta do Facebook da Starbucks!

Outras coisas que podem ser interessantes são a quantidade exata de seguidores / seguidores e muito mais. Então vá e dê um pico🙂


## Procurando conteúdo excluído do Instagram

Todos sabemos que o conteúdo on-line pode ser removido tão rápido quanto foi carregado. Portanto, procurar qualquer conteúdo excluído pode ser interessante.

Há pouco tempo, escrevemos um blog sobre como encontrar conteúdo excluído , com uma seção que explica especificamente como encontrar quaisquer postagens / perfis de mídia social que foram excluídos.

No blog, nos referimos ao Archive.org como um bom recurso para encontrar postagens antigas do Instagram, com um exemplo do perfil do Instagram de DJ Hardwell (clique aqui para o perfil arquivado e aqui para o perfil atual).

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-30-at-21.42.18.png)

>Esquerda: Archive.org
>Direita: Instagram.com/hardwell

Ao analisar pessoas famosas, há uma grande chance de que outras contas imitem as de pessoas famosas. Por exemplo; existem várias contas da estrela da realidade Kim Kardashian onde elas repostam tudo o que ela faz no Instagram ou postam tudo o que postam no Snapchat em uma [conta do Instagram](https://www.instagram.com/kimkardashiansnap).

Ao examinar essas 'contas de fãs', você poderá encontrar quaisquer dados que já tenham sido excluídos.

Outra maneira de procurar conteúdo excluído é usar o [Google](https://google.com/).

Como você deve saber, existem muitos sites diferentes que também usam as postagens do Instagram para exibir em seus sites. Ao usar o Google Dork, você pode encontrar sites usando postagens do Instagram e pode encontrar algum conteúdo excluído. Isso porque esses sites podem ficar um pouco atrasados nas postagens reais do Instagram.


Use: -site: instagram.com palavra-chave do instagram -twitter

- **site: instagram** = para excluir resultados do site instagram.com
- **instagram** = para se concentrar nas postagens do Instagram
- **keyword** = substituir 'keyword' pela palavra-chave ou nome de usuário que você está procurando .
- **twitter** = porque o Twitter fornece muitos falsos positivos nesses resultados.

Exemplo: -site: instagram.com instagram hardwell -twitter

![](https://osintcurio.files.wordpress.com/2019/09/screenshot-2019-09-25-at-21.40.56.png?w=1024)

>Exemplo: -site: instagram.com instagram hardwell -twitter

Ou você pode tentar configurar uma ferramenta de monitoramento da web para detectar qualquer alteração em um site. Esse tipo de ferramenta pode capturar o que está mudando na página e, dessa forma, você não perderá nenhuma postagem.


## Pesquisando no Twitter o conteúdo do Instagram

Outra maneira de encontrar contas do Instagram de pessoas em que você possa estar interessado ou qualquer postagem relacionada a um tópico específico é pelo Twitter.


O Twitter mudou muito recentemente. Felizmente, [@Dutch_osintguy](http://twitter.com/dutch_osintguy) escreveu um [blog](https://osintcurio.us/2019/08/01/muting-the-twitter-algorithm-and-using-basic-search-operators-for-better-osint-research/) sobre como navegar por tudo isso. E existem ótimas maneiras de explorar o Twitter e encontrar perfis ou postagens do Instagram.

Primeiro, você não precisará de uma conta no Twitter para pesquisar no Twitter. Basta navegar no [Twitter.com/explore](https://twitter.com/explore) para usar a barra de pesquisa superior.

Agora, para pesquisar o conteúdo do Instagram, use as seguintes consultas de pesquisa:

- [instagram.com/p](https://twitter.com/search?q=instagram.com%2Fp&src=typed_query&f=live) (exibirá tweets contendo 'instagram.com/p')
- [fonte: Instagram party](https://twitter.com/search?q=source%3Ainstagram%20party&src=typed_query&f=live) (exibirá tweets contendo a palavra 'party' com Publicações no Instagram. Altere a palavra 'festa' para o que você estiver procurando.)
- [filtro do instagram: links](https://twitter.com/search?q=filter%3Alinks%20instagram&src=typed_query&f=live) (tweets que contêm um URL e a palavra 'Instagram'.)


Ao executar essas consultas, mude para os tweets 'Mais recentes' para ver as postagens mais recentes.

Além disso, quando você estiver confortável pesquisando no Twitter, tente 'fazer malabarismos com as consultas' e criar consultas mais abrangentes para encontrar exatamente o que está procurando. Por exemplo: [instagram.com/p near:Amsterdam within:15mi](https://twitter.com/search?q=instagram.com%2Fp%20near%3AAmsterdam%20within%3A15mi&src=typed_query&f=live)

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-30-at-22.07.59.png)

>Não se esqueça de selecionar 'Últimas' para ver as postagens mais recentes!


## Procurando fotos mais antigas marcadas para um local

[A OSINT Combine](http://twitter.com/osintcombine) construiu este incrível mecanismo de pesquisa para ajudá-lo a encontrar fotos mais antigas marcadas em um local no Instagram (clique [aqui](https://www.osintcombine.com/instagram-explorer) ).

No ' Pesquisando Instagram - parte 1 ', nos referimos a um [vídeo do YouTube](https://youtu.be/FYnfKghpJBw) que explica um método bastante abrangente para calcular esse número que você pode usar para pesquisar postagens mais antigas marcadas em um local. Bem, o OSINT Combine resolveu esse problema para você com o mecanismo de pesquisa deles. Funciona bem fácil; basta colar o URL de qualquer local do Instagram e ajustar a data. Clique no ícone de pesquisa verde para pesquisar, role para baixo até a seção 'Mais recente' e pronto! Existem as postagens do Instagram em que você está interessado!

Atenção : o Instagram ficou on-line no dia 24 de agosto de 2011. Você não encontrará postagens anteriores a esta data.

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-28-at-20.37.40.png)

>1. Pesquise sua localização no Instagram, selecione a localização e copie o URL.
>2. Após o URL selecionado na caixa 'Find Photos', selecione uma data e clique no botão verde
>3. Role para baixo no Instagram até 'Most recent' para ver fotos da data selecionada


## Procurando apenas vídeos do Instagram

No ' Searching Instagram - part 1 ', mostramos como pesquisar hashtags e encontrar as histórias e postagens do Instagram compartilhadas com essa hashtag específica. Mas se você estiver procurando apenas vídeos compartilhados com uma hashtag específica, o [skimagram.com](http://skimagram.com/) o ajudará.

Basta digitar a hashtag que você está procurando e selecionar (à direita, mostrado na caixa vermelha na captura de tela abaixo), se estiver procurando vídeos ou postagens. Selecione o ícone de vídeo para procurar apenas vídeos.

Atenção : isso só pesquisará vídeos, não o Instagram Stories.

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-28-at-20.22.08.png)

>Exemplo do Skimagram.com

## Procurando várias hashtags

O Instagram.com não permite pesquisar facilmente várias hashtags. E isso pode ser algo que você precisará fazer para restringir seus resultados relevantes. Embora não tenhamos encontrado um mecanismo de pesquisa especial apenas para isso, o Google pode ajudá-lo nesse meio tempo.

Use o seguinte dork do Google para pesquisar várias hashtags:


![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-30-at-22.16.02.png)

>Use: inurl: instagram.com/p #summer #amsterdam

Por alguma razão, às vezes recebo resultados diferentes ao colocar as hashtags entre aspas. Portanto, tente as duas, apenas para ter 100% de certeza de que está pesquisando todas as opções possíveis. E você pode expandir isso o quanto quiser.

Se você não tiver certeza de como uma hashtag está escrita ou se perguntar se há hashtags que incluem mais palavras, consulte [Keywordtool.io/instagram](https://keywordtool.io/instagram) . O Keywordtool permite pesquisar apenas as primeiras letras de uma hashtag e ele conclui o maior número possível de opções. Também indica quantas postagens podem ser encontradas com essa hashtag específica.

Um bônus é que você também pode pesquisar no Google, YouTube, Bing, Amazon, eBay, Play Store e Twitter.


![](https://osintcurio.files.wordpress.com/2019/09/screenshot-2019-09-25-at-21.01.39.png?w=1024)


>Exemplo de palavra-chavetool.io/instagram

## Pesquisando palavras-chave em uma postagem do Instagram

Na primeira postagem, sugerimos usar o Google para pesquisar por palavras-chave usadas nas postagens. Isso pode ser feito usando um operador do Google ( Inurl: instagram.com/p/ “keyword”  (substitua 'keyword' por qualquer palavra-chave que você gosta) .É claro que você pode usar a seção 'Ferramentas' no Google para selecionar um específico intervalo de tempo.

Se você estiver procurando outro site para fazer isso por você, consulte [mulpix.com/instagram](http://mulpix.com/instagram/) . Essa ferramenta também oferece a opção de filtrar entre postagens e vídeos. Também fornece estatísticas sobre as palavras-chave usadas.

![](https://osintcurio.files.wordpress.com/2019/09/screenshot-2019-09-25-at-21.17.07.png?w=1024)


>Exemplo de mulpix.com/instagram

## Visualizando histórias anonimamente

Deseja ver histórias públicas anonimamente? Use [stalker-stories.com](http://stalker-stories.com/) para visualizar histórias públicas sem precisar fazer logon em uma conta do Instagram.

Bônus extra é que o site também permite que você baixe as histórias.

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-28-at-20.39.43.png)

>Stalkerstories.com

## Rastreando seus 'seguidores'

O The Wired escreveu um [artigo](https://www.wired.com/story/whos-in-town-map-instagram-location-history/) sobre esse aplicativo muito interessante chamado 'Quem está na cidade?' Este aplicativo permite que você se conecte à sua conta do Instagram e poderá ver onde seus amigos (as pessoas que você segue) fizeram check-in. Em um mapa, você pode ver para onde eles foram (isso pode incluir onde moram, trabalham. , treino, etc). Embora isso possa ser interessante no caso de você querer encontrar pessoas que você segue, isso pode ser muito interessante da perspectiva do OSINT. Se você tem uma conta de pesquisa e segue um tipo específico de pessoas, isso pode lhe dar uma visão muito boa de onde elas podem ir e do que elas podem gostar.

Se você quiser saber como criar uma 'conta de pesquisa', clique [aqui](https://osintcurio.us/2018/12/27/the-puppeteer/) , escrevemos um blog e explicamos o que você deve levar em consideração.

Quem está na cidade? pode ser baixado [aqui](https://whosintown.app/) (iOS e Android).

![](https://osintcurio.files.wordpress.com/2019/07/screenshot-2019-07-28-at-20.42.30.png)


>Whosintown.app

## Saber quando seus seguidores/seguindo estão mais ativos

Digamos que você tenha um perfil de pesquisa com muitos seguidores (deve ter mais de 100) e esteja interessado em saber quem deles pode ser mais ativo. Talvez porque você possa personalizar as postagens para elas ou descobrir mais sobre o seu grupo-alvo.

Nesse caso, você pode considerar mudar sua conta do Instagram para uma conta 'comercial'. Esta é uma opção que você pode fazer por si mesmo. Você não precisará da permissão do Instagram para ativar esta opção.

Aqui está como você o ativa no seu perfil ( Atenção : só é possível através do aplicativo móvel):


1. Abra sua conta do Instagram no aplicativo móvel
2. Clique no canto inferior direito do ícone do boneco no aplicativo
3. Escolha o menu 'hambúrguer' no canto superior direito
4. Escolha o ícone de roda dentada 'Configurações'
5. Selecione 'Conta'
6. Escolha 'Alternar para o perfil comercial'

Agora, você é solicitado a fornecer alguns detalhes de contato, como seu endereço de e-mail, número de telefone ou local físico. Isso ocorre porque quando você deseja ser um 'perfil comercial', é importante que seus clientes possam entrar em contato com você. Esteja ciente de que isso também significa que as pessoas que visualizam seu perfil podem reconhecer que você é uma conta comercial.

Se você tiver cem seguidores ou mais, poderá ver o [Insights](https://help.instagram.com/1533933820244654) . As ideias são análises dos seus seguidores.

Esses Insights podem informar quando seus seguidores estão ativos, seu sexo, idade e muito mais. Se você estiver interessado, confira este blog da [Wordstream](https://www.wordstream.com/blog/ws/2018/11/01/instagram-analytics), explicando como usar sua conta do Instagram para fins de marketing. Mas continue lendo com você 'osint-glasses'.


## Estatísticas em um perfil específico do Instagram

No primeiro post 'Pesquisando no Instagram', sugerimos o uso do [Statflux.com](http://statflux.com/) para mostrar estatísticas em uma conta do Instagram. No exemplo da parte 1, usamos o perfil de Mark Zuckbergs como exemplo.

Mas [Stalkture.com](https://stalkture.com/) mostra ainda mais dados. Confira as estatísticas no [perfil de Zuckerberg](https://stalkture.com/a/zuck/314216):


![](https://osintcurio.files.wordpress.com/2019/09/screenshot-2019-09-25-at-21.25.04.png?w=1024)

>Exemplo de Stalkture.com/a/zuck/314216

Ao rolar para baixo, você não apenas verá as estatísticas de classificação, mas também os filtros usados, as postagens mais populares / comentadas / curtidas e muito mais. Dê uma volta!

---

Author: [TECHNISETTE](https://osintcurio.us/author/technisette/)

[Artigo Original](https://osintcurio.us/2019/10/01/searching-instagram-part-2/)










