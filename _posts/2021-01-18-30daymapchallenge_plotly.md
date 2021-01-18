---
layout: single
permalink: /articles/30daymapchallenge_plotly/
title : "Visualisation des statistiques Twitter du 30 DayMapChallenge 2020 via Plotly" 
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/30dmc_stats.png
  overlay_filter: 0.3
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/30dmc_stats.png
excerpt:
  Affichage de données Twitter via Plotly et rendu HTML

og_image: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/30dmc_stats.png

comments: true
share: true
toc: true
toc_label: "Plan"
toc_icon: "chart-line"
toc_sticky: true
---

Cet article fait partie d'une série de 3 articles expliquant le processus de création derrière celui donnant des statistiques autour du 30DayMapChallenge 2020 que [vous pouvez trouver ici](https://aurelienchaumet.github.io/articles/30daymapchallenge_stats_fr/).
{: .notice--info}

[![twitter twint](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_sortie_import.png){: .align-center}](/articles/30daymapchallenge_scraping_twitter)

[Le premier article](/articles/30daymapchallenge_scraping_twitter) détaille la manière de récupérer les données en masse provenant de Twitter et les préparer grâce à Pandas.

[![twitter plotly](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_plotly.png){: .align-center}](/articles/30daymapchallenge_plotly)

Ce deuxième article traite de la construction du graphique sur les finishers via Plotly.

![twitter bokeh heroku](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_bokeh.png){: .align-center}

Le dernier expliquera comment construire le graphique interactif sur les statistiques générales via Bokeh et déployé sur Heroku.

----

Maintenant que nous avons récupéré et commencé à préparer les données qui nous intéressent, nous allons pouvoir envisager leur visualisation.

## Plotly, une bibliothèque de visualisation polyvalente

