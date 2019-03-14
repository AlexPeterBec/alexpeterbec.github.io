---
published: true
title: "Assemblage de neurones"
excerpt: "Notions globales, représentations"
toc: true
toc_sticky: true
toc_label: "Réseaux de neurones"
toc_icon: "ruler-combined"
comments: true
author_profile: false
header:
  overlay_image: "assets/images/tensorflow/cover.jpg"
  teaser: "assets/images/tensorflow/cover.jpg"
categories: [neural, nets]
---
<script type="text/javascript" async
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

# Vue globale des réseaux de neurones

On a vu dans les articles de la première partie, l'exemple de la regression logistique, composé d'un seul élément appelé neurone, qui effectue :
- La multiplication matricielle des poids, et somme avec le terme de biais b.
- Le passage dans une fonction d'activation sigma.

On va maintenant passer à une représentation plus "profonde" et considérer des couches successives de neurones. Chaque rond sur le schema est un neurone effectuant les opérations vues ci-dessus.

<div align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/c/c2/MultiLayerNeuralNetworkBigger_english.png" alt="Kafka APIs">
</div>

Avant, on utilisait simplement le terme w pour désigner les poids associés à chaque variables d'entrée. On a besoin de complexifier l'écriture pour prendre en compte la notion de couche dans nos variables et ne pas toujours utiliser les mêmes. La notation commune est $$W^{[1]}, z^{[1]}, b^{[1]}$$ pour désigner les grandeurs associées à la première couche, ainsi de suite.

On verra dans la suite que les mécanismes de propagation forward/backward s'appliquent aussi bien avec un réseau en plusieurs couches.

# Représentation des réseaux de neurones

Reprenons la représentation de notre réseau de neurones :

<div align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/c/c2/MultiLayerNeuralNetworkBigger_english.png" alt="Kafka APIs">
</div>

On peut décomposer le schema en différentes parties :
- La couche d'entrée, les variables en entrée.
- Une couche cachée. "Cachée" car les valeurs contenues dans ces neurones ne sont pas observées, et elles ne sont pas fixées par les entrées/sorties définies par notre ensemble de données d'entrainement.
- La couche de sortie, responsable de la valeur de sortie estimée par le réseau.

## Taille du réseau

Pour déterminer la taille du réseau, on compte le nombre de couches sans prendre en compte la couche d'entrée. Dans l'exemple ci-dessus, on a un réseau à deux couches.

## Dimensions des paramètres

Pour la couche 1 (hidden layer), la **matrice des poids** $$W^{[1]}$$ est de dimension $$[3, 3]$$. Car pour chacun des 3 neurones de la couche 1, on va associer une combinaison des 3 variables d'entrée : [neurones dans la couche, valeurs passées à chaque neurone].

On peut remarquer que la dimension du vecteur de poids va correspondre avec le nombre de valeurs passées à chaque neurone. Pour la couche d'entrée, chaque neurone reçoit une seule flèche : le vecteur de poids associé à cette couche sera de dimension $$[3, 1]$$.

Concernant **le biais** de la couche cachée $$B^{[1]}$$ : chacun des neurones possède un biais, on a donc un vecteur de dimension $$[3, 1]$$.

De manière générale, il est important de garder les dimensions à l'esprit lorsque l'on conçoit un réseau de neurones. La dimension des matrices de paramètres d'une couche dépend de la couche précédente, et de la configuration de la couche considérée.

# Sources

- <a href="https://www.coursera.org/learn/neural-networks-deep-learning/home/welcome" target="_blank">Deep Learning course</a> (Coursera - Andrew Ng)
