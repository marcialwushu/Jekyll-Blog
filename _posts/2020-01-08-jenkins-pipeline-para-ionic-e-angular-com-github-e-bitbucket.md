---
layout: post
title:  "Jenkins Pipeline para Ionic e Angular com Github e Bitbucket"
date:   2020-01-08 17:59:38 -0200
categories: jekyll update
---


O Ionic é uma das melhores estruturas de desenvolvimento de aplicativos para dispositivos móveis disponíveis no mercado atualmente. A maioria das organizações no mundo recente está usando o Jenkins como uma ótima ferramenta para automatizar processos de construção, integração contínua e implantação automatizada. Jenkins ajuda as organizações a automatizar todos os aspectos do desenvolvimento e economizar um tempo precioso para os desenvolvedores. Esta publicação também demonstra como usar o pipeline GitHub e Bitbucket para integração e implantação contínuas do aplicativo Ionic.

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/pipeline.png?raw=true)

## Por que Bitbucket?

Nos últimos dias, o número de usuários do GitHub está migrando seus repositórios para o Bitbucket. Os usuários podem obter tudo o que tinham no Github no Bitbucket com muitas outras opções, como repositórios particulares com espaço limitado. O Bitbucket possui um pipeline para processar a integração e entrega contínua incorporada e também possui um melhor espelhamento. Este artigo explica o poder do Jenkins na criação e implantação de aplicativos iOS usando o pipeline de Bitbucket.

**Tutorial em vídeo - Pipeline Jenkins para Ionic e Angular com Github e Bitbucket**

[![](https://i.ytimg.com/vi/q5voVJb3rHI/hqdefault.jpg)](https://youtu.be/q5voVJb3rHI)

## Instalação do Jenkins

Baixe o software Jenkins em https://jenkins.io/download/


![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/step1.png?raw=true)

Conceda permissões de leitura e gravação para a pasta secrets . Você terá uma senha de administrador da Jenkin.

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/step2.png?raw=true)

Instale plugins padrão.

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/step3.png?raw=true)

Configure a senha do administrador.

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/step4.png?raw=true)

Se você quiser, pode modificar a porta do servidor.

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/step5.png?raw=true)

Agora pronto para usar Jenkins.

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/step6.png?raw=true)



## Configuração Ionic

```
$ sudo npm install -g ionic cordova
```


### Criar e iniciar um projeto ionic

Aqui, o novo comando iônico cuidará dos arquivos de dependência do projeto. Use o comando ionic serve para iniciar o aplicativo.

```
$ ionic start ionicJenkins tabs

$ cd ionicJenkins

$ ionic serve
```

## Estágios do projeto ionic

Você precisa implementar os seguintes estágios para o projeto Ionic ou Angular para automatizar o processo. Você pode ignorar o Web Build , se não quiser publicar no site.

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/stages.png?raw=true)

### Estágio 1 - NPM Install

download das dependências do node.

```
$ npm install
```

### Etapa 2 - iOS Build

ionic, isso é apenas para usuários de Mac.

```
$ ionic cordova build ios --release
```

### Etapa 3 - Android Build

Android build para lançamento. Certifique-se de instalar o Android Studio com todas as dependências

```
$ ionic cordova build android --release
```

### Etapa 4 - APK Sign

Assinando o arquivo APK. Vou explicar mais no meu próximo artigo.

```
$ jarsigner -storepass your_password -keystore keys/yourkey.keystore platforms/android/app/build/outputs/apk/release/app-release-unsigned.apk nameApp
```

### Etapa 5 - Web Build (Angular Project)

Pasta de distribuição da Web

```
$ npm run build --prod
```

### Etapa 6 - Firebase Deployment  

nuvem do Firebase, saiba mais sobre a implantação do projeto Angular no Firebase

```
$ firebase deploy --token "YourTokenKey"
```

## Arquivo de pipeline do Jenkins

Crie um arquivo de pipeline com o nome Jenkinsfile sem nenhuma extensão de arquivo. Use o comando vi no terminal ou cmder (Windows)

```
$  vi Jenkinsfile
```


**Jenkinsfile**

Inclua todos os estágios no pipeline do Jenkins.


```json

   agent any
      environment {
         PATH='/usr/local/bin:/usr/bin:/bin'
      }
   stages {
      stage('NPM Setup') {
      steps {
         sh 'npm install'
      }
   }

   stage('IOS Build') {
   steps {
      sh 'ionic cordova build ios --release'
     } 
  }

   stage('Android Build') {
   steps {
      sh 'ionic cordova build android --release'
   }
  }

   stage('APK Sign') {
   steps {
      sh 'jarsigner -storepass your_password -keystore keys/yourkey.keystore platforms/android/app/build/outputs/apk/release/app-release-unsigned.apk nameApp'
   }
   }

   stage('Stage Web Build') {
      steps {
        sh 'npm run build --prod'
    }
  }

   stage('Publish Firebase Web') {
      steps {
      sh 'firebase deploy --token "Your Token Key"'
   }
  }

   stage('Publish iOS') {
      steps {
       echo "Publish iOS Action"
    }
   }

   stage('Publish Android') {
     steps {
    echo "Publish Android API Action"
   }
  }

 }
}

```

## Criar novo item de pipeline Jenkins

Jenkins menu click , clique em Novo item e forneça o nome.

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/itemname.png?raw=true)

## Pipeline multibranch

Esta opção vem com a configuração de arquivo Jenkins padrão. Se essas opções não estiverem disponíveis, vá para Gerenciar Jenkins e pesquise e instale o plug-in Multibranch

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/multipipe.png?raw=true)

## Branch Source

Aqui, selecione a fonte da sua filial como Github, Bitbucket etc.

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/branch.png?raw=true)

## Adicionar credenciais

Configure com suas credenciais de repositório.

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/github.png?raw=true)

## Adicione Proprietário

Proprietário como o nome de usuário do seu repositório. Isso promoverá com todos os detalhes do seu repositório. Agora escolha sua ramificação de arquivo Jenkins de desenvolvimento

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/projects.png?raw=true)

## Configuração da compilação

Se o seu arquivo Jenkins estiver em um local diferente, altere o caminho aqui e salve o pipeline

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/confi.png?raw=true)

## Scanning The Branch Index

Jenkins verificará as ramificações de seu repositório

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/scan.png?raw=true)

## Pipeline

Pipeline branch foi criada. Você pode clicar no nome da filial e executar a compilação.

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/branchPipe.png?raw=true)


## Run Build Now

o menu Build Now a direita clique no link 

![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/menu.png?raw=true)

## Etapas do pipeline


![](https://github.com/srinivastamada/9lessonsImages/blob/master/jenkins/stages.png?raw=true)

---

Autor:  [SRINIVAS TAMADA](https://www.blogger.com/profile/17418084732618477326)

[Artigo Original](https://www.9lessons.info/2018/08/jenkins-pipeline-ionic-github-bitbucket.html)












