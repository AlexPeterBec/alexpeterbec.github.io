---
published: true
title: "Assemblage de neurones"
excerpt: "Notions globales, représentations"
toc: true
toc_sticky: true
toc_label: "Réseaux de neurones"
toc_icon: "microchip"
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

## Un neurone

On a vu dans les articles de la première partie, l'exemple de la regression logistique, composé d'**un seul élément appelé neurone**.


<div align="center">
    <img src="https://ml-cheatsheet.readthedocs.io/en/latest/_images/neuron.png" alt="Neuron" vspace="10">
</div>

On a vu qu'il effectuait les opérations suivantes :
- La multiplication matricielle des poids (w) par les variables d'entrée, et ajoute le terme de biais (b).
- Le passage dans une fonction d'activation sigma.

## Beaucoup de neurones

On va maintenant passer à une représentation plus "profonde" et considérer des couches successives de neurones. Chaque rond sur le schema est un neurone effectuant les opérations ci-dessus.

<div align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/c/c2/MultiLayerNeuralNetworkBigger_english.png" alt="NN">
</div>

Avant, on utilisait simplement le terme w pour désigner les poids associés à chaque variables d'entrée. On a maintenant besoin de complexifier l'écriture pour **prendre en compte la notion de couches** dans nos variables et ne pas toujours utiliser les mêmes. La notation commune est $$W^{[1]}, z^{[1]}, b^{[1]}$$ pour désigner les grandeurs associées à la première couche, ainsi de suite.

On verra dans la suite que les mécanismes de propagation forward/backward s'appliquent aussi bien avec un réseau en plusieurs couches.

# Représentation des réseaux de neurones

Reprenons la représentation de notre réseau de neurones :

<div align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/c/c2/MultiLayerNeuralNetworkBigger_english.png" alt="NN">
</div>

On peut décomposer le schema en différentes parties :
- La couche d'**entrée/input**, les variables en entrée.
- Une couche **cachée/hidden**. "Cachée" car les valeurs contenues dans ces neurones ne sont pas observées, et elles ne sont pas fixées par les entrées/sorties définies par notre ensemble de données d'entrainement.
- La couche de **sortie/output**, responsable de la valeur de sortie estimée par le réseau.

## Taille du réseau

Pour déterminer la taille du réseau, on compte le nombre de couches sans prendre en compte la couche d'entrée. Dans l'exemple ci-dessus, on a un réseau à deux couches.

## Dimensions des paramètres

Pour la couche 1 (hidden layer), la **matrice des poids** $$W^{[1]}$$ est de dimension $$[3, 3]$$. Car pour chacun des 3 neurones de la couche 1, on va associer une combinaison des 3 variables d'entrée : [neurones dans la couche, valeurs passées à chaque neurone].

On peut remarquer que la dimension du vecteur de poids va correspondre avec le nombre de valeurs passées à chaque neurone. Pour la couche d'entrée, chaque neurone reçoit une seule flèche : le vecteur de poids associé à cette couche sera de dimension $$[3, 1]$$.

Concernant **le biais** de la couche cachée $$B^{[1]}$$ : chacun des neurones possède un biais, on a donc un vecteur de dimension $$[3, 1]$$.

De manière générale, il est important de **garder les dimensions à l'esprit** lorsque l'on conçoit un réseau de neurones. La dimension des matrices de paramètres d'une couche dépend de la couche précédente, et de la configuration de la couche considérée.

# Propagation et calcul de la valeur de sortie

<div align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/c/c2/MultiLayerNeuralNetworkBigger_english.png" alt="NN">
</div>

## Ecriture des fonctions dans la couche cachée

Concentrons-nous sur un seul noeud du réseau : Le **premier neurone de la couche cachée**. Nous avons vu qu'il effectue deux opérations : La multiplication de matrices pour calculer Z, puis l'application d'une fonction d'activation sur Z, pour finalement obtenir A.

> Notation : $$a^{[l]}_{i}$$ la valeur de **a** pour la couche *l*, et pour le noeud *i* dans cette couche.

Expressions de Z et A pour le premier neurone de la couche cachée :
$$z^{[1]}_{1} = w^{[1]\intercal}_{1} x + b^{[1]}_{1}$$
$$a^{[1]}_{1} = \sigma (z^{[1]}_{1})$$

De même pour chaque neurone dans la couche cachée.

## Produit de matrice pour la couche cachée

On a les équations suivantes pour chacun des 3 neurones de la couche cachée :

$$z^{[1]}_{1} = w^{[1]\intercal}_{1} x + b^{[1]}_{1}$$

$$z^{[1]}_{2} = w^{[1]\intercal}_{2} x + b^{[1]}_{2}$$

$$z^{[1]}_{2} = w^{[1]\intercal}_{3} x + b^{[1]}_{3}$$

On peut rassembler les poids $$w^{[1]\intercal}_{i}$$ dans une matrice (Ici de taille 3x3). On a un vecteur par ligne puisque ce sont des transposées.

Pour obtenir la **matrice des Z** (première opération dans les neurones) de la couche , on va multiplier la matrice des poids par les données en entrée, (ici le vecteur $$[x_{1}, x_{2}, x_{3}]$$), et on ajoute le vecteur colonne des poids B.

$$\left[ \begin{array}{c} z_{1} z_{2} z_{3} \end{array} \right] =\left[ \begin{array}{cccc}
w_{1}[1] & w_{1}[2] & w_{1}[3] w_{2}[1] & w_{2}[2] & w_{2}[3]
w_{3}[1]  & w_{3}[2] & w_{3}[3] \end{array} \right]
.\left[ \begin{array}{c}x_{1} x_{2} x_{3} \end{array} \right] +
\left[ \begin{array}{c}b_{1} b_{2} b_{3} \end{array} \right]$$

La matrice résultante (3, 1) correspond bien aux valeurs Z que l'on va passer à la fonction d'activation, on peut l'appeler $$Z^{[1]}$$.

Pour chacune des couches on va utiliser le **même type de formules**, c'est la **taille des matrices** qui va varier selon le nombre de neurones, et selon le nombre de neurones de la couche précédente.

Dans la suite, nous verrons comment traiter ces opérations multiples grâce à la vectorisation en Python.

# Sources

- <a href="https://www.coursera.org/learn/neural-networks-deep-learning/home/welcome" target="_blank">Deep Learning course</a> (Coursera - Andrew Ng)
