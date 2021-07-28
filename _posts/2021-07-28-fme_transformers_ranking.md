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

## Introduction

[FME](https://www.safe.com/) est sans doute l'un des ETL les plus répandus dans le monde dans les entreprises et les collectivités.  
Comme tout bon ETL (Extract-Transform-Load), il permet de lire des données [(+ de 500 formats différents)](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_ReadersWriters/Format-List-All.htm#All), de les transformer et de les charger dans un des formats supportés par FME.  
Il est édité par la société canadienne Safe.

IMAGE SAFE

Au-delà de la rapidité de certaines opérations réalisées, l'autre puissance de FME réside dans son interface graphique.  
Il fonctionne sur le système de box qu'on connecte entre elles.  
Ces box peuvent être de plusieurs types :

- Reader : permet de lire les données en entrée
- Writer : permet d'écrire les données en sortie
- Transformers

## Qu'est-ce qu'un Transformer ?

Les Transformers sont les opérateurs qui permettent de réaliser les opérations sur les données.  
Quelques transformers permettent également de lire des données, mais ne nous égarons pas...

![gif chemin](https://media.giphy.com/media/jFem9jFckQ6oU/giphy.gif "Gif chemin"){: .align-center}

Il existe environ 500 transformers, sans compter ceux publiés directement par des utilisateurs [sur le hub officiel de Safe](https://hub.safe.com/?page=1&page_size=10&order=updated_at_desc).

Sur le hub, il y a à ce jour 715 transformers publiés, ce qui nous fait donc un total de transformers autour des 1200 :smile:
{: .notice--info}

Chaque Transformer a bien sûr sa propre fonction et est utile pour une tache bien définie.

Par exemple, Tester, comme son l'indique, est utilisé pour tester des valeurs d'attributs. Il possède en sortie 2 ports "Passed" et "Failed" afin de trier les données en fonction d'une ou plusieurs conditions de test que vous définissez.

Il n'est évidemment pas utile de connaître l'ensemble des Transformers FME pour travailler avec. Si cela peut être un passe-temps sans doute intéressant de les apprendre toutes...  
L'aide dans le logiciel FME, complétée par les ressources officielles en ligne permettent quasiment toujours de s'en sortir même sans connaître a priori les noms des Transformers que vous aurez besoin d'utiliser.

En revanche, un certain nombre de Transformers sont utilisés très fréquemment. Tout cela dépend bien sûr du type de données sur lequel vous avez l'habitude de travailler.  
Si vous utilisez FME comme un ETL spatial, le Dissolver et le SpatialRelator vous seront aucun doute plus utile qu'à une personne travaillant sur des données sans dimension géographique :wink:.

Et c'est ici qu'intervient le classement des Transformers !!

## Classement des transformers

Safe met notamment à disposition [la liste de tous les Transformers officiels sur son site internet](https://www.safe.com/transformers/), classés par popularité.  
Cette popularité est calculée à partir des retours des utilisateurs auprès de Safe.

Cela donne une bonne idée de leur utilisation et surtout de leur évolution au fil des années.

Vous trouverez ci-dessous, le classement des 30 Transformers les plus plebiscités, à la date du 28 juillet 2021.

_[Vous pouvez également le consulter directement ici.](https://public.tableau.com/views/FMETransformersRankingJuly2021/FMETransformersranking?:language=fr-FR&publish=yes&:display_count=n&:origin=viz_share_link:showVizHome=no#5)_

En passant la souris sur la barre d'un Transformer, vous verrez également son évolution apparaître depuis 2018.
{: .notice--info}

<iframe id="Classement_Transformers_FME"
    title="Classement Transformers FME"
    width="1000"
    height="700"
    src="https://public.tableau.com/views/FMETransformersRankingJuly2021/FMETransformersranking?:language=fr-FR&publish=yes&:display_count=n&:origin=viz_share_link:showVizHome=no#5">
</iframe>

## Analyse et réflexions personnelles

Les réflexions suivantes proviennent de mon expérience personnelle et pourraient bien sûr différer pour vous.  
Je suis d'ailleurs curieux d'avoir d'autres avis sur ces Transformers !

### Tester forever

Ici, je pense qu'il n'y a pas vraiment photo, ni trop de débat. Compliqué de passe à côté du [Tester](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/tester.htm?Highlight=tester) dans un workbench FME... Donc j'imagine qu'il mérite sa place de numéro indétrôné depuis 2018.

Je viens d'ouvrir au hasard 6 projets et tous en contenaient au moins 2 :smile:.

### AttributeManager passe second

[L'AttributeManager](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/attributemanager.htm) est pour moi un des Transformers incontournables, tant il remplit de fonctions à lui tout seul.

Il a été released en 2016 et quelle release ! Il permet de :

- renommer des champs
- supprimer des champs
- créer des champs
- définir les valeurs d'un champ que ce soit par une opération arithmétique, des valeurs conditionnelles ou une concaténation de champs
- utiliser des paramètres

Il peut donc en théorie remplacer les Transformers qui réalisent ces opérations :

- AttributeCreator
- AttributeCopier
- AttributeRenamer
- AttributeKeeper
- AttributeRemover

Il peut également remplacer d'autres Transformers qui réalisent des opérations sur les chiffres comme AttributeRounder ou bien l'AreaCalculator qui permet de calculer la superficie d'objets géométriques (en utilisant la fonction Area dans l'Editeur Arithmétique de l'AttributeManager).  
Et je suis sûr d'en oublier un tas d'autres !

Vous aurez compris que personnellement je ne m'en passerai pas, donc pas étonnant qu'il soit à la 2ème place depuis 2 ans.

En revanche, ce que je comprends moins, c'est le fait que Safe laisse encore coexister tous ces Transformers alors que celui-là pourrait tout à fait les remplacer sans douleur.

Essayons-nous à un test de performance qui expliquerait peut-être leur coexistence en fonction des cas d'usage.

#### Test de l'AttributeManager en face to face avec ses ancêtres

#### Test de l'AttributeManager en remplacement d'un enchaînement de ses prédécesseurs

## Conclusion

Cette nouvelle possibilité offerte dans la dernière mise à jour de Tableau permet de réaliser de nombreuses améliorations en termes d'interface en simplifiant le design de certains dashboards.

Il est possible d'imaginer par exemple qu'un graphique pop directement à la sélection d'un élément sur un graphique lié, sans pourautant être affiché en permanence.

En bref, encore bien des choses à imaginer grâce à Tableau !

----

Cet article m'a [été inspiré par un post de Samuel Parsons](https://www.linkedin.com/posts/samuel-parsons-b9184b97_tableau-activity-6824262186844610560-Mp7N), que je tiens à remercier vivement pour m'avoir (enfin) poussé à comprendre le fonctionnement des conteneurs et leur nouvelle rétractabilité !!

N'hésitez pas à commenter directement en dessous, ou à m'envoyer un [message sur Twitter](https://twitter.com/messages/compose?recipient_id=938055192221765634), je vous répondrai avec plaisir :pray: !
