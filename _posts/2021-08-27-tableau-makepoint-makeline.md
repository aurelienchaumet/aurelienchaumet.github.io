---
layout: single
permalink: /articles/tableau_makepoint_makeline/
title : "Tableau - MakePoint et MakeLine : Fonctionnement et cas d'usage" 
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/tableau_makepoint_makeline.png
  overlay_filter: 0.3
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/tableau_makepoint_makeline.png
excerpt:
  Il est de plus en plus simple de réaliser des cartes avec Tableau, et ces nouvelles fonctions permettent de nouveaux horizons

og_image: https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/tableau_makepoint_makeline.png

comments: true
share: true
toc: true
toc_label: "Plan"
toc_icon: "chart-line"
toc_sticky: true
---

Les cartes commencent à être de plus en plus simples à réaliser sur Tableau.  
Et ça se ressent également sur les fonctionnalités disponibles pour les utilisateurs, notamment grâce à une dernière fonctionnalité cartographique (sortie avec la 2020.4), [la possibillité de gérer plusieurs couches de données](https://www.tableau.com/fr-fr/blog/2020/12/tableau-release-prep-browser-map-layers-RMT-linux) !

Lorsqu'un champ géométrique existe dans votre source de données, Tableau le détecte automatiquement et génère la visualisation de cette géométrie. Tout cela se fait très bien.

Le problème résidait avant 2019 et la version 2019.2, dans le fait que, parfois, les données ne contiennent pas de géométries en tant que tel mais uniquement des coordonnées X et Y (XX, YY par exemple :smirk:).

Dans ce cas, il fallait passer par une application tierce pour générer un champ géométrique et ouvrir ensuite le fichier retravaillé dans Tableau.

Maintenant, grâce aux fonctions [MakeLine](https://help.tableau.com/current/pro/desktop/fr-fr/functions_functions_spatial.htm#cr%C3%A9er-une-source-de-donn%C3%A9es-spatiales-%C3%A0-laide-de-makepoint) et [MakePoint](https://help.tableau.com/current/pro/desktop/fr-fr/functions_functions_spatial.htm#cr%C3%A9er-une-visualisation-%C3%A0-laide-de-makeline), pour les géométries ponctuelles et linéaires plus besoin de cette préparation préalable !

## Paramétrage des fonctions

Les 2, en tant que fonctions spatiales, peuvent être utilisées dans un champ calculé.

Let's map !

### MakePoint

#### Création d'une géométrie ponctuelle

Lorsqu'on crée un champ calculé 'Point', l'aide intégrée dans Tableau nous donne quelques indications quant à ce qu'on doit faire avec cette fonction.

![aide makepoint](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/makepoint.png "Aide MakePoint"){: .align-center}

Plutôt simple d'utilisation, il suffit de mettre à l'intérieur de la fonction MakePoint, un champ Latitude et un champ Longitude, séparés par une virgule.

`MAKEPOINT([Lat],[Long]`

Pour l'exemple, des données personnelles, issues d'un suivi GPS d'un tour en vélo, seront utilisées ici.
{: .notice--info}

Lorsque vous glissez le champ calculé 'Points' dans la vue, Tableau génèrera automatiquement la géométrie ponctuelle créée par la fonction MakePoint.

![points strava](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/points_strava.png "Points GPS d'une balade à vélo"){: .align-center}
Easy nan ?

![gif easy](https://media1.giphy.com/media/3o7btNa0RUYa5E7iiQ/giphy.gif?cid=ecf05e47g42x2t9igqgbewrhaueoolz97t4wmvuhf7af5rqq&rid=giphy.gif&ct=g "Gif easy"){: .align-center}

Si on souhaite pouvoir avoir des informations sur chaque point, il faudra glisser l'identifiant unique des points (stop_id dans cet exemple) sur la carte Détails.

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

`MAKEPOINT([Lat],[Long], SRID)`

Le SRID étant le code EPSG de la projection utilisée.

Pour de plus amples informations sur les systèmes de projection, je vous invite à lire [cet article](https://docs.qgis.org/2.14/fr/docs/gentle_gis_introduction/coordinate_reference_systems.html).

### MakeLine

Maintenant que nous avons des points, pourquoi ne pas les relier pour en faire des lignes :smile: ?

### Création d'une ligne

Encore une fois l'aide de Tableau nous indique clairement quoi faire.

![aide makeline](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/makeline.png "Aide Makeline"){: .align-center}

Il suffit d'indiquer un point de départ et un point d'arrivée dans la fonction MakeLine.

`MAKELINE(geometry1, geometry2)`

Si on prend un exemple simple avec 2 points, il suffit donc de créer 2 champs calculés :

- Départ : `MAKEPOINT(45.94733,-1.290894)`
- Arrivée : `MAKEPOINT(7.318882,80.837402)`

Puis de créer un 3ème champ calculés pour les relier :

- Trajet de vacances : `MAKELINE(Départ, Arrivée)`

Glissez les 3 champs créés dans une vue.  
Et voilà ! Encore une fois, rien de compliqué !

![trajets vacances](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/trajet_vacances.png "Futur trajet de vacances ?"){: .align-center}

Une chose remarquable : comme expliqué précédemment, le fait de représenter le globe à plat crée des déformations.  
Cela implique que le chemin le plus court entre nos 2 points n'est pas une ligne droite sur une carte, alors qu'elle l'est en réalité.

Pour compenser cela et représenter la réalité, Tableau crée une courbure.

## Cas d'usage

Je recense ici 2 cas d'usage principaux quant à l'utilisation de création de points et de lignes sur Tableau.

### Carte origine-destination

Les cartes origine-destination permettent de représenter des flux entrants et/ou sortants d'un ou plusieurs points.

Un des exemples les plus simples à comprendre (pas forcément à représenter...) sont les flux domicile-travail. Cela permet, par exemple, de répondre à la question "Où travaillent les actifs résidant sur telle commune ?"

Pour creuser cet exemple, il faut tout d'abord aller récupérer [la base flux de mobilité de l'INSEE](https://www.insee.fr/fr/statistiques/4509353).  
Ce fichier donne, pour chaque commune le nombre de personnes y résidant ainsi que leur lieu de travail.  
Les communes sont décrites par leur Codgeo qui est l'identifiant unique de chaque commune.

Pour récupérer les coordonnées d'un point de la commune, il faut donc avoir sous la main un fichier recensant chaque commune avec un point (ou le générer).

Une fois cela fait, il ne reste qu'à réaliser 2 jointures dans Tableau :

- entre le Codgeo de la commune de résidence et la table de points par commune
- entre le Codgeo de la commune de travail et la table de points par commune

Il ne reste qu'à créer 3 champs calculés :

![makepoint residence](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/makepoint_residence.png "Création du point résidence"){: .align-center}

![makepoint travail](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/makepoint_travail.png "Création du point travail"){: .align-center}

![makeline flux](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/makeline_flux.png "Création du linéaire de flux domicile travail"){: .align-center}

On glisse le champ "Flux actifs" et là c'est tout moche !

![flux tous](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/flux_tous.png "Tous les flux d'un coup !"){: .align-center}

Sont représentés ici, l'ensemble des flux domicile-travail de toutes les communes, ce n'est donc évidemment que peu lisible !

Il est possible de visualiser, par commune les communes de travail, en ajoutant :

- un filtre par "Codgeo - Nom de commune"
- le Codgeo de résidence en Détail
- le Codgeo de travail en Détail
- la Taille en fonction du nombre d'actifs

![flux st trojan](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/flux_st_trojan.png "Flux des actifs de St Trojan les Bains"){: .align-center}

Cette représentation seule n'est sans doute pas la plus pertinente, ni la plus simple à lire, mais elle peut servir de carte de situation dans un dashboard plus complet.
{: .notice--info}

![dahsboard domicile travail](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/exemple_dashboard_flux.png "Dashboard flux domicile travail"){: .align-center}

### Création d'itinéraires

L'intérêt du MAKELINE réside également dans le fait de pouvoir reconstituer des routes ou des itinéraires.

Repartons des données issues du tracking d'activité en vélo. Chaque point est recueilli suivant un intervalle de temps. Donc, en toute logique, pour tracer l'itinéraire suivi, il suffit de relier chaque point avec le suivi et ainsi de suite.

Dans cet exemple, il suffit de réaliser une "auto-jointure" sur la source de donnée, en indiquant dans le champ de jointure que nous souhaitons que chaque point soit relié au suivant, grâce à l'expression `[Track Segment Point Index]-1`.

![jointure itself](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/jointure_itself.png "Auto jointure"){: .align-center}

Ensuite, il suffit de créer 3 champs calculés :

- Points précédents, sur les champs de la 1ère table
- Points suivants, sur les champs de la seconde table
- Tracé, qui fait la jonction entre chaque point et le suivant

![points precedents](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/points_precedents_strava.png "Création du point précédent"){: .align-center}

![points suivants](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/points_suivants_strava.png "Création du point suivant"){: .align-center}

![trace parcours](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/trace_strava.png "Tracé du parcours emprunté"){: .align-center}

On glisse le champ Tracé et c'est réglé !

Libre à vous, ensuite de réaliser quelques analyses et autres peaufinages esthétiques.

Grâce à la fonction DISTANCE de Tableau, il est possible d'afficher la vitesse par segment.
{: .notice--info}

![trace parcours vitesse](https://dl01fbzxdpfby.cloudfront.net/images/tableau/makepoint_makeline/itineraires_suivi_strava_vitesse.png "Tracé du parcours emprunté avec la vitesse par tronçon"){: .align-center}

## Conclusion

Tableau propose, grâce à ces deux fonctions MakePoint et MakeLine de nouvelles fonctionnalitéés cartographiques très intéressantes, comme nous avons pu le voir à travers les 2 cas d'usage présentées.

Il existe également maintenant [d'autres fonctions spatiales](https://help.tableau.com/current/pro/desktop/fr-fr/functions_functions_spatial.htm#liste-des-fonctions-spatiales-dans-tableau), répondant à d'autres cas d'usage, comme Buffer (uniquement sur un ponctuel) ou Zone qui permet de calculer la superficie d'un polygone.

Sans doute encore pas mal d'analyses cartographiques à créer !

## Sources

- Annonce de la release : https://www.tableau.com/about/blog/2019/6/geospatial-analysis-made-easy-two-new-spatial-functions-makepoint-and-makeline
- Article Biztory : https://www.biztory.com/blog/spatial-functions-in-tableau
- MakePoint par Tableau Tim : https://www.youtube.com/watch?v=tM0mMsbU-fg
- MakeLine toujours par Tableau Tim : https://www.youtube.com/watch?v=fAxVy3TZC-o
- How to create routes with the MAKEPOINT and MAKELINE functions par Andy Kriebel : https://www.youtube.com/watch?v=54Bao2IneKA

----

N'hésitez pas à commenter directement en dessous, ou à m'envoyer un [message sur Twitter](https://twitter.com/messages/compose?recipient_id=938055192221765634), je vous répondrai avec plaisir :pray: !
