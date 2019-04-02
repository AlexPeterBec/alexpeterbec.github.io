---
published: true
title: "Stratégie machine learning"
excerpt: "Partie 1"
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

Ces deux articles sur les stratégies machine learning regroupent les bonnes pratiques pour implémenter des algorithmes.

L'idée est d'y voir plus clair sur les décisions à prendre pour améliorer son algorithme deep learning. Les possibilités d'améliorations sont tellement nombreuses qu'il faut savoir dans quelle direction chercher : Quantité et diversité des données, algorithmes d'optimisation, taille du réseau, dropout, batchnorm etc..

# Orthogonalisation

> Orthogonalisation : Savoir quels paramètres modifier pour arriver à un effet désiré.

## Comparaison avec une voiture

Pour conduire une voiture on agit principalement sur 3 paramètres : le volant, l'accelerateur, le frein. Ces trois paramètres sont indépendants, et il n'existe pas de levier ou de pédale qui soit une combinaison de deux paramètres. On qualifie donc ces 3 paramètres d'orthogonaux.

## Chaine de l'espoir du modèle

Lorsque l'on design un algorithme de machine learning on fait des hypothèses successives sur les performances de notre modèle, depuis le set d'entrainement jusqu'aux données dans l'application finale. Pour agir sur ces performances, on dispose à chaque étape de leviers adaptés :

- Bonnes performances sur le set d'entrainement (ex : Taille du réseau, Optimizers..)
- Bonnes performances sur le set de developpement (ex : Regularisation, Grand train set)
- Bonnes performances sur le test set (ex : grand dev set)
- Bonnes performances dans l'appli finale (ex : changement de la fonction de coût, changement du test/dev set)

# Evaluation du modèle

[Par ici pour un article détaillé sur l'évaluation des algorithmes](https://alexpeterbec.github.io/metrics/scoring/algorithm-scoring/)

## One metric to rule them all

La mise au point de modèles étant un processus iteratif, on souhaite à chaque étape, évaluer l'impact de nos changements. Afin d'avoir les idées claires sur cet impact, il est préférable de choisir une seule métrique qui refletera bien les performances souhaitées.

**Par exemple :** Au lieu de comparer des doubles métriques Precision/Recall, on les embarque dans le f1-score, la moyenne harmonique des deux mesures.

> L'idée est de se simplifier la vie, afin d'avoir une seule métrique pour évaluer nos "améliorations".

## Optimiser et satisfaire des contraintes

On dispose parfois de plusieurs mesures, qu'il n'est pas possible de combiner : par exemple, la précision et le temps d'execution. On fait alors la distinction entre deux types de contraintes :
- **Optimiser** : Quand on souhaite maximiser ou minimiser une grandeur (comme la précision, le f1-score, la fonction de perte..) 
- **Satisfaire** : Pas besoin de descendre le plus bas possible, juste se situer dans une fenêtre acceptable (Satisfaire un temps de prédiction de moins de 100ms, satisfaire un seuil de faux positifs sur une période de temps)

> Quand on dispose de N métriques différentes, en choisir une à optimiser, et satisfaire les autres.

## Distribution Train / Dev / Test

C'est une des premières étapes pour commencer à travailler sur un ensemble de données. 

- Choisir un couple dev/test qui reflète les **données sur lesquelles le modèle va être sollicité** dans le futur.
- Il est important que dev/test possède la même distribution.

# Sources

- [Coursera - Deep Learning](www.coursera.org/learn/neural-networks-deep-learning)