Si vous commencez en datavisualisation sur Python, vous allez forcément très vite en venir à vouloir réaliser des représentations interactives et donc mettre de côté (pour ne pas dire, laisser tomber) [Matplotlib](https://matplotlib.org/).  
Bien que cette bibliothèque propose énormément de types de graphiques différents, et qu'elle soit très accessible, vous allez assez rapidement avoir envie de passer votre souris pour faire apparaître un tooltip et avoir des informations sur ce point là en particulier. Ou même vouloir ajouter des filtres, des sélecteurs... Et que sais-je d'autre encore !

![icone plotly](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/plotly.png "Icône Plotly") C'est ici que [Plotly](https://plotly.com/python/) entre en scène !

### Principes de Plotly

Plotly est une bibliothèque très polyvalente, dans le sens où elle est accessible en Python, R ou Julia.

De plus, elle est extrêmement simple à prendre en main, interactive par nature, très bien documentée et la communauté est plutôt active. Que demander de plus ?

Vous trouverez l'ensemble des types de graphiques que Plotly est susceptible de produire à cette adresse : <https://plotly.com/python/>

J'utilise ici le module `plotly.express` qui est une première approche de ce que Plotly peut faire.  
Enormément de choses sont gérés simplement par le module, mais il a tout de même moins de possibilités que le module `plotly.graph_objects`, qui lui, est beaucoup plus complet et maléable.
{: .notice--warning}

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
pip install "notebook>=5.3" "ipywidgets>=7.5"
```

:exclamation: Ou remplacez `pip` par `conda` si vous travaillez avec Anaconda :wink:
{: .notice--success}

Vous pouvez maintenant afficher votre premier graphique via Plotly !

```python
import plotly.graph_objects as go
fig = go.Figure(data=go.Bar(y=[2, 3, 1]))
fig.show()
```

<iframe width="100%" height="400"
    src="/data/30daymapchallenge_coulisses/premier_graphique_plotly.html">
</iframe>

Ca c'était de l'exemple utile ! :smile:

Jusque là tout va bien ? On avance alors !!

## Visualisation des statistiques des finishers

### Objectifs de visualisation

Avant de rentrer dans le vif du sujet, arrêtons-nous une seconde et demandons-nous ce que nous souhaitons voir (et a fortiori montrer) ?

Nous partons ici du postulat que nous avons déjà exploré la donnée et que nous savons ce que nous voulons en faire.  
Dans ce cas-là, la meilleure chose à faire est de rédiger un petit cahier des charges pour soi.

Cela permettra de mettre en exergue :

- Ce que nous voulons montrer
- Comment nous souhaitons l'afficher
- Les fonctionnalités autour du graphique

Dans notre cas précis, nous voulons avoir une image des statistiques sociales des personnes ayant fini le 30DayMapChallenge en remplissant les 30 thèmes quotidiens.  
En reprenant le tiercé précédent dans l'ordre, cela pourrait donner par exemple :

- Le **nombre de likes de chaque tweet** pour l'ensemble des **finishers**
- Représenté par un **graphique en barre**
- Avec la possibilité de connaître **au survol d'autres données** comme, le nombre total de likes du participant ainsi que le nombre de tweets sur le challenge

Ce qui donnerait quelque chose comme ça :

<iframe width="100%" height="600"
    src="/data/30daymapchallenge_stats/finisher_stats.html">
</iframe>

[Ou ici en plein écran :smile:](https://aurelienchaumet.github.io/data/30daymapchallenge_stats/finisher_stats.html)

Cette combinaison n'est qu'un exemple et les données issues de Twint [comme expliqué dans le premier article](https://aurelienchaumet.github.io/articles/30daymapchallenge_scraping_twitter/), possèdent d'autres données.
{: .notice--warning}

### Préparation de la donnée

La prochaine question, avant de commencer à jouer avec Plotly (mais promis ça va très vite arriver !), est : est-ce que mes données répondent aux besoins identifiés plus haut ?

Et la réponse est (comme presqu'à chaque fois...) NON ! (Enfin pas loin ce coup-ci, étant donné qu'on a commencé à préparer le terrain)

#### Création des statistiques par participant

On commence par importer les bibliothèques dont nous allons avoir besoin

```python
import pandas as pd
import plotly.express as px
```

- Pandas va nous servir à travailler nos données
- Plotly à les représenter

Ensuite, il faut lire le fichier :

```python
tweets = pd.read_csv("20.12.02_tweets_ok_with_counts.csv")
```

:exclamation: On le stocke dans `tweets` afin de s'en resservir plus facilement par la suite
{: .notice--success}

Nous avons besoin pour la suite du nombre de tweets et du nombre total de likes par participant.  
On utilise la fonction `groupby` afin de compter (ou de sommer) les colonnes nous intéressant :

```python
# Récupère le nombre de tweets par participant
tweets_count = tweets.groupby('handle').count().reset_index().rename(columns={'tweet_id':'Number of tweets'})[['handle', 'Number of tweets']]

# Récupère le nombre total de likes par participant
tweets_sum = tweets.groupby('handle').sum().reset_index().rename(columns={'likes_count':'Total likes'})[['handle', 'Total likes']]
```

Il faut ensuite remettre ces données aggrégées par participant dans le dataframe de départ (que nous renommerons par la même occasion `tweets_stats`; car il contient maintenant des statistiques...) :

```python
# Fusionne les deux en un dataframe
tweets_sum_count = pd.merge(tweets_count, tweets_sum, left_on = ['handle'], right_on = ['handle'])

# Fusionne le dernier avec le tout premier
tweets_stats = pd.merge(tweets, tweets_sum_count, left_on = ['handle'], right_on = ['handle']).rename(columns={'handle':'Participant', 'likes_count':'Number of likes on this tweet'})
```

La première ligne fusionne les 2 dataframes créés précédemment avec les nouvelles statistiques.  
Alors que la 2ème ligne, fusionne ce dernier avec le dataframe `tweets` de départ. Cette même ligne nous permet également de renommer 2 colonnes (`handle` en `Participant` et `likes_count` en `Number of likes on this tweet`).

Nous avons maintenant une ligne = une participation au challenge, avec le nombre de tweets totaux du participant, ainsi que son nombre de tweets !

#### Filtrage des finishers

Encore un dernier coup de Pandas :panda_face: et on peut aller visualiser la donnée !

Il nous faut maintenant filtrer les finishers.

Voici le code que j'ai utilisé :

```python
# Donne la liste des jours participés par participan
list_day = tweets_stats.groupby(tweets_stats['Participant'])['Day'].apply(list)

# Envoie l'information True ou False sur le fait que les participants ont participé aux 30 jours dans un dataframe
day30 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 20, 30]
list = list_day.apply(lambda x: all([k in x for k in day30]))
list_frame = pd.DataFrame(list).reset_index()

# Récupère l'information des finishers dans le dataframe de statistiques
tweets_finisher = pd.merge(tweets_stats, list_frame, left_on ='Participant', right_on = 'Participant')

# Filtre les finishers et renomme des colonnes
tweets_stats_finisher = tweets_finisher.loc[tweets_finisher['Day_y'] == True].rename(columns={'Day_x':'Jour', 
                                                                                              'Number of tweets': 'Nombre de tweets',
                                                                                              'Number of likes on this tweet': 'Nombre de likes de ce tweet'})
