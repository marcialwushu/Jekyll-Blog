---
layout: post
title:  "Watch Out Google, DARPA Just Open Sourced All This Swish 'Dark Web' Search Tech"
date:   2017-11-26 20:50:31 -0200
categories: jekyll update
---

![](https://blogs-images.forbes.com/thomasbrewster/files/2015/04/DIG1-e1429287668368-1940x1091.png)


Google appears to be an indomitable force. But, with today's release from the US military's research arm of its Memex search technologies and Europe's competition investigation into the Mountain View giant, it might be a propitious time for tech-minded entrepreneurs to start building a Google killer.

DARPA's Memex search technologies have garnered much interest due to their initial mainstream application: to uncover human trafficking operations taking place on the "dark web", the catch-all term for the various internet networks the majority of people never use, such as Tor, Freenet and I2P. And a significant number of law enforcement agencies have inquired about using the technology. But Memex promises to be disruptive across both criminal and business worlds.

Christopher White, who leads the team of Memex partners, which includes members of the Tor Project, a handful of prestigious universities, NASA and research-focused private firms, tells FORBES the project is so ambitious in its scope, it wants to shake up a staid search industry controlled by a handful of companies: Google, Microsoft and Yahoo.

![](https://blogs-images.forbes.com/thomasbrewster/files/2015/04/DIG2-1940x1285.jpg)

Putting those grandiose ideas into action, DARPA will today open source various components of Memex, allowing others to take the technologies and adapt them for their own use. As is noticeable from the list of technologies below, there's great possibility for highly-personalised search, whether for agents trying to bring down pedophiles or the next Silk Road, or anyone who wants a less generic web experience. Here's an exclusive look at who is helping DARPA build Memex and what they're making available on the [Open Catalogue](https://opencatalog.darpa.mil/) today:

>[Uncharted Software](https://uncharted.software/), [University of Southern California](https://www.usc.edu/) and [Next Century Corporation](https://nextcentury.com/)

These three have produced the front-end interfaces, called TellFinder and DIG, currently being used by Memex's law enforcement partners. "They’re very good at making things look slick and shiny. Processing and displaying information is really hard and quite subjective," says White.

![](https://blogs-images.forbes.com/thomasbrewster/files/2015/04/ApertureTiles_3_DrillDownDetails.jpg)

# ArrayFire

The [ArrayFire](https://arrayfire.com/) tech is a software library designed to support accelerated computing, turbo-boosting web searches over [GPUs](http://www.nvidia.com/object/what-is-gpu-computing.html). "A few lines of code in ArrayFire can replace dozens of lines of parallel computing code, saving users valuable time and lowering development costs," the blurb for the technology reads.

# Carnegie Mellon University

[CMU](https://www.cmu.edu/index.html) is building various pieces of the Memex puzzle, but its TJBatchExtractor is what's going open source today. It allows a user to extract data, such as a name, organisation or location, from advertisements. It was put to good use in the anti-human trafficking application already in use by law enforcement agencies.

# Diffeo

[Diffeo's](https://diffeo.com/) Dossier Stack learns what a user wants as they search the internet. "Instead of relying on Google’s ranking to tell you what’s important, you can say, "I want the Thomas that’s in the UK not the US, so don’t send me anything that has US-oriented information," explains White.

# Hyperion Gray

As featured in [a recent FORBES article on Memex](https://www.forbes.com/sites/thomasbrewster/2015/04/10/darpa-memex-search-going-open-source-check-it-out/), [Hyperion Gray's](http://www.hyperiongray.com/) crawlers are designed to replicate human interaction with websites. "Think of what they do as web crawling on steroids," says White. Its AutoLogin component takes authentication credentials funnelled into the system to crawl into password-protected areas of websites, whilst Formasaurus does the same but for web forms, determining what happens when fields are filled in. The Frontera, SourcePin and Splash tools make it easy for the average user to organise and view the kind of content they want in their results. Its HG Profiler code looks for matches of data across different pages where there's no hyperlink making it obvious. Hyperion Gray also built Scrapy-­Dockerhub, which allows easy repackaging of crawlers into [Docker containers](https://www.forbes.com/sites/benkepes/2015/03/05/aiming-to-leverage-dockers-growth-red-hat-launches-its-own-container-specific-os/#53827b399238), allowing for "better and easier web crawling", notes White.

# [IST Research](http://istresearch.com/) and [Parse.ly](https://www.parse.ly/)

These two firms have built infrastructure "for real-time, scalable web crawling on distributed systems that uses a kind of queuing architecture and allows for streaming", explains White. "These tools [Scrapy Cluster, pykafka and steamparse] are major infrastructure components so that you can build a very scalable, real-time web crawling architecture."

# Jet Propulsion Laboratory

This [NASA-based organisation](https://www.jpl.nasa.gov/) has crafted a slew of Memex building blocks, four of which - ImageCat, FacetSpace, LegisGATE and ImageSpace - are applications built on top of [Apache Software Foundation](https://www.apache.org/) projects that allow users to analyse and manipulate vast numbers of images and masses of text. "Think of them as utilities that could be useful on their own but could also be components of a software system," says White. JPL also created a video and image analysis system called SMQTK to rank that kind of visual content based on relevance, making it easy for the user to connect files to the topic they care about. Its Memex Explorer brings all those tools together under a common interface.

# [MIT Lincoln Laboratory](https://www.ll.mit.edu/)

Three of MIT's contributions - Text.jl, MITIE, Topic - are natural language processing tools. They allow the user, for example, to search for where two organisations are mentioned in different documents, or to ask for terse descriptions of what a document or a webpage is about.

# New York University

[NYU](http://www.nyu.edu/), in collaboration with JPL and Continuum Analytics, has created an interface called Topic, which lets the user interact with "focused crawlers", which consistently update indexes to produce what’s relevant to the user, always "narrowing the thing they’re crawling", notes White. "We have a few of these different kinds of crawlers as it’s not clear for every domain what the right crawling strategy is.

# [Qadium](https://qadium.com/)

This San Francisco firm has submitted a handful of utilities that allow for "data marshalling", a way to organise data so it can be inspected in different ways.

# [Sotera Defense Solutions](http://www.soteradefense.com/)

This government contractor has created the aptly-named DataWake. It collects all links that the user didn't click on but could, and maybe should, have. This "wake" includes the data behind those links.

# SRI International

[SRI](https://www.sri.com/) is working alongside the [Tor Project](https://www.torproject.org), the US Navy and some of the original creators of Tor, the anonymising browser that encrypts traffic and loops users through a number of servers to protect their identities. SRI has developed a "dark crawler" called the Hidden Service Forum Spider, that grabs content from Hidden Services - those sites hosted on Tor nodes and are used for especially private services, be they drug markets or human rights forums for those living under repressive regimes. The HSProbe, meanwhile, looks for Hidden Service domains. The Memex team is keen to learn more about the darker corners of the web, partly to help law enforcement clean it of illegal content, but also to get a better understanding of how big the unmapped portions of the internet are.

DARPA is funding the Tor Project, which is one of the most active supporters of privacy in the technological world, and the US Naval Research Laboratory to test the Memex tools. DARPA said Memex wasn't about destroying the privacy protections offered by Tor, even though it wanted to help uncover criminals' identities. "None of them [Tor, the Navy, Memex partners] want child exploitation and child pornography to be accessible, especially on Tor. We’re funding those groups for testing," says White.

# Stanford University

DeepDive from [Stanford](https://www.stanford.edu/) turns text and multimedia into "knowledge bases", creating connections between relationships of the different people or groups being searched for. "It’s machine learning tech for inferring patterns, working relationships... finding links across a very large amount of documents," adds White.

---

Thomas Fox-Brewster , Forbes Staff
I cover crime, privacy and security in digital and physical form

[README](https://www.forbes.com/sites/thomasbrewster/2015/04/17/darpa-nasa-and-partners-show-off-memex/#1bffc787378d)

