---
layout: single
permalink: /articles/30daymapchallenge_scraping_twitter/  
title : "Scraping de données Twitter via Twint et préparation des données via Pandas" 
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_sortie_import.png
  overlay_filter: 0.3
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_sortie_import.png
excerpt:
  Comment récupérer des données de Twitter via Twint et les préparer via Pandas - Exemple des données du 30DayMapChallenge

og_image: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_sortie_import.png

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

Ce premier article détaille la manière de récupérer les données en masse provenant de Twitter et les préparer grâce à Pandas.

[![twitter plotly](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_plotly.png){: .align-center}](/articles/30daymapchallenge_plotly)

[Le deuxième](/articles/30daymapchallenge_plotly) traite de la construction du graphique sur les finishers via Plotly.

![twitter bokeh heroku](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_bokeh.png){: .align-center}

Le dernier expliquera comment construire le graphique interactif sur les statistiques générales via Bokeh et déployé sur Heroku.

----

L'un des évènements sociaux marquants de la fin d'année 2020 reste pour bon nombre de cartographes le [30DayMapChallenge](https://github.com/tjukanovt/30DayMapChallenge).  
Le concept où chacun peut réaliser des cartes l'intéressant, de la manière dont il le souhaite et partage tout ça auprès d'un public averti, tout en se confrontant à d'autres réalisations, sur des thèmes imposés est vraiment intéressant.

Ce challenge totalement non officiel reste un moment unique de partage cartographique à travers le monde et [la collection réalisée par David Friggens](https://david.frigge.nz/30DayMapChallenge2020/maps.html) en est un exemple implacable.

Toutes ces cartes sont un matériel vraiment très intéressant d'étude concernant la cartographie, et c'est pourquoi j'ai essayé d'en [ressortir quelques statistiques dans un précédent article](https://aurelienchaumet.github.io/articles/30daymapchallenge_stats_fr/), principalement du point de vue social du challenge.

![article statistiques 30daymapchallenge](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/article_stats_30dmc.png "Article statistiques 30DayMapChallenge"){: .align-center}

J'ai pour cela utilisé (et appris à m'en servir par la même occasion) un certain nombre d'outils en Python :

- Twint pour récupérer les données
- Plotly pour [visualiser les statistiques des finishers](https://aurelienchaumet.github.io/articles/30daymapchallenge_stats_fr/#finishers)
- Bokeh pour [visualiser les statistiques de l'ensemble des participants](https://aurelienchaumet.github.io/articles/30daymapchallenge_stats_fr/#statistiques-g%C3%A9n%C3%A9rales)

Comme dit précédemment, ce premier article traitera de la manière de récupérer les données intéressantes venant de Twitter, grâce à Twint, ainsi que d'une première préparation de la donnée.

## Scraping de Twitter

David Friggens a vraiment réalisé un travail spectaculaire de collecte des différents tweets afférant au 30DayMapChallenge. Mais très honnêtement, même si le travail de récupération se fait automatiquement, la classification en fonction des jours (et donc des thèmes) est assez fastidieux pour une seule personne.  
J'ai donc apporté ma pierre à l'édifice en scrapant également ces données de mon côté, en les confrontant à celles de David, puis en lui renvoyant ce qui m'apparaissait commem manquant de son côté.

Wait... Scrap what ??

### Définition du webscraping

Je m'arrête rapidement sur [la définition du scraping](https://fr.wikipedia.org/wiki/Web_scraping), qui ne consiste en aucun cas à gratter frénétiquement des tickets issus de la FDJ. C'est en réalité un processus qui permet de collecter des données se situant sur internet.  
Cela évite d'avoir des copier-coller longs et fortement fastidieux à réaliser à la main.

Un robot (il faut le voir non pas comme Nono ce gentil robot, mais plutôt comme un algorithme) est configuré pour récupérer les données qui nous intéressent, à l'endroit où cela nous sied, et les remet dans un format qui nous est approprié, à l'endroit où on le souhaite. C'est beau dit comme ça...

Ce robot va ici être construit en Python.

### Twint ou comment récupérer facilement des données de Twitter

Il est possible de récupérer les données de Twitter via Tweepy, une bibliothèque Python.  
Ses principales limites sont que vous ne pourrez récupérer que les 3 200 premiers tweets d'une timeline, couplé à un nombre limité toutes les 15 minutes.

Mais il y a mieux ! Une autre bibliothèque s'appelant [Twint](https://github.com/twintproject/twint) existe et s'affranchit de ces limitations (car elle ne fait pas appel à l'API de Twitter).  

#### Installation de Twint

L'installation est ultra simple, il suffit de taper dans un terminal de commande :

```python
pip3 install twint
```

Et logiquement, c'est réglé !

>Si vous souhaitez avoir d'autres manières de l'installer, vous les trouverez dans [le wiki de Twint](https://github.com/twintproject/twint/wiki/Setup).

#### Utilisation générique de Twint

Il y a ensuite 2 manières de s'en servir :

- Pour les cas d'usage les plus simples, vous pouvez passer par une commande CLI

  ```python
  twint -u username
  ```

  Par exemple, récupèrera l'ensemble des tweets de `username`.

  ```python
  twint -s pineapple
  ```

  Ce deuxième exemple ramènera l'ensemble des tweets contenant `pineapple`.

- Pour les cas un peu plus poussés, il faudra passer par l'usage du Module

  ```python
  import twint

  # Configure
  c = twint.Config()
  c.Username = "realDonaldTrump"
  c.Search = "great"

  # Run
  twint.run.Search(c)
  ```

  Ici, vous récupèrerez l'ensemble des tweets de Donald Trump contenant `great`.  
  _L'exemple cité provient de la documentation de Twint et ne réflète en aucun cas un quelconque intérêt pour le fond_

L'avantage de cette deuxième méthode réside dans le fait de povuoir utiliser des fonctions pythoniques, et vous pourrez ainsi vous en servir dans un script plus élaboré.

Dans les deux cas, des options existent pour enregistrer le résultat de la recherche directement en csv.

Vous trouverez plus d'informations sur [les fonctions utilisables ici](https://github.com/twintproject/twint/wiki/Configuration), ainsi que [plusieurs exemples ici](https://github.com/twintproject/twint/wiki/Scraping-functions).

#### Utilisation de Twint pour récupérer les tweets du 30DayMapChallenge

À la base, ce qui nous intéresse plus particulièrement est la possibilité de récupérer les tweets publiés pour le 30DayMapChallenge.  
Il suffit de demander (toujours) gentiment à Twint de nous ramener les tweets contenant `30daymapchallenge`.  
Pour cela, j'ai utilisé la deuxième méthode.  
Même si dans ce cas précis la recherche n'a rien de complexe, je souhaitais comprendre comment m'en servir.

>Pour les curieux, je pense qu'il aurait suffi de quelque chose comme ça avec la première méthode:
>
>```python
>twint -s 30daymapchallenge --since "2020-09-01 00:00:00" -o file.csv --csv
>```
>
>`--since` permet de spécifier une date de départ du scrap, pour être sûr de ne pas récupérer les tweets du challenge 2019.  
>`-o file.csv --csv` permet de spécifier le nom du fichier de sorti (ainsi que son emplacement), et le format dans lequel le fichier est souhaité.

Le code que j'ai utilisé est donc le suivant :

```python
import nest_asyncio
nest_asyncio.apply()

import twint

# Configure
c = twint.Config()
c.Search = "30daymapchallenge"
c.Store_csv = True
c.Since = "2020-10-01"
c.Until = "2020-12-02"
c.Output = "2020-12-02.tweets.csv"

# Run
twint.run.Search(c)
```

Cela mérite quelques explications :

- J'ai réalisé ce scrape via un notebook Jupyter, et il était indispensable d'ajouter la commande `nest_asyncio.apply()` pour que le notebook ne plante pas
- On crée un objet `c` qui permet de paramétrer ce que nous allons demander à Twint
- Puis on définit ces paramètres (dans l'ordre d'apparition au générique) :
  - on cherche les tweets contenant 30daymapchallenge
  - on veut les stocker en csv
  - à partir du 1er octobre 2020
  - jusqu'au 2 décembre 2020 (pour l'exemple d'utilisation du c.Until)
  - on le stocke dans un fichier qui s'appelle `2020-12-02.tweets.csv`
  - et on lui demande ~~d'aller faire un tour en courant~~ de récupérer les données !

Rien de très compliqué ici, mais job done (Comme disent les américains) !

Ce qui est pratique avec Twint, c'est qu'il renvoie pas mal d'informations sur chaque tweet, comme par exemple :

- l'identifiant du tweet
- la date du post
- le nom de la personne l'ayant posté
- le contenu du tweet
- le nombre de likes, retweets et échanges du tweet
- les hashtags inclus dans le tweet

Cette liste n'est pas exhaustive, mais elle contient les éléments qui nous intéresseront par la suite.

Cela peut ressembler à ça :

![sortie tweets twint](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats_coulisses/tweets_sortie_twint.png "Un exemple de sortie après récupération par Twint"){: .align-center}

## Pandas à la rescousse de la préparation de la donnée

Si vous avez déjà travaillé en Python avec des données, j'imagine que vous avez utilisé [la bibliothèque Pandas](https://pandas.pydata.org/). Elle est très utile pour préparer et analyser des données.  
Et dans notre cas, nous en avons besoin pour affiner le fichier que Twint nous a sorti.

### Installation de Pandas

Rien de très compliqué encore une fois pour l'installer :

```python
pip install pandas
```

>Vous trouverez [plus d'informations ici](https://pandas.pydata.org/pandas-docs/stable/getting_started/install.html) en fonction de votre configuration.

### Création d'une nouvelle colonne `day`

Nous allons avoir besoin d'automatiser au maximum le remplissage de la catégorie **Day**.  
En effet, pour les analyses ultèrieures, il va être intéressant de catégoriser les participations en fonction des thèmes quotidiens.  
Les participants mettent en grande partie quelque chose du genre `Day1` ou `Day01`.

> :exclamation: Je tiens à dire que ce n'est pas le bout de code pour lequel je suis le plus fier, car il n'apparait clairement pas comme étant optimisé, mais je n'ai rien trouvé de mieux pour l'instant et il fonctionne.  
Attention les yeux !

```python
import pandas as pd

tweets = pd.read_csv("2020-12-02.tweets.csv")

tweets.loc[tweets['tweet'].str.contains('Day1', case = False) | tweets['tweet'].str.contains('Day 1', case = False) | tweets['tweet'].str.contains('Day01', case = False) | tweets['tweet'].str.contains('Day 01', case = False),'day'] = '1'  
tweets.loc[tweets['tweet'].str.contains('Day2', case = False) | tweets['tweet'].str.contains('Day 2', case = False) | tweets['tweet'].str.contains('Day02', case = False) | tweets['tweet'].str.contains('Day 02', case = False),'day'] = '2'  
tweets.loc[tweets['tweet'].str.contains('Day3', case = False) | tweets['tweet'].str.contains('Day 3', case = False) | tweets['tweet'].str.contains('Day03', case = False) | tweets['tweet'].str.contains('Day 03', case = False),'day'] = '3'  
tweets.loc[tweets['tweet'].str.contains('Day4', case = False) | tweets['tweet'].str.contains('Day 4', case = False) | tweets['tweet'].str.contains('Day04', case = False) | tweets['tweet'].str.contains('Day 04', case = False),'day'] = '4'  
tweets.loc[tweets['tweet'].str.contains('Day5', case = False) | tweets['tweet'].str.contains('Day 5', case = False) | tweets['tweet'].str.contains('Day05', case = False) | tweets['tweet'].str.contains('Day 05', case = False),'day'] = '5'  
tweets.loc[tweets['tweet'].str.contains('Day6', case = False) | tweets['tweet'].str.contains('Day 6', case = False) | tweets['tweet'].str.contains('Day06', case = False) | tweets['tweet'].str.contains('Day 06', case = False),'day'] = '6'  
tweets.loc[tweets['tweet'].str.contains('Day7', case = False) | tweets['tweet'].str.contains('Day 7', case = False) | tweets['tweet'].str.contains('Day07', case = False) | tweets['tweet'].str.contains('Day 07', case = False),'day'] = '7'  
tweets.loc[tweets['tweet'].str.contains('Day8', case = False) | tweets['tweet'].str.contains('Day 8', case = False) | tweets['tweet'].str.contains('Day08', case = False) | tweets['tweet'].str.contains('Day 08', case = False),'day'] = '8'  
tweets.loc[tweets['tweet'].str.contains('Day9', case = False) | tweets['tweet'].str.contains('Day 9', case = False) | tweets['tweet'].str.contains('Day09', case = False) | tweets['tweet'].str.contains('Day 08', case = False),'day'] = '9'  
tweets.loc[tweets['tweet'].str.contains('Day10', case = False) | tweets['tweet'].str.contains('Day 10', case = False),'day'] = '10'  
tweets.loc[tweets['tweet'].str.contains('Day11', case = False) | tweets['tweet'].str.contains('Day 11', case = False),'day'] = '11'  
tweets.loc[tweets['tweet'].str.contains('Day12', case = False) | tweets['tweet'].str.contains('Day 12', case = False),'day'] = '12'  
tweets.loc[tweets['tweet'].str.contains('Day13', case = False) | tweets['tweet'].str.contains('Day 13', case = False),'day'] = '13'  
tweets.loc[tweets['tweet'].str.contains('Day14', case = False) | tweets['tweet'].str.contains('Day 14', case = False),'day'] = '14'  
tweets.loc[tweets['tweet'].str.contains('Day15', case = False) | tweets['tweet'].str.contains('Day 15', case = False),'day'] = '15'  
tweets.loc[tweets['tweet'].str.contains('Day16', case = False) | tweets['tweet'].str.contains('Day 16', case = False),'day'] = '16'  
tweets.loc[tweets['tweet'].str.contains('Day17', case = False) | tweets['tweet'].str.contains('Day 17', case = False),'day'] = '17'  
tweets.loc[tweets['tweet'].str.contains('Day18', case = False) | tweets['tweet'].str.contains('Day 18', case = False),'day'] = '18'  
tweets.loc[tweets['tweet'].str.contains('Day19', case = False) | tweets['tweet'].str.contains('Day 19', case = False),'day'] = '19'
tweets.loc[tweets['tweet'].str.contains('Day20', case = False) | tweets['tweet'].str.contains('Day 20', case = False),'day'] = '20'
tweets.loc[tweets['tweet'].str.contains('Day21', case = False) | tweets['tweet'].str.contains('Day 21', case = False),'day'] = '21'
tweets.loc[tweets['tweet'].str.contains('Day22', case = False) | tweets['tweet'].str.contains('Day 22', case = False),'day'] = '22'
tweets.loc[tweets['tweet'].str.contains('Day23', case = False) | tweets['tweet'].str.contains('Day 23', case = False),'day'] = '23'
tweets.loc[tweets['tweet'].str.contains('Day24', case = False) | tweets['tweet'].str.contains('Day 24', case = False),'day'] = '24'
tweets.loc[tweets['tweet'].str.contains('Day25', case = False) | tweets['tweet'].str.contains('Day 25', case = False),'day'] = '25'
tweets.loc[tweets['tweet'].str.contains('Day26', case = False) | tweets['tweet'].str.contains('Day 26', case = False),'day'] = '26'
tweets.loc[tweets['tweet'].str.contains('Day27', case = False) | tweets['tweet'].str.contains('Day 27', case = False),'day'] = '27'
tweets.loc[tweets['tweet'].str.contains('Day28', case = False) | tweets['tweet'].str.contains('Day 28', case = False),'day'] = '28'
tweets.loc[tweets['tweet'].str.contains('Day29', case = False) | tweets['tweet'].str.contains('Day 29', case = False),'day'] = '29'
tweets.loc[tweets['tweet'].str.contains('Day30', case = False) | tweets['tweet'].str.contains('Day 30', case = False),'day'] = '30'
```

Oui c'est très moche... Mais efficace :smile: !  

- La première ligne permet d'importer la bibliothèque pandas en tant que `pd`.  
- La deuxième déclare le csv créé via Twint sous le nom de `tweets` afin de pouvoir s'en resservir ensuite.  
- Le reste permet de peupler une nouvelle colonne `day` en fonction de ce qu'il peut y avoir dans le champ `tweet`  
S'il voit `Day1`, `Day 1`, `Day01` ou `Day 01`, le champ `day` sera peuplé de `1`, et ainsi de suite...  
L'idéal serait de le faire également pour d'autres langues afin de maximiser l'automatisation.

Une fois cela effectué, il y a encore un gros travail de vérification à réaliser à la main pour les tweets dont le champ `day` n'aura pas été peuplé.  
Travail fort fastidieux, mais indispensable pour récupérer un maximum de participations !

Prochain article à paraître très bientôt pour la visualisation sous Plotly !
