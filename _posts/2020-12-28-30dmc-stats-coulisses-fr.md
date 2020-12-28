---
layout: single
permalink: /articles/30daymapchallenge_stats_bts_fr/  
title : "30 DayMapChallenge 2020 Statistiques - Dans les coulisses" 
classes: wide
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/30dmc_stats_header_sd.png
  overlay_filter: 0.3
  caption: "Poster created by [Haifeng Niu](https://twitter.com/niu_haifeng)"
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/30dmc_stats_header_sd.png
excerpt:
  Explications du process ayant mené à l'analyse des statistiques du 30DayMapChallenge 2020

og_image: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats/30dmc_stats_header.webp

comments: true
share: true
toc: true
toc_label: "Statistics"
toc_icon: "chart-line"
---

L'un des évènements sociaux marquants de la fin d'année 2020 reste pour moi le [30DayMapChallenge](https://github.com/tjukanovt/30DayMapChallenge).  
Le concept où chacun peut réaliser des cartes l'intéressant, de la manière dont il le souhaite et partage tout ça auprès d'un public averti, tout en se confrontant à d'autres réalisations, sur des thèmes imposés est vraiment intéressant.

Ce challenge totalement non officiel reste un moment unique de partage cartographique à travers le monde et [la collection réalisée par David Friggens](https://david.frigge.nz/30DayMapChallenge2020/maps.html) en est un exemple implacable.

Toutes ces cartes sont un matériel vraiment très intéressant d'étude concernant la cartographie, et c'est pourquoi j'ai essayé d'en [ressortir quelques statistiques dans un précédent article](https://aurelienchaumet.github.io/articles/30daymapchallenge_stats_fr/), principalement du point de vue social du challenge.

IMAGE

J'ai pour cela utilisé (et appris à m'en servir par la même occasion) un certain nombre d'outils en Python :

- Twint pour récupérer les données
- Plotly pour [visualiser les statistiques des finishers](https://aurelienchaumet.github.io/articles/30daymapchallenge_stats_fr/#finishers)
- Bokeh pour [visualiser les statistiques de l'ensemble des participants](https://aurelienchaumet.github.io/articles/30daymapchallenge_stats_fr/#statistiques-g%C3%A9n%C3%A9rales)

Je souhaitais donc partager ici la manière dont j'ai récupéré et traité ces données, et comment je me suis servi de ces outils pour y arriver.

## DataMining

Comme évoqué précédemment, David Friggens a vraiment réalisé un travail spectaculaire de collecte des différents tweets afférant au 30DayMapChallenge. Mais très honnêtement, même si le travail de récupération se fait automatiquement, la classification en fonction des jours (et donc des thèmes) est assez fastidieux pour une seule personne.  
J'ai donc apporté ma pierre à l'édifice en scrapant également ces données de mon côté, en les confrontant à celles de David, puis en lui renvoyant ce qui m'apparaissait commem manquant de son côté.

Wait... Scrap what ??

### Définition du webscraping

Je m'arrête rapidement sur la définition du scraping, qui ne consiste en aucun cas à gratter frénétiquement des tickets issus de la FDJ. C'est en réalité un processus qui permet de collecter des données se situant sur internet.  
Cela évite d'avoir des copier-coller longs et fortement fastidieux à réaliser à la main.

Un robot, ou un algorithme, est configuré pour récupérer les données qui nous intéressent, à l'endroit où cela nous sied, et les remet dans un format qui nous est approprié, à l'endroit où on le souhaite. C'est beau dit comme ça...

### Twint ou comment récupérer facilement des données de Twitter

Il est possible de récupérer les données de Twitter via Tweepy, une librairie Python.  
Ses principales limites sont que vous ne pourrez récupérer que les 3 200 premiers tweets d'une timeline, couplé à un nombre limité toutes les 15 minutes.

Mais il y a mieux ! Une autre librairie s'appelant [Twint](https://github.com/twintproject/twint) existe et s'affranchit de ces limitations (car elle ne fait pas appel à l'API de Twitter).  

#### Installation de Twint

L'installation est ultra simple, il suffit de taper dans un terminal de commande :

```python

pip3 install twint

```

Et logiquement, c'est réglé !

#### Utilisation générique de Twint

Il y a ensuite 2 manières de s'en servir :

- Pour les cas d'usage les plus simples, vous pouvez passer par une commande CLI
  ```python

  twint -u username

  ```
  Cela récupèrera l'ensemble des tweets de username

  ```python

  twint -s pineapple

  ```
  Cela vous ramènera l'ensemble des tweets contenant pineapple

- Pour les cas un peu plus poussés, il faudra passer par l'usage du Module

  ```python

  import twint

  # Configure
  c = twint.Config()
  c.Username = "realDonaldTrump"
  c.Search = "great"

  # Run
  twint.run.Search(c)

  ```
  Ici, vous récupèrerait l'ensemble des tweets de Donald Trump contenant "great"
  _L'exemple cité provient de la documentation de Twint et ne réflète en aucun cas un quelconque intérêt pour le fond_

L'avantage de cette deuxième méthode est que des fonctions pythoniques peuvent être utilisées, et vous pourrez ainsi vous en servir dans un script plus élaboré.

#### Utilisation de Twint pour récupérer les tweets du 30DayMapChallenge

![site david maps](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats/capture_david_site.webp "David Frigge's site, which collect all submissions"){: .align-center}

## Finishers
