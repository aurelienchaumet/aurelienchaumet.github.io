---
layout: single
permalink: /articles/30daymapchallenge_plotly/  
title : "Visualisation des statistiques Twitter du 30 DayMapChallenge 2020 via Plotly" 
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/30dmc_stats.png
  overlay_filter: 0.3
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/30dmc_stats.png
excerpt:
  Affichage de données Twitter via Plotly et rendu html

og_image: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/30dmc_stats.png

comments: true
share: true
toc: true
toc_label: "Plan"
toc_icon: "chart-line"
toc_sticky: true
---

>Cet article fait partie d'une série de 3 articles expliquant le processus de création derrière celui donnant des statistiques autour du 30DayMapChallenge 2020 que [vous pouvez trouver ici](https://aurelienchaumet.github.io/articles/30daymapchallenge_stats_fr/).  

[![twitter twint](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_sortie_import.png){: .align-center}](/articles/30daymapchallenge_scraping_twitter)

[Le premier article](/articles/30daymapchallenge_scraping_twitter) détaille la manière de récupérer les données en masse provenant de Twitter et les préparer grâce à Pandas.

[![twitter plotly](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_plotly.png){: .align-center}](/articles/30daymapchallenge_plotly)

Le deuxième traite de la construction du graphique sur les finishers via Plotly.

![twitter bokeh heroku](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_bokeh.png){: .align-center}

Le dernier expliquera comment construire le graphique interactif sur les statistiques générales via Bokeh et déployé sur Heroku.

----

Maintenant que nous avons récupéré et commencé à préparer les données qui nous intéressent, nous allons pouvoir envisager leur visualisation.

## Plotly, une bibliothèque de visualisation polyvalente

Si vous commencez en datavisualisation sur Python, vous allez forcément très vite en venir à vouloir réaliser des représentations interactives et donc mettre de côté (pour ne pas dire, laisser tomber) [Matplotlib](https://matplotlib.org/).  
Bien que cette bibliothèque propose énormément de types de graphiques différents, et qu'elle soit très accessible, vous allez assez rapidement avoir envie de passer votre souris pour faire apparaître un tooltip et avoir des informations sur ce point là en particulier. Ou même vouloir ajouter des filtres, des sélecteurs... Et que sais-je d'autre encore !

C'est ici que [Plotly](https://plotly.com/python/) entre en scène !

### Principes de Plotly

Plotly est une bibliothèque très polyvalente, dans le sens où elle est accessible en Python, R ou Julia.

De plus, elle est extrêmement simple à prendre en main, interactive par nature, très bien documentée et la communauté est plutôt active. Que demander de plus ?

Vous trouverez l'ensemble des types de graphiques que Plotly est susceptible de produire à cette adresse : <https://plotly.com/python/>

### Installation

Côté installation, comme souvent, rien de bien complexe :

- Via Pip

  ```python
  pip install plotly==4.14.3
  ```

- Via Conda

  ```python
  conda install -c plotly plotly==4.14.3
  ```

Si vous souhaitez l'utiliser dans un [Jupyter Notebook](https://jupyter.org/), pensez également à installer `notebook` et `ipywidgets` :

```python
pip install "notebook>=5.3" "ipywidgets>=7.5
```

>Ou remplacez `pip` par `conda` si vous travaillez avec Anaconda :wink:

Vous pouvez maintenant afficher votre premier graphique via Plotly !

```python
import plotly.graph_objects as go
fig = go.Figure(data=go.Bar(y=[2, 3, 1]))
fig.show()
```

<iframe width="100%" height="400"
    src="https://aurelienchaumet.github.io/data/30daymapchallenge_coulisses/premier_graphique_plotly.html">
</iframe>

Ca c'était de l'exemple utile ! :smile:

Jusque là tout va bien ? On avance alors !!

## Visualisation des statistiques des finishers

### Objectifs de visualisation

Avant de rentrer dans le vif du sujet, arrêtons-nous une seconde et demandons ce que nous souhaitons voir (et a fortiori montrer)?

Nous partons ici du postulat que nous avons déjà exploré la donnée et que nous savons ce que nous voulons en faire.  
Dans ce cas-là, la meilleure chose à faire est de rédiger un petit cahier des charges pour soi.  
Cela permettra de connaître :

- Ce que nous voulons montrer
- Comment nous souhaitons l'afficher
- Les fonctionnalités autour du graphique

Dans notre cas précis, nous voulons avoir une image des statistiques sociales des personnes ayant fini le 30DayMapChallenge en remplissant les 30 thèmes quotidiens.  
En reprenant le tiercé précédent dans l'ordre, cela pourrait donner par exemple :

- Le **nombre de likes de chaque tweet** pour l'ensemble des **finishers**
- Représenté par un **graphique en barre**
- Avec la possibilité de connaître **au survol d'autres données** comme, le nombre de likes total du participant ainsi que le nombre de tweets sur le challenge

Ce qui donnerait quelque chose comme ça :

<iframe width="100%" height="600"
    src="https://aurelienchaumet.github.io/data/30daymapchallenge_stats/finisher_stats.html">
</iframe>

[Ou ici en plein écran :smile:](https://aurelienchaumet.github.io/data/30daymapchallenge_stats/finisher_stats.html)

> Cette combinaison n'est qu'un exemple et les données issues de Twint [comme expliqué dans le premier article](https://aurelienchaumet.github.io/articles/30daymapchallenge_stats_fr/), possèdent d'autres données.

### Code Python

La prochaine question, avant de commencer jouer avec Plotly (mais promis ça va très vite arriver !), est : est-ce que mes données répondent aux besoins identifiés plus haut ?

Et la réponse est (comme presqu'à chauqe fois...) NON ! (Enfin pas loin)

#### Création des statistiques par participant

#### Filtrage des finishers

#### Dataviz !!
