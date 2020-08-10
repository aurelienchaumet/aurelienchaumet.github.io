---
layout: archive
---
# (Geo)Data Science avec Python — Le parcours du débutant
## *Pourquoi et comment un géomaticien cherche à programmer en Python*

Cela fait maintenant 3 mois que je me suis mis en tête d’apprendre à coder en Python. Pas uniquement pour le plaisir (même si j’adore apprendre à utiliser de nouveaux outils 🤓), mais pour utiliser Python en lien avec des sujets d’intérêt personnel et professionnel que sont le traitement de données, la datavisualisation et la géomatique.

Mon métier est d’accompagner des collectivités locales à exprimer leurs besoins thématiques (foncier, urbanisme, déchets, espaces naturels…) et tenter de trouver une manière d’y répondre grâce à l’utilisation de données. Le process classique, une fois la remontée de besoins effectuée, est de trouver les données nécessaires, la manière de les nettoyer, de les mettre en forme, de les visualiser et de les remettre à disposition.

J’utilise principalement des logiciels propriétaires (FME, Tableau, GEO Software…) pour effectuer ces différentes tâches (hormis QGIS qui est libre 🤟), et la question de la reproductibilité peut se poser.

De plus, ces logiciels peuvent offrir une certaine souplesse dans leur paramétrage, mais parfois, je me retrouve bloqué face à une incompréhension dans la manière dont un logiciel effectue une tâche particulière.

Ce sont ces raisons qui m’ont poussées à m’intéresser à Python, car il est possible de faire énormément de choses grâce à ce langage de programmation.

## Intérêts

### Mais quel rapport entre un sympathique reptile et les données ?

Python est un langage de programmation, notamment utilisé dans le domaine de l’analyse et la visualisation de données, géographiques ou plates.

Pour un historique rapide, je vous conseille la lecture de cet article.
http://leaderswithouttitle.github.io/PythonLWT/History.html

Sa popularité continue de grandir auprès de la communauté des data scientist car il possède énormément de librairies dédiées au cycle de vie des données, comme NumPy (fonctions mathématiques et statistiques), Pandas (traitement des données), Geopandas (le pendant géographique de Pandas) ou encore Plotly et Bokeh (visualisation).

### Pourquoi écrire des articles sur Python

Après avoir lu **[cet article](https://towardsdatascience.com/7-reasons-you-should-blog-during-your-data-science-journey-4f542b05dab1)** rédigé par **[John DeJesus](https://medium.com/@j.dejesus22)**, je me suis dit qu’il était sans doute temps que je relate les (quelques) connaissances et compétences, que j’ai pu commencer à glaner lors de mon apprentissage de Python pour les data sciences.

A la fois pour partager différentes sources d’information, mais également pour infirmer le fait que j’avais bien réussi à intégrer tout cela, et que je suis donc en capacité de les utiliser dorénavant.

Je ne prétends pas être un expert Python, bien au contraire ! Il me faudra plusieurs années pour maîtriser les différents aspects et techniques nécessaires à ce vaste domaine qu’est Python appliqué à la data science.

**Je souhaite en revanche montrer qu’il est possible de se former seul, à distance et à bas coût sur ce champ de compétences.**

Mon objectif a travers ces articles est de me pousser à continuer à faire des progrès sur Python, mais également de m’améliorer dans la manière de partager des informations.

J’ai souhaité rédiger ces articles en français car j’ai rencontré beaucoup de littérature anglophone, ce qui peut apparaître complexe de prime abord (en plus d’apprendre un langage de programmation).

*Un exemple de réalisation programmée en python :*
![Anomalies dans les températures mondiales, mars 2016. Source: https://www.ncdc.noaa.gov/sotc/global/201603](/assets/images/geodatascience-avec-python/exemple1.gif)

### Avantages
#### Un apprentissage simple
J’ai beaucoup lu que Python était relativement simple à apprendre et c’est vrai. Évidemment, cela demande tout de même du temps et des efforts. Je ressens également qu’il est impératif d’avoir des objectifs clairs afin de garder la motivation présente pour continuer.

Si vous vous lancez dans cette aventure, partez des le départ avec un projet en tête. Même s’il est personnel et qu’il n’a pas de finalités professionnelles directes. Cela aide à avancer dans les concepts et surtout dans les librairies Python disponibles (il y en a des tonnes et sont adaptées à chaque besoin).  
Pour cela, il m’arrive parfois d’aller sur data.gouv.fr et de choisir un jeu de données qui m’est inconnu, sur une thématique qui m’intéresse. J’y trouve plusieurs avantages :

- Cela me permet de creuser une thématique que j’apprécie (foncier, occupation du sol, déchets, transports… Il y a beaucoup de thématiques différentes, vous y trouverez forcément une qui vous intéressera 😊)

- J’essaye de tout faire avec Python : lecture des données, nettoyage, explorations, croisements avec d’autres données, visualisations… Cela me force à me former et me renseigner sur la manière de faire ce que je souhaite. Sans passer sur un autre outil avec lequel je saurai réaliser toutes ces phases d’exploration et de visualisation des données

#### Concentration sur les objectifs finaux
Étant donné que coder en Python est (pour moi 😁) moins intuitif que l’utilisation de logiciels plus packagés comme FME pour le nettoyage et la préparation des données, ou encore Tableau pour la visualisation des donnés, cela m’a permis de définir des objectifs clairs sur ce que je souhaite faire des données.

Les logiciels cités plus haut permettent (quand on les maîtrise) d’aller plus vite sur la manière de faire certaines tâches (vérification visuelle de la cohérence de la donnée, jointure de données…), mais ont tendance à m’amener sur des résultats dont je n’ai pas fondamentalement besoin.
Coder peut, tout du moins au départ, être un peu chronophage et cela m’impose donc de savoir exactement ce que je veux faire, étape par étape, et rend donc le procès de feature engineering plus clair, concis et surtout (🔥spoiler du point suivant !) transparent.

#### Eviter l’effet boîte noire
Les logiciels qui permettent de faire les mêmes tâches que Python, peuvent souvent être des boîtes noires. Même si un ETL (Extract, Transform and Load) comme FME possède énormément de paramètres pour chaque transformer, cela n’en reste pas moins opaque dans son fonctionnement. Si vous souhaitez créer une fonction de A à Z en Python, c’est possible !

Et même en utilisant les librairies existantes sur Python (qui sont en réalité des morceaux de code python déjà préparés et empaquetés), la communauté et la documentation est telle, qu’il n’est pas si complexe de connaître leur fonctionnement.

#### Python est un des langages les plus utilisés et demandés
Sur Stackoverflow (une des plus grandes communautés de développeurs), presque 1 500 000 questions posées traitent de Python. D’après l’enquête menée par le site internet en 2019 auprès de la communauté, Python est, pour la 3ème année consécutive, le langage que les développeurs ne le connaissant pas souhaitent apprendre le plus. Il est également le 2ème langage le plus apprécié par ceux le pratiquant (source en anglais). Il est également considéré comme le langage connaissant la plus grosse progression dans son utilisation.

Il existe sur Github (site de référence permettant le partage de code, s’appuyant sur la gestion de version collaborative) pas loin de 1 million de répertoires référencés en lien avec Python.

Pour finir, David Antzelevich, un étudiant du bootcamp data science de Thinkful.com, a étudié 7 000 offres d’emploi sur le marche de la data science. Python est le langage ressortant le plus fréquemment (source en anglais)
