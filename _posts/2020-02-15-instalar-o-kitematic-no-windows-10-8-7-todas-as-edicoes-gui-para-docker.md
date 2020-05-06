---
layout: post
title:  "Instalar o Kitematic no Windows 10, 8 e 7 todas as edições? GUI para Docker"
date:   2020-02-15 17:59:38 -0200
categories: jekyll update
---


Neste post, mostrarei como instalar o Kitematic no Windows 10, 8 e 7 todas as edições. Kitematic é uma GUI do Docker que facilita o gerenciamento de contêineres do Docker. Anteriormente, expliquei o que é o Docker e como ele pode facilitar a vida dos proprietários de servidores domésticos. Além disso, também mostramos como instalar o Docker no Windows 10 Pro / Ent de 64 bits e em outras edições , bem como no Ubuntu . Ontem, vimos como instalar o SickRage no Docker na linha de comando. Mas, embora seja fácil, e se você tivesse uma GUI para Docker que facilite a instalação e o gerenciamento de contêineres? É disso que trata a Kitematic. Parece emocionante? Vamos ver como instalar o Kitematic no Windows 10, 8 e 7 todas as edições.

**Leitura obrigatória**: Servidor de Mídia Doméstico Smart Ultimate com Docker e Ubuntu 18.04 - Básico

![](https://www.smarthomebeginner.com/images/2016/12/install-kitematic-on-windows-feat-740x400.png)

>Kitematic é uma GUI do Docker que facilita o gerenciamento de contêineres

Índice [ ocultar ]

- Instale o Kitematic no Windows - GUI para Docker
- Instale o Kitematic no Windows 10 Pro, Ent e Edu do Windows 10
    - Crie uma pasta Kitematic
    - Faça o download do Kitematic para Windows
    - Extraia o Kitematic para Windows
- Instale o Kitematic no Windows 7, 8 e 10 (32 bits, 64 bits não Pro / Ent / Edu)
    - Comece a usar o Kitematic no Windows
    


## INSTALE O KITEMATIC NO WINDOWS - GUI PARA DOCKER

Na minha opinião, mesmo se você é um profissional de linha de comando, a GUI do Kitematic Docker pode acelerar significativamente a criação e o gerenciamento de contêineres do docker. O método para configurar o Kitematic no Windows depende da versão e edição do Windows. Este guia aborda os dois cenários: A) como instalar o Kitematic nas edições Professional, Enterprise e Education do Windows 10 e B) Windows 7 (todas as edições), 8 (todas as edições, Windows 10 de 32 bits e Windows 10 de 64 bits) bit não Pro / Ent / Edu. Se você usa o VirtualBox ou o VMware para outros aplicativos de virtualização, o método B é o caminho a seguir, independentemente da versão e edição do Windows.


## A. INSTALE O KITEMATIC NO WINDOWS 10 PRO, ENT E EDU DO WINDOWS 10

Nos Windows 10 Pro, Ent e Edu de 64 bits, o Hyper-V pode ser ativado. Isso permite que o Docker seja instalado nativamente. Isso, no entanto, não oferece a opção de instalar o Kitematic no Windows durante a instalação do Docker. Não tema, a configuração da GUI Kitematic para Docker é bastante fácil.

### 1. Crie uma pasta Kitematic

Primeiro, crie uma pasta para instalar o kitematic no Windows 10. Navegue ```C:\Program Files\Docker``` e crie uma nova pasta chamada ```Kitematic```, como mostrado abaixo.


