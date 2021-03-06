---
layout: post
title:  "CTF - Capture The Flag"
date:   2019-03-25 00:43:31 -0200
categories: jekyll update
---

# CTFS

## O QUE SÃO CTFS?

CTF significa Capture the Flag. No âmbito da informática, são competições que envolvem diversas competências dos profissionais/estudantes/entusiastas para a resolução de desafios relacionados à infosec (segurança da informação), com o objetivo de capturar a bandeira (normalmente um código) e pontuar.

## TIPOS DE CTFS:

Existem dois tipos de CTFs, os Jeopardy-style (estilo Quiz), que normalmente são online e servem como Qualificatórias para as Finais de Attack/Defense, que são realizadas on-site (offline). Ainda há a possibilidade do evento ser “híbrido”, e misturar os dois tipos, como é o caso do CTF brasileiro Pwn2Win.

**Attack/Defense**: de forma genérica, as equipes recebem uma VM com diversos serviços (alguns vulneráveis), e o objetivo é capturar as bandeiras alheias e proteger as do seu time com patchs.

**Jeopardy-style**: são apresentadas questões de diversas categorias, níveis de dificuldade e pontuações. As categorias variam de competição pra competição, mas as principais são:

- **Reversing** (Eng. Reversa). Ex: [Rev 100 – 2º HnR](http://ctf-br.org/wiki/hnr/hnr2/r100-it-rules/).
- **Crypto** (Criptografia). Ex: [Crypto 100 – SECCON 2014](http://ctf-br.org/wiki/seccon/seccon2014/c100-easy-cipher/).
- **Forensics** (Forense). Ex: [For 20 – Pwn2Win 2014](http://ctf-br.org/wiki/pwn2win/pwn2win2014/f20-k1k0/).
- **Miscellaneous** (Diversos). Ex: [Misc 100 – 3º HnR](http://ctf-br.org/wiki/hnr/hnr4/m100/).
- **Trivias** (Triviais).
- **Web Hacking**. Ex: [Web 100 – SECCON 2014](http://ctf-br.org/wiki/seccon/seccon2014/w100-jspuzzle/).
- **Networking** (Redes).
- **Pwnables/Exploitation** (Exploração de binários). Ex: [Exploitation 20 – ADCTF 2014](http://ctf-br.org/wiki/adctf/adctf2014/day-20-easypwn/).
- **PPC** (Professional Proramming and Coding). Ex: [PPC  7 – ADCTF 2014](https://ctf-br.org/wiki/adctf/adctf2014/p7-reader-day-7-2/).


Para saber mais, acesse: <https://ctftime.org/ctf-wtf/>

## DOCS 

Disponibilizaremos aqui links para materiais (artigos, guias, palestras, etc) e tudo mais que podem ajudá-lo em sua trajetória no Maravilhoso Mundo das Competições Capture the Flag! Eventualmente tentaremos traduzir alguns docs para ajudar quem ainda não tem familiaridade com a língua inglesa.

- [A Brief History of CTF](https://psifertex.github.io/a-brief-history-of-ctf/) – Bela apresentação do psifertex, contando um pouco da história dos CTFs.

- [CTF Field Guide](https://trailofbits.github.io/ctf/index.html), por [Trail of Bits](https://www.trailofbits.com/) – “Guia de Campo” que pretende nortear novos players e pessoas que desejam começar a trabalhar com segurança da informação.

- [CTF CheatSheet](https://github.com/rudymatela/ultimate-cheat-sheets/releases/download/ctf-v0.3/ctf-ucs-0.3.pdf), por Rudy “[Rryy](https://matela.com.br/)” Matela – Cheatsheet conciso de comandos que podem ser utilizados para facilitar a vida durante os CTFs. Foi feito pelo Rryy, membro do CTF-BR.

- [CTF Resources](http://ctfs.github.io/resources/) – estilo nosso /docs, englobando muita coisa sobre CTFs.

- [Awesome CTF](https://github.com/dossantos87/awesome-ctf) – outra coleção de links bem interessante.

- [CTF Heaven](https://github.com/thezakman/CTF-Heaven) – repositório do TheZakMan, membro do Projeto.

- [Maximum CTF: Getting the Most Out of Capture the Flag](https://www.youtube.com/watch?v=okPWY0FeUoU), por Jordan “[psifertex](https://twitter.com/psifertex)” Wiens – Palestra ministrada na DEF CON 17 por um dos maiores contribuidores/entusiastas da cena, o psifertex. É um dos organizadores do [Ghost in the Shellcode](http://ghostintheshellcode.com/), o CTF que tem o game [Pwn Adventure](http://pwnadventure.com/) como uma das atrações principais.

- [Hacking Games in a Hacked Game](https://vimeo.com/132900706): outra palestra do [psifertex](https://twitter.com/psifertex), juntamente com Rusty Wagner, ministrada na [Infiltrate 2015](http://infiltratecon.org/speakers.html#games).

- [On the Battlefield with the Dragons](https://www.youtube.com/watch?v=h6oLWmzgDGc), por [Dragon Sector](http://dragonsector.pl/) – Palestra ministrada pelo capitão e vice-campeão do Dragon Sector (melhor time de 2014) no evento [CONFidence](http://2014.confidence.org.pl/en/) deste mesmo ano. Eles citam diversos exemplos de challenges que já resolveram, o que nos mostra claramente a diversidade e multidisciplinaridade que os CTFs proporcionam.

- [Pwning (sometimes) with style](http://j00ru.vexillium.org/blog/24_03_15/dragons_ctf.pdf), por [Dragon Sector](http://dragonsector.pl/) – Dragons’ notes on CTFs.

- [MHacks Tinfoil Security Tech Talk: Zero to Zeroday](https://www.youtube.com/watch?v=Jnh8PK9iQco) – Palestra introdutória de CTFs ministrada por Shane Wilton. Sem sombra de dúvidas uma das melhores!

- [USENIX Enigma 2016 – Building a Competitive Hacking Team](https://www.youtube.com/watch?v=-r-B1uOj0W4) – Palestra do tylerni7, do [PPP](http://pwning.net/) (Plaid Parliament of Pwning), falando sobre seu time e o mundo dos CTFs.

- [USENIX Enigma 2016 – Capture the Flag: An Owner’s Manual](https://www.usenix.org/conference/enigma2016/conference-program/presentation/genovese) – Palestra ministrada por Vito Genovese, um dos organizadores do CTF da DEF CON! [Slides](https://www.usenix.org/sites/default/files/conference/protected-files/enigma16_slides_genovese.pdf) e [Vídeo](https://www.youtube.com/watch?v=BshccRicu8Q).

- [DEF CON 23 – Machine vs. Machine: Inside DARPA’s Fully Automated CTF](https://www.youtube.com/watch?v=gnyCbU7jGYA) – Mais uma palestra do psifertex, explicando o funcionamento da competição automatizada de pwning criada pela DARPA (Defense Advanced Research Projects Agency).

- [Meet the PPP](http://kernelmag.dailydot.com/issue-sections/headline-story/16863/plaid-parliament-of-pwning-hacker-ctf/) – Conhecendo o melhor time da atualidade.

- [DEF CON in the news: A profile of this year’s CTF champs Plaid Parliament of Pwning!](https://www.inverse.com/article/19402-plaid-parliament-of-pwning-wins-defcon-again)

- [A DEF CON CTF 2016 Overview](https://dttw.tech/posts/r1rHSpdY) – Overview do evento de um membro do PPP, time vencedor.

- [LiveOverflow Youtube Channel](https://www.youtube.com/channel/UClcE-kVhqyiHCcjYwcpfj9w/videos) – Muitos vídeos bons e didáticos.

- [Entrevista com o CyKoR](https://blog.avatao.com/Interview-CyKor/) – Time que bateu o PPP nas Finals da DEF CON 2015.

## ONDE TREINAR?

- [Shellterlabs](http://shellterlabs.com/) – Rede social brasileira de segurança da informação, com challenges de vários CTFs famosos.

- [akictf](http://ctf.katsudon.org/) – Wargame feito pelo akiym, membro do time japonês dodododo. Tem challenges com dificuldade crescente envolvendo diversas categorias.

- [pwnable.kr](http://pwnable.kr/) – Site com challenges somente de exploitation.

- [pwnable.tw](http://pwnable.tw/) – Semelhante ao pwnable.kr, porém criado pelo pessoal do HITCON.

- [canyouhack.it](http://canyouhack.it/) – Site com challenges de diversas categorias.

- [reversing.kr](http://reversing.kr/challenge.php) – Site com diversos challenges de reversing, sendo a maioria binários do Windows (PE).

- [crackmes.de](http://crackmes.de/) – Mais challenges de reversing, focado especificamente em cracks.

- [challenges.re](http://challenges.re/) – Mais reversing.

- [id0-rsa.pub](https://id0-rsa.pub/) – Crypto challenges.

- [cryptopals.com](http://cryptopals.com/) – Challenges de criptografia feitos pela Matasano.

- [eudyptula-challenge.org](http://eudyptula-challenge.org/) – Challenges de programming referentes ao kernel do linux.

- [microcorruption.com](http://microcorruption.com/) – Challenges de exploitation.

- [ringzer0team.com](http://ringzer0team.com/) – Outro site com diversos challenges de muitas categorias.

- [chall.tasteless.eu](http://chall.tasteless.eu/) – Challenges criados pelo time internacional Tasteless.

- [root-me.org](http://www.root-me.org/) – Challenges diversos e conta com material de apoio.

- [CTF Learn](http://ctflearn.com/) – Plataforma feita com os challenges dos próprios players. Você também pode adicionar o seu!

- [PwnerRank](https://www.pwnerrank.com/) – Plataforma com challenges de praticamente todas categorias pra treinar.

- [Tigress](http://tigress.cs.arizona.edu/challenges.html) – Challenges de RE referente ao The Tigress C Diversifier/Obfuscator. Alguns challenges unsolvable.

- [Stereotyped Challenges](https://chall.stypr.com/) – vários challenges web feitos pelo stypr, player do dcua.

- [Hack the Box](http://hackthebox.eu/) – destaque para os vários challenges que simulam cenários reais de pentest.

## CTFS NACIONAIS?

[Hacking n’ Roll](http://hackingnroll.com/) – CTF organizado pelo pessoal do [INSERT](http://www.insert.uece.br/) (Information Security Research Team), do Ceará. Já fizeram 5 edições, sendo a partir da segunda, que ocorreu em 2012, em formato Jeopardy, com duração de 24 horas consecutivas, nos moldes das competições internacionais.

[Pwn2Win CTF](https://pwn2win.party/) – Inspirado no Hacking n’ Roll, o time brasileiro [Epic Leet Team](http://www.ctf-br.org/wiki/elt), formado em 2012 para jogar a segunda edição do HnR, criou seu próprio CTF em 2014, utilizando elementos de CTFs Jeopardy e Attack/Defense. O evento tornou-se internacional a partir da [segunda edição](https://ctf-br.org/2016/04/pwn2win-ctf-2016-bastidores/), que ocorreu em 2016.

[3DSCTF](http://3dsctf.win/) – O time [318br](http://318br.sh/) fez a primeira edição do 3DSCTF no final de 2016. Foi internacional e teve duração de 168 horas.

## WRITE-UPS?

Uma boa forma de aprender é vendo write-ups de challenges que você tentou mas não conseguiu fazer, ou ainda para ver as diversas soluções para o mesmo desafio. Nos links abaixo você consegue achar write-ups facilmente:

- [Projeto CTF-BR Repo](https://www.ctf-br.org/write-ups) (pt-BR)

- [CTFTime Repo](https://ctftime.org/writeups)

- [GitHub Repo](https://github.com/ctfs)

## PRÓXIMO CTF?

Basta acompanhar o [CTFTime](http://ctftime.org/), site referência no meio, pois ele possui uma área de “Upcoming Events“. Além disso, possui um ranking global com o score dos times durante o ano, sendo que cada CTF, dependendo da dificuldade e outros fatores, possui um peso para definir sua pontuação. A fórmula utilizada para calcular o rating pode ser vista [aqui](https://ctftime.org/rating-formula/).

Se você está começando, busque jogar nos CTFs com rating baixo, ou High School.




# Awesome CTF [![Build Status](https://travis-ci.org/apsdehal/awesome-ctf.svg?branch=master)](https://travis-ci.org/apsdehal/awesome-ctf) [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

A curated list of [Capture The Flag](https://en.wikipedia.org/wiki/Capture_the_flag#Computer_security) (CTF) frameworks, libraries, resources, softwares and tutorials. This list aims to help starters as well as seasoned CTF players to find everything related to CTFs at one place.

### Contributing

Please take a quick look at the [contribution guidelines](https://github.com/apsdehal/ctf-tools/blob/master/CONTRIBUTING.md) first.

#### _If you know a tool that isn't present here, feel free to open a pull request._

### Why?

It takes time to build up collection of tools used in ctf and remember them all. This repo helps to keep all these scattered tools at one place.


### Contents

- [Awesome CTF](#awesome-ctf)
  - [Create](#create)
    - [Forensics](#forensics)
    - [Platforms](#platforms)
    - [Steganography](#steganography)
    - [Web](#web)
  - [Solve](#solve)
    - [Attacks](#attacks)
    - [Bruteforcers](#bruteforcers)
    - [Cryptography](#crypto)
    - [Exploits](#exploits)
    - [Forensics](#forensics-1)
    - [Networking](#networking)
    - [Reversing](#reversing)
    - [Services](#services)
    - [Steganography](#steganography-1)
    - [Web](#web-1)

- [Resources](#resources)
  - [Operating Systems](#operating-systems)
  - [Starter Packs](#starter-packs)
  - [Tutorials](#tutorials)
  - [Wargames](#wargames)
  - [Websites](#websites)
  - [Wikis](#wikis)
  - [Writeups Collections](#writeups-collections)

# Create

*Tools used for creating CTF challenges*

## Forensics

*Tools used for creating Forensics challenges*

- [Dnscat](https://wiki.skullsecurity.org/Dnscat) - Hosts communication through DNS
- [Registry Dumper](http://www.kahusecurity.com/downloads/RegistryDumper_v0.2.7z) - Dump your registry

## Platforms

*Projects that can be used to host a CTF*

- [CTFd](https://github.com/isislab/CTFd) - Platform to host jeopardy style CTFs from ISISLab, NYU Tandon
- [FBCTF](https://github.com/facebook/fbctf) - Platform to host Capture the Flag competitions from Facebook
- [HackTheArch](https://github.com/mcpa-stlouis/hack-the-arch) - CTF scoring platform
- [Mellivora](https://github.com/Nakiami/mellivora) - A CTF engine written in PHP
- [NightShade](https://github.com/UnrealAkama/NightShade) - A simple security CTF framework
- [OpenCTF](https://github.com/easyctf/openctf) - CTF in a box. Minimal setup required
- [PicoCTF Platform 2](https://github.com/picoCTF/picoCTF-Platform-2) - A genericized version of picoCTF 2014 that can be easily adapted to host CTF or programming competitions.
- [PyChallFactory](https://github.com/pdautry/py_chall_factory) - Small framework to create/manage/package jeopardy CTF challenges
- [RootTheBox](https://github.com/moloch--/RootTheBox) - A Game of Hackers (CTF Scoreboard & Game Manager)
- [Scorebot](https://github.com/legitbs/scorebot) - Platform for CTFs by Legitbs (Defcon)
- [SecGen](https://github.com/cliffe/SecGen) - Security Scenario Generator. Creates randomly vulnerable virtual machines


## Steganography

*Tools used to create stego challenges*

Check solve section for steganography.


## Web

*Tools used for creating Web challenges*

*JavaScript Obfustcators*

- [Metasploit JavaScript Obfuscator](https://github.com/rapid7/metasploit-framework/wiki/How-to-obfuscate-JavaScript-in-Metasploit)
- [Uglify](http://marijnhaverbeke.nl//uglifyjs)


# Solve

*Tools used for solving CTF challenges*

## Attacks

*Tools used for performing various kinds of attacks*

- [Bettercap](https://github.com/bettercap/bettercap) - Framework to perform MITM (Man in the Middle) attacks.
- [Layer 2 attacks](https://github.com/tomac/yersinia) - Attack various protocols on layer 2

## Crypto

*Tools used for solving Crypto challenges*

- [FeatherDuster](https://github.com/nccgroup/featherduster) - An automated, modular cryptanalysis tool
- [Hash Extender](https://github.com/iagox86/hash_extender) - A utility tool for performing hash length extension attacks
- [PkCrack](https://www.unix-ag.uni-kl.de/~conrad/krypto/pkcrack.html) - A tool for Breaking PkZip-encryption
- [RSACTFTool](https://github.com/Ganapati/RsaCtfTool) - A tool for recovering RSA private key with various attack
- [RSATool](https://github.com/ius/rsatool) - Generate private key with knowledge of p and q
- [XORTool](https://github.com/hellman/xortool) - A tool to analyze multi-byte xor cipher

## Bruteforcers

*Tools used for various kind of bruteforcing (passwords etc.)*

- [Hashcat](https://hashcat.net/hashcat/) - Password Cracker
- [John The Jumbo](https://github.com/magnumripper/JohnTheRipper) - Community enhanced version of John the Ripper
- [John The Ripper](http://www.openwall.com/john/) - Password Cracker
- [Nozzlr](https://github.com/intrd/nozzlr) - Nozzlr is a bruteforce framework, trully modular and script-friendly.
- [Ophcrack](http://ophcrack.sourceforge.net/) - Windows password cracker based on rainbow tables.
- [Patator](https://github.com/lanjelot/patator) - Patator is a multi-purpose brute-forcer, with a modular design.

## Exploits

*Tools used for solving Exploits challenges*

- [DLLInjector](https://github.com/OpenSecurityResearch/dllinjector) - Inject dlls in processes
- [libformatstr](https://github.com/hellman/libformatstr) - Simplify format string exploitation.
- [Metasploit](http://www.metasploit.com/) - Penetration testing software
- [one_gadget](https://github.com/david942j/one_gadget) -  A tool to find the one gadget `execve('/bin/sh', NULL, NULL)` call
  - `gem install one_gadget`
- [Pwntools](https://github.com/Gallopsled/pwntools) - CTF Framework for writing exploits
- [Qira](https://github.com/BinaryAnalysisPlatform/qira) - QEMU Interactive Runtime Analyser
- [ROP Gadget](https://github.com/JonathanSalwan/ROPgadget) - Framework for ROP exploitation
- [V0lt](https://github.com/P1kachu/v0lt) - Security CTF Toolkit

## Forensics

*Tools used for solving Forensics challenges*

- [Aircrack-Ng](http://www.aircrack-ng.org/) - Crack 802.11 WEP and WPA-PSK keys
  - `apt-get install aircrack-ng`
- [Audacity](http://sourceforge.net/projects/audacity/) - Analyze sound files (mp3, m4a, whatever)
  - `apt-get install audacity`
- [Bkhive and Samdump2](http://sourceforge.net/projects/ophcrack/files/samdump2/) - Dump SYSTEM and SAM files
  - `apt-get install samdump2 bkhive`
- [CFF Explorer](http://www.ntcore.com/exsuite.php) - PE Editor
- [Creddump](https://github.com/moyix/creddump) - Dump windows credentials
- [DVCS Ripper](https://github.com/kost/dvcs-ripper) - Rips web accessible (distributed) version control systems
- [Exif Tool](http://www.sno.phy.queensu.ca/~phil/exiftool/) - Read, write and edit file metadata
- [Extundelete](http://extundelete.sourceforge.net/) - Used for recovering lost data from mountable images
- [Fibratus](https://github.com/rabbitstack/fibratus) - Tool for exploration and tracing of the Windows kernel
- [Foremost](http://foremost.sourceforge.net/) - Extract particular kind of files using headers
  - `apt-get install foremost`
- [Fsck.ext4](http://linux.die.net/man/8/fsck.ext3) - Used to fix corrupt filesystems
- [Malzilla](http://malzilla.sourceforge.net/) - Malware hunting tool
- [NetworkMiner](http://www.netresec.com/?page=NetworkMiner) - Network Forensic Analysis Tool
- [PDF Streams Inflater](http://malzilla.sourceforge.net/downloads.html) - Find and extract zlib files compressed in PDF files
- [ResourcesExtract](http://www.nirsoft.net/utils/resources_extract.html) - Extract various filetypes from exes
- [Shellbags](https://github.com/williballenthin/shellbags) - Investigate NT\_USER.dat files
- [UsbForensics](http://www.forensicswiki.org/wiki/USB_History_Viewing) - Contains many tools for usb forensics
- [Volatility](https://github.com/volatilityfoundation/volatility) - To investigate memory dumps


*Registry Viewers*
- [RegistryViewer](http://www.gaijin.at/en/getitpage.php?id=regview) - Used to view windows registries
- [Windows Registry Viewers](http://www.forensicswiki.org/wiki/Windows_Registry) - More registry viewers


## Networking

*Tools used for solving Networking challenges*

- [Bro](https://www.bro.org/) - An open-source network security monitor.
- [Masscan](https://github.com/robertdavidgraham/masscan) - Mass IP port scanner, TCP port scanner.
- [Monit](https://linoxide.com/monitoring-2/monit-linux/) - A linux tool to check a host on the network (and other non-network activities). 
- [Nipe](https://github.com/GouveaHeitor/nipe) - Nipe is a script to make Tor Network your default gateway.
- [Nmap](https://nmap.org/) - An open source utility for network discovery and security auditing.
- [Wireshark](https://www.wireshark.org/) - Analyze the network dumps.
  - `apt-get install wireshark`
- [Zmap](https://zmap.io/) - An open-source network scanner.


## Reversing

*Tools used for solving Reversing challenges*

- [Androguard](https://github.com/androguard/androguard) - Reverse engineer Android applications
- [Angr](https://github.com/angr/angr) - platform-agnostic binary analysis framework
- [Apk2Gold](https://github.com/lxdvs/apk2gold) - Yet another Android decompiler
- [ApkTool](http://ibotpeaches.github.io/Apktool/) - Android Decompiler
- [Barf](https://github.com/programa-stic/barf-project) - Binary Analysis and Reverse engineering Framework
- [Binary Ninja](https://binary.ninja/) - Binary analysis framework
- [BinUtils](http://www.gnu.org/software/binutils/binutils.html) - Collection of binary tools
- [BinWalk](https://github.com/devttys0/binwalk) - Analyze, reverse engineer, and extract firmware images.
- [Boomerang](https://github.com/nemerle/boomerang) - Decompile x86 binaries to C
- [ctf_import](https://github.com/docileninja/ctf_import) – run basic functions from stripped binaries cross platform
- [Frida](https://github.com/frida/) - Dynamic Code Injection
- [GDB](https://www.gnu.org/software/gdb/) - The GNU project debugger
- [GEF](https://github.com/hugsy/gef) - GDB plugin
- [Hopper](http://www.hopperapp.com/) - Reverse engineering tool (disassembler) for OSX and Linux
- [IDA Pro](https://www.hex-rays.com/products/ida/) - Most used Reversing software
- [Jadx](https://github.com/skylot/jadx) - Decompile Android files
- [Java Decompilers](http://www.javadecompilers.com) - An online decompiler for Java and Android APKs
- [Krakatau](https://github.com/Storyyeller/Krakatau) - Java decompiler and disassembler
- [Objection](https://github.com/sensepost/objection) - Runtime Mobile Exploration
- [PEDA](https://github.com/longld/peda) - GDB plugin (only python2.7)
- [Pin](https://software.intel.com/en-us/articles/pin-a-dynamic-binary-instrumentation-tool) A dynamic binary instrumentaion tool by Intel
- [Plasma](https://github.com/joelpx/plasma) - An interactive disassembler for x86/ARM/MIPS which can generate indented pseudo-code with colored syntax.
- [Pwndbg](https://github.com/pwndbg/pwndbg) - A GDB plugin that provides a suite of utilities to hack around GDB easily. 
- [radare2](https://github.com/radare/radare2) - A portable reversing framework
- [Triton](https://github.com/JonathanSalwan/Triton/) - Dynamic Binary Analysis (DBA) framework
- [Uncompyle](https://github.com/gstarnberger/uncompyle) - Decompile Python 2.7 binaries (.pyc)
- [WinDbg](http://www.windbg.org/) - Windows debugger distributed by Microsoft
- [Xocopy](http://reverse.lostrealm.com/tools/xocopy.html) - Program that can copy executables with execute, but no read permission
- [Z3](https://github.com/Z3Prover/z3) - a theorem prover from Microsoft Research

*JavaScript Deobfuscators*

- [Detox](http://relentless-coding.org/projects/jsdetox/install) - A Javascript malware analysis tool
- [Revelo](http://www.kahusecurity.com/tools/Revelo_v0.6.zip) - Analyze obfuscated Javascript code

*SWF Analyzers*
- [RABCDAsm](https://github.com/CyberShadow/RABCDAsm) - Collection of utilities including an ActionScript 3 assembler/disassembler.
- [Swftools](http://www.swftools.org/) - Collection of utilities to work with SWF files
- [Xxxswf](https://bitbucket.org/Alexander_Hanel/xxxswf) -  A Python script for analyzing Flash files.

## Services

*Various kind of useful services available around the internet*

- [CSWSH](http://ironwasp.org/cswsh.html) - Cross-Site WebSocket Hijacking Tester
- [Request Bin](http://requestb.in/) - Lets you inspect http requests to a particular url

## Steganography

*Tools used for solving Steganography challenges*

- [Convert](http://www.imagemagick.org/script/convert.php) - Convert images b/w formats and apply filters
- [Exif](http://manpages.ubuntu.com/manpages/trusty/man1/exif.1.html) - Shows EXIF information in JPEG files
- [Exiftool](https://linux.die.net/man/1/exiftool) - Read and write meta information in files
- [Exiv2](http://www.exiv2.org/manpage.html) - Image metadata manipulation tool
- [ImageMagick](http://www.imagemagick.org/script/index.php) - Tool for manipulating images
- [Outguess](https://www.freebsd.org/cgi/man.cgi?query=outguess+&apropos=0&sektion=0&manpath=FreeBSD+Ports+5.1-RELEASE&format=html) - Universal steganographic tool
- [Pngtools](http://www.stillhq.com/pngtools/) - For various analysis related to PNGs
  - `apt-get install pngtools`
- [SmartDeblur](https://github.com/Y-Vladimir/SmartDeblur) - Used to deblur and fix defocused images
- [Steganabara](https://www.openhub.net/p/steganabara) -  Tool for stegano analysis written in Java
- [Stegbreak](https://linux.die.net/man/1/stegbreak) - Launches brute-force dictionary attacks on JPG image
- [StegCracker](https://github.com/Paradoxis/StegCracker) - Steganography brute-force utility to uncover hidden data inside files 
- [stegextract](https://github.com/evyatarmeged/stegextract) - Detect hidden files and text in images 
- [Steghide](http://steghide.sourceforge.net/) - Hide data in various kind of images
- [Stegsolve](http://www.caesum.com/handbook/Stegsolve.jar) - Apply various steganography techniques to images
- [Zsteg](https://github.com/zed-0xff/zsteg/) - PNG/BMP analysis

## Web

*Tools used for solving Web challenges*

- [BurpSuite]() - A graphical tool to testing website security. 
- [Commix](https://github.com/commixproject/commix) - Automated All-in-One OS Command Injection and Exploitation Tool.
- [Hackbar](https://addons.mozilla.org/en-US/firefox/addon/hackbar/) - Firefox addon for easy web exploitation
- [OWASP ZAP](https://www.owasp.org/index.php/Projects/OWASP_Zed_Attack_Proxy_Project) - Intercepting proxy to replay, debug, and fuzz HTTP requests and responses
- [Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en) - Add on for chrome for debugging network requests
- [Raccoon](https://github.com/evyatarmeged/Raccoon) - A high performance offensive security tool for reconnaissance and vulnerability scanning
- [SQLMap](https://github.com/sqlmapproject/sqlmap) - Automatic SQL injection and database takeover tooli
- [W3af](https://github.com/andresriancho/w3af) -  Web Application Attack and Audit Framework.
- [XSSer](http://xsser.sourceforge.net/) - Automated XSS testor


# Resources

*Where to discover about CTF*

## Operating Systems

*Penetration testing and security lab Operating Systems*

- [Android Tamer](https://androidtamer.com/) - Based on Debian
- [BackBox](https://backbox.org/) - Based on Ubuntu
- [BlackArch Linux](https://blackarch.org/) - Based on Arch Linux
- [Fedora Security Lab](https://labs.fedoraproject.org/security/) - Based on Fedora
- [Kali Linux](https://www.kali.org/) - Based on Debian
- [Parrot Security OS](https://www.parrotsec.org/) - Based on Debian
- [Pentoo](http://www.pentoo.ch/) - Based on Gentoo
- [URIX OS](http://urix.us/) - Based on openSUSE
- [Wifislax](http://www.wifislax.com/) - Based on Slackware

*Malware analysts and reverse-engineering*

- [Flare VM](https://github.com/fireeye/flare-vm/) - Based on Windows
- [REMnux](https://remnux.org/) - Based on Debian

## Starter Packs

*Collections of installer scripts, useful tools*

- [CTF Tools](https://github.com/zardus/ctf-tools) - Collection of setup scripts to install various security research tools.
- [LazyKali](https://github.com/jlevitsk/lazykali) - A 2016 refresh of LazyKali which simplifies install of tools and configuration.

## Tutorials

*Tutorials to learn how to play CTFs*

- [CTF Field Guide](https://trailofbits.github.io/ctf/) - Field Guide by Trails of Bits
- [CTF Resources](http://ctfs.github.io/resources/) -  Start Guide maintained by community
- [Damn Vulnerable Web Application](http://www.dvwa.co.uk/) PHP/MySQL web application that is damn vulnerable
- [How to Get Started in CTF](https://www.endgame.com/blog/how-get-started-ctf) - Short guideline for CTF beginners by Endgame
- [MIPT CTF](https://github.com/xairy/mipt-ctf) - A small course for beginners in CTFs (in Russian)

## Wargames

*Always online CTFs*

- [Backdoor](https://backdoor.sdslabs.co/) - Security Platform by SDSLabs.
- [Crackmes](https://crackmes.one/) - Reverse Engineering Challenges
- [Ctfs.me](http://ctfs.me) - CTF All the time
- [Exploit Exercises](https://exploit-exercises.com/) - Variety of VMs to learn variety of computer security issues.
- [Gracker](http://gracker.org) - Binary challenges having a slow learning curve, and write-ups for each level.
- [Hack The Box](https://www.hackthebox.eu) - Weekly CTFs for all types of security enthusiasts.
- [Hack This Site](https://www.hackthissite.org/) - Training ground for hackers.
- [Hacking-Lab](https://hacking-lab.com/) - Ethical hacking, computer network and security challenge platform.
- [Hone Your Ninja Skills](https://honeyourskills.ninja/) - Web challenges starting from basic ones.
- [IO](http://io.netgarage.org/) - Wargame for binary challenges.
- [Microcorruption](https://microcorruption.com) - Embedded security CTF
- [Over The Wire](http://overthewire.org/wargames/) - Wargame maintained by OvertheWire Community
- [Pwnable.kr](http://pwnable.kr/) - Pwn Game
- [Pwnable.tw](https://pwnable.tw/) - Binary wargame
- [Pwnable.xyz](https://pwnable.xyz/) - Binary Exploitation Wargame
- [Reversin.kr](http://reversing.kr/) - Reversing challenge
- [Ringzer0Team](https://ringzer0team.com/) - Ringzer0 Team Online CTF
- [Root-Me](https://www.root-me.org/) - Hacking and Information Security learning platform.
- [ROP Wargames](https://game.rop.sh/) - ROP Wargames
- [SmashTheStack](http://smashthestack.org/) - A variety of wargames maintained by the SmashTheStack Community.
- [VulnHub](https://www.vulnhub.com/) - VM-based for practical in digital security, computer application & network administration.
- [W3Challs](https://w3challs.com) - A penetration testing training platform, which offers various computer challenges, in various categories.
- [WebHacking](http://webhacking.kr) - Hacking challenges for web.
- [WeChall](https://www.wechall.net/) - Always online challenge site.
- [WTHack OnlineCTF](https://onlinectf.com) - CTF Practice platform for every level of cyber security enthusiasts. 


*Self-hosted CTFs*

- [Juice Shop CTF](https://github.com/bkimminich/juice-shop-ctf) - Scripts and tools for hosting a CTF on [OWASP Juice Shop](https://www.owasp.org/index.php/OWASP_Juice_Shop_Project) easily.

## Websites

*Various general websites about and on ctf*

- [CTF Time](https://ctftime.org/) - General information on CTF occuring around the worlds
- [Reddit Security CTF](http://www.reddit.com/r/securityctf) - Reddit CTF category

## Wikis

*Various Wikis available for learning about CTFs*

- [Bamboofox](https://bamboofox.torchpad.com/) - Chinese resources to learn CTF
- [ISIS Lab](https://github.com/isislab/Project-Ideas/wiki) - CTF Wiki by Isis lab
- [OpenToAll](http://wiki.opentoallctf.com/) - Open To All Knowledge Base

## Writeups Collections

*Collections of CTF write-ups*

- [Captf](http://captf.com/) - Dumped CTF challenges and materials by psifertex
- [CTF write-ups (community)](https://github.com/ctfs/) - CTF challenges + write-ups archive maintained by the community
- [CTFTime Scrapper](https://github.com/abdilahrf/CTFWriteupScrapper) - Scraps all writeup from ctf time and organize which to read first
- [pwntools writeups](https://github.com/Gallopsled/pwntools-write-ups) - A collection of CTF write-ups all using pwntools
- [Shell Storm](http://shell-storm.org/repo/CTF/) - CTF challenge archive maintained by Jonathan Salwan
- [Smoke Leet Everyday](https://github.com/smokeleeteveryday/CTF_WRITEUPS) - CTF write-ups repo maintained by SmokeLeetEveryday team.


### LICENSE

CC0 :)

--- 

- https://ctf-br.org/docs/
- https://wheresmykeyboard.com/2016/07/hacking-sites-ctfs-wargames-practice-hacking-skills/
- https://github.com/apsdehal/awesome-ctf/blob/master/README.md
- https://ctftime.org/ctfs
