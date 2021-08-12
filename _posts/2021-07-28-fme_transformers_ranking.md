---
layout: single
permalink: /articles/fme_transformers_ranking/
title : "FME : Exploration du classement des Transformers FME" 
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/fme/transformers_ranking/fme_lizard_trophy.png
  overlay_filter: 0.3
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/fme/transformers_ranking/fme_lizard_trophy.png
excerpt:
  Comment utilisez-vous les différents transformers FME ?

og_image: https://dl01fbzxdpfby.cloudfront.net/images/fme/transformers_ranking/fme_lizard_trophy.png

comments: true
share: true
toc: true
toc_label: "Plan"
toc_icon: "chart-line"
toc_sticky: true
---

## Introduction

[FME](https://www.safe.com/) est sans doute l'un des ETL les plus répandus dans le monde dans les entreprises et les collectivités.  
Comme tout bon ETL (Extract-Transform-Load), il permet de lire des données [(+ de 500 formats différents)](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_ReadersWriters/Format-List-All.htm#All), de les transformer et de les charger dans un des formats supportés par FME.  
Il est édité par la société canadienne Safe.

![logo safe](https://dl01fbzxdpfby.cloudfront.net/images/fme/transformers_ranking/safe.png "Logo Safe"){: .align-center}

Au-delà de la rapidité de certaines opérations réalisées, l'autre puissance de FME réside dans son interface graphique.  
Il fonctionne sur le système de box qu'on connecte entre elles.  
Ces box peuvent être de plusieurs types :

- Reader : permet de lire les données en entrée
- Writer : permet d'écrire les données en sortie
- Transformers

## Qu'est-ce qu'un transformer ?

Les transformers sont les opérateurs qui permettent de réaliser les opérations sur les données.  
Quelques transformers permettent également de lire des données, mais ne nous égarons pas...

![gif chemin](https://media.giphy.com/media/jFem9jFckQ6oU/giphy.gif "Gif chemin"){: .align-center}

Il existe environ 500 transformers, sans compter ceux publiés directement par des utilisateurs [sur le hub officiel de Safe](https://hub.safe.com/?page=1&page_size=10&order=updated_at_desc).

Sur le hub, il y a à ce jour 715 transformers publiés, ce qui nous fait donc un total de transformers autour des 1200 :smile:
{: .notice--info}

Chaque transformer a bien sûr sa propre fonction et est utile pour une tache bien définie.

Par exemple, Tester, comme son l'indique, est utilisé pour tester des valeurs d'attributs. Il possède en sortie 2 ports "Passed" et "Failed" afin de trier les données en fonction d'une ou plusieurs conditions de test que vous définissez.

Il n'est évidemment pas utile de connaître l'ensemble des transformers FME pour travailler avec. Si cela peut être un passe-temps sans doute intéressant de les apprendre toutes...  
L'aide dans le logiciel FME, complétée par les ressources officielles en ligne permettent quasiment toujours de s'en sortir même sans connaître a priori les noms des transformers que vous aurez besoin d'utiliser.

En revanche, un certain nombre de transformers sont utilisés très fréquemment. Tout cela dépend bien sûr du type de données sur lequel vous avez l'habitude de travailler.  
Si vous utilisez FME comme un ETL spatial, le Dissolver et le SpatialRelator vous seront aucun doute plus utile qu'à une personne travaillant sur des données sans dimension géographique :wink:.

Et c'est ici qu'intervient le classement des transformers !!

## Classement des transformers

Safe met notamment à disposition [la liste de tous les transformers officiels sur son site internet](https://www.safe.com/transformers/), classés par popularité.  
Cette popularité est calculée à partir des retours des utilisateurs auprès de Safe.

Cela donne une bonne idée de leur utilisation et surtout de leur évolution au fil des années.

Vous trouverez ci-dessous, le classement des 30 transformers les plus plebiscités, à la date du 28 juillet 2021.

_[Vous pouvez également le consulter directement ici.](https://public.tableau.com/views/FMETransformersRankingJuly2021/FMETransformersranking?:language=fr-FR&publish=yes&:display_count=n&:origin=viz_share_link:showVizHome=no#5)_

En passant la souris sur la barre d'un transformer, vous verrez également son évolution apparaître depuis 2018.
{: .notice--info}

<iframe id="Classement_Transformers_FME"
    title="Classement Transformers FME"
    width="1000"
    height="700"
    src="https://public.tableau.com/views/FMETransformersRankingJuly2021/FMETransformersranking?:language=fr-FR&publish=yes&:display_count=n&:origin=viz_share_link:showVizHome=no#5">
</iframe>

## Analyse et réflexions personnelles

Les réflexions suivantes proviennent de mon expérience personnelle et pourraient bien sûr différer pour vous.  
Je suis d'ailleurs curieux d'avoir d'autres avis sur ces transformers !

### Tester forever

Ici, je pense qu'il n'y a pas vraiment photo, ni trop de débat. Compliqué de passe à côté du [Tester](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/tester.htm?Highlight=tester) dans un workbench FME... Donc j'imagine qu'il mérite sa place de numéro indétrôné depuis 2018.

Je viens d'ouvrir au hasard 6 projets et tous en contenaient au moins 2 :smile:.

### AttributeManager passe second

[L'AttributeManager](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/attributemanager.htm) est pour moi un des transformers incontournables, tant il remplit de fonctions à lui tout seul.  

Il a été released en 2016 et quelle release ! Il permet de :

- renommer des champs
- supprimer des champs
- créer des champs
- définir les valeurs d'un champ que ce soit par une opération arithmétique, des valeurs conditionnelles ou une concaténation de champs
- utiliser des paramètres

Il peut donc en théorie remplacer les transformers qui réalisent ces opérations :

- AttributeCreator
- AttributeCopier
- AttributeRenamer
- AttributeKeeper
- AttributeRemover

Il peut également remplacer d'autres transformers qui réalisent des opérations sur les chiffres comme l'AttributeRounder ou bien l'AreaCalculator qui permet de calculer la superficie d'objets géométriques (en utilisant la fonction Area dans l'Editeur Arithmétique de l'AttributeManager).  
Et je suis sûr d'en oublier un tas d'autres !

Vous aurez compris que personnellement je ne m'en passerai pas, donc pas étonnant qu'il soit à la 2ème place depuis 2 ans.

En revanche, ce que je comprends moins, c'est le fait que Safe laisse encore coexister tous ces transformers, alors que celui-ci pourrait tout à fait les remplacer sans douleur.

Vous trouverez dans un prochain article un test de performance qui tente de comprendre leur coexistence en fonction de cas d'usage.

### L'ascension du DuplicateFilter

Passé depuis 2019 de la 18ème place à la 7ème place en juillet de cette année, le [DuplicateFilter](http://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/duplicatefilter.htm) réalise une belle progression !

Il est extrêmement pratique pour détecter des doublons dans les données. Il est possible de lui spécifier un ou plusieurs attributs à prendre en compte pour détecter ces doublons.  
De là à expliquer ce soudain regain d'intérêt de la communauté...

### L'éternel Inspector

Pour ceux ayant commencé à travailler avec FME avant la version 2018, l'[Inspector](http://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/inspector.htm) était un outil indispensable !

Il permet de voir les éléments à la sortie d'un transformer.

Et pourquoi ai-je parlé de la version 2018 ? Car c'est cette année que SAFE a sorti le Feature Caching ([que Mark Ireland a comparé très judisiceusement à un écureuil](https://www.safe.com/blog/2018/05/caching-data-fme-evangelist174/)).

Le Feature Caching vous laisse la possibilité de garder en mémoire les données à chaque étape d'un workbench. Et donc à chaque sortie de transformer. J'imagine que c'est ce qui explique sa (lente) décroissance initiée en 2021.  
Même s'il subit (de manière plutôt inexpliquée pour moi), un regain de reconnaissance en ce milieu d'année.

J'imagine que certains l'utilisent encore sur de gros workbenchs qui tournent déjà depuis un moment, pour inspecter très ponctuellement certaines étapes.  
Car il ne faut pas oublier que le Feature Caching, en fonction des données et de votre workbench, peut manger pas mal de ressources et donc demander du temps.  
Mais au prix d'une praticité sans pareil !

Petit tips, vous avez la possibilit d'insérer un Inspector en réalisant un clic droit n'importe où à l'intérieur d'un workbench.
{: .notice--info}

IMAGE DE L'INSERTION DE L'INSPECTOR

### Junction is here

[Junction](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Workbench/Workbench/Using-Junctions.htm) n'est (d'après moi) pas un transformer à part entière. Il ne réalise aucune modification de la donnée. Mais il permet, notamment d'y voir un peu plus clair dans ses workbenchs, d'où son utilité et son entrée à la 27ème place du classement.

Il est apparu en 2016 [avec la possibilité de cacher des connexions](https://www.safe.com/blog/2016/05/fmeevangelist150/).

L'idée est de rassembler plusieurs connexions en un seul et même point, appelé Junction.  
Personnellement je m'en sers également pour "amener" une connexion déjà existante sur une partie distante d'un workbench, comme dans l'exemple ci-dessous.

IMAGE D'UNE JONCTION PROPRE

Vous admettrez que c'est légèrement plus élégant et lisible que de laisser l'ensemble des jonctions telles qu'elles...

IMAGE SANS JONCTION TOUT MOCHE

## Ranking de mes propres workbenchs

Après ce petit tour du classement officiel des transformers FME, je vous propose mon propre classement, basée sur l'utilisation que j'en ai.

Pour le réaliser, j'ai utilisé le Reader FME Workspace (FMW) qui permet de lire les métadonnées des workspaces créés.  
Ce Reader donne notamment l'ensemble des transformers utilisés.

Vous trouverez ci-dessous les transformers que j'ai le plus utilisés cette année.  
En passant la souris sur la barre d'un transformer, vous verrez également son évolution apparaître depuis 2016.
{: .notice--info}

<iframe id="Classement_Transformers_FME"
    title="Classement Transformers FME"
    width="1000"
    height="700"
    src="https://public.tableau.com/views/FMETransformersPersoRanking/FMETRANSFORMERSrankingperso?publish=yes&:display_count=n&:origin=viz_share_link:showVizHome=no#2">
</iframe>

### AttributeManager forever

Quand je vous disais plus haut que j'aurais du mal à me passer de l'attributeManager, je ne mentais pas :smile:

Sur 335 transformers utilisés dans 16 workbenchs cette année, j'ai utilisé l'AttributeManager 66 fois, soit 20% de l'ensemble des transformers utilisés.

Alors que le tester n'arrive qu'au 4ème rang de mon côté.

### FeatureMerger et autres transformers que j'utilise sur des données spatiales

Le FeatureMerger est au 2ème rang des transformers que j'utilise le plus. Pas très étonnant, car au quotidien je passe pas mal de temps àc roiser des données.

Données notamment spatiales, ce qui explique la position de transformers plus spécifiques, comme l'AreaCalculator (que je pourrais très bien remplacer par l'AttributeManager d'ailleurs...), le VertexCreator (qui permet de créer des géométries ponctuelles à partir de coordonnées), le CenterPointReplacer (que j'utilise fréquemment pour réaliser des jointures spatiales) ou encore le SpatialRelator.

Le BANGeocoder est [un transformer personnalisé publié par Geonov](https://hub.safe.com/publishers/geonov/transformers/bangeocoder) et permet de réaliser du géoréférencement français.  
Petit bijou de siplicité d'utilisation, j'en profite d'ailleurs pour remercier [Mathieu Ambrosy](https://twitter.com/geonov_fr?lang=fr) pour celui-ci car il est fort pratique !

## Conclusion

J'espère que ce petit tour des différents transformers les plus utilisés par la communauté (et par moi-même) vous aura intéressé, voire même donné des idées !

Et n'oubliez pas qu'il en existe un bon millier, et que si vous avez besoin de réaliser quelque chose sur de la donnée (quelque soit le format, à peu de chose près), FME a surement un transformer pour ça !

----

N'hésitez pas à commenter directement en dessous, ou à m'envoyer un [message sur Twitter](https://twitter.com/messages/compose?recipient_id=938055192221765634), je vous répondrai avec plaisir :pray: !
