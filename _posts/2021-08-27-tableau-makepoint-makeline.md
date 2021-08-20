---
layout: single
permalink: /articles/tableau_makepoint_makeline_fr/
title : "Tableau : MakePoint et MakeLine : Fonctionnement et cas d'usage" 
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/fme_lizard_perf.png
  overlay_filter: 0.3
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/fme_lizard_perf.png
excerpt:
  Il est de plus en plus simple de réaliser des cartes avec Tableau, et ces nouvelles fonctions permettent de nouveaux horizons

og_image: https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/fme_lizard_perf.png

comments: true
share: true
toc: true
toc_label: "Plan"
toc_icon: "chart-line"
toc_sticky: true
---

You can find an [english version of this article here](/articles/tableau_makepoint_makeline_en/) :smirk:

Les cartes commencent à être de plus en plus simples à réaliser sur Tableau.  
Et ça se ressent également sur les fonctionnalités disponibles pour les utilisateurs, notamment grâce à une dernière fonctionnalité cartographique (sortie avec la 2020.4), [la possibillité de gérer plusieurs couches de données](https://www.tableau.com/fr-fr/blog/2020/12/tableau-release-prep-browser-map-layers-RMT-linux) !

Lorsqu'un champ géométrique existe dans votre source de données, Tableau le détecte automatiquement et génère la visualisation de cette géométrie. Tout cela se fait très bien.

Le problème résidait avant 2019 et la version 2019.2, dans le fait que, parfois, les données ne contiennent pas de géométries en tant que tel mais uniquement des coordonnées X et Y (XX, YY par exemple :smirk:).

Dans ce cas, il fallait passer par une application tierce pour générer un champ géométrique et ouvrir ensuite le fichier retravaillé dans Tableau.

Maintenant, grâce aux fonctions [MakeLine](https://help.tableau.com/current/pro/desktop/fr-fr/functions_functions_spatial.htm#cr%C3%A9er-une-source-de-donn%C3%A9es-spatiales-%C3%A0-laide-de-makepoint) et [MakePoint](https://help.tableau.com/current/pro/desktop/fr-fr/functions_functions_spatial.htm#cr%C3%A9er-une-visualisation-%C3%A0-laide-de-makeline), pour les géométries ponctuelles et linéaires plus besoin de cette préparation préalable !

## Paramétrage des fonctions

Les 2, en tant que fonctions spatiales, peuvent être utilisées dans un champ calculé.

Allons-y !

### MakePoint

#### Création d'une géométrie ponctuelle

Lorsqu'on crée un champ calculé 'Point', l'aide intégrée dans Tableau nous donne quelques indications quant à ce qu'on doit faire avec cette fonction.

CAPTURE AIDE MAKEPOINT

Plutôt simple d'utilisation, il suffit de mettre à l'intérieur de la fonction MakePoint, un champ Latitude et un champ Lonigtude, séparas par une virgule.

`MAKEPOINT([Lat],[Long]`

Lorsque vous glissez le champ calculé 'Point' dans la vue, Tableau génèrera automatiquement la géométrie ponctuelle créée par la fonction MakeLine.

CAPTURE TABLEAU POINT

Easy nan ?

![gif easy](https://media1.giphy.com/media/3o7btNa0RUYa5E7iiQ/giphy.gif?cid=ecf05e47g42x2t9igqgbewrhaueoolz97t4wmvuhf7af5rqq&rid=giphy.gif&ct=g "Gif easy"){: .align-center}

Si on souhaite pouvoir avoir des informations sur chaque point, il faudra glisser XXX sur la carte Détails.

#### Paramétrage de la projection

Lorsqu'on représente des données géographiques sur une carte, nous sommes obligés de mettre à plat notre globe terrestre.

Pour cela, on utilise ce qu'on appelle une projection.  
Il en existe un nombre incalculable.  
Et pour que tout cela fonctionne, il faut définir un système de projection.  
Par exemple, en France métropolitaine, nous utilisons communément le Lambert 93 (code EPSG : 2154).

Par défaut, Tableau considère que la projection utilisée dans vos coordonnées est le WGS84 (code EPSG : 4326). Un des systèmes de projections les plus répandues et notamment utilisées pour représenter des données à l'échelle mondiale.

En résumé, lorsque vous utilisez la fonction MakePoint comme présentée plus haut, vos coordonnées doivent ressembler à 1.271667, 45.920587.  
Ce même point dans le système Lambert 93 ressemble plutôt à 369087.44, 6544608.

Si jamais vos coordonnées ne sont pas en WGS84, il suffit de le spécifier à Tableau dans la fonction MakePoint :

`MAKEPOINT([Lat],[Long], SRID`

Le SRID étant le code EPSG de la projection utilisée.

Pour de plus amples informations sur les systèmes de projection, je vous invite à lire [cet article](https://docs.qgis.org/2.14/fr/docs/gentle_gis_introduction/coordinate_reference_systems.html).

### MakeLine

Maintenant que nous avons des points, pourquoi ne pas les relier pour en faire des lignes :smile: ?

### Création d'une ligne

Encore une fois l'aide de Tableau nous indique clairement quoi faire.

Il suffit d'indiquer un point de départ et un point d'arrivée dans la fonction MakeLine.

`MAKELINE(geometry1, geometry2)`

Si on prend un exemple simple avec 2 points, il suffit donc de créer 2 champs calculés :

- Point 1 : `MAKEPOINT(45.94733,1.290894)`
- Point 2 : `MAKEPOINT(18.524345,88.289824)`

Puis de créer un 3ème champ calculés pour les relier :

- Prochain trajet de vacances : `MAKELINE(Point 1, Point 2)`

Glissez ce dernier champ dans une vue.  
Et voilà ! Encore une fois, rien de compliqué !

CAPTURE LIGNE

Une chose remarquable : comme expliqué précédemment, le fait de représenter le globe à plat crée des déformations.  
Cela implique que le chemin le plus court entre nos 2 points n'est pas une ligne droite sur une carte, alors qu'elle l'est en réalité.

Pour compenser cela et représenter la réalité Tableau crée une courbure.

## Cas d'usage

### Carte origine-destination

aa

### Création d'itinéraires

![comparaison 1V1](https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/1V1.png "Comparaison 1V1"){: .align-center}

## Conclusion

Après ces quelques tests rapides, je pense qu'il y a du vrai dans mon hypothèse de départ.

En réalité, nous avons tout intérêt à utiliser un **transformer historique** type AttributeQuelquechose plutôt que l'AM, uniquement dans le cas où **une seule opération** est réalisée.

Dès lors, que **plusieurs opérations** sont enchaînées, il ne faut surtout pas se priver d'utiliser directement l'**AttributeManager** afin de gagner en temps de traitement !!

**_Métaphore du Leatherman_**. CQFD...

![gif barack obama drop the mic](https://media.giphy.com/media/3o7qDEq2bMbcbPRQ2c/giphy.gif "Barack drops the mic"){: .align-center}

Même s'il est toujours de bon ton de se méfier de l'ordre dans lequel les opérations sont réalisées.  
Comme dit précédemment, évitez par exemple, dans un même AM de supprimer un attribut si vous souhaitez réaliser un calcul de champ ou une concaténation sur celui-ci :smirk:.

----

N'hésitez pas à commenter directement en dessous, ou à m'envoyer un [message sur Twitter](https://twitter.com/messages/compose?recipient_id=938055192221765634), je vous répondrai avec plaisir :pray: !
