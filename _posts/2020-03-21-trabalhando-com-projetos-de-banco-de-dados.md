---
layout: post
title:  "Trabalhando com Projetos de Banco de Dados"
date:   2020-03-21 17:59:38 -0200
categories: jekyll update
---

Neste artigo, vou falar sobre como desenvolver e implantar um projeto de banco de dados, também conhecido como um aplicativo da camada de dados usando o Visual Studio. Em meu artigo anterior, Introdução aos aplicativos da camada de dados usando o Visual Studio, forneci uma visão geral dos aplicativos da camada de dados e como podemos criar um usando o Visual Studio. Este artigo é uma continuação do artigo anterior. Aconselho você a dar uma olhada nisso antes de prosseguir com isso, pois esta é uma continuação do anterior. Para o artigo, eu usaria o Visual Studio 2019, no entanto, você pode usar qualquer outra versão do Visual Studio.

Neste artigo, mencionarei como criar objetos de banco de dados como tabelas, procedimentos armazenados e usar variáveis SQLCMD nos scripts. Também demonstrarei como organizar seu código para os projetos de banco de dados usando estruturas de diretório. Finalmente, iremos construir o projeto de banco de dados e implantá-lo em uma instância do SQL Server. 


## Criando a Estrutura do Projeto e as Melhores Práticas

Vamos primeiro começar criando uma estrutura de diretório para nosso projeto. Essa não é uma lista compreensiva; no entanto, é minha recomendação criar uma estrutura de diretório antes de iniciar o desenvolvimento. Será mais fácil gerenciar seu código posteriormente, quando você tiver muitos arquivos para gerenciar. A ideia principal é criar diretórios individuais para cada um dos esquemas que usaremos no projeto. Por exemplo, se pretendemos desenvolver o código para dois esquemas - “dbo” e “estágio“, devemos criar diretórios de nível pai para os esquemas e, em seguida, organizar os outros objetos sob eles.

Para criar um novo diretório no projeto de banco de dados, clique com o botão direito do mouse no nome do projeto e selecione Adicionar e, em seguida, selecione Nova Pasta.

