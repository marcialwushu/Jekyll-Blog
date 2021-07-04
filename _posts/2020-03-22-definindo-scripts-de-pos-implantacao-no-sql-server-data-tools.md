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
