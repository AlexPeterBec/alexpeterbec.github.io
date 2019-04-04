---
published: true
title: "Stratégie machine learning"
excerpt: "Partie 2"
toc: true
toc_sticky: true
toc_label: "Strategy 2"
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

# Analyse des erreurs

Avant que notre algorithme ne dépasse les capacités humaines, c'est une bonne pratique de s'intéresser spécifiquement aux erreurs pour corriger certains défauts.

## Estimer la marge de progression

Une fois qu'un défaut de l'algorithme a été identifié, il faut pouvoir évaluer si le temps de travail pour corriger ce défaut aura vraiment un impact. Pour cela, il faut évaluer "manuellement" :

Sur un ensemble de 100 images mal classifiées, si seulement 5 correspondent à des chiens, on sait que la marge d'amélioration sera assez faible, puisque l'on agira sur seulement 5% du taux d'erreur.

Dans la plupart des cas, on sait identifier **plusieurs idées** d'amélioration pour l'algorithme. On peut alors travailler sur 100 exemples mal classifiés, et présenter chaque idée en colonne, pour obtenir un **pourcentage de responsabilité** pour chacune des pistes. Grâce à cela, on sait quelle pistes de travail seront les plus pertinentes.

## Nettoyage des données

Que faire quand on se rend compte que les données d'entrainement comportent des valeurs incorrectes ?

Il se trouve que les algorithmes deep learning sont **robustes aux erreurs aléatoires** lors de l'entrainement. En revanche, ils sont **sensibles aux erreurs systematiques**.

- Quelles que soient les **actions** prises pour améliorer les performances, il est important de les effectuer simultanément sur le **train et et le test set**, afin de conserver une distribution identique des données.
- Concernant les labels incorrects, il faut analyser les exemples où l'algorithme a bien prédit (possible coup de chance sur un mauvais label et une bonne classification).
- On peut arriver à une distribution différentes si on modifie les labels sur les sets de validation (dev/test), c'est acceptable tant que les distributions dev/test sont cohérentes entre elles.

## Se lancer et itérer

Au moment d'adresser une nouvelle tâche, le plus important est de constituer un set de données **train/dev/test** et mettre rapidement en route **premier modèle simple**. On appelle ça le **Quick & Dirty**.

Ensuite, on utilisera des methodes d'analyse de biais et variance pour **améliorer progressivement** le modèle et aborder chaque difficulté dans un ordre d'importance.


# Disparité des train/test sets

# Transfert et Multi-tâches

# End-to-end deep learning

# Sources

- [Coursera - Deep Learning](www.coursera.org/learn/neural-networks-deep-learning)
