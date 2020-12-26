---
layout: post
title:  "Como escrever testes automatizados para aplicativos de console"
date:   2020-03-17 17:59:38 -0200
categories: jekyll update
---

Eu não sei sobre o resto de vocês, mas ainda me vejo escrevendo muitos aplicativos de console. Na maioria das vezes, são utilitários ou serviços ou algum tipo de customização ou scripts de automação de processos. Até recentemente, se eu quisesse escrever testes automatizados para eles, teria que separar a lógica de negócios do próprio programa e testar as funções. Embora seja obviamente uma boa prática para qualquer projeto moderadamente complexo, às vezes pode ser muito complicado para o que é necessário. Além disso, isso não funciona para testes de aceitação do usuário de caixa preta .

## A classe System.Console

No .NET Framework, os aplicativos de console giram em torno, bem, da classe Console . Você obtém a entrada do usuário com ```Console.Read()``` (e ```ReadLine()``` e ```ReadKey()``` e assim por diante). Por outro lado, você envia a saída para o usuário com ```Console.Write()``` e ```Console .WriteLine()``` .
Portanto, vamos dar uma olhada no código dentro do .NET Framework. A propósito, usei o JustDecompile da Telerik para navegar pelo código. Se você ainda não tem um descompilador de escolha, sugiro que dê uma olhada nele. É simples, elegante e gratuito (e não, não tenho estoque).

Então, aqui está o código por trás de Console.ReadLine ():

```cs
   1: public static string ReadLine()
   2: {
   3:     return Console.In.ReadLine();
   4: }
```


E aqui está Console.WriteLine () :

```cs
   1: public static void WriteLine()
   2: {
   3:     Console.Out.WriteLine();
   4: }
```

Acontece que os métodos de leitura e gravação do Console são meramente métodos de passagem que chamam os mesmos métodos nas propriedades In e Out TextReader e TextWriter (novamente - respectivamente).

As classes de leitor e escritor de texto, como tão eloquentemente colocado nas descrições das aulas no MSDN, “representam um leitor [e escritor] que pode ler [e escrever] uma série sequencial de caracteres”. Bem, isso ainda é mais útil do que algumas descrições que eu vi ... De qualquer forma, eles são os pais abstratos das classes leitor (e escritor) de string e stream . Por que isso é importante? Bem, as propriedades In e Out são, por padrão, definidas para os fluxos de entrada do teclado e saída da tela.

Agora, se ao menos houvesse uma maneira de redirecionar esses streams ...

Digite Console.SetIn () e Console.SetOut () respectivamente. Hmm, isso é muito mais respeito do que normalmente mostro em uma postagem de blog ...

Com **SetIn** , posso redirecionar o **In** texto-leitor para uma [**StringReader**](http://msdn.microsoft.com/en-us/library/system.io.stringreader.aspx) , e com **SetOut** , eu redirecionar a saída para um [**StringWriter**](http://msdn.microsoft.com/en-us/library/system.io.stringwriter.aspx).

Agora posso inicializar facilmente o leitor de string com um valor que contém qualquer entrada ou conjunto de entradas que desejo usar, e o aplicativo de console lerá os caracteres ou linhas conforme necessário. Posso então ler a saída do escritor de string e compará-la com os resultados esperados.

E a parte mais bonita de tudo isso é que não há (quase) **necessidade de modificar o aplicativo do console de forma alguma** para que isso funcione.

## Exemplo

O exemplo a seguir foi escrito em C #, usando MS-Test (perdoe-me) para testar o código. O aplicativo é simples e reproduz o jogo 7-Boom (uma variação local do jogo [BizzBuzz](http://en.wikipedia.org/wiki/Bizz_buzz) ). Como você verá, exceto para tornar a classe **Program** e o método **Main()** públicos nas linhas 1 e 3, para que eu possa acessar o código de outro assembly (teste), não fiz nada que não faria em qualquer outro aplicativo de console :

```cs

   1: public class Program
   2: {
   3:     public static void Main()
   4:     {
   5:         Console.Write("Enter upper limit: ");
   6:         var range = int.Parse(Console.ReadLine());
   7:  
   8:         for (var i = 0; i < range; i++)
   9:         {
  10:             var num = ((i % 7 == 0) || i.ToString().Contains('7')) ? "BOOM" : i.ToString();
  11:             Console.Write("{0}, ", num);
  12:         }
  13:     }
  14: }


```

E aqui está um teste:

```cs

   1: // Arrange
   2: using (var sw = new StringWriter())
   3: {
   4:     using (var sr = new StringReader("100"))
   5:     {
   6:         Console.SetOut(sw);
   7:         Console.SetIn(sr);
   8:  
   9:         // Act
  10:         SevenBoom.Program.Main();
  11:  
  12:         // Assert
  13:         var result = sw.ToString();
  14:         Assert.IsFalse(result.Contains('7'));
  15:     }
  16: }


```

É isso aí! Eu defino a entrada que o usuário teria inserido na linha 7 e redireciono a E / S nas linhas 6-7. Resta afirmar que a produção da linha 14 atende às expectativas.

A propósito, isso funciona exatamente da mesma forma em Java e em C#. A diferença é que em Java você usará System.setIn() e System.setOut() para definir os PrintStreams (as propriedades In e Out usadas em Console.Read & Console.Write).

Portanto, agora você pode escrever aplicativos de console orientados por teste (e orientados por comportamento) com maior facilidade.

Espero que isto ajude,


---


[Artigo Original](http://www.softwareandi.com/2012/02/how-to-write-automated-tests-for.html?m=1)

