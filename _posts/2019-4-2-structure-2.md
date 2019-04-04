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

## Différentes sources

Dans cette partie on verra les subtilités de travailler avec des jeux de données qui n'ont pas tous la même distribution.

Exemple : On crée une appli de classificaiton d'images et on dispose de 200.000 images bien propres trouvées sur internet pour entrainer notre classifieur, et 10.000 images provenant de vrais photos soumises par des utilisateurs, c'est sur ces 10.000 que l'on souhaite avoir les meilleures performances.

La solution qui vient d'abord à l'esprit serait de mélanger toutes les données, puis de les diviser en train/dev/test sets. En pratique on préferera la distribution suivante :
- Train : 205.000 images, celles du web, et la moitié des images réelles.
- Dev : 2.500 images réelles.
- Test : 2.500 images réelles.

Ainsi, on se concentre mieux sur les données importantes. La règle générale est d'évaluer le modèle sur les données qui nous intéressent.

## Analyse biais-variance

Quand on utilise des données de distributions différentes entre le train et le dev/test, il est difficile d'évaluer la cause réelle de sous-performance :
- Est-ce le modèle qui n'arrive pas à généraliser sur de nouvelles images ?
- Est-ce un problème de différence de distribution ?

Pour répondre à ces questions, on va créer un nouveau dataset, le **train-dev set**. C'est une sous-partie du train set que l'on va cacher lors de l'entrainement, ainsi on sait mieux évaluer :

| Erreur Train | Erreur Train-dev | Erreur dev |
|:--------------:|:------------------:|:------------:|
| 1% | 9% | 10% |
| 1% | 1.5% | 10% |

- Dans le premier cas : Il y a un problème de variance, le modèle n'arrive pas à bien performer sur le train-dev, alors que les données sont proches du train set.
- Dans le second cas : La différence des données pose problème, le modèle n'apprend pas suffisamment pour réussir une tâche plus complexe, ou trop différente.

## Solution pour réduire la disparité

Toujours dans le cas ou l'on dispose d'un train/dev/test avec des distribution différentes. La première chose à faire est d'analyser manuellement sur quels aspects les données diffèrent. Ensuite, selon les aspects identifiés, on peut essayer de générer artificiellement de nouvelles données.

A partir des données dont on dispose et selon le cas d'usage, on dispose de moyens pour transformer nos données et les faire ressembler au cas d'usage final. C'est à dire faire apprendre à notre modèle des données proches de celles sur lesquelles on va l'évaluer.

Par exemple, pour un système de reconnaissance vocale dans une voiture, on va mélanger des enregistrements audio avec des bruits de fond de voiture.

# Transfert et Multi-tâches

# End-to-end deep learning

# Sources

- [Coursera - Deep Learning](www.coursera.org/learn/neural-networks-deep-learning)
