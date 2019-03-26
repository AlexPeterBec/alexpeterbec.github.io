---
published: true
title: "Premières étapes de conception"
excerpt: "Itération, Regularisation, Normalisation"
toc: true
toc_sticky: true
toc_label: "First steps"
toc_icon: "microchip"
comments: true
author_profile: false
header:
  overlay_image: "assets/images/covers/cover6.png"
  teaser: "assets/images/covers/cover6.png"
categories: [deep-learning]
---
# Approche de conception

## Démarche itérative

La conception de réseaux de neurones est un processus iteratif. Comme il n'y a pas de valeur prédéfinie pour chaque type de problème, il faut expérimenter et tirer des conclusions. A chaque itération, on peut être amené à repenser :

- Le nombre de couches du réseau
- Le nombre de neurones par couche, leur fonctions d'activation
- Le pas d'apprentissage

## Train-test split

Avant toute chose, il est important de **séparer les données** en ensemble d'entrainement, de validation, et de test.

Il faut également s'assurer que les données utilisées ont des distributions cohérentes. Il faut par exemple entrainer et tester le réseau sur le même type d'images

*Exemple : Si on souhaite utiliser du deep learning dans une application mobile, où les utilisateurs fournissent leur propres images, et que l'on entraine le réseau sur des images parfaitement cadrées et professionnelles. On se doute que les performances dans l'application n'auront rien à voir car les utilisateurs donneront au réseau des imgaes de mauvaises qualité, pas forcément bien cadrées.*

Ces notions sont abordées plus en détail dans [cet article](https://alexpeterbec.github.io/metrics/scoring/algorithm-scoring/#split--train-validation-test).

## Compromis biais-variance

Le biais et la variance sont deux caractéristiques qui dégradent les performances du réseau. On cherche à les minimiser.

Au final, on veut que notre algorithme ait une bonne performance sur des données qu'il n'a jamais vu. Et on veut également que ces performances soient stables sur un ensemble de cas d'usages, on veut que le réseau puisse "généraliser".

Ces notions sont abordées plus en détail dans [cet article](https://alexpeterbec.github.io/metrics/scoring/algorithm-scoring/#dilemme-biais-variance).

## Schematisation de la démarche

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/nn1/nn-iter.png){: .align-center}

# Régularisation du modèle

L1, L2, DropOut

# Premiers traitements : 

- Normalisation
- explosion du gradient
- Initialisation des poids

# Sources

- [Coursera - Deep Learning](www.coursera.org/learn/neural-networks-deep-learning)
