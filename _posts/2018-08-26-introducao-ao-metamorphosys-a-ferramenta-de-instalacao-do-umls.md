---
layout: post
title:  "Introdução ao MetamorphoSys - A Ferramenta de Instalação do UMLS"
date:   2018-08-26 02:43:31 -0200
categories: jekyll update
---



## O que é o UMLS?

O Unified Medical Language System é um repositório de vocabulários biomédicos desenvolvido pela National Library of Medicine dos EUA.

A UMLS integra mais de 2 milhões de nomes para cerca de 900.000 conceitos de mais de 60 famílias de vocabulários biomédicos, bem como 12 milhões de relações entre esses conceitos.

Os vocabulários integrados no Metathesaurus da UMLS incluem:

- Taxonomia NCBI
- Ontologia Genética
- The Medical Subject Headings (MeSH)
- OMIM
- A Base de Conhecimento Simbólica Anatômica Digital.

Um uso poderoso do UMLS é vincular informações de saúde, termos médicos, nomes de medicamentos e códigos de faturamento em diferentes sistemas de computadores. Alguns exemplos disso são:

- Vinculando termos e códigos entre seu médico, sua farmácia e sua companhia de seguros
- Coordenação de atendimento ao paciente entre vários departamentos dentro de um hospital

O UMLS tem muitos outros usos, incluindo recuperação de mecanismos de pesquisa, mineração de dados, relatório de estatísticas de saúde pública e pesquisa de terminologia.

Além dos dados, o UMLS inclui ferramentas para personalizar o Metathesaurus (MetamorphoSys), para gerar variantes lexicais de nomes de conceitos (lvg) e extrair conceitos UMLS do texto (MetaMap).

## O que é o MetamorphoSys?

O MetamorphoSys é o assistente de instalação da UMLS e a ferramenta de personalização do Metathesaurus incluída em cada versão da UMLS. Ele instala uma ou mais das fontes de conhecimento da UMLS.

MetamorphoSys é usado para:

- Criar um subconjunto personalizado de Metathesaurus da UMLS e é necessário para instalar as fontes de conhecimento UMLS mais atuais.
- Navegando e consultando o Metathesaurus.
- Obtendo e exportando os scripts de carregamento para uso em outros aplicativos.

## Então, vamos começar e configurar a ferramenta!

## Passo 1:

Primeiro, precisamos acessar o portal UTS (UMLS Terminology Services) para baixar a ferramenta e os arquivos relacionados.

Precisamos solicitar uma licença e inscrever-se para uma conta UTS (UMLS Terminology Services). Solicitar uma licença UMLS e criar uma conta UTS é um processo de duas etapas

- Envie sua solicitação de licença
- Autentique o pedido após o recebimento do e-mail
- Mais sobre solicitações de licença estão disponíveis [aqui](http://www.nlm.nih.gov/databases/umls.html#license_request).

## Passo 2:

Depois de fazer o login no UTS, siga o link UMLS Knowledge Sources abaixo do título Downloads na barra de menu.

![](http://blog.appliedinformaticsinc.com/wp-content/uploads/2015/05/umls.jpg)

Existem dois lançamentos principais mostrados:

- A versão completa: A versão completa inclui todos os vocabulários do Metathesaurus.
- A versão ativa: A versão ativa inclui apenas vocabulários ativamente atualizados no Metathesaurus.

Então, vamos com o download de arquivos completos de lançamento. Os arquivos de lançamento são bem grandes; o download só é recomendado com uma conexão de internet de alta velocidade.

Atualmente os arquivos mostrados para o ano de 2014 estão listados abaixo, e aqueles em negrito são os arquivos de dados com tamanho grande, e o em verde é a própria ferramenta:

- 2014AB.CHK
- 2014AB.MD5
- 2014AB-1-meta.nlm (1.5 GB)
- 2014AB-2-meta.nlm (1.4 GB)
- 2014AB-otherks.nlm (1 GB)
- mmsys.zip (250 MB)
- Copyright_Notice.txt
- README.txt
- 2014AB UMLS Active Release Files

## Etapa 3:

Então agora começamos a definir o ambiente para configurar a ferramenta em si.

A ferramenta mmsys é baseada em java, portanto, certifique-se de ter o JRE em sua máquina; aqui está um bom link, se você ainda não o instalou na sua máquina (você pode verificar digitando java –version no seu terminal).

Para ter certeza de que estamos na mesma página; Copie todos os arquivos baixados na mesma pasta.

- Agora extraia o conteúdo do mmsys.zip na mesma pasta.
- Abra uma janela de terminal e mude para o diretório dos arquivos baixados. Digite o comando apropriado para sua plataforma:

  - ./run.bat (Windows)
  - ./run_mac.sh (ou clique no arquivo run_mac.command)
  - ./run_linux.sh

- Talvez seja necessário permitir que as permissões de execução dos arquivos acima permitam que elas executem e iniciem a ferramenta. Em sistemas baseados em unix nós apenas fazemos isso por:

  - sudo chmod 777 run_linux.sh

- Se tudo correr bem, a ferramenta Metamorphosys será lançada (veja imagem abaixo):

![](http://blog.appliedinformaticsinc.com/wp-content/uploads/2015/05/umls-1.jpg)

## Passo 4:

Para validar todas as coisas estão intactas basta clicar em Arquivo> Validar Distribuição,

![](http://blog.appliedinformaticsinc.com/wp-content/uploads/2015/05/validation-tool.png)

Após a conclusão da validação, você receberá o log de validação. Então, finalmente, você está pronto para instalar os recursos UMLS (Navegador, Scripts de Carregamento, etc).

Na próxima parte, começaremos a instalar a ferramenta, obtendo scripts SQL para trabalhar / navegar por dados localmente e muito mais.

[Artigo Original](http://blog.appliedinformaticsinc.com/getting-started-with-metamorphosys-the-umls-installation-tool/)

Tradução: [Cleilson](https://marcialwushu.github.io/)