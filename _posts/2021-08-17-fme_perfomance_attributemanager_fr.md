---
layout: single
permalink: /articles/fme_performance_attributemanager/
title : "FME : Test de performance comparative entre l'AttributeManager et certains transformers équivalents" 
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/conteneurs_retractables.png
  overlay_filter: 0.3
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/conteneurs_retractables.png
excerpt:
  Est-ce que seules les performances peuvent expliquer la cohabitation de plusieurs transformers FME équivalents ?

og_image: https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/conteneurs_retractables.png

comments: true
share: true
toc: true
toc_label: "Plan"
toc_icon: "chart-line"
toc_sticky: true
---

## Pourquoi un test de performance ?

[Comme expliqué dans le précédent article](https://aurelienchaumet.github.io/articles/fme_transformers_classement/), je trouve étonnant que SAFE laisser cohabiter plusieurs transformers qui auraient les mêmes fonctions.

Je formule donc l'hypothèse qu'en fonction des cas d'usage, les performances ne doivent pas être les mêmes. Voyons voir cela d'un peu plus près, en prenant, pour le test, 4 transformers que l'AttributeManager pourrait remplacer foncontionnellement parlant :

- [AttributeRenamer](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/attributerenamer.htm), pour renommer les attributs
- [AttributeCreator](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/attributecreator.htm), qui permet de créer de nouveaux attributs
- [AttributeKeeper](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/attributekeeper.htm), qui ne garde que les attributs sélectionnés
- [AreaCalculator](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/areacalculator.htm), permettant de calculer la superficie de polygones

Pour réaliser ce test, j'ai récupéré [les parcelles PCI (Plan Cadastral Informatisé) de la Charente-Maritime](https://cadastre.data.gouv.fr/data/etalab-cadastre/2021-04-01/geojson/departements/17/), environ 1Go de données, avec 1 671 935 lignes.
{: .notice--info}

_Nous appellerons le transfromer AttributeManager *AM* dans la suite de cet article afin d'éviter de surcharger la lecture._

Vous trouverez le workbench qui m'a permis de réaliser les tests de performance ici :
METTRE LE LIEN

### Test de l'AM en face to face avec ses ancêtres

Pour tenter de gagner un peu de temps, le [Feature Caching](https://www.safe.com/blog/2018/05/caching-data-fme-evangelist174/) est activé pour l'ensemble des tests suivants, uniquement après la lecture de la donnée entrante.  
A chaque fois qu'un test de process est indiqué, j'ai fait tourner 5 fois le même transformer (ou enchainement de transformers) et fait la moyenne des 5 temps.

Concernant l'AM face à ses ancètres, un par un, vous trouverez le résumé des temps ci-dessous :

![comparaison 1V1](https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/1V1.png "Comparaison 1V1"){: .align-center}

Pour l'instant, hormis sur la création d'attributs où un doute peut subsister (l'écart étant plutôt mince), les Transformers spécifiques apparaissent comme plus performants que l'AM.

C'est un peu comme si vous aviez un [Leatherman](https://fr.wikipedia.org/wiki/Leatherman) et un tournevis cruciforme sous la main, et que vous n'avez que des vis cruciforme à poser. Vous irez sans doute plus vite en vous servant du tournevis.

### Test de l'AM en remplacement d'un enchaînement de ses prédécesseurs

Réalisons maintenant des enchaînement des 4 précédents transformers comparés aux même taches effectuées dans l'AM.

Avant toute chose, il est à noter qu'un seul AM peut, parfois, ne pas remplir les mêmes fonctions que les transformers à tache unique.  
Par exemple, si vous souhaitez créer un nouvel Attribut 2 à partir d'un Attribut 1 déjà existant, et supprimer l'Attribut 1 dans la foulée.  
Il suffit d'enchainer un AttributeCreator puis un AttributeRemover (ou AttributeKeeper pour ceux qui aiment cocher plein de cases :smile:). Ici, un seul AM ne suffira pas.  
En effet, si vous dites dans les paramètres de l'AM que vous souhaitez à la fois créer un champ à partir d'un attribut et le supprimer, il risque de ne pas comprendre ce que vous voulez lui faire faire...

![fme pas comprendre](https://dl01fbzxdpfby.cloudfront.net/images/fme/transformers_ranking/fme_pas_comprendre.png "FME pas comprendre"){: .align-center}

Enchainement de 2 transformers :

![comparaison 2V1](https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/2V1.png "Comparaison 2V1"){: .align-center}

Enchainement de 3 transformers :

![comparaison 3V1](https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/3V1.png "Comparaison 3V1"){: .align-center}

Enchainement des 4 transformers mono taches :

![comparaison 4V1](https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/4V1.png "Comparaison 4V1"){: .align-center}

On se rend compte ici, que lorsq'au moins 2 transformers historiques sont enchaînés, face à un unique AM, les gains de temps sont là.  
Et il peut parfois même être 2x fois plus rapide !

J'imagine que l'AM est optimisé, lorsqu'il y a plusieurs taches à réaliser, pour qu'elles se réalisent le plus rapidement possible.

Pour reprendre la métaphore du Leatherman, si vous devez visser des cruciformes, redresser une tige, ouvrir une bière (il peut le faire !), cette fois , vous gagnerez du temps en prenant le Leatherman plutôt que d'aller chercher chaque outil un par un dans votre boîte à outils.

### Test d'enchainement d'AM

- AttributeCreator (création d'un Attribut 1, Attribut 2 et d'un Attribut 3 = Attribut 1 + Attribut 2) + AttributeKeeper (on ne garde que l'Attribute 3) : 139 secondes
- AM qui crée les 3 attributs + AM qui ne garde que l'Attribut 3 : 148 secondes

## Conclusion

Après ces quelques tests rapides, je pense qu'il y a du vrai dans mon hypothèse de départ.  
En réalité, nous avons tout intérêt à utiliser un transformer historique type AttributeQuelquechose plutôt que l'AM, uniquement dans le cas où une seule opération est réalisée.

Dès lors, que plusieurs opérations sont enchaînées, il ne faut surtout pas se priver d'utiliser directement l'AM afin de gagner en temps de traitement !!

Même s'il est toujours de bon ton de se méfier de l'ordre dans lequel les opérations sont réalisées.  
Comme dit précédemment, évitez par exemple, dans un même AM de supprimer un attribut si vous souhaitez réaliser un calcul de champ ou une concaténation sur celui-ci :smirk:.

----

N'hésitez pas à commenter directement en dessous, ou à m'envoyer un [message sur Twitter](https://twitter.com/messages/compose?recipient_id=938055192221765634), je vous répondrai avec plaisir :pray: !
