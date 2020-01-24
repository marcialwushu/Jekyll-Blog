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

O arquivo APK final pode ser usado para teste (compilações de depuração) ou liberado na natureza, por meio de uma plataforma de distribuição como o Google Play ou como um pacote APK autônomo que pode ser carregado de lado pelos usuários.

## Inspeção APK

Agora você tem algum conhecimento básico do formato do arquivo APK e podemos começar a analisar esses arquivos.

>**Nota**: O APK do PDF Viewer do PSPDFKit com o nome do pacote ```com.pspdfkit.viewer``` será usado em todos os exemplos abaixo.

Antes de começarmos a inspecionar arquivos APK, primeiro precisamos acessá-los. Isso é simples ao trabalhar com seus próprios aplicativos, pois você já deve ter acesso aos APKs deles. Aplicativos de terceiros podem ser extraídos de qualquer dispositivo em que estejam instalados:

```
adb pull `adb shell pm path 'com.pspdfkit.viewer' | cut -d ':' -f 2` pdf-viewer.apk

```


## Descompactar

Como afirmado anteriormente, um APK é basicamente um arquivo zip. Assim, podemos usar qualquer ferramenta de descompactação ou navegador de arquivos com suporte para arquivos zip para examinar o conteúdo de um APK. Isso, no entanto, tem um caso de uso muito limitado:


