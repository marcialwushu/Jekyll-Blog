---
layout: post
title:  "ANÁLISE QUALITATIVA DE CÓDIGO COM SONARQUBE"
date:   2020-01-20 17:59:38 -0200
categories: jekyll update
---

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e376a07663eaa488ffabb77/dcb1fa2fe36d2779ac760dbc2efb816d/resultado-analise-05.png)

## INTRODUÇÃO


Qualidade de código é um assunto, por vezes, pouco debatido. Muitas vezes, nos limitamos a entender este tema por um simples “código que funciona”. Mas, isto é realmente suficiente?


## AFINAL, O QUE É QUALIDADE DE CÓDIGO?


Existem muitas definições sobre o que é um bom código. Recentemente, li o excelente livro Clean Code (Robert Martin, 2009) e lá temos diversas definições sobre o tema. Mas um ponto em comum entre os autores que contribuíram para o livro é: um bom código é simples e eficiente. Para alcançar tal objetivo, diversos programadores ao longo dos anos criaram algumas dezenas de regras e design patterns, a fim de resolver este problema.


## O SONARQUBE

O SonarQube é uma plataforma de código aberto desenvolvida pela SonarSource para inspeção contínua da qualidade do código para realizar revisões automáticas com análise estática de código para detectar bugs, códigos cheirosos e vulnerabilidades de segurança em 20+ linguagens de programação.

Ele oferece relatórios sobre código duplicado, padrões de codificação, testes de unidade, cobertura de código, complexidade de código, comentários, bugs e vulnerabilidades de segurança. (Fonte: Wikipedia)


## VAMOS FAZER UM PROJETO DE EXEMPLO…


Agora, vamos criar um projeto de exemplo. O código fonte deste projeto pode ser encontrado em https://gitlab.com/orlandoburli/calculadora-de-impostos.


![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e376a07663eaa488ffabb77/54254aa9b330d7c3724283d7c4dbc807/codigo-01.png)


>Fig.1 – Código fonte da aplicação a ser analisada.

O projeto é simples, é uma calculadora de impostos. Uma simples classe que recebe um valor bruto e calcula ICMS e IPI, e devolve o valor líquido.


## PREPARANDO O AMBIENTE


Para sermos rápidos e práticos, vamos usar um container docker para rodar o sonarqube. Para isso, basta executar o comando:


```
docker run -d --name sonarqube -p 9000:9000 sonarqube

```

Com isso, já temos o Sonar Qube executando em sua máquina. Para acessá-lo, abra em seu navegador o endereço http://localhost:9000 e entre com o usuário admin e senha admin.


![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e376a07663eaa488ffabb77/bda275a1dc4ab133d5d081c6f1897d23/sonar-tela-inicial-01.png)


>Fig. 2 – Tela Inicial do Sonar Qube


## RODANDO A ANÁLISE

Vamos, agora, executar a análise do código. Para isso, basta entrar no diretório do projeto e executar o comando maven: ```mvn sonar:sonar```

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e376a07663eaa488ffabb77/21cbbf9505e8281e45df2b1c4f9a992f/resultado-comando-sonar-01.png)

>Fig. 3 – Resultado da execução do código do sonar.


## RESULTADO DA ANÁLISE

Agora, vamos ver o resultado desta análise. No nosso projeto, ele apontou informações importantes, conforme abaixo:

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e376a07663eaa488ffabb77/d34ef136dbef9eb9973c186e55d6e9ba/resultado-analise-01.png)


>Fig. 4 – Tela inicial do sonar com o resultado do projeto

A primeira informação que temos é a nota: A para nosso projeto. Isso quer dizer que o projeto está bem, de acordo com os gateways de qualidade, pois se trata de um projeto pequeno.

Porém, ele aponta algumas irregularidades, o que quer dizer que ainda não estamos perfeitos: Diz que temos 3 “code smells” (código mal-feito, em tradução livre). Também diz que temos 0% de cobertura de testes.

Vamos, então, detalhar o que ele está apontando como “code smells”:


![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e376a07663eaa488ffabb77/a0f7ffcdba65b05493d316984f0e2469/resultado-analise-05_(1).png)

>Fig. 5 – Detalhamento dos “code smells” apontados pelo SonarQube.

Vamos, agora, analisar os 3 itens, ponto a ponto:

**Move the array designator from the variable to the type**

Este item está relacionado a esta linha de código:

```
public static void main(final String args[]) {
```



Ele está dizendo que o array de args[] deveria estar no tipo String, e não no nome da variável, deixando o código desta maneira:

```
public static void main(final String[] args) {
```

**Replace this use of System.out or System.err by a logger**


Este item está relacionado a esta linha de código:

```
System.out.println(new Calculadora().calcularValorLiquido(100.00));
```

Como estamos imprimindo a saída no console, ele diz que é uma má prática fazer isso em projetos. Então, ele nos sugere usar alguma biblioteca de log para escrevermos na saída do console.

**Immediately return this expression instead of assigning it to the temporary variable “valorLiquido”.**

Este item está relacionado a esta linha de código:

```
final double valorLiquido = valorBruto - icms - ipi;
```

Basicamente, ele está dizendo que não há necessidade de eu criar a variável ```valorLiquido```, e que eu deveria retornar imediatamente o valor da expressão ```valorBruto - icms - ipi```.


Sendo assim, este trecho de código mudaria para:


```
public double calcularValorLiquido(final double valorBruto) {

	final double icms = valorBruto * 0.12;
	final double ipi = valorBruto * 0.03;

	return valorBruto - icms - ipi;
}
```

Desta forma, nosso código final completo ficou assim:


```
package br.com.orlandoburli.calculadora;

import java.util.logging.Logger;

public class Calculadora {

	private static Logger logger = Logger.getLogger("calculadora");

	public static void main(final String[] args) {
		logger.info(String.format("Valor líquido: %1$,.2f", new Calculadora().calcularValorLiquido(100.00)));
	}

	public double calcularValorLiquido(final double valorBruto) {

		final double icms = valorBruto * 0.12;
		final double ipi = valorBruto * 0.03;

		return valorBruto - icms - ipi;
	}
}
```

## RE-EXECUTANDO A ANÁLISE

Com as alterações sugeridas implementadas, vamos agora executar a análise novamente, executando o comando mvn sonar:sonar.


![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e376a07663eaa488ffabb77/4670104fc660f80fdeded3d1464ab87a/nova-analise-01.png)

>Fig. 6 – Resultado da nova análise

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e376a07663eaa488ffabb77/bcdd18817652e3d1cc22801e304c0cb2/nova-analise-02.png)

>Fig. 7 – Detalhe do Resultado da nova análise

Veja que agora temos apenas 1 code smell, referente à nossa nova implementação usando logger. Ele diz que esse método deve ser chamado de forma condicional, de forma que ele não execute a expressão contida no logger se o nível de log INFO não estiver habilitado – uma boa prática que resulta em ganho de performance. Você pode continuar refatorando seu código até o ponto em que ficar satisfeito, ou até zerar os “code smells”.


## CONCLUSÃO

O SonarQube é uma excelente ferramenta, e que está em constante evolução. Vale muito a pena utilizá-la em seus projetos, para que você não tenha simplesmente um código que funcione, mas um código que funcione bem, seguindo todo um conjunto de boas práticas.


---

Autor: [ORLANDO BURLI JÚNIOR](https://blog.impulso.network/author/orlandoburli/)

[Artigo Original](https://blog.impulso.network/analise-qualitativa-de-codigo-com-sonarqube/)



