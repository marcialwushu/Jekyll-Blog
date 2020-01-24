---
layout: post
title:  "Inspecionando arquivos APK"
date:   2020-01-09 17:59:38 -0200
categories: jekyll update
---


![](https://pspdfkit.com/images/blog/2019/inspecting-apk-files/article-header-cde00e41.png)

Este artigo apresenta os conceitos básicos da engenharia reversa do Android. Uma das aplicações mais úteis dessas técnicas é a engenharia reversa de seus próprios aplicativos para avaliar o quão difícil seria abusar do seu código privado (por exemplo, contornar as verificações de licença). Outro aplicativo útil é aprender como um determinado aplicativo resolve um problema técnico interessante ou trabalha com problemas de plataforma ou fornecedor.

Observe que as informações neste artigo não se destinam a pirataria ou outros usos ilegais. Seu principal objetivo é mostrar como inspecionar aplicativos Android existentes apenas para fins educacionais.

## O que são arquivos APK?

Os aplicativos Android são distribuídos como arquivos APK. Os arquivos APK são basicamente arquivos [ZIP](https://en.wikipedia.org/wiki/Zip_(file_format)) semelhantes aos arquivos [JAR](https://en.wikipedia.org/wiki/JAR_(file_format)) usados ​​para empacotar bibliotecas Java. Um arquivo APK contém código de aplicativo no formato de arquivo [DEX](https://source.android.com/devices/tech/dalvik/dex-format.html) , bibliotecas nativas, recursos, ativos etc. Ele deve ser assinado digitalmente com um certificado para permitir a instalação em um dispositivo Android.

## Conteúdo do pacote APK

Um arquivo APK é um pacote compactado que contém os seguintes arquivos e diretórios:

- ```assets``` - diretório com ativos de aplicativo.
- ```res```- diretório com todos os recursos que não são compilados resources.arsc. Estes são todos os recursos, exceto os arquivos res/values. Todos os recursos XML são convertidos em [XML binário](https://en.wikipedia.org/wiki/Binary_XML) e todos os .pngarquivos são otimizados (trituradores) para economizar espaço e melhorar o desempenho do tempo de execução ao inflar esses arquivos.
- ```lib``` - diretório com bibliotecas nativas compiladas usadas pelo seu aplicativo. Contém vários diretórios - um para cada arquitetura de CPU suportada ( [ABI](https://pspdfkit.com/guides/android/current/faq/architectures/) ).
- ```META-INF``` - diretório com metadados APK, como sua assinatura.
AndroidManifest.xml- manifesto do aplicativo no formato de arquivo [XML binário](https://en.wikipedia.org/wiki/Binary_XML) . Ele contém metadados do aplicativo - por exemplo, nome, versão, permissões etc.
- ```classes.dex``` - arquivo com o código do aplicativo no formato de arquivo [Dex](https://source.android.com/devices/tech/dalvik/dex-format.html) . Pode haver arquivos .dex adicionais (nomeados ```classes2.dex``` etc.) quando o aplicativo usa [multidex](https://developer.android.com/studio/build/multidex) .
- ```resources.arsc``` - arquivo com recursos pré-compilados, como seqüências de caracteres, cores ou estilos.

## Processo de compilação do APK

O processo de compilação do aplicativo Android é bastante complexo. Vamos nos aprofundar um pouco para que você possa entender de alto nível como o APK é produzido.

1. O processo começa com o código-fonte do aplicativo em Java / Kotlin, junto com suas dependências. Primeiro, esse código-fonte é compilado no bytecode Java usando compiladores Java / Kotlin. Observe que as dependências do aplicativo já estão compiladas e não requerem processamento adicional nesta etapa. Isso inclui as dependências do Android enviadas como arquivos [AAR](https://developer.android.com/studio/projects/android-library#aar-contents) e dependências apenas do Java na forma de arquivos [JAR](https://en.wikipedia.org/wiki/JAR_(file_format)) .
2. O bytecode Java produzido na etapa anterior, juntamente com todas as dependências, é convertido em arquivos Dex contendo o bytecode Dalvik que podem ser executados em dispositivos Android. Isso produz o classes.dexarquivo (ou vários classes*.dexarquivos, se o multidex estiver ativado).
3. Os recursos do aplicativo são compilados com a [Ferramenta de empacotamento de ativos Android](https://developer.android.com/studio/command-line/aapt2) . Essa ferramenta processa todos os recursos em um formato binário otimizado para uso do Android. Sua saída é um arquivo APK com todos os recursos, exceto o código - ou seja, os diretórios assetse res, o resources.arscarquivo com recursos pré-compilados e o manifesto do aplicativo.
4. O código do aplicativo compilado com todos os classes.dexarquivos produzidos na etapa 2 e as bibliotecas nativas são compactados no arquivo APK.
5. O arquivo APK é então otimizado com [zipalign](https://developer.android.com/studio/command-line/zipalign) . Esta etapa garante que todos os dados não compactados no arquivo APK estejam alinhados com um limite de quatro bytes para melhorar o desempenho do tempo de execução ao acessar grandes dados binários, como imagens.
6. Por fim, o arquivo APK é assinado digitalmente para que possa ser verificado e instalado em qualquer dispositivo Android.


---

[Artigo Original](https://pspdfkit.com/blog/2019/inspecting-apk-files/)



