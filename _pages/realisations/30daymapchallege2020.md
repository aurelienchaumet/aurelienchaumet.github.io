---
layout: single
permalink: /realisations/30daymapchallenge/  
title : "30 DayMapChallenge 2020"   
header:
  overlay_image: /assets/images/30daymapchallenge/map_challenge_themes_2020_ac.jpg
  overlay_filter: 0.3
excerpt:
  Cartes réalisées pour le 30DayMapChallenge 2020

toc: true
toc_label: "Participations"
toc_icon: "globe"

gallery:
  - url: "/assets/images/30daymapchallenge/day1_pop_city_17.png"
    image_path: "/assets/images/30daymapchallenge/day1_pop_city_17.png"
    alt: "points charente maritime commune"
    title: "Population de la Charente-Maritime répartie à la commune"
  - url: "/assets/images/30daymapchallenge/day1_pop_square_17.png"
    image_path: "/assets/images/30daymapchallenge/day1_pop_square_17.png"
    alt: "points charente maritime grid"
    title: "Population de la Charente-Maritime répartie sur une grille de 200m de coté"
  - url: "/assets/images/30daymapchallenge/day1_pop_building_17.png"
    image_path: "/assets/images/30daymapchallenge/day1_pop_building_17.png"
    alt: "points charente maritime bati"
    title: "Population de la Charente-Maritime répartie aléatoirement dans les bâtiments"

gallery1bis:
  - url: "/assets/images/30daymapchallenge/day1_pop_city_lr.png"
    image_path: "/assets/images/30daymapchallenge/day1_pop_city_lr.png"
    alt: "points la rochelle commune"
    title: "Population de la Rochelle répartie à la commune"
  - url: "/assets/images/30daymapchallenge/day1_pop_square_lr.png"
    image_path: "/assets/images/30daymapchallenge/day1_pop_square_lr.png"
    alt: "points la rochelle grid"
    title: "Population de la Rochelle répartie sur une grille de 200m de coté"
  - url: "/assets/images/30daymapchallenge/day1_pop_building_lr.png"
    image_path: "/assets/images/30daymapchallenge/day1_pop_building_lr.png"
    alt: "points la rochelle bati"
    title: "Population de la Rochelle répartie aléatoirement dans les bâtiments"
---

## Jour 1 - Points

{% include gallery class="full" %}

Les données viennent du jeu de données de 2015 [Données carroyées - Carreau de 200m](https://www.insee.fr/fr/statistiques/4176290?sommaire=4176305), issu du recensement de la population de l'INSEE.

La première carte place aléatoirement 1 point = 1 habitant à l'échelle de la commune.

La deuxième précise le trait en utilisant la grille de 200m de côté fournie par l'INSEE.

La dernière est une tentative de représentation à l'échelle [des bâtiments de la couche PCI Vecteur de la DGFIP.](https://cadastre.data.gouv.fr/datasets/plan-cadastral-informatise) Le principe est de placer (toujours aléatoirement) 1 point = 1 habitant, mais en combinant la grille de 200m de côté et les bâtiments. Le nombre d'habitants recensés dans chaque grille est rebasculé dans le (ou les) bâtiment(s) se situant dans cette même grille.

{% include gallery id="gallery1bis" class="full" %}
