---
published: true
title: "Assemblage de couches"
excerpt: "Application des concepts sur L couches"
toc: true
toc_sticky: true
toc_label: "Multi-layer neural nets"
toc_icon: "microchip"
comments: true
author_profile: false
header:
  overlay_image: "assets/images/covers/cover6.png"
  teaser: "assets/images/covers/cover6.png"
categories: [deep-learning]
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

Jusqu'à maintenant, on a vu la forward & bckward propagation des réseaux de neurones, avec la regression logistique, et avec une couche cachée. On a aussi vu la vectorisation et l'initialisation aléatoire des poids.

# Réseaux profonds

## Ajout de couches

On a vu le modèle de la regression logistique, qui peut être vu comme un réseau de profondeur 1. Avec une couche cachée, on a un réseau de profondeur 2. Ainsi de suite.

Les récentes avancées dans le domaine des réseaux de neurones ont montré que l'on pouvait modéliser des **problèmes de plus en plus complexes** grâce à des réseaux de plus en plus **profonds**. Dans la conception des réseaux, on complexifie progressivement notre réseau, en surveillant les améliorations apportées.

## Notations

Considérons un réseau de profondeur 4 :

![image-center](https://www.cs.swarthmore.edu/~bryce/cs63/s18/labs/nn.png){: .align-center}

- $L=4$ : le nombre de couches (sans *input layer*)
- $n^{[l]}$ : le nombre d'unités dans la couche $l$
- Pour chaque couche $l$ on note $a^{[l]}=g^{[l]}(z^{[l]})$ les activations.
- $w^{[l]}$ et $b^{[l]}$ les poids et biais pour calculer $z^{[l]}$.
- La prédiction $\hat y = a^{[L]}$ qui est l'activation de la dernière couche du réseau.

# Forward propagation

Considérons un réseau de profondeur 4 :

![image-center](https://www.cs.swarthmore.edu/~bryce/cs63/s18/labs/nn.png){: .align-center}

## Propagation d'un exemple d'entrainement

Pour la première couche du réseau, on propage le premier exemple d'entrainement :

$$a^{[1]} = g(w^{[1]}.x+b^{[1]})$$

Pour la seconde couche :

$$z^{[2]} = w^{[2]}.a^{[1]}+b^{[2]}$$

$$a^{[2]} = g^{[2]}(z^{[2]})

On voit que l'on **propage les éléments d'activation** de la première couche, lors du calcul des activations de la seconde couche, et ainsi de suite jusqu'à l'estimation de $\hat y$ :

$$\hat y = g^{[4]}(w^{[4]}.a^{[3]}+b^{[4]})$$

## Propagation vectorisée

Avec la vectorisation, on propage tout les exemples d'entrainement à la fois. 
- X est $A^{[0]}$ : les exemples d'entrainements regroupés en colonnes.
- Z est la matrice calculée pour chaque couche.

$$Z^{[1]} = w^{[1]}.X+b^{[1]} = w^{[1]}.A^{[0]}+b^{[1]}$$

$$A^{[1]} = g^{[1]}(Z^{[1]})$$

Ici le calcul de chaque couche est iteratif, il y a une boucle For sur l'ensemble des couches.

# Sources

- [Coursera - Deep Learning](www.coursera.org/learn/neural-networks-deep-learning)
