---
published: true
title: "Stratégie machine learning"
excerpt: "Partie 1"
toc: true
toc_sticky: true
toc_label: "Strategy 1"
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

Pour conduire une voiture on agit principalement sur 3 paramètres : le volant, l'accelerateur, le frein. Ces trois paramètres sont indépendants, et il n'existe pas de levier ou de pédale qui soit une combinaison de deux paramètres. On qualifie ces 3 paramètres d'orthogonaux.

## Chaine de l'espoir du modèle

Lorsque l'on design un algorithme de machine learning on fait des hypothèses successives sur les performances de notre modèle, depuis le set d'entrainement jusqu'aux données dans l'application finale. Pour agir sur ces performances, on dispose à chaque étape de leviers adaptés :

- Bonnes performances sur le set d'**entrainement** (ex : Taille du réseau, Optimizers..)
- Bonnes performances sur le set de **developpement** (ex : Regularisation, Grand train set)
- Bonnes performances sur le **test** set (ex : grand dev set)
- Bonnes performances dans l'**appli finale** (ex : changement de la fonction de coût, changement du test/dev set)

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

## Changements sur les sets et les metrics

Quand la meilleure valeur pour la métrique d'évaluation ne correspond pas à l'algorithme choisi par nous/l'utilisateur, il est temps de faire des changements dans la manière d'évaluer les algos. Une manière possible est d'ajouter un poids correspondant à un nouveau critère dans la fonction d'évaluation.

Aussi, quand les performances en conditions réelles ne sont pas satisfaisantes, il faut repenser le dev/test set pour qu'ils reflètent mieux les données utilisées au final.

# Comparaison à un humain

Ces dernières années, les équipes de recherche en machine learning ont comparé leurs algorithmes aux performances humaines, pour deux raisons :
- Au vue des avancées récentes des algorithmes, c'est une question qui se pose car dans de plus en plus de domaines, les algorithmes sont équivalent ou meilleurs que des humains.
- Aussi, la stratégie de developpement est plus efficace quand on s'attaque à des tâches faisables par un humain.

Dans cette partie on va distinguer deux seuils de performance :
- Le taux d'**erreur humaine** : C'est la performance moyenne d'un humain sur une tâche donnée.
- Le taux d'**erreur du classifieur de Bayes** : C'est la meilleure performance possible, ce n'est pas nécessairement une erreur nulle. Par exemple pour la transcription audio, certains exemples sont tellement incompréhensibles qu'on ne peut pas considérer qu'un algorithme saura le comprendre.

## Le biais évitable

Retour au problème biais-variance.

Au moment d'évaluer notre algorithme et choisir quelle partie améliorer, il faut raisonner en termes de biais et de variance :
- Le **biais évitable**, c'est quand notre algortihme est à 8% d'erreur quand un humain est à 1% d'erreur. Ici, on doit se demander comment faire pour mieux apprendre sur le train set en premier lieu, avant de regarder les performances sur le test set (réseau plus grand, entrainement plus long, meilleure fonction d'optimisation, recherche de meilleur paramètres).
- La **variance indésirable**, c'est quand notre algorithme est proche des performances d'un humain sur le train set, mais se dégrade sur le test set. On doit alors se tourner vers la régularisation (L2, DropOut, data augmentation) pour réduire cette variance, ou bien disposer de plus de données, recherche de meilleurs paramètres).

Deux règles d'usage général pour l'amélioration des modèles :

- On sait limiter le **biais évitable** : Les performances sur le train set sont bonnes.
- On sait limiter la **variance** du modèle : La performance sur le train set se généralise bien à de nouvelles données.

## Bien cerner l'erreur humaine

Dans la partie précédente, on a vu qu'il était important de se référer à l'erreur humaine au moment d'évaluer le modèle. Cependant, l'erreur humaine peut être variable, par exemple pour reconnaitre une pathologie sur une image radio :
- Erreur humaine moyenne : 3%
- Erreur d'un médecin : 1%
- Erreur d'un médecin expérimenté : 0.7%
- Erreur d'un groupe de médecins expérimentés : 0.3%

A ce moment là, on peut dire que l'erreur du classifieur de Bayes sera inférieure ou égale à 0.3%. C'est plutôt à cette valeur qu'on va comparer notre modèle dans un premier temps.

## Quand l'ordinateur est meilleur

Voici quelques exemples de domaines pour lesquels les algorithmes sont meilleurs que l'humain :
- Prédiction de clic sur les publicités.
- Recommandation de produits.
- Logistique (prédiction du temps de transit)
- Prédire la capacité de remboursement d'un emprunteur.

Ces domaines sont des exemples qui ne sont pas soumis à la perception naturelle, et où l'accumulation d'une masse de données structurées permet aux algorithmes de repérer des motifs statistiques mieux que les humains.

Dans d'autres champs d'application, les algorithmes ont mis plus de temps à rattrapper/dépasser les performances humaines :
- Reconnaissance vocale
- Certaines tâches de reconnaissance d'images
- Certaines applications médicales pointues (ECG, cancers)

# Sources

- [Coursera - Deep Learning](www.coursera.org/learn/neural-networks-deep-learning)