- Podemos extrair recursos e ativos que não são processados ou são apenas otimizados durante o processo de compilação. Isso inclui assetsrecursos brutos (in ```res/raw```) e .pngdrawables (que são otimizados, mas ainda estão no formato PNG).
- Não podemos obter muitas informações dos .dexarquivos, pois esses são arquivos binários.
- Não é possível ler recursos binários ( [XML binário](https://en.wikipedia.org/wiki/Binary_XML) e ```resources.arsc```) ou um binário ```AndroidManifest.xml```.

## Android Studio APK Analyzer

A maneira mais simples de decodificar o conteúdo de um APK é usando o Android Studio, que inclui uma ferramenta APK Analyzer que fornece um conjunto abrangente de ferramentas para analisar arquivos APK com uma interface de usuário correspondente. O APK Analyzer pode ser chamado por:

- Arraste e solte o APK na janela do Android Studio.
- Selecionando o APK no item de menu Build> Analyze APK.

## Navegador de arquivos

O APK Analyzer fornece ao navegador de arquivos tamanhos de arquivo e sua porcentagem relativa de todo o tamanho do APK. Esse recurso é útil para identificar as maiores partes do seu aplicativo ao otimizar seu tamanho.

## Decodificador de Recursos Binários

Recursos codificados em binários e ```AndroidManifest.xml``` são decodificados pelo APK Analyzer. Ter acesso ao decodificado AndroidManifest.xmlé especialmente útil para verificar os resultados da fusão de manifesto usada ao criar aplicativos com vários módulos.

![](https://pspdfkit.com/images/blog/2019/inspecting-apk-files/APKAnalyzer-Manifest-289da205.png)

Também temos acesso a recursos descompilados que fazem parte do arquivo de recursos pré-compilados (ou seja ```resources.arsc```).


![](https://pspdfkit.com/images/blog/2019/inspecting-apk-files/APKAnalyzer-Resources-33c42f71.png)

## Dex Decoder

O APK Analyzer fornece um bom suporte para decodificar arquivos Dex.

O recurso mais útil aqui é a coluna Métodos referenciados que mostra as contagens para todas as referências de métodos. Essas informações são úteis ao analisar o número de referências nos aplicativos, a fim de permanecer abaixo do limite de métodos de 64K.


![](https://pspdfkit.com/images/blog/2019/inspecting-apk-files/APKAnalyzer-MethodsCount-fb8e5833.png)

Podemos navegar por todo o código e procurar o uso de classes e métodos clicando com o botão direito do mouse nos nomes de classe ou método e selecionando a opção Localizar usos. Também podemos descompilar classes e métodos em smali bytecode, selecionando a opção Show Bytecode no mesmo menu de contexto.

O que é [smali](https://github.com/JesusFreke/smali) bytecode , você pergunta? Bem, é uma sintaxe de desmontador para o [Dalvik bytecode](https://source.android.com/devices/tech/dalvik/dalvik-bytecode.html) . Sua sintaxe está fora do escopo deste artigo, mas explicaremos como descompilar APKs para um código Java mais legível mais adiante.

## Apktool

O Apktool é uma solução abrangente para desmontar aplicativos Android que possuem mais recursos que o APK Analyzer. Permite extrair e decodificar todos os arquivos no APK com um único comando:

```
apktool d pdf-viewer.apk
```

Isso produz um diretório com recursos decodificados e um manifesto decodificado, junto com o bytecode smali desmontado. O maior benefício do uso do Apktool é a capacidade de editar esses dados desmontados e compilá-los novamente em um arquivo APK em funcionamento. Novamente, isso está fora do escopo deste artigo.

## Extraindo Código Java

Já vimos como inspecionar APKs e desmontar arquivos Dex em códigos de bytes pequenos. Existem algumas ferramentas que podem descompilar o código do aplicativo em um código Java razoavelmente limpo.

Vamos usar essas duas ferramentas:

- [dex2jar](https://github.com/pxb1988/dex2jar) é o conjunto de ferramentas para trabalhar com arquivos Android ```.dex``` e Java ```.class```.
- O [Java Decompiler](http://jd.benow.ca/) (JD-GUI) é um utilitário que exibe o código-fonte Java para ```.class``` ou ```.jar``` arquivos com código de bytes Java.

O primeiro passo é converter o [bytecode Dalvik](https://source.android.com/devices/tech/dalvik/dalvik-bytecode.html) do nosso APK no arquivo JAR com o bytecode Java. Usaremos o prático ```d2j-dex2jar``` do pacote dex2jar:

```
d2j-dex2jar -f pdf-viewer.apk
```

Isso produz o ```pdf-viewer.jar``` arquivo que pode ser aberto diretamente na JD-GUI.

![](https://pspdfkit.com/images/blog/2019/inspecting-apk-files/jd-gui-dc501bfb.png)

A JD-GUI suporta a navegação básica por código - por exemplo, navegando para símbolos sublinhados, procurando símbolos por nome e resolvendo a hierarquia de tipos. No entanto, se você sentir falta do seu editor favorito, poderá extrair todas as fontes em Arquivo> Salvar todas as fontes e abri-las no seu editor de sua escolha.

## ProGuard

Como você pode ver nas capturas de tela acima, a maioria dos símbolos no código descompilado é nomeada com nomes de uma ou duas letras. Esse é o resultado da ofuscação do código do PDF Viewer com o [ProGuard](https://www.guardsquare.com/en/products/proguard#manual/usage.html) . Isso melhora a velocidade e torna um pouco mais difícil para um invasor em potencial navegar pela nossa lógica de negócios interna.

Observe que eu usei a expressão "um pouco mais difícil" na frase anterior. Isso porque o ProGuard dificilmente é suficiente para garantir a segurança do código privado do seu aplicativo. Qualquer pessoa com tempo suficiente pode entender seu código, mesmo ao usar o ProGuard. Você nunca deve incluir nenhuma informação crítica nos negócios em seus aplicativos, pois isso pode ser mal utilizado por alguém com tempo e conhecimento suficientes.

Alguns aplicativos também estão usando soluções comerciais de ofuscação, como o DexGuard , que tornam quase impossível fazer engenharia reversa. O [DexGuard](https://www.guardsquare.com/en/products/dexguard) executa etapas de ofuscação adicionais sobre o ProGuard, incluindo criptografia em tempo de execução de todas as classes e ativos de strings. Use essas soluções se desejar proteger seus aplicativos (em termos práticos) das técnicas de engenharia reversa descritas neste artigo.

## Conclusão

Espero que as técnicas e ferramentas apresentadas neste artigo tenham fornecido informações valiosas sobre como é fácil desmontar a maioria dos aplicativos Android. Espero também que as ferramentas descritas neste artigo se tornem adições indispensáveis ​​ao cinto de ferramentas de desenvolvimento do Android, permitindo melhorar a qualidade dos seus aplicativos, fornecendo informações sobre os APKs de produção.




---

Autor: [Tomáš Šurín](https://twitter.com/tomassurin)

[Artigo Original](https://pspdfkit.com/blog/2019/inspecting-apk-files/)