```

Le fait de passer par une liste dans la première partie, évite d'avoir à réaliser une boucle (ce qui est préférable lorsqu'on travaille avec des dataframes).

Sur la dernière partie, on filtre les finishers en utilisant la colonne jointe lors de la fusion précédente, et on en profite pour faire un coup de renommage de colonnes, histoire de passer en français :smile:

### Dataviz

Ca y est, nous y sommes ! Nous allons pouvoir utiliser pour la première fois de cet article la bibliothèque dont il est question !

Comme je le disais en introduction, Plotly est plutôt simple d'utilisation.

#### Première visualisation

Pour commencer, nous pouvons réaliser un graphique en barre, avec les participants en abscisse et le nombre de likes de chaque tweet en ordonnées :

```python
fig = px.bar(tweets_stats_finisher, x='Participant', y='Nombre de likes de ce tweet')

fig.show()
```

<iframe width="100%" height="600"
    src="/data/30daymapchallenge_coulisses/finishers_premier_essai.html">
</iframe>

Comme je vous l'avais dit, c'est assez simple :

- `px.bar` crée un graphique en barre
- on appelle le fichier source `tweets_stats_finisher`
- on indique ce que Plotly doit représenter en x et en y, directement par le nom des colonnes
- et on appelle la visualisation du graphique avec `fig.show()`

Tout fonctionne très bien, mais pour l'instant, ce n'est pas très convaincant visuellement...

#### Ajustement de la couleur, du tri et des infobulles

Pour affiner le graphique, il n'y a qu'à passer des paramètres supplémentaires dans le `px.bar()` !

Premièrement, ajoutons un peu de couleur grâce à... `color` !!  
En indiquant le champ sur lequel doit se baser la couleur, Plotly sort une rampe de couleurs automatiquement.

```python
fig = px.bar(tweets_stats_finisher, 
            x='Participant', 
            y='Nombre de likes de ce tweet',
            color='Participant')

fig.show()
```

<iframe width="100%" height="600"
    src="/data/30daymapchallenge_coulisses/finishers_couleur.html">
</iframe>

Autre étape, la donnée doit être présentée du plus grand nombre de tweets totaux au plus faible.

Il n'y a qu'à demander poliment (toujours).  
Plutôt que de passer le dataframe `tweets_stats_finisher` tel quel, trions le :

```python
fig = px.bar(tweets_stats_finisher.sort_values(by=['Total likes','Jour'], ascending=False), 
            x='Participant', 
            y='Nombre de likes de ce tweet',
            color='Participant')

fig.show()
```

Ici le tri est effectué directement sur 2 champs :

- `Total likes` pour le tri évoqué plus haut.  
- `Jour` permet de trier les barres empilées pour chaque participant : le premier tweet aura ses statistiques en haut de la barre et le dernier tout en bas.

<iframe width="100%" height="600"
    src="/data/30daymapchallenge_coulisses/finishers_tri.html">
</iframe>

J'ai déjà dit que Plotly était interactif par nature, dans le sens où (si vous ne l'avez pas encore remarqué sur les précédents graphiques), lorsque vous passez votre souris sur un élément, une infobulle s'affiche.

Ce qui est bien, mais pas top ! Car nous n'avons pas exactement les informations souhaitées mais uniquement celles affichées en x et y.

```python
fig = px.bar(tweets_stats_finisher.sort_values(by=['Total likes','Jour'], ascending=False), x='Participant', y='Nombre de likes de ce tweet',
             hover_data=['Total likes', 'Nombre de tweets', 'Jour', 'Nombre de likes de ce tweet'],
             color='Participant')

fig.show()
```

Encore une fois, c'est très simple !  
Il suffit d'ajouter le paramètre `hover_data =` suivi des champs qui nous intéressent.

Et voilà donc le résultat final :

<iframe width="100%" height="600"
    src="/data/30daymapchallenge_coulisses/finisher_hover.html">
</iframe>

#### Export en html

Afin de pouvoir afficher dynamiquement ces différents graphiques, j'ai choisi comme option de les exporter en format HTML.  
Et Plotly a une fonction pour ça !

Il suffit d'indiquer

```python
fig.write_html("NOM_DU_FICHIER.html")
```

en fin de script, et il se charge de tout !

## Conclusions

Nous venons de voir que Plotly est plutôt simple pour une première approche de la visualisation de données sous Python, en créant un graphique, aggrémenté de quelques paramètres.

Dans le dernier article de cette série, sera traité la création d'un graphique avec [Bokeh](https://bokeh.org/).  
J'avais décidé à l'époque de tester une autre bibliothèque, qui me permettrait d'intégrer des fonctions de filtre et de sélection.  
_Ce que Plotly sait faire grâce à [Dash](https://plotly.com/dash/), mais ça c'est une toute autre histoire :smile:_

----

N'hésitez pas à commenter directement en dessous, ou à m'envoyer un [message sur Twitter](https://twitter.com/messages/compose?recipient_id=938055192221765634), je vous répondrai avec plaisir :pray: !
