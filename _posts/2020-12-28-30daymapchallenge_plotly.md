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

### Principes de Plotly et installation

Plotly est une bibliothèque très polyvalente, dans le sens où elle est accessible en Python, R ou Julia.

De plus, elle est extrêmement simple à prendre en main, interactive par nature, très bien documentée et la communauté est plutôt active. Que demander de plus ?

Côté installation, comme souvent, rien de bien complexe :

- Via Pip

  ```python
  pip install plotly==4.14.3
  ```

- Via Conda

  ```python
  conda install -c plotly plotly==4.14.3
  ```

Si vous souhaitez l'utiliser dans un [Jupyter Notebook](https://jupyter.org/), pensez également à installer `notebook` et `ipywidget` :

```python
pip install "notebook>=5.3" "ipywidgets>=7.5
```

>Ou remplacez `pip` par `conda` si vous travaillez avec conda :wink:

Jusque là tout va bien ? On avance alors !!

### 
