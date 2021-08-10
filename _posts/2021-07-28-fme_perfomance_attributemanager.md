---
layout: single
permalink: /articles/fme_transformers_ranking/
title : "FME : Exploration du classement des Transformers FME" 
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/conteneurs_retractables.png
  overlay_filter: 0.3
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/conteneurs_retractables.png
excerpt:
  Comment utilisez-vous les différents transformers FME ?

og_image: https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/conteneurs_retractables.png

comments: true
share: true
toc: true
toc_label: "Plan"
toc_icon: "chart-line"
toc_sticky: true
---

## Pourquoi un test de performance ?

Comme expliqué dans l'article précédent LIEN ARTICLE RANKING, je trouve étonnant que SAFE laisser cohabiter plusieurs transformers qui auraient les mêmes fonctions.

Je formule donc l'hypothèse qu'en fonction des cas d'usage, les performances ne doivent pas être les mêmes.

Pour réaliser ce test, j'ai récupéré [les parcelles PCI (Plan Cadastral Informatisé) de la Charente-Maritime](https://cadastre.data.gouv.fr/data/etalab-cadastre/2021-04-01/geojson/departements/17/), environ 1Go de données, avec 1 671 935 lignes.
{: .notice--info}

#### Test de l'AM en face to face avec ses ancêtres

Pour tenter de gagner un peu de temps, le [Feature Caching](https://www.safe.com/blog/2018/05/caching-data-fme-evangelist174/) est activé pour l'ensemble des tests suivants.  
A chaque fois qu'un test de process est indiqué, j'ai fait tourner 5 fois le même transformer (ou enchainement de transformers) et fait la moyenne des 5 temps.

| Transformer ancêtre  | Temps          | Temps AM | Plus rapide |
| :--------------- |:---------------|:-----|:-----|
| AttributeRenamer  | 1 minute 12.6 secondes | 1 minute 39.5 secondes | Ancêtre +37% |
| AttributeCreator  | 2 minutes 48.2 secondes | 2 minutes 47.5 secondes | AM +0.2% |
| AttributeKeeper  | 51.6 secondes | 58.3 secondes | Ancêtre +13% |
| AreaCalculator  | 1 minute 22.3 secondes | 1 minute 25.7 secondes | Ancêtre +4% |

Pour l'instant, hormis sur la création d'attributs où un doute peut subsister (l'écart étant plutôt mince), les Transformers spécifiques apparaissent comme plus performants que l'AM.

#### Test de l'AM en remplacement d'un enchaînement de ses prédécesseurs

Cette fois, j'ai réalisé un enchaînement des 4 précédents transformers comparés aux même taches effectuées dans l'AM.

Avant toute chose, il est à noter qu'un seul AM peut, parfois, ne pas remplir les mêmes fonctions que les transformers à tache unique.  
Par exemple, vous souhaitez créer un nouvel Attribut 2 à parti d'un Attribut 1 déjà existant, et supprimer l'Attribut 1 dans la foulée.  
Il suffit d'enchainer un AttributeCreator puis un AttributeRemover (ou AttributeKeeper). Ici, un seul AM ne suffira pas.  
En effet, si vous dites dans les paramètres de l'AM que vous souhaitez à la fois créer un champ à partir d'un attribut et le supprimer en même temps, il risque de ne pas comprendre ce que vous voulez lui faire faire...

![fme pas comprendre](https://dl01fbzxdpfby.cloudfront.net/images/fme/transformers_ranking/fme_pas_comprendre.png "FME pas comprendre"){: .align-center}

Enchainement de 2 transformers :

- AttributeRenamer+AttributeCreator : 4 minutes 45 seconds
- AM équivalent : 3 minutes 10.9 seconds
- Gain de l'AM : +33%

- AttributeKeeper+AreaCalculator : 1 minute 42.6 seconds
- AM équivalent : 1 minute 0.4 second
- Gain de l'AM : +41%

- AttributeCreator+AttributeKeeper : 6 minutes 52.5 seconds (met plus de temps que l'enchaînement des 4 ???)
- AM équivalent :  3 minutes 1.5 seconds
- Gain de l'AM : +56%

Enchainement de 3 transformers :

- AttributeRenamer+AttributeCreator+AttributeKeeper : 4 minutes 37.2 seconds
- AM équivalent : 2 minutes 54 seconds
- Gain de l'AM : +37%

- AttributeCreator+AttributeKeeper+AreaCalculator : 6 minutes 3.7 seconds
- AM équivalent : 3 minutes 8 seconds
- Gain de l'AM : +48%

Enchainement des 4 transformers mono taches :

- Historiques : 5 minutes 32.1 seconds
- AM : 3 minutes 15.5 seconds
- Gain de l'AM : +41%

## Conclusion

Cette nouvelle possibilité offerte dans la dernière mise à jour de Tableau permet de réaliser de nombreuses améliorations en termes d'interface en simplifiant le design de certains dashboards.

Il est possible d'imaginer par exemple qu'un graphique pop directement à la sélection d'un élément sur un graphique lié, sans pourautant être affiché en permanence.

En bref, encore bien des choses à imaginer grâce à Tableau !

----

Cet article m'a [été inspiré par un post de Samuel Parsons](https://www.linkedin.com/posts/samuel-parsons-b9184b97_tableau-activity-6824262186844610560-Mp7N), que je tiens à remercier vivement pour m'avoir (enfin) poussé à comprendre le fonctionnement des conteneurs et leur nouvelle rétractabilité !!

N'hésitez pas à commenter directement en dessous, ou à m'envoyer un [message sur Twitter](https://twitter.com/messages/compose?recipient_id=938055192221765634), je vous répondrai avec plaisir :pray: !
