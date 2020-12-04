---
layout: single
permalink: /articles/30daymapchallenge_stats_fr/  
title : "Statistiques 30 DayMapChallenge 2020"   
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
toc_label: "Statistics"
toc_icon: "chart-line"
---

Maintenant que le 30DayMapChallenge 2020 est fini, nous n'avons plus qu'à retourner à nos activités habituelles et à attendre 2021 pour voir d'autres cartes fabuleuses !

Un des sujets qui m'intéressent personnellement est la représentation de données, qu'elles soient géographiques ou non. Pour ce faire j'ai commencé à apprendre à utiliser Python cette année, afin de compléter mes compétences.

J'ai donc décidé d'utiliser toute la splendide matière qui a été produite durant le challenge de cette année pour m'entraîner, et dans un même temps, produire quelques dataviz et tenter de sortir quelques insights !

Vous trouverez ici, au fur et à mesure de sa rédaction, l'ensemble des dataviz et les chiffres qui en ressortiront.

## Jeu de données

Pour parvenir à de bonnes visualisations (ou du moins justes), il est nécessaire d'avoir un bon jeu de données. Pour arriver à cela, j'ai récupéré le travail de dingue réalisé par [David Friggens.](https://twitter.com/dakvid) Il a recensé [sur un TSV](https://david.frigge.nz/30DayMapChallenge2020/) un maximum de participations. J'ai ajouté encore quelques cartes supplémentaires en forant Twitter grâce à [Twint](https://github.com/twintproject/twint), qui est d'ailleurs un outil vraiment très intéressant. _(Je réaliserai sûrement un article sur cette partie un peu plus tard)_

Et si jamais vous ne l'avez pas encore vu passé, faites un tour sur le site de David, une partie affiche l'ensemble des cartes recensées, accessibles grâce à une série de filtres ! De plus, si vous voyez une carte manquante ou que vous voulez compléter des métadonnées, n'hésitez pas et aller lire les instructions pour le faire ici.

## Finishers

Afin de commencer à explorer ce jeu de données, j'ai décidé de commencer par rendre hommage aux finisher. Ces personnes, sans doute un peu folles/au moins passionnées, ayant réalisé l'intégralité des 30 jours/thèmes !

Ce qui est sûr c'est qu'avec la charge de travail que ça représente, la géo-productivité a du sacrément en prendre un coup pendant le mois de novembre !

Jusqu'à maintenant, grâce à ce que j'ai pu récupéré, j'ai identifié 76 finishers !

Vous trouverez, ci-dessous quelques statistiques liées aux finishers à la date du 2 décembre 2020. J'ai réalisé le graphique avec [Plotly](https://plotly.com/), et je mettrai très prochainement le code sur un gist très prochainement.

En résumé, ça représente :

- **2 310 tweets** :bird:
- **2 366 réponses** :raising_hands: -_la participation avec le plus de réponses en a 29_
- **9 243 retweets** :incoming_envelope: -_la participation avec le plus de retweets en a 235_
- **53 056 likes** :heart: -_la participation avec le plus likes en a 941_

Je développerai par la suite ce genre de statistiques sociales, avec l'ensemble des participants !

Sur la visualisation suivante, vous trouverez chaque finisher, avec le nombre de tweets ainsi que les statistiques sociales liées en passant votre souris (ou doigt) sur chaque barre.

>Si vous lisez cet article sur appareil mobile, je vous conseille de passer en mode paysage.
>Vous pouvez également [cliquer ici](https://aurelienchaumet.github.io/data/30daymapchallenge_stats/finisher_stats.html), pour visualiser le graphique dans une nouvelle fenêtre.

<iframe width="100%" height="820"
    src="https://aurelienchaumet.github.io/data/30daymapchallenge_stats/finisher_stats.html">
</iframe>
