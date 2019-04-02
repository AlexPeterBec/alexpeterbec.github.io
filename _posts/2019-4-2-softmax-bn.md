---
published: true
title: "Batch normalization et regression Softmax"
excerpt: ""
toc: true
toc_sticky: true
toc_label: "Softmax & BN"
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

# Batch Normalisation

La BatchNorm (BN) rend l'apprentissage des hyperparamètres plus efficaces et rend le réseau de neurones plus robuste. La BN est une des avancées les plus importantes des réseau de neurones.

On a déjà vu que la normalisation des entrées d'un neurone peut améliorer l'apprentissage du réseau. Cela fonctionne bien pour les entrées d'un neurone, pour un modèle simple.

> Mais qu'en est-t-il avec un réseau plus profond ?

Avec un réseau plus profond, chaque couche prend en entrée les valeurs d'activation de la couche précédente. Le principe de la BN est de normaliser les valeurs d'activation de la couche précédente (valeurs A ou Z) pour apprendre plus vite les paramètres de la couche considérée. 

> Principe de la Batch Norm

Comme son nom l'indique, on se concentre sur un unique batch. La BN consiste à appliquer une normalisation sur les valeurs de Z (soustraire la moyenne et diviser par la variance) pour obtenir $$Z_{norm}$$.

La nouvelle valeur de Z est alors obtenue en appliquant deux nouveaux paramètres $$\gamma$$ et $$\beta$$, qui serviront à contrôler la BN.

Ces opérations permettent de garder le contrôle sur les valeurs d'activation dans les couches cachées afin d'avoir des valeurs fixes de moyenne/variance.

# Softmax Regression

La regression softmax est une généralisation de la regression logistique, pour les problème de classification *1 parmi C classes*.

Dans la plupart des modèles précédents, on utilisait une fonction d'activation sigmoïde au bout du réseau pour une classification binaire. Lorsqu'on utilise une fonction softmax en bout de réseau, on résoud les problèmes **multiclasses**.

A partir des valeurs d'activation Z, la couche softmax donne pour chaque classe une probabilité normalisée (somme = 1 sur l'ensemble des classes).


# Sources

- [Coursera - Deep Learning](www.coursera.org/learn/neural-networks-deep-learning)
