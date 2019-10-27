---
layout: post
title:  "Como corrigir palavras-chave japonesas que invadiram seu site WordPress?"
date:   2019-10-27 17:57:31 -0200
categories: jekyll update
---


## Japanese Keyword Hack

### O que é spam japonês de SEO no WordPress

O hack de palavras-chave em japonês, também conhecido como spam SEO japonês, spam de pesquisa japonês ou spam de símbolos japoneses, pode ser devastador de se ver no seu site WordPress. Certos sites do WP se queixam de serem afetados por esse tipo de spam de pesquisa que resulta na aparência de páginas invadidas com um título e conteúdo diferentes. Os resultados da pesquisa do Google exibirão as páginas / URLs infectados com caracteres japoneses.

Sites baseados em Sistema de Gerenciamento de Conteúdo (CMS) como WordPress, OpenCart, Drupal ou Magento, quando invadidos, resultam na criação de novas páginas cheias de palavras-chave em japonês com spam (normalmente vistas em index.php, tags e URLs de categorias). Essas páginas infectadas contêm links afiliados para lojas que vendem mercadorias de marca falsificada. Os hackers geram receita com esses links externos inseridos na página do seu site.

### Como identificar o hack de palavras-chave japonesas ?

O Japanese Keyword Hack é um tipo de hack que afeta principalmente os arquivos principais e o banco de dados do site. Navegar por cada arquivo para detectar o hack é um processo cansativo. Você pode seguir três abordagens diferentes para detectar se seu site foi infectado com esse tipo de invasão. Abaixo mencionados são as maneiras de verificar este hack:

### Execute uma verificação de segurança:

Para começar, você pode executar uma verificação de segurança aqui

