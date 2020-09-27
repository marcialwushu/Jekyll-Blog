---
layout: post
title:  "Criando Windows Services em C#"
date:   2020-03-05 17:59:38 -0200
categories: jekyll update
---

Nesta postagem, veremos como começar a usar C # e .NET criando um serviço básico do Windows com essas tecnologias.

Aqui, vou explicar os serviços do Windows em C # .NET.

- Introdução dos serviços do Windows.
- Como criar serviços do Windows em C # .NET.

## Introdução

Os serviços do Windows normalmente iniciam quando o sistema operacional inicializa e executa um aplicativo em segundo plano. O Windows Services executa aplicativos em sua própria sessão. Ele começa automaticamente ou podemos pausar, parar e reiniciá-lo manualmente.

Você pode encontrar serviços das seguintes maneiras

- Vá para o Painel de Controle e selecione “Serviços” dentro de “Ferramentas Administrativas”.
- Abra a janela Executar (Window + R), digite services.msc e pressione Enter.

## Como criar um serviço do Windows

### Passo 1

Abra o Visual Studio, vá para Arquivo> Novo e selecione Projeto. Agora selecione um novo projeto na caixa de diálogo e selecione “Window Service” e clique no botão OK.

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image001.png)

### Passo 2

Vá para Visual C # -> ”Windows Desktop” -> ”Windows Service,” dê ao seu projeto um nome apropriado e clique em OK

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image002.png)

Depois de clicar em OK, a tela abaixo aparecerá, que é o seu serviço

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image003.png)

### etapa 3

Clique com o botão direito na área em branco e selecione “Adicionar instalador”.

## Adicionando instaladores ao serviço

Antes de executar um serviço do Windows, você precisa instalar o instalador, que o registra no Gerenciador de controle de serviços.

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image004.png)

Após adicionar o instalador, o ProjectInstaller adicionará no seu projeto e o arquivo ProjectInstakker.cs será aberto. Não se esqueça de salvar tudo (pressionando a tecla ctrl + shift + s)

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image005.png)

O Gerenciador de Soluções tem a seguinte aparência:

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image006.png)

### Passo 4

Clique com o botão direito na área em branco e selecione “Exibir código”

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image007.png)

### Etapa 5

Possui um Construtor, que contém o  InitializeComponent método.

O  InitializeComponent método contém a lógica que cria e inicializa os objetos da interface do usuário arrastados na superfície do formulário e fornece a grade de propriedades do Designer de formulários.

Muito importante: nunca tente chamar nenhum método antes de chamar o  InitializeComponent método.  

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image008.png)

### Etapa 6

Selecione o  ```InitializeComponent``` método e pressione a tecla F12 para ir para a definição.

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image008.png)

### Etapa 7

Agora adicione a linha abaixo durante a instalação do serviço:


```cs
this.serviceProcessInstaller1.Account = System.ServiceProcess.ServiceAccount.LocalSystem;
```

Você também pode adicionar uma descrição e exibir o nome do serviço (opcionalmente).


```cs
this.serviceInstaller1.Description = "My First Service demo";  
this.serviceInstaller1.DisplayName = "MyFirstService.Demo";
```

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image009.png)

### Etapa 8

Nesta etapa, implementaremos um cronômetro e um código para chamar um serviço em um determinado momento. Vamos criar uma escrita simples em um arquivo de texto.


![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image010.png)


### Classe Service1.cs 

