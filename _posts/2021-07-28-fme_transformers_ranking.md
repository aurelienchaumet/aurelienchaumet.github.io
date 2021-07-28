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

<div class='tableauPlaceholder' id='viz1627484356766' style='position: relative'><noscript><a href='#'><img alt='FME Transformers ranking ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;FM&#47;FMETransformersRankingJuly2021&#47;FMETransformersranking&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='FMETransformersRankingJuly2021&#47;FMETransformersranking' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;FM&#47;FMETransformersRankingJuly2021&#47;FMETransformersranking&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='fr-FR' /><param name='filter' value='publish=yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1627484356766');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else { vizElement.style.width='100%';vizElement.style.height='827px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>

## Conclusion

Cette nouvelle possibilité offerte dans la dernière mise à jour de Tableau permet de réaliser de nombreuses améliorations en termes d'interface en simplifiant le design de certains dashboards.

Il est possible d'imaginer par exemple qu'un graphique pop directement à la sélection d'un élément sur un graphique lié, sans pourautant être affiché en permanence.

En bref, encore bien des choses à imaginer grâce à Tableau !

----

Cet article m'a [été inspiré par un post de Samuel Parsons](https://www.linkedin.com/posts/samuel-parsons-b9184b97_tableau-activity-6824262186844610560-Mp7N), que je tiens à remercier vivement pour m'avoir (enfin) poussé à comprendre le fonctionnement des conteneurs et leur nouvelle rétractabilité !!

N'hésitez pas à commenter directement en dessous, ou à m'envoyer un [message sur Twitter](https://twitter.com/messages/compose?recipient_id=938055192221765634), je vous répondrai avec plaisir :pray: !
