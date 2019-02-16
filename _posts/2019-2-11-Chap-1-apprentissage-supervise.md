---
published: true
title: "Stats 1 - Apprentissage supervisé"
excerpt: "Définitions et principes de base"
classes: wide
comments: true
header:
  image: "assets/images/curves-led.jpg"
categories: [definitions, statistiques]
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

# Introduction
Pour chacun des datasets, on trouve un ensemble de variables pouvant être qualifiées de données *d'entrée*, qui sont mesurées ou prédéfinies. Celles-ci ont une influence sur la ou les variables de *sortie*. Pour chaque exemple, le but est d'utiliser les variables d'entrée pour prédire la valeur des variables de sortie.

Dans la litterature statistique, les entrées sont appelées les *prédicteurs*, et plus classiquement les *variables indépendantes*. Dans la reconnaissance de motifs, le terme *features* est préféré. Les sorties sont quant à elles appelées *réponses* ou bien *variables dépendantes*.

# Types de variables et définitions
Les formes de variables en *sortie* peuvent varier :

- Un résultat **quantitatif**, où certaines valeurs sont plus grandes que les autres, et les mesures proches en valeur sont proches par leur nature.
- Un résultat **qualitatif, catégorique, discret**, admet qu'il existe un nombre fini de valeurs de sortie : 3 classes d'Iris, 10 digits à reconnaitre. Il n'y a pas d'ordre parmi ces classes et on trouve souvent des valeurs descriptives plutôt que des nombres.

Pour ces deux types de sorties, il est logique de penser à utiliser les entrées pour prédire les sorties. Cette distinction entre les types de sorties a amené à considérer deux types de problèmes : La *regression* quand il s'agit de prédire une valeur numérique, la *classification* quand il s'agit de prédire une valeur qualitative. Nous verrons que ces deux problème ont beaucoup en commun et peuvent être vus comme une tâche d'approximation de fonction.

Le type d'entrée peut également varier. Il peut exister des mesures qualitatives *et* quantitatives dans le même ensemble d'entrée. Il existe par conséquent des méthodes adaptées au type d'entrée considérée, certaines pour les mesures qualitatives ou quantitatives en particulier, d'autres pour les deux sans distinction.

Un troisième type de variable est la *catégorielle ordonnée*, comme par exemple : *Small, Medium, Large*, où il y a en effet un ordre logique dans les valeurs, mais pas de notion de mesure ou d'ordre de grandeur.

Les variables qualitatives sont habituellement représentées numériquement par des codes. Le cas le plus simple est le binaire quand on considère par exemple *Succes ou Echec*, on peut alors représenter cette valeur par le binaire 0/1 ou -1/1. Pour des raisons qui se revèleront évidentes, ces codes numériques sont parfois appelés *cibles*. Quand il y a plus de deux catégories, plusieurs options existent : La plus efficace est l'encodage via des *dummy variables* où l'on représente une mesure pouvant prendre K valeurs comme un vecteur de K mesures binaires, où une seule valeur peut prendre la valeur 1. Bien qu'il existe des encodages plus compacts, les *dummy variables* sont symétriques dans les niveaux de factorisation

![image](/assets/images/mnist.png?raw=true){: .center-image }

# Deux approches simples

Dans cette partie, nous verrons deux méthodes simples et efficaces de prédictions : Le modèle linéaire entrainé via les moindres carrés, et la prédiction basée sur les K plus proches voisins.

- Le **modèle linéaire** fait hypothèses très importantes sur la distribution des données, fournit donc des prédictions stables, mais potentiellement erronées.
- La méthode des **K plus proches voisins** fait des hypothèses moins fortes sur les données : Ses prédictions sont plus précises, mais peuvent être instables.

 
### Modèles linéaires et moindre carrés

Le modèle linéaire a été un pilier de la statistique durant les 30 dernières années et reste un outil très important à ce jour. On considère un vecteur d'entrée $$X^T = (X_1, X_2, ..., X_p)$$, et on prédit la sortie Y selon le modèle suivant.

### Methode des plus proches voisins
### Des moindres carrés aux plus proches voisins

# Théorie de la décision statistique

# Méthodes locales en grandes dimensions

# Modèles, Apprentissage supervisé, Approximation
### Un modèle statistique pour la distribution jointe Pr(X, Y)
### Apprentissage supervisé
### Approximation de fonction

# Modèles de regression structurés
### Difficulté du problème

# Classes d'estimateurs restreints
### Pénalisation et Methodes Bayesiennes
### Méthodes à noyau et Regression locale
### Fonctions de base et Methodes de dictionnaires

# La sélection de modèles - Le compromis biais-variance