```cs
using System;  
using System.Collections.Generic;  
using System.ComponentModel;  
using System.Data;  
using System.Diagnostics;  
using System.IO;  
using System.Linq;  
using System.ServiceProcess;  
using System.Text;  
using System.Threading.Tasks;  
using System.Timers;  
namespace MyFirstService {  
    public partial class Service1: ServiceBase {  
        Timer timer = new Timer(); // name space(using System.Timers;)  
        public Service1() {  
            InitializeComponent();  
        }  
        protected override void OnStart(string[] args) {  
            WriteToFile("Service is started at " + DateTime.Now);  
            timer.Elapsed += new ElapsedEventHandler(OnElapsedTime);  
            timer.Interval = 5000; //number in milisecinds  
            timer.Enabled = true;  
        }  
        protected override void OnStop() {  
            WriteToFile("Service is stopped at " + DateTime.Now);  
        }  
        private void OnElapsedTime(object source, ElapsedEventArgs e) {  
            WriteToFile("Service is recall at " + DateTime.Now);  
        }  
        public void WriteToFile(string Message) {  
            string path = AppDomain.CurrentDomain.BaseDirectory + "\\Logs";  
            if (!Directory.Exists(path)) {  
                Directory.CreateDirectory(path);  
            }  
            string filepath = AppDomain.CurrentDomain.BaseDirectory + "\\Logs\\ServiceLog_" + DateTime.Now.Date.ToShortDateString().Replace('/', '_') + ".txt";  
            if (!File.Exists(filepath)) {  
                // Create a file to write to.   
                using(StreamWriter sw = File.CreateText(filepath)) {  
                    sw.WriteLine(Message);  
                }  
            } else {  
                using(StreamWriter sw = File.AppendText(filepath)) {  
                    sw.WriteLine(Message);  
                }  
            }  
        }  
    }  
}
```

Explicação do código - o código acima irá chamar um serviço a cada 5 segundos e criar uma pasta se não existir e escrever nossa mensagem.

### Etapa 9: reconstruir seu aplicativo

Clique com o botão direito em seu projeto ou solução e selecione Reconstruir.

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image011.png)

### Etapa 10

Pesquise “prompt de comando” e execute o programa como administrador:

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image012.png)

### Etapa 11

Acione o comando abaixo no prompt de comando e pressione Enter.


```
cd C:\Windows\Microsoft.NET\Framework\v4.0.30319
```

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image013.png)

### Etapa 12

Agora vá para a pasta de origem do projeto> bin> Debug e copie o caminho completo do arquivo Windows Service.exe



![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image014.png)


![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image015.png)

### Etapa 13 

Abra o prompt de comando, dispare o comando abaixo e pressione Enter.

**Sintaxe**

InstallUtil.exe  +  Seu caminho copiado + \ seu nome de serviço + .exe

**Nosso caminho**

InstallUtil.exe C: \ Users \ Faisal-Pathan \ source \ repos \ MyFirstService \ MyFirstService \ bin \ Debug \ MyFirstService.exe


![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image016.png)

### Etapa 14

Abra os serviços seguindo as etapas abaixo:

1. Pressione a tecla Window + R.
2. Digite services.msc
3. Encontre o seu serviço.

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image017.png)

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image018.png)

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image019.png)

### Saída de serviço  

![](https://www.c-sharpcorner.com/article/create-windows-services-in-c-sharp/Images/image020.png)

Uma pasta de log será criada em sua pasta bin. 

Se você deseja desinstalar o serviço, dispare o comando abaixo.

1. Sintaxe InstallUtil.exe -u + Seu caminho copiado + \ seu nome de serviço + .exe
2. Nosso caminho InstallUtil.exe -u C: \ Users \ Faisal-Pathan \ source \ repos \ MyFirstService \ MyFirstService \ bin \ Debug \ MyFirstService.exe


## Resumo

Neste artigo, aprendemos como criar um serviço do Windows e instalá-lo / desinstalá-lo usando o InstallUtil.exe em um prompt de comando.

Espero ter explicado cada etapa com clareza e que possa ser facilmente compreendida por todos os desenvolvedores. Você pode deixar feedback / comentários / perguntas para este artigo. Por favor, deixe-me saber se você gostou e entendeu este artigo e como eu poderia melhorá-lo.

Eu também carreguei este projeto no GitHub,  [aqui](https://github.com/faisal5170/WindowsService).


---

Autor: [Faisal Pathan](https://dzone.com/users/3360923/faisal5170.html)

[Artigo Original](https://dzone.com/articles/create-windows-services-in-c)