[![](https://secure.wphackedhelp.com/blog/wp-content/uploads/2017/08/wordpress-security-check.jpg)](https://secure.wphackedhelp.com/scanner.html?affCode=wphhorganic)

### Usando a Pesquisa do Google para identificar páginas invadidas

A pesquisa no Google pode ser o passo inicial para identificar as páginas infectadas no site do WorPress. Para descobrir essas páginas, abra a pesquisa do Google e digite: site: [URL raiz do seu site]

O Google exibirá todas as páginas indexadas do site, incluindo as que foram invadidas. Navegue pelos resultados da pesquisa e verifique se há URLs com aparência suspeita. Caso você encontre algum site com títulos ou descrições em caracteres japoneses, é possível que o site tenha sido infectado.

![Wordpress-Japanese-Keyword-Hack-Search](https://secure.wphackedhelp.com/blog/wp-content/uploads/2018/02/Wordpress-Japanese-Keyword-Hack-Search-3.png)

No entanto, se a pesquisa do Google não fornecer esse conteúdo invadido, tente um mecanismo de pesquisa diferente com os mesmos termos principais. Pode ser que outros mecanismos de pesquisa exibam o conteúdo / URLs infectados que foram removidos do índice do Google.

### Usando o Google Search Console para detectar o conteúdo invadido

O Google aconselha os webmasters a registrar seus sites no Search Console para receber notificações oportunas em caso de invasão. Para procurar as páginas invadidas, acesse o Search Console> ferramenta Security Issue. A ferramenta verificará se alguma das páginas invadidas foi indexada pelo Google.

![](https://secure.wphackedhelp.com/blog/wp-content/uploads/2018/02/japanese-seo-spam-google-search-console-security-issue.png)

### Use Fetch com o Google para detectar cloaking

A camuflagem é uma técnica comum implementada pelos hackers para exibir diferentes URLs ou conteúdo para os usuários e mecanismos de pesquisa do que eles esperavam. O proprietário do site pode ser enganado e exibir um erro de página vazia ou HTTP 404, enquanto o site ainda pode estar invadido. [A ferramenta Fetch do Google](https://www.google.com/webmasters/tools/googlebot-fetch) no Google Search Console deve ser usada para verificar a ocultação. A ferramenta ajudará a ver o conteúdo oculto subjacente.

![](https://secure.wphackedhelp.com/blog/wp-content/uploads/2018/02/Use-Fetch-as-Google.png)


### Como corrigir hack de palavras-chave em japonês no WordPress?

- Antes de começar, é essencial que o site infectado seja temporariamente offline. Isso fornecerá um tempo para remover o hack e também evitará que os usuários visitem as páginas invadidas.
- Além disso, faça um backup dos arquivos principais e do banco de dados do site antes de fazer alterações neles. O backup também conteria as páginas invadidas e deve ser referido apenas se o conteúdo necessário for removido acidentalmente.
- Mantenha uma cópia de todos os arquivos com os quais você trabalha.
- Os métodos sugeridos ou implementados para resolver a preocupação requerem um conhecimento técnico. É recomendável procurar assistência de um profissional para lidar com o problema, se você tiver menos conhecimento sobre JavaScript, arquivos PHP ou CMS do seu site. Você pode nos consultar ou pedir ajuda ao seu provedor de hospedagem.

Para corrigir spam seo japonês do site WordPress, basta seguir estas etapas.

- Remova as contas recém-criadas do Search Console
- Verifique seu arquivo .htaccess
- Use Fetch  como ferramenta do Google
- Remova todos os arquivos e scripts maliciosos
- Verificar arquivos modificados recentemente
- Verifique seu Sitemap
- Execute uma verificação de malware usando o WP Hacked Help
- Criar lista de URLs infectados
- Enviar para remoção na ferramenta de URL no console de pesquisa

Para mais detalhes veja:

### Remover contas recém-criadas suspeitas do Search Console

Os hackers costumam usar uma maneira comum de adicionar contas spam do Gmail como administradores para fazer alterações nas configurações do seu site. Verifique sua conta do Search Console e encontre os novos usuários que foram adicionados.

Se você não reconhecer nenhum usuário, revogue imediatamente o acesso ao site. Para confirmar a legitimidade de um usuário, visite a [página de verificação do Search Console](https://www.google.com/webmasters/verification) que fornecerá uma lista de usuários verificados para o site. Ao clicar em Detalhes da verificação, você pode visualizar todos os usuários verificados para o site.

Para excluir permanentemente um usuário do Search Console, você pode consultar a seção Remover proprietário da Central de Ajuda [Gerenciando usuários, proprietários e permissões](https://support.google.com/webmasters/answer/2453966). O usuário pode ser excluído com êxito somente após remover o token de verificação associado.

Por exemplo, isso foi encontrado em um modelo de um gerador de porta com spam:

```html
<meta name = "confirm-v1" content = "JxC + bn8NTCEfKZIdusC9WQELc8FEwbi8p32wf9q0QGA =">
```

Essa linha de código permite que hackers verifiquem a propriedade de sites comprometidos. Fique de olho nas [verificações maliciosas do Google Search Console](https://blog.sucuri.net/2015/09/malicious-google-search-console-verifications.html)

### Verifique seu arquivo .htaccess

Os invasores usam um arquivo .htaccess para criar tokens de verificação gerados dinamicamente, a fim de criar contas com spam no Search Console. Além disso, esse arquivo é comumente usado para enganar os usuários, mecanismos de pesquisa e redirecioná-los para as páginas maliciosas.

Encontre o arquivo .htaccess no seu site pesquisando o local do arquivo .htaccess em um mecanismo de pesquisa junto com o nome do seu CMS. Nos resultados da pesquisa, faça uma lista de todos os locais de arquivos obtidos. Substitua todos esses arquivos .htaccess por uma versão padrão do arquivo .htaccess.

### Etapas para substituir .htaccess infectado.

Você pode substituir seu .htaccess por uma cópia totalmente nova. Os hackers geralmente usam o htaccess e criam tokens de verificação gerados dinamicamente para redirecionar usuários, caso um site wordpress esteja sendo redirecionado para outro site ou criando páginas de spam sem sentido (tags / categorias) com viagra etc. em urls.


#### Passo 1

- Localize o arquivo .htaccess no WordPress / pesquise "local do arquivo .htaccess"
- Certifique-se de mostrar os arquivos .htaccess ocultos
- Se você tiver 1 ou mais arquivos .htaccess
- então,
- Faça uma lista de todos os locais dos arquivos .htaccess.

#### Passo 2

- Substitua todos os arquivos .htaccess por uma versão limpa ou padrão do arquivo .htaccess.
- Para vários sites com vários arquivos .htaccess, localize uma versão limpa de cada um e substitua.
- No caso de arquivo .htaccess padrão, ele provavelmente pode estar infectado
- Salve uma cópia do arquivo .htaccess
- exclua o arquivo .htaccess infectado do seu site.

Às vezes, pode ser necessário verificar uma regra de reescrita .htaccess antes de aplicá-la. [Use essa ferramenta](http://htaccess.mwl.be/) para testar suas regras de reescrita. Veja também - [.htaccess hackeado Cleanup](https://secure.wphackedhelp.com/blog/wordpress-htaccess-hacked-exploit-cleanup/)

![](https://secure.wphackedhelp.com/blog/wp-content/uploads/2018/02/htaccess-file.png)

### Remova todos os arquivos e scripts maliciosos

- Você deve analisar cuidadosa e minuciosamente seu site WordPress para detectar o código malicioso. A maioria dos hackers direciona os arquivos JavaScript e PHP para invadir um site. Os scripts e códigos são modificados que resultam em páginas invadidas. verifique o tema do wordpress em busca de malware e remova esses códigos para ajudar a limpar o site do wordpress.
- Reinstalando arquivos CMS: para um site baseado em CMS, reinstale todos os arquivos principais para limpar qualquer conteúdo invadido. No entanto, assegure-se de manter um backup de todos os arquivos antes da reinstalação, pois o processo resultará na perda de qualquer personalização feita nos arquivos. Além disso, reinstale os arquivos de quaisquer plugins, módulos, extensões ou temas usados no site.
- É provável que a maioria dos arquivos afetados tenha sido detectada usando os métodos discutidos até o momento. No entanto, é necessário procurar os arquivos recentemente modificados e o mapa do site antes de chegar a uma conclusão.


### Verificar arquivos modificados recentemente

Para procurar os arquivos modificados mais recentemente, use o SSH para fazer login na sua conta do servidor da Web e, em seguida, execute o seguinte comando:

>find/path-of-www -type f -printf ‘%TY-%Tm-%Td %TT %p\n’ | sort -r

Navegue pelos arquivos e veja se você encontrou alguma alteração duvidosa no código. Nesse caso, substitua os arquivos pela versão de backup limpa.

### Verifique seu sitemap

É provável que um hacker adicione um novo mapa do site para que as páginas japonesas de spam de SEO sejam indexadas rapidamente. Verifique se há links suspeitos no seu sitemap e, se detectado, atualize imediatamente seus arquivos principais com uma versão de backup limpa.

![](https://secure.wphackedhelp.com/blog/wp-content/uploads/2018/02/Check-your-sitemap.png)

### Executar uma verificação de malware

Seu servidor da Web pode estar infectado com malware e arquivos maliciosos. É recomendável que você verifique o servidor para detectar arquivos e vírus suspeitos. Verifique a ferramenta Scanner de vírus no cPanel fornecido pelo host da web.

- Analise o seu site usando o WPHackedHelp

![](https://secure.wphackedhelp.com/blog/wp-content/uploads/2018/02/Scan-wordpress-website-free-tool.png)

Depois de listar uma variedade de métodos que exigem conhecimento técnico, vamos considerar uma abordagem mais inteligente, que consome menos tempo e tira o fardo de seus ombros. O [WP Hacked Help](https://secure.wphackedhelp.com/) implementa um plano sistemático para limpar seu site WordPress. O site é completamente verificado e as falhas detectadas são tratadas por uma equipe de especialistas para fornecer a você um site livre de códigos maliciosos. Dentro de um curto espaço de tempo, seu site voltará a funcionar, funcionando com eficiência como antes.

- Verifique o site no Google depois de limpo

É necessário garantir que o site não seja mais afetado por nenhum conteúdo invadido. Torne seu site ativo e use a ferramenta Fetch do Google para detectar se algum conteúdo / URL infectado não foi removido.

O conselho apresentado acima é eficaz para ajudar você a voltar ao seu site "normal" novamente. No entanto, quando o site estiver limpo, implemente dicas de segurança para evitar ataques semelhantes no futuro.

### Como remover URLs de spam de SEO japonês dos resultados do Google?

Depois de limpar seu site, reenvie-o no novo console de pesquisa do Google por meio da nova opção de inspeção de URL na versão atualizada do console de pesquisa ou abra https://search.google.com/search-console/inspect?resource_id=https: //xyz.com.

![](https://secure.wphackedhelp.com/blog/wp-content/uploads/2018/02/URL-Inspection-search_google-console.png)

>> Você também pode enviar manualmente seus URLs com spam que renderizaram 404 após a limpeza do site, através da opção Remover URL no console de pesquisa. Isso removerá seu site que estava exibindo conteúdo de spam dos resultados de pesquisa do Google.

>> Verifique seu arquivo robots.txt, certifique-se de bloquear as tags / páginas de categoria do googlebot. Atualize o robots.txt no console de pesquisa também.

>> Em seguida, vá para a interface do console de pesquisa antiga e selecione a opção REMOVER URL, como visto na imagem abaixo. Isso pode levar muito tempo. Pode demorar uma semana para o Google remover completamente suas páginas de spam seo do idioma japonês dos resultados da pesquisa.

![](https://secure.wphackedhelp.com/blog/wp-content/uploads/2018/02/remove-spam-pages-from-google-Search-Console.png)

### Para sua referência: (Guia visual passo a passo)

![](https://secure.wphackedhelp.com/blog/wp-content/uploads/2018/02/WordPress-Japanese-Keyword-Hack-remove-japanese-seo-spam-pages-from-google.png)

---

[ORIGINAL](https://secure.wphackedhelp.com/blog/fix-wordpress-japanese-keywords-hack/)
