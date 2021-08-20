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



## Paramétrage des fonctions

### MakePoint

### MakeLine

## Cas d'usage

### Carte origine-destination

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
