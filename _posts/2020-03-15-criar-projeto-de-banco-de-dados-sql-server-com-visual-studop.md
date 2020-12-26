---
layout: post
title:  "Criar projeto de banco de dados SQL Server com Visual Studio"
date:   2020-03-15 17:59:38 -0200
categories: jekyll update
---

## Introdução

Quando trabalhamos em qualquer projeto, um banco de dados desempenha um papel importante e depois de algum tempo, quando o número de tabelas, visualizações e procedimentos aumenta - torna-se muito difícil gerenciar os scripts.

E mesmo depois disso, quando gerenciamos os scripts, ainda precisamos comparar em qual script trabalhamos e quais permanecem em qualquer banco de dados específico. Existem muitas ferramentas boas disponíveis no mercado para comparar bancos de dados, mas a maioria delas é paga.

Portanto, neste artigo, aprenderemos como podemos gerenciar nossos scripts de banco de dados usando o projeto de banco de dados SQL Server do Visual Studio.

Podemos criar um novo projeto de banco de dados e importar o esquema do banco de dados de um banco de dados existente, um arquivo de script .sql ou um aplicativo da camada de dados (.dacpac). Podemos então invocar as mesmas ferramentas de designer visual (Transact-SQL Editor, Table Designer) disponíveis para o desenvolvimento do banco de dados conectado para fazer alterações no projeto de banco de dados offline e publicar as alterações de volta no banco de dados de produção. As alterações também podem ser salvas como um script a ser publicado posteriormente. Usando o painel Propriedades do projeto, podemos alterar a plataforma de destino para diferentes versões do SQL Server (incluindo SQL Azure).

## Pré-requisito

- VS2015 ou VS2017 deve ser instalado em sua máquina.
- Servidor SQL - para importar script de banco de dados e publicar scripts novos ou alterados.

Vamos começar!!

1. Abra o VS e crie um novo projeto a partir do Menu, selecione Arquivo >> Novo >> Projeto.

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image001.png)

2. Selecione SQL Server >> SQL Server Database Project. Agora, digite o nome do projeto e pressione OK.

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image002.jpg)

3. Depois que o projeto é criado, podemos ver o projeto de banco de dados no Solution Explorer.

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image003.jpg)

4. Clique com o botão direito em DemoDatabase Project e em Import >> .dacpac ou Database / Script para importar scripts do banco de dados existente.

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image004.jpg)

5. Em seguida, selecionamos Banco de dados >> Selecione a conexão.

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image005.jpg)

6. Insira as credenciais e o nome do banco de dados >> conectar

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image006.png)

7. Agora, podemos ver o nome do servidor, o nome do banco de dados em Conexão do banco de dados de origem >> Iniciar

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image007.png)

8. Importou com sucesso todos os scripts para logins, esquemas, tabelas, procedimentos, etc. >> Selecione Concluir 

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image008.jpg)

9. Todos os scripts são importados para a solução - agora podemos adicionar ou alterar scripts a partir daqui.

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image009.png)

10. Vamos criar uma réplica do banco de dados azure que importamos para a solução no servidor local - clique com o botão direito nas propriedades e selecione Destino

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image010.png)

11. Para publicar scripts no banco de dados, selecione Publicar

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image011.png)

12. Agora, selecione o servidor e banco de dados onde devemos publicar os scripts - botão Editar

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image012.jpg)

13. Insira o nome do servidor, a autenticação e selecione o banco de dados no menu suspenso. Pressione Test Connection apenas para garantir que as informações fornecidas estão corretas. Em seguida, pressione OK.

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image013.png)

14. Podemos salvar um perfil usando o botão Salvar perfil como - para que não tenhamos que inserir novamente as configurações relacionadas à conexão na próxima vez. Depois disso, podemos gerar script ou publicar as alterações diretamente no banco de dados.

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image014.jpg)

15. Se pressionarmos Generate Script, podemos ver o script comparado na nova aba do Visual Studio. Podemos verificar o script e depois disso pressione Executar

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image015.png)

16. As alterações são publicadas com sucesso no banco de dados local.

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image016.jpg)

17. Podemos verificar nosso banco de dados usando o SQL Server Management Studio.

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image017.png)

Todas as tabelas, procedimentos, visualizações, etc. foram preenchidos como estão. Não precisamos escrever nenhum script de migração como costumávamos fazer para a migração do banco de dados.

E depois disso, sempre que houver alterações nas tabelas ou nos procedimentos basta fazer as alterações nos scripts da solução e publicá-los no banco de dados - o VS irá criar o alter script de acordo.

Assim, gerenciar nosso banco de dados agora se torna mais fácil usando o SQL Server Database Project.

---

Autor: [Srashti Jain](https://www.c-sharpcorner.com/members/srashti-jain)

[Artigo Original](https://www.c-sharpcorner.com/article/create-sql-server-database-project-with-visual-studio/)


