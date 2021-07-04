---
layout: post
title:  "Definindo scripts de pós-implantação no SQL Server Data Tools"
date:   2020-03-22 17:59:38 -0200
categories: jekyll update
---

## Problema

Talvez eu tenha me precipitado um pouco, mas comecei a usar o SQL Server Data Tools (SSDT) no Visual Studio 2010. Desde então, me tornei o maior fã do SSDT. A ferramenta é muito mais fácil de usar do que os antigos projetos de banco de dados do VS 2010. Mas, infelizmente, por algum motivo, não consigo fazer meus scripts de pós-implantação funcionarem quando publico o projeto em um banco de dados ativo. Tenho vários scripts de pós-implantação que preenchem diferentes tabelas de pesquisa em meu banco de dados. Mas quando vejo essas tabelas no SQL Server Management Studio depois de publicar, os dados simplesmente não estão lá. Qualquer ajuda que você possa dar seria muito apreciada. Confira esta dica para saber mais. 

## Solução

Seu entusiasmo é compreensível, dada a reação positiva esmagadora ao SSDT entre os desenvolvedores do SQL Server. É ótimo, por exemplo, ter uma visão de designer e uma visão T-SQL (mostrada abaixo) quando você está projetando ou refatorando tabelas SQL. O fato de as alterações em ambas as visualizações serem imediatamente sincronizadas e verificadas quanto à sintaxe torna a experiência do usuário agradável e eficiente. 

![](https://www.mssqltips.com/tipImages2/2852_TableDesigner.gif)

Como você provavelmente sabe, outro motivo para a popularidade do SSDT é a estrutura de pasta achatada do tipo de projeto dentro do Gerenciador de Soluções do Visual Studio. O SSDT apresenta um novo modelo de projeto no Visual Studio (o tipo * .sqlproj) que substitui efetivamente o tipo de projeto de banco de dados VS 2010 mais antigo. Uma das diferenças entre os dois é que o tipo de projeto antigo tinha muitas (e muitas!) Pastas junto com muitos (e muitos!) Arquivos de script diferentes. Aqui está um exemplo do antigo tipo de projeto de banco de dados no Visual Studio. 

![](https://www.mssqltips.com/tipImages2/2852_DbProjectFolders.png)

Compare isso com a nova estrutura de pastas de um projeto SSDT abaixo. Você também deve ter em mente que agora (felizmente) os scripts de objeto relacionados à criação de tabelas não estão espalhados por meia dúzia de pastas como era o caso para projetos * .dbproj. Aqui está um exemplo do novo tipo de projeto SSDT * .sqlproj no VS Solution Explorer: 

![](https://www.mssqltips.com/tipImages2/2852_SqlProjectFolders.png)

Observe que as antigas pastas Pós-implantação e Pré-implantação sumiram. Em vez disso, você obtém uma estrutura de projeto agradável e limpa que é dinamicamente adaptada com base nos objetos existentes em seu banco de dados importado. Portanto, se o banco de dados Northwind contivesse funções definidas pelo usuário no momento da importação, também haveria uma pasta para esses objetos. Claro, isso não resolve as pastas de implantação ausentes (eu sei, eu sei, você amou essas pastas, não é?). O Visual Studio, é claro, facilita a adição de suas próprias pastas a qualquer tipo de projeto, portanto, se você realmente deseja segregar os scripts pós-implantação em uma pasta separada, certamente pode fazê-lo. 

![](https://www.mssqltips.com/tipImages2/2852_AddaFolder.png)

É bom saber também que, se você passar pelo exercício de conversão de um projeto de banco de dados antigo para o novo tipo de projeto SSDT, tenha certeza de que a estrutura e os scripts da pasta Script / Implantação existentes serão preservados no novo projeto SSDT.

## Então, quantos scripts de pós-implantação você possui?

Na verdade, a única resposta correta para essa pergunta é "uma". (E, sim, o Visual Studio irá avisá-lo se você tentar adicionar mais de um script de pós-implantação ao projeto.) Por convenção, muitas pessoas chamam esse arquivo de algo como MainDeployment.sql. Nesse único script de pós-implantação, normalmente o arquivo contém uma lista de SQLCMD: r comandos de leitura que incluem (analisam) scripts externos adicionais. O script de pós-implantação e cada um dos scripts externos incluídos deve ter as propriedades de arquivo de script apropriadas para funcionar da maneira que você deseja. "Então, quais são essas propriedades?", Você pode perguntar. Bem, suponha que eu tenha adicionado uma estrutura de pastas de Scripts | Pós-implantação para meu projeto SSDT conforme ilustrado abaixo.

![](https://www.mssqltips.com/tipImages2/2852_SqlProjWithFoldersByMike.png)

Agora posso clicar com o botão direito na pasta Post-Deployment, clicar em Add New Item e selecionar User Scripts from Installed Templates. Clicar no modelo Post-Deployment Script adiciona o script ao meu projeto. 

![](https://www.mssqltips.com/tipImages2/2852_AddPostDeploymentScript.png)

Uma vez que o arquivo de modelo é adicionado, simplesmente clique com o botão direito em seu nome no Solution Explorer e selecione Propriedades no menu de contexto. Podemos ver que uma das propriedades do arquivo para o script de pós-implantação define uma ação de construção de PostDeploy. Dependendo de seus requisitos de construção, você pode escolher Copiar ou Não Copiar o arquivo de script para o Diretório de saída. 

![](https://www.mssqltips.com/tipImages2/2852_PostDeployBuildAction.png)

Como mencionei antes, às vezes os desenvolvedores gostam de organizar vários arquivos na pasta Pós-implantação e incluí-los do arquivo de script pós-implantação por meio do comando SQLCMD: r read. Em nosso último exemplo, adicionei um arquivo de script externo separado chamado AlterDbSizeGrowth.sql ao projeto para alterar o tamanho e as características de crescimento do banco de dados Northwind. 

```sql
/* Please do not change the database path or name variables. It will be properly coded for build 
and deployment.  This example is using sqlcmd variable substitution. */
ALTER DATABASE [$(DatabaseName)]
 MODIFY FILE
 (
  NAME = [$(DatabaseName)],
  SIZE = 6MB, FILEGROWTH = 1MB
 )
GO     
ALTER DATABASE [$(DatabaseName)]
 MODIFY FILE
 (
  NAME = [$(DatabaseName)_log],
  SIZE = 2MB, FILEGROWTH = 1MB
 )
GO  
```

Para este script, uma vez que é um arquivo externo que é 'incluído' no script de pós-implantação, as propriedades de arquivo apropriadas são significativamente diferentes. Aqui, a Ação de construção é Nenhuma, conforme mostrado abaixo. 

## Próximos passos

- Sempre verifique a ação Build para todos os scripts em uma pasta Post-Deployment.
- Certifique-se de que Build Action seja PostDeployment para o único script de pós-implantação.
- Certifique-se de que Build Action seja None para qualquer arquivo de script externo incluído em um script de pós-implantação.
- Saiba mais sobre as ferramentas disponíveis no SQL Server. 


---


Autor: [Mike Bishop](https://www.mssqltips.com/sqlserverauthor/101/mike-bishop/)

[Artigo Original](https://www.mssqltips.com/sqlservertip/2852/defining-post-deployment-scripts-in-the-sql-server-data-tools/)
     