![](https://www.smarthomebeginner.com/images/2016/12/01-create-kitematic-folder-on-windows10.png)

Você pode receber um aviso de segurança do Windows porque está modificando uma pasta protegida. Ignore o aviso e pressione "Continuar".

### 2. Faça o download do Kitematic para Windows

Verifique se o Docker está em execução. Caso contrário, execute-o no menu de aplicativos do Windows. Aguarde cerca de um minuto para o mecanismo do Docker iniciar. Em seguida, clique com o botão direito do mouse no ícone da bandeja do Docker e clique em "Abrir Kitematic", conforme mostrado na figura abaixo.


![](https://www.smarthomebeginner.com/images/2016/12/01-open-kitematic-on-docker-win-10-pro.png)

>Clique com o botão direito do mouse no ícone da bandeja do docker e abra o Kitematic

Você verá uma solicitação para baixar o Kitematic for Windows. Clique em "Download".

![](https://www.smarthomebeginner.com/images/2016/12/02-download-kitematic-for-windows.png)


>Faça o download do Kitematic no Windows

O Kitematic será baixado como ```Kitematic-Windows.zip``` arquivo. Salve-o em um local conhecido.

### 2. Extraia o Kitematic para Windows

O próximo passo é o passo principal, você deverá extrair o ```Kitematic-Windows.zip``` para o seguinte local:

```
C: \ Arquivos de programas \ Docker \ Kitematic
```

Clique com o botão direito do mouse ```Kitematic-windows.zip``` e selecione "Extrair tudo". Na janela exibida, especifique o caminho de extração, como mostrado abaixo:


![](https://www.smarthomebeginner.com/images/2016/12/03-extract-kitematic-for-windows10.png)

>Extrair Kitematic para Windows

Observe que a pasta de extração padrão aparecerá como "Kitematic-Windows". Você terá que alterar manualmente o caminho correto mostrado acima e pressionar "Extrair". É isso aí. Agora você configurou o Kitematic no Windows 10.

Guias recomendados:

- [O Docker Book: Containerization é a nova virtualização](https://www.amazon.com/Docker-Book-Containerization-new-virtualization-ebook/dp/B00LRROTI4/?tag=htpcbeg-20)
- [Livro de receitas do Docker: soluções e exemplos](https://www.amazon.com/product/dp/149191971X/?tag=htpcbeg-20)


## B. INSTALE O KITEMATIC NO WINDOWS 7, 8 E 10 (32 BITS, 64 BITS NÃO PRO / ENT / EDU)

Se você não possui a edição Pro / Ent / Edu do Windows 10 de 64 bits ou a possui, mas deseja usar a virtualização VirtualBox ou VMware para outros aplicativos, será necessário instalar a Kitematic GUI for Docker usando esse método, que é muito mais simples. que o método A. Nesta versão do Windows, a instalação do Kitematic é feita através do Docker ToolBox. Durante a instalação do Docker com o Docker Toolbox, você também terá a opção de instalar o Kitematic. Caso contrário, siga nosso guia de instalação do Docker com Docker Toolbox, faça o download do Docker Toolbox e execute o instalador. Quando apresentado aos componentes do Docker Toolbox para instalação, verifique se "Kitematic for Windows" está marcado, conforme mostrado abaixo.


![](https://www.smarthomebeginner.com/images/2016/12/03-select-docker-toolbox-components-to-install.png)

>Selecione os componentes da caixa de ferramentas do Docker a serem instalados

Desmarque os componentes que você já possui e conclua a instalação para configurar o Kitematic no Windows 7, 8 e 10 (algumas edições).

### Comece a usar o Kitematic no Windows

Agora que você possui o Kitematic no Windows, abra-o no ícone da bandeja do sistema do Docker (se o método A foi usado) ou no menu Aplicativos (se o método B foi usado). Se você usou o método B, o Kitematic irá parar no meio do caminho durante o início com um erro. Pressione "Use VirtualBox" para continuar iniciando o Kitematic. Após o início bem-sucedido, você verá a tela de registro / login do Docker Hub. Registre-se ou faça login, como mostra a figura abaixo. Você também pode optar por pular esta etapa usando o botão "Pular para agora".


![](https://www.smarthomebeginner.com/images/2016/12/04-sign-up-for-docker-hub-account-740x349.png)

>Registre-se na conta do Docker Hub

Depois de fazer o login, uma nova palavra de possibilidades é a ponta dos dedos. Você pode instalar qualquer um dos contêineres oficiais do docker listados na tela inicial da Kitematic ou procurar o aplicativo em contêiner (por exemplo, Sonarr) e criar um novo contêiner, como mostrado abaixo.


![](https://www.smarthomebeginner.com/images/2016/12/05-install-docker-containers-from-docker-hub-740x206.png)


>Instalar aplicativos em contêiner no Docker Hub


Certifique-se de instalar apenas contêineres de membros da comunidade conhecidos ou com classificações / downloads altos. O Docker isola completamente os contêineres do SO subjacente. Portanto, você não pode prejudicar seu sistema operacional. Assim, você pode instalar e destruir contêineres como desejar, sem causar danos. Então vá em frente, instale o Kitematic no Windows e aproveite o gerenciamento de seus contêineres com a incrível GUI do Docker.

---

Author: [ANAND](https://www.smarthomebeginner.com/author/anand/)

[Arte Original](https://www.smarthomebeginner.com/install-kitematic-on-windows/)


