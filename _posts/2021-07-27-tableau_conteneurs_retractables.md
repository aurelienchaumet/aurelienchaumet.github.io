---
layout: single
permalink: /articles/tableau_conteneurs_retractables/
title : "Tableau : Utilisation des conteneurs rétractables" 
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/conteneurs_retractables.png
  overlay_filter: 0.3
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/conteneurs_retractables.png
excerpt:
  Paramétrage et utilisation de conteneurs rétractables sur Tableau

og_image: https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/conteneurs_retractables.png

comments: true
share: true
toc: true
toc_label: "Plan"
toc_icon: "chart-line"
toc_sticky: true
---

Cela fait un moment que j'avais envie de rédiger des articles sur l'utilisation de [Tableau Software](https://www.tableau.com/fr-fr), qui est aujourd'hui une des solutions de DataViz et d'exploration de données à la fois simple à prendre en main et complexe lorsqu'on souhaite pousser le vice :wink:.  
C'est un outil que j'utilise quasiment quotidiennement depuis 3 ans, sur lequel je me suis formé seul, grâce aux ressources présentes sur le web.

J'espère que cet article apportera ma pierre à l'édifice de la connaissance Tableau-esque !

N'hésitez pas à commenter et à me faire des retours sur votre propre expérience.

[Les données utilisées pour cet article](https://legacy.data.gouv.fr/fr/datasets/donnees-relatives-aux-aides-exceptionnelles-aux-artisans-et-commercants-dans-le-cadre-de-lepidemie-de-covid-19/#_) sont issues du jeu de données _Données relatives aux aides exceptionnelles aux artisans et commerçants dans le cadre de l'épidémie de COVID-19_ depuis data.gouv.fr.
{: .notice--info}

----

## Ajouter un bouton Afficher/Masquer

Tableau Software a apporté lors de [sa dernière mise à jour 2021.2](https://www.tableau.com/fr-fr/support/releases/desktop/2021.2) une fonctionnalité extrêmement intéressante et utile : la possibilité d'afficher/masquer n'importe quel objet d'un dashboard.

Comme vous pouvez le voir ci-dessous, il suffit d'aller dans les options de l'object en question (une feuille, un conteneur, un bloc texte...) et de sélectionner "Ajouter un bouton Afficher/Masquer".  
Apparait alors un bouton flottant avec une croix. Si vous cliquez dessus en maintenant `Alt` sur votre clavier, cela aura pour effet de masquer l'objet précédemment sélectionné. Un nouveau `Alt+Clic` et l'élément réapparait ! :sparkles:

![objet retractable](https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/objet_retractable.gif "Gif objet rétractable"){: .align-center}

Auparavant, et depuis la version 2019.2, seuls les conteneurs flottants avaient cette possibilité.
{: .notice--info}

## Conteneurs rétractables

Cette nouvelle est intéressante, mais comme vous avez pu le constater, paramétré en l'état, le fait de masquer un objet laisse un gros blanc sur le dashboard. Ce qui n'est que peu esthétique...

Et c'est là que la magie opère !  
Etant donné que nous pouvons masquer n'importe quel objet, essayons sur des conteneurs, mais pas n'importe lesquels, les fixes !

![conteneur fixe retractable](https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/conteneur_retractable.gif "Gif conteneur fixe rétractable"){: .align-center}

Alors là comme ça, vous serez bien tentés de me dire "Mais quelle est la différence entre ces 2 GIF ?? Quel procédé subtil et magique as-tu utilisé ?" ou même "C'est sorcellerie messire !!"

![sorcellerie](https://media.giphy.com/media/MrHFzd4JQ22Zy/giphy.gif "Sorcellerie"){: .align-center}

### Mais d'ailleurs, c'est quoi un conteneur ?

Revenons un peu en arrière. Un conteneur, dans Tableau et [d'après Tableau itself](https://help.tableau.com/current/pro/desktop/fr-fr/dashboards_organize_floatingandtiled.htm#regrouper-les-%C3%A9l%C3%A9ments-%C3%A0-laide-de-conteneurs-de-disposition) :

> Les conteneurs de disposition vous permettent de regrouper des éléments de tableau de bord afin de pouvoir les positionner rapidement. Lorsque vous modifiez la taille et l'emplacement des éléments dans un conteneur, les autres éléments de conteneur s'ajustent automatiquement.

Grosso modo, lorsque vous designez votre dashboard, plutôt que de glisser-déposer vos feuilles, vous pouvez d'abord glisser-déposer des objets appelés Horizontal et Vertical, qui sont donc nos fameux conteneurs. Vous pouvez ensuite venir glisser-déposer vos feuilles à l'intérieur de ces conteneurs et ils s'arrangeront beaucoup mieux les uns envers les autres.

Si votre design a été réfléchi en amont et est bien préparé (as always bien sûr !), l'agencement des conteneurs n'est pas très complexe.

### La magie de la collapsibilité des conteneurs

Non, je ne vous parlerai pas d'un coup d'un seul d'effondrement sociétal. Mais plutôt de ce que j'ai appelé plus haut la rétractabilité des conteneurs, traduit de l'anglais _collapsible containers_.

Etant donné qu'un conteneur est réactif à ce qu'il contient, nous allons nous en servir pour que les graphiques situés sur la gauche du dashboard puissent emplir la place laissée libre par le graphique de droite lorsqu'il se masque.

Nous souhaitons arriver à cette disposition :

![disposition souhaitée](https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/disposition.png "Disposition souhaitée"){: .align-center}

Le fait que "aides par benef" (le graphique de droite) soit à l'intérieur du même conteneur que les 2 autres (situés dans le dernier Horizontal) va leur permettre de prendre sa place lorsqu'il sera masqué.

![la ruse est finaude](https://media.giphy.com/media/i3OheHKgFAqha/giphy.gif "La ruse est finaude"){: .align-center}

Pour ce faire, il suffit de glisser d'abord un conteneur horizontal. Puis d'y insérer le graphique qui sera à droite. Ensuite un conteneur vertical sur la gauche, à l'intérieur du premier conteneur. Et il n'y a plus qu'à mettre dans ce dernier conteneur, les 2 graphiques que nous voulons garder à gauche !

![mise en place](https://dl01fbzxdpfby.cloudfront.net/images/tableau/conteneur_retractable/mise_en_place.gif "Mise en place"){: .align-center}

Et voilà !! Maintenant, il n'y a plus qu'à effectuer la manipulation décrite en début d'article. A savoir sélectionner le graphique de droite, ouvrir ses options grâce à la petite flèche pointant vers le bas, "Ajouter un bouton Afficher/Masquer" et le tour est joué !

Vous pouvez par la suite modifier l'apparence du bouton en mettant l'image que vous souhaitez, ajouter une légende ou même faire des conteneurs de boutons (ça pourra être pour un prochain article :smile:) !

![dingue](https://media.giphy.com/media/12GP2pkws57gd2/giphy.gif "Dingue"){: .align-center}

Vous pouvez [télécharger le fichier Tableau directement depuis mon profil Tableau Public](https://public.tableau.com/app/profile/aurelien.chaumet/viz/Tuto-Conteneursrtractables/Pasdeconteneur-Pasdechocolat?publish=yes).

## Conclusion

Cette nouvelle possibilité offerte dans la dernière mise à jour de Tableau permet de réaliser de nombreuses améliorations en termes d'interface en simplifiant le design de certains dashboards.

Il est possible d'imaginer par exemple qu'un graphique pop directement à la sélection d'un élément sur un graphique lié, sans pourautant être affiché en permanence.

En bref, encore bien des choses à imaginer grâce à Tableau !

----

Cet article m'a [été inspiré par un post de Samuel Parsons](https://www.linkedin.com/posts/samuel-parsons-b9184b97_tableau-activity-6824262186844610560-Mp7N), que je tiens à remercier vivement pour m'avoir (enfin) poussé à comprendre le fonctionnement des conteneurs et leur nouvelle rétractabilité !!

N'hésitez pas à commenter directement en dessous, ou à m'envoyer un [message sur Twitter](https://twitter.com/messages/compose?recipient_id=938055192221765634), je vous répondrai avec plaisir :pray: !