![](https://www.sqlshack.com/wp-content/uploads/2021/01/creating-new-directories-for-the-schemas.png)

Figura 1 - Criação de novos diretórios para os esquemas

Depois de criar os diretórios para seus esquemas, a próxima etapa é criar diretórios para cada um dos principais objetos de banco de dados que você irá desenvolver. Por exemplo, podemos precisar criar tabelas, procedimentos armazenados, funções e visualizações em cada um desses esquemas. Portanto, criaríamos um diretório para cada um deles em ambos os esquemas. Você pode consultar o diagrama abaixo para entender como os diretórios devem ser criados. 


![](https://www.sqlshack.com/wp-content/uploads/2021/01/project-directory-structure-e1611315439638.png)

Figura 2 - Estrutura do diretório do projeto

Você pode adicionar diretórios à medida que se sentir confortável para usar. Isso é apenas para organizar seu código, pois essas estruturas não importam durante a construção ou implantação do aplicativo.

## Criação de objetos de banco de dados

Agora que criamos nossa estrutura de diretório, vamos criar os objetos de banco de dados individuais. Vamos primeiro criar uma tabela no esquema dbo.

Clique com o botão direito no diretório Tables, selecione Add e então selecione Tables. Como alternativa, você também pode selecionar Novo item na lista suspensa e, em seguida, selecionar Tabelas na lista. 


![](https://www.sqlshack.com/wp-content/uploads/2021/01/creating-tables-in-the-data-tier-application.png)

Figura 3 - Criação de tabelas no aplicativo da camada de dados

No painel Novo item, selecione Tabelas e forneça um nome para a tabela. Você pode seguir as práticas recomendadas ao nomear as tabelas de dimensão e de fato, no entanto, para manter as coisas simples, vamos manter os nomes simples também. 

![](https://www.sqlshack.com/wp-content/uploads/2021/01/naming-tables-in-the-project.png)

Figura 4 - Tabelas de nomenclatura no projeto

Depois que o nome for fornecido, clique em Adicionar e você verá o painel do designer de tabela aberto no Visual Studio. Neste painel, existem dois componentes principais, o painel de design e o painel do editor T-SQL. Usando o Painel de Projeto, você pode criar a estrutura da tabela sem escrever nenhum código T-SQL. Basta inserir os nomes das colunas e selecionar o tipo de dados no menu suspenso e pronto. Ele irá gerar automaticamente os nomes das colunas para o seu aplicativo, que você pode ver no editor T-SQL abaixo. Este é um recurso muito útil e ajuda a desenvolver tabelas rapidamente sem ter que se preocupar em escrever todo o T-SQL manualmente. É aconselhável verificar a consulta SQL assim que a tabela for concluída. 

![](https://www.sqlshack.com/wp-content/uploads/2021/01/create-table-using-design-pane.png)

Figura 5 - Crie uma tabela usando o Painel de Projeto

Da mesma forma, você também pode adicionar tabelas e outros objetos, como procedimentos armazenados, em outros esquemas. Você também pode adicionar este projeto sob controle de origem, como Git. Isso o ajudará a manter uma versão do banco de dados conforme você continua com o desenvolvimento. Sempre que você atualizar seu código, certifique-se de atualizar o número da versão na propriedade do arquivo DACPAC. Portanto, toda vez que você pode implantar uma nova versão de seu código no servidor de banco de dados. 


## Building e Deployment

Agora que adicionamos nossos objetos de banco de dados ao projeto, estamos prontos para começar a construir o projeto e implantá-lo no servidor de banco de dados. Antes disso, precisaremos nos certificar dos dois itens a seguir.

- O diretório de construção - O diretório no qual os arquivos de construção serão colocados
- A conexão de banco de dados de destino - em qual servidor de banco de dados o projeto de banco de dados será implantado

Você pode visualizar o diretório de construção visualizando as Propriedades do projeto e, em seguida, selecionar Construir. Por padrão, deve estar em “bin\Debug\“.

Visualizando o diretório de construção do projeto

![](https://www.sqlshack.com/wp-content/uploads/2021/01/viewing-the-build-directory-for-the-project.png)

Figura 6 - Visualização do diretório de construção do projeto

Para a Conexão de banco de dados de destino, clique em Depurar e editar a string de conexão de destino. Certifique-se de apontar para o servidor de banco de dados correto, caso contrário, o projeto de banco de dados será implantado em algum outro servidor não pretendido. 

![](https://www.sqlshack.com/wp-content/uploads/2021/01/selecting-target-database-string.png)

Figura 7 - Seleção da string do banco de dados de destino

Observe o nome do banco de dados de destino na string de conexão. É com esse nome que o banco de dados será criado no servidor.

Agora que verificamos ambos os detalhes, vamos prosseguir e construir o projeto de banco de dados. Para construir o projeto, você pode clicar em Build na barra de Menu e selecionar Build Solution. Alternativamente, você também pode pressionar Ctrl + Shift + B para construir seu projeto.

Assim que você começar a construir seu projeto de banco de dados, verá a saída da janela abaixo, que se parece com a figura a seguir. 

![](https://www.sqlshack.com/wp-content/uploads/2021/01/build-output.png)

Figura 8 - Build output do projeto de banco de dados

Agora você também pode verificar os arquivos de construção navegando até o diretório de construção que verificamos nas etapas acima. 

![](https://www.sqlshack.com/wp-content/uploads/2021/01/build-directory.png)

Figura 9 - Construir diretório

No diretório de construção, haverá principalmente três arquivos disponíveis, conforme a seguir.

- Arquivo DACAPC - O arquivo de construção do projeto de banco de dados
- Arquivo DLL - contém a extensão do aplicativo
- PDB - contém o banco de dados de depuração do programa

Agora, vamos implantar este projeto de banco de dados no local do banco de dados de destino. Clique com o botão direito no projeto e selecione Publicar. O painel Publicar banco de dados é exibido onde você precisa verificar a conexão do banco de dados de destino. Além disso, certifique-se de marcar as caixas de seleção que dizem Registrar como um aplicativo da camada de dados. 

![](https://www.sqlshack.com/wp-content/uploads/2021/01/publish-database-pane.png)

Figura 10 - Painel de Publicação de Banco de Dados

Depois de verificar os detalhes, você pode clicar no botão Publicar. Você notará que o painel de Operações de Ferramentas de Dados dispara e o progresso está sendo exibido. A implantação levará algum tempo, dependendo do número de objetos no projeto de banco de dados. 

![](https://www.sqlshack.com/wp-content/uploads/2021/01/database-publish-successful.png)

Figura 11 - Publicação do banco de dados com sucesso

Agora você pode ir em frente e verificar o banco de dados no SQL Server Management Studio. Como você pode ver na figura abaixo, o banco de dados foi criado e contém as colunas que definimos no projeto de banco de dados. 

![](https://www.sqlshack.com/wp-content/uploads/2021/01/database-created-in-sql-server.png)

## Conclusão

Neste artigo, demonstrei como definir uma estrutura de diretório para organizar seu código. Também entendemos como criar vários objetos de banco de dados dentro da estrutura de diretório que definimos. Por fim, construímos e implantamos nosso projeto usando o Visual Studio e verificamos esse banco de dados no SQL Server usando o SQL Server Management Studio. Nos artigos a seguir, demonstrarei os usos mais avançados dos aplicativos de banco de dados. 

---

Autor: [Aveek Das](https://www.sqlshack.com/author/aveek-das/)

[Artigo Original](https://www.sqlshack.com/working-with-database-projects/)
