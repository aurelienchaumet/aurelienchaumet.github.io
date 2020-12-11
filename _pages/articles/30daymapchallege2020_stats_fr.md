---
layout: single
permalink: /articles/30daymapchallenge_stats_fr/  
title : "Statistiques 30 DayMapChallenge 2020"   
classes: wide
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats/30dmc_stats_header.webp
  overlay_filter: 0.3
  caption: "Poster créé par [Haifeng Niu](https://twitter.com/niu_haifeng)"
excerpt:
  Quelques statistiques sur le 30DayMapChallenge 2020 avec Python

og_image: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats/30dmc_stats_header.webp

comments: true
share: true
toc: true
toc_label: "Statistiques"
toc_icon: "chart-line"
---

Maintenant que le 30DayMapChallenge 2020 est fini, nous n'avons plus qu'à retourner à nos activités habituelles et à attendre 2021 pour voir d'autres cartes fabuleuses !

Un des sujets qui m'intéresse personnellement est la représentation de données, qu'elles soient géographiques ou non. Pour ce faire, j'ai commencé à apprendre à utiliser Python cette année, afin de compléter mes compétences.

J'ai donc décidé d'utiliser toute la splendide matière qui a été produite durant le challenge de cette année pour m'entraîner, et dans un même temps, produire quelques dataviz et tenter de sortir quelques insights !

Vous trouverez ici, au fur et à mesure de sa rédaction, l'ensemble des dataviz et des chiffres qui en ressortiront.

## Jeu de données

Pour parvenir à de bonnes visualisations (ou du moins justes), il est nécessaire d'avoir un bon jeu de données. Pour arriver à cela, j'ai récupéré le travail de dingue réalisé par [David Friggens.](https://twitter.com/dakvid) Il a recensé [sur un TSV](https://docs.google.com/spreadsheets/d/1j2iLnWtBATMxpvDZLXlqaOd0zmcclyg8VIgkPgVMklQ/edit?usp=sharing) un maximum de participations. J'ai ajouté encore quelques cartes supplémentaires en forant Twitter grâce à [Twint](https://github.com/twintproject/twint), qui est d'ailleurs un outil vraiment très intéressant. _(Je réaliserai sûrement un article sur cette partie un peu plus tard)_

Et si jamais vous ne l'avez pas encore vu passé, faites un tour sur le site de David, [une partie affiche l'ensemble des cartes recensées](https://david.frigge.nz/30DayMapChallenge2020/maps.html), accessibles grâce à une série de filtres ! De plus, si vous voyez une carte manquante ou que vous voulez compléter des métadonnées, n'hésitez pas et [aller lire les instructions pour le faire ici.](https://david.frigge.nz/30DayMapChallenge2020/)

## Finishers

Afin de commencer à explorer ce jeu de données, j'ai décidé de commencer par rendre hommage aux finishers. Ces personnes, sans doute un peu folles (ou au moins passionnées !), ayant réalisé l'intégralité des 30 jours/thèmes !

Une chose dont je suis sûr, c'est qu'avec la charge de travail que ça représente, la géo-productivité mondiale a du sacrément en prendre un coup pendant le mois de novembre !

Jusqu'à maintenant, grâce à ce que j'ai pu récupéré, j'ai identifié **76 finishers** !

Vous trouverez, ci-dessous quelques statistiques liées aux finishers à la date du 2 décembre 2020. J'ai réalisé le graphique avec [Plotly](https://plotly.com/), et je mettrai très prochainement le code sur un gist.

En résumé, ça représente :

- **2 310 tweets** :bird:
- **2 366 réponses** :raising_hand: _la participation avec le plus de réponses en a 29_
- **9 243 retweets** :incoming_envelope: _la participation avec le plus de retweets en a 235_
- **53 056 likes** :heart: _la participation avec le plus de likes en a 941_

Je développerai par la suite ce genre de statistiques sociales, avec l'ensemble des participants !

Sur la visualisation suivante, vous trouverez chaque finisher, avec le nombre de tweets ainsi que les statistiques sociales liées en passant votre souris (ou doigt :point_down:) sur chaque barre.

>Si vous lisez cet article sur appareil mobile, je vous conseille de passer en mode paysage.  
>Vous pouvez également [cliquer ici](https://aurelienchaumet.github.io/data/30daymapchallenge_stats/finisher_stats_fr.html), pour visualiser le graphique dans une nouvelle fenêtre.

<iframe width="100%" height="820"
    src="https://aurelienchaumet.github.io/data/30daymapchallenge_stats/finisher_stats_fr.html">
</iframe>

## Statistiques générales

Concernant l'ensemble des participations, je compte :

- **833 participants**
- **7 184 cartes**, soit une moyenne de 240 cartes par jour...
- **136 266 likes**
- **24 740 retweets**

Ça commence à faire un paquet de cartes, et de personnes likant et retweetant !

Afin d'explorer ces données plus visuellement, j'ai conçu un dashboard via [Bokeh](https://docs.bokeh.org/en/latest/), histoire de continuer à me former à de noubeaux outils et pour changer un peu de Plotly.

> L'affichage au démarrage visualise les données par jour, aggrégées pour l'ensemble des participations.  
> Vous pouvez sélectionner un participant en particulier, via la barre de sélection en bas de l'application.

[_Vous pouvez cliquer ici pour l'afficher dans une nouvelle page._](http://stats-30daymapchallenge.herokuapp.com/bokeh_basics)  
_Malheureusement, je n'ai pas encore réussi à trouver un moyen, pour les appareils mobiles, d'afficher les données qui sont disponibles en passant la souris sur chaque bar..._

<iframe width="100%" height="820"
    src="https://stats-30daymapchallenge.herokuapp.com/bokeh_basics">
</iframe>

Côté technique, je l'ai hébergé sur [Heroku](https://www.heroku.com/).  
J'imagine par la suite rédiger un tuto à la fois sur le cheminement purement pythonesque de tout ça (côté Twint, Plotly et Bokeh), ainsi que sur la manière de déployer une application sur Heroku. Tout ça n'est pas très complexe, mais ça peut mériter de garder en mémoire quelques astuces et pièges dans lesquels ne pas tomber.

Quelques observations sur ces données :

- Enorme succès pour le démarrage du challenge, **le jour 1 (Points) est celui qui a connu le plus de likes (12 336) et de retweets (2 365).**  
On peut noter une sorte de **plateau médian autour de 4 500 likes** sur le reste des jours, avec tout de même 3 pics pour les jour 2 (Lignes), 11 (3D) et 12 (Cartes réalisées sans un logiciel SIG). Fort à parier que ces 2 derniers thèmes sont plus aptes à produire de l'engagement plus générique.  
**Le jour 25 (COVID-19) est celui ayant connu le moins de likes (1 982)**, sans doute du à 2 facteurs : le trop plein des gens pour cette thématique et l'approche de Thanksgiving aux Etats-Unis (comme noté par [Nicolas Lambert sur ses propres statistiques](https://neocarto.hypotheses.org/12028))
- Les finishers sont d'énormes pourvoyeurs de contenus (évidemment) mais également de likes et retweets.  
-- Ils représentent **9% des participants** avec 2 310 cartes (soit 32% de l'ensemble des soumissions)  
-- Leurs cartes représentent **37% des likes et retweets totaux**  

---

_**A suivre...**_
