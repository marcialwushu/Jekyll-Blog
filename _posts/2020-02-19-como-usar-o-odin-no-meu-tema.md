---
layout: post
title:  "Como usar o Odin no meu tema?"
date:   2020-02-19 17:59:38 -0200
categories: jekyll update
---


E ae, meu povo. Tudo bem?

Hoje eu venho falar um pouco do fucking framework [Odin](http://wpod.in/):

![](https://i1.wp.com/mariovalney.com/wp-content/uploads/2016/06/odin-logo-stacked.png?w=757&ssl=1)

>Um framework que chuta bundas!

Criado pelo [Grupo WordPress Brasil](https://www.facebook.com/groups/wordpress.brasil), Odin é um framework com objetivo de turbinar e agilizar o desenvolvimento de temas para WordPress.

## Como conheci

Antes de falar das funcionalidades dele ou de como usar no seu tema, vou falar de como conheci o Odin.

Desenvolvo com o WordPress há um tempo já e fui melhorando meu código a cada tema desenvolvido (sempre que possível, prefiro desenvolver o tema “do zero”, com um front-end próprio para o projeto) e criei [minha própria classe de criação de conteúdo](https://gist.github.com/mariovalney/c8a37371a9c618fc0dad29d628577d0d), afinal o WordPress não é só um CMS (o considero um framework bem robusto) e nos permite criar nossos próprios [formatos de conteúdo](https://codex.wordpress.org/Post_Types) (além de regras de usuário, taxonomias, conectar com o banco e mais meio milhão de coisas), como vocês devem saber.

Ela otimizou bastante meu trabalho e resolvi criar logo outras classes para tudo o que eu geralmente preciso: plugins, taxonomias, opções do tema e Ajax. Mas antes, fui procurar se já não havia algo do tipo e encontrei o Odin. Simplesmente perfeito.

P.S.: Nunca contribui com o Odin, mas pretendo pegar algo pra fazer lá, assim que possível, para “pagar” pelo uso :P


## Como criar um tema do zero com o Odin

Se você quer criar um tema desde o início, basta fazer o download no [site oficial](http://wpod.in/) e ser feliz alterando o nome da pasta, o arquivo style.css e seguir alterando os arquivos que já estão lá.

Se você não lembra da Hierarquia de Modelos do WordPress, consulte a [documentação oficial](https://codex.wordpress.org/pt-br:Hierarquia_de_Modelos_WordPress) para refrescar a memória e depois é só ir consultando a documentação do Odin, que é muito foda boa:


## Conteúdo:

- [Custom Post Types/Tipos de conteúdo](https://github.com/wpbrasil/odin/wiki/Classe-Odin_Post_Type)
- [Taxonomias personalizadas](https://github.com/wpbrasil/odin/wiki/Classe-Odin_Taxonomy)
- [Custom Post Status/Status de posts personalizados](https://github.com/wpbrasil/odin/wiki/Classe-Odin_Post_Status)
- [Opções para termos](https://github.com/wpbrasil/odin/wiki/Classe-Odin_Term_Meta)

## Administração:

- [Metaboxes/Opções para posts/páginas](https://github.com/wpbrasil/odin/wiki/Classe-Odin_Metabox)
- [Opções para perfis de usuários](https://github.com/wpbrasil/odin/wiki/Classe-Odin_User_Meta)
- [Opções para o Tema](https://github.com/wpbrasil/odin/wiki/Classe-Odin_Theme_Options)
- [Personalizando o Admin](https://github.com/wpbrasil/odin/wiki/Customizando-o-Admin)

## Outras:

- [Formulários de contato](https://github.com/wpbrasil/odin/wiki/Classe-Odin_Contact_Form)
- [Shortcodes integrados](https://github.com/wpbrasil/odin/wiki/Classe-Odin_Shortcodes)
- [Usando o Grunt](https://github.com/wpbrasil/odin/wiki/Usando-o-Grunt)
- [Usando o Sass](https://github.com/wpbrasil/odin/wiki/Usando-o-Sass)

Preciso nem dizer que a classe **Odin_Theme_Options** é extremamente útil, né?

## Como alterar meu tema com o Odin

Agora sim! O maior objetivo desse texto é ajudar a galera que já possui um tema ou vai criar um Tema Filho e quer usar algumas funcionalidades do Odin. Lembrando que, pelo menos, uma noção de WordPress e PHP são obrigatórias para tudo na vida mexer nos arquivos dos temas, plugins ou mesmo para usar o Odin.

Antes de qualquer coisa, se você quer alterar um tema comprado (ou não) e ainda quer manter as alterações quando fizer atualizações, considere [criar um Tema Filho](https://mariovalney.com/como-criar-um-tema-filho-child-theme-para-wordpress/).

### 1 – Adicione o core

Com tudo no lugar, faça download do Odin e jogue a pasta **/core** para dentro do seu tema. Copiar e colar.

### 2 – Inclua os arquivos

Vá no seu **functions.php** e adicione, logo no começo (ou onde você achar melhor), os arquivos das classes que você vai querer:

```php
// See in Matrix =D
// Nesse exemplo, iremos usar a classe de metaboxes:
require_once get_template_directory() . '/core/classes/class-metabox.php'
```

### 3 – Código!

Agora que você já incluiu os arquivos e sabe o que quer, basta olhar a documentação específica de cada Classe para aprender a usá-la.

A documentação é bem completa, por exemplo, vamos adicionar uma metabox para uma segunda imagem destacada:

>O problema: meus posts precisam, além da Imagem Destacada, uma imagem específica para o compartilhamento no Facebook.

Já adicionamos os arquivos e “chamamos” a classe no functions.php, certo? Então agora é código.
Olhando a documentação, vimos que para [criar uma metabox](https://github.com/wpbrasil/odin/wiki/Classe-Odin_Metabox#criando-um-metabox) basta instanciar a classe. E pelo exemplo faremos isso dentro da [action init](https://codex.wordpress.org/Plugin_API/Action_Reference/init) (prometo tirar um dia para explicar os Hooks – actions e filters), então vamos adicionar a [action](https://codex.wordpress.org/Plugin_API/Action_Reference):


```php
// See in Matrix =D
add_action( 'init', 'meu_tema_metabox_segunda_imagem' );
```

E agora criamos a função, instanciando a classe:


```php
// See in Matrix =D
function meu_tema_metabox_segunda_imagem() {
    $segunda_imagem_metabox = new Odin_Metabox(
        'segunda_imagem', // Slug/ID do Metabox (obrigatório)
        __( 'Imagem do Facebook', TEXTDOMAIN ), // Título do Metabox já pronto para tradução (obrigatório)
        'post', // Slug do Post Type, sendo possível enviar apenas um valor ou um array com vários (opcional)
        'side', // Contexto (opções: normal, advanced, ou side) (opcional)
        'low' // Prioridade (opções: high, core, default ou low) (opcional)
    );
}

```


Pronto! Já podemos ver a metabox:

![](https://i0.wp.com/mariovalney.com/wp-content/uploads/2016/06/Metabox-vazia.png?resize=301%2C415&ssl=1)


Agora precisamos [adicionar os campos](https://github.com/wpbrasil/odin/wiki/Classe-Odin_Metabox#adicionando-campos-no-metabox). A documentação também é bastante clara nessa parte e podemos criar vários tipos de campos e mais de 1 campo por vez.

No momento, queremos apenas 1 campo e será um campo de imagem, então acrescento à função o código abaixo:


```php
// See in Matrix =D
function meu_tema_metabox_segunda_imagem() {
    $segunda_imagem_metabox = new Odin_Metabox(
        'segunda_imagem', // Slug/ID do Metabox (obrigatório)
        __( 'Imagem do Facebook', TEXTDOMAIN ), // Título do Metabox já pronto para tradução (obrigatório)
        'post', // Slug do Post Type, sendo possível enviar apenas um valor ou um array com vários (opcional)
        'side', // Contexto (opções: normal, advanced, ou side) (opcional)
        'low' // Prioridade (opções: high, core, default ou low) (opcional)
    );
 
    $segunda_imagem_metabox->set_fields(
        array(
            array(
                'id'          => 'imagem_facebook', // ID único do Campo (obrigatório)
                'label'       => __( 'Escolha uma imagem para o Facebook', TEXTDOMAIN ), // Label do Campo (obrigatório)
                'type'        => 'image', // Tipo do Campo (obrigatório)
                'description' => __( 'Recomendamos um tamanho mínimo de 1200x630.', TEXTDOMAIN ) // Descrição do campo (opcional)
            )
        )
    );
}
```

Agora a metabox ficou assim:



![](https://i1.wp.com/mariovalney.com/wp-content/uploads/2016/06/Metabox-de-Imagem.png?resize=291%2C334&ssl=1)


Legal, né? O comportamento já está todo aí. Basta usar!!!

### 4 – Alterando o Tema

Agora que o WordPress já cuida do upload e cadastro desse campo, você só precisa “imprimir” a imagem no seu tema, né? Para recuperar o valor do campo basta fazer:


```php
// See in Matrix =D
<?php get_post_meta( $post->ID,'imagem_facebook', true ); ?>
```

Voltando ao nosso exemplo, como nosso problema dita que queremos alterar a imagem exibida no compartilhamento do Facebook, começamos a pesquisar nos arquivos e notamos que no **header.php** tem o seguinte código:

```php
// See in Matrix =D
<?php
    $facebook_image = get_option( 'meu_tema_facebook_image_default', '' );
?>
<meta property="og:image"  content="<?php echo $facebook_image ?>" >

```

Então precisamos verificar se estamos mostrando a página do Post e então pegar o valor que cadastramos com ajuda do Odin:


```php
// See in Matrix =D
<?php
    global $post;
 
    $facebook_image = get_option( 'meu_tema_facebook_image_default' );
 
    if ( is_singular( 'post' ) ) {
        $facebook_image = get_post_meta( $post->ID, 'imagem_facebook', true ); // Recuperando o valor
        $facebook_image = wp_get_attachment_image_src( $facebook_image, 'full' ); // Recuperando os dados do attachment (no tamanho full)
        $facebook_image = $facebook_image[0]; // Pegando a URL (primeiro parâmetro)
    }
?>
<meta property="og:image"  content="<?php echo $facebook_image ?>" >

```


Pronto! Tudo OK.

Sobre o código, esqueci de comentar, mas tem na documentação: o tipo de campo image armazena apenas o ID da imagem. Sendo assim, temos que usar uma das funções que ele recomenda: eu escolhi a [wp_get_attachment_image](https://developer.wordpress.org/reference/functions/wp_get_attachment_image_src/)_src que retorna a URL, dentre outras informações para montarmos o HTML.

Ainda sobre o código: ele é bem simples. Não validei no caso de não ter imagem cadastrada, nem de ter algum problema, afinal é só pra entender a lógica do negócio.


## Quer contribuir com o Odin?

Eu ainda não fiz o fork, nem sugeri nada lá, mas assim que tiver tempo vou atrás de retribuir o trabalho da galera ajudando no que eu puder.

O Odin é um projeto totalmente Open Source, então quem quiser contribuir, basta ir [clicar aqui e ir no GitHub](https://github.com/wpbrasil/odin/blob/master/docs/README-pt_BR.md#contribua-com-o-projeto) dar uma olhada.



## Conclusão

E por hoje é só.

O foco hoje foram os desenvolvedores iniciantes e a galera que precisa mexer no próprio site e se arrisca pelos códigos. Notei que aparece muita gente assim no grupo do WordPress Brasil e assim terei esse artigo para indicar sempre que aparecer alguém com dúvida.

Espero que tenha ajudado a você e não esqueça de compartilhar a palavra curtindo e enviando para os amigos, nem de deixar seu comentário abaixo.


---

Author: [Mário Valney](https://mariovalney.com/sobre/)

[Artigo Original](https://mariovalney.com/como-usar-o-odin-no-meu-tema/)


