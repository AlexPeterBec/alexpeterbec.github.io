---
published: true
title: "Evaluation des algorithmes"
excerpt: "Datasets, scores, courbes, taux"
toc: true
toc_sticky: true
toc_label: "Algorithm Metrics"
toc_icon: "ruler-combined"
comments: true
author_profile: false
header:
  overlay_image: "assets/images/tensorflow/cover.jpg"
  teaser: "assets/images/tensorflow/cover.jpg"
categories: [metrics, scoring]
---

Quand on travaille avec les algorithmes, on finit toujours par devoir évaluer leur performances, notamment pour :
- Quantifier l'impact d'un changement d'hyper-paramètres (paramètres de l'algorithme).
- Connaitre les performances du modèle, et le comparer à d'autres approches, comme dans les challenge Kaggle par exemple.

Dans cet article nous verrons :
1. Comment **segmenter les données** pour calculer les scores.
2. La matrice de confusion pour la **classification binaire**.
3. Mesures de performance pour les problèmes de **classification**.

# Segmentation des données pour l'évaluation

## Train / Validation / Test split
C'est la première étape quand on commence à travailler avec un ensemble de données. Cela consiste à séparer nos données en deux sous-ensembles :
- Un set d'entrainement, le **train set**. Qui sera composé de la majorité des données, servant à entrainer notre modèle.
- Un set de validation, le **validation set**. Qui est utilisé dans le cycle de développement, permet de fournir une évaluation non-biaisée du modèle lors de la recherche des hyper-paramètres.
- Un set de test, le **test set**. Il s'agit d'une partie du dataset que l'on va cacher à l'algorithme et représentera 20% du volume de données disponible. C'est sur cet ensemble que l'algorithme sera évalué à la toute fin.

Le train/validation/test split est une technique très répandue, qui fonctionne bien lorsque l'on dispose d'une **grande quantité de données**, car il faut "sacrifier" un pourcentage des données, pour l'évaluation du modèle.

<div align="center">
    <img src="https://qph.fs.quoracdn.net/main-qimg-e4755860eefa095dcab79659e356cf56" alt="Evaluation Flow-chart" vspace="10">
</div>

## Validation croisée / K-fold

La validation croisée est une extension du train/test split. On parle aussi de **cross-validation** ou **cv** dans les paramètres des algorithmes. Elle est utilisée quand la **quantité de données est limitée**, ou bien quand on dispose des ressources/temps nécessaires pour effectuer **plusieurs passages** sur les données.

Le principe de la validation croisée est de faire une boucle pour que tout le dataset d'entrainement ait servi d'ensemble de validation. On parle de **folds** et on en utilise généralement 5 ou 7. C'est à dire que le dataset d'entrainement sera séparé en 7 parties et qu'on effectue **7 passages** (entrainement et évaluation sur validation set).

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/machine-learning/cross-validation.png){: .align-center}

Les **métriques** d'évaluation calculées sur chacun des sets de validation, sont finalement **moyennées** pour présenter une métrique de validation.

La cross-validation est une **bonne pratique** qu'il faut prendre comme habitude. Elle permet d'évaluer de manière plus précise le modèle, et de mieux se protéger du sur-apprentissage.

Dans le K-fold, on peut donc faire varier K de 2 à N :
- Pour *K=2*, on sépare le dataset d'entrainement en deux. C'est la séparation la plus grossière possible.
- Pour *K=N*, avec N le nombre de données d'entrainement. On cache uniquement une valeur à chaque passage, on parle de *Leave-one-out*. C'est un traitement généralement très couteux en temps de calcul.
- Les valeurs de K utilisées sont généralement **5, 7, 10**, qui sont des valeurs acceptables, mais il n'y a pas de règle formelle.

> Plus on augmente K, plus la difference entre les sets entrainement/validation est grande, on se rapproche d'un set d'entrainement complet. En se rapprochant du set d'entrainement complet, le biais introduit est plus faible.


## Variantes de la validation croisée

- On a déjà vu plus haut la **Leave-one-out cross-val**.
- La **stratified k-fold** cross validation, est une version pour les jeux de données **déséquilibrés**. On va introduire une contrainte d'équilibre des classes soit conservé (de 0 et de 1 par exemple).
- La validation croisée **répétée** : On effectue plusieurs fois le process de KFold, avec un tirage aléatoire lors de la constitution des folds à chaque itération.

# La matrice de confusion

Dans la partie précédente, on a évoqué la mesure de scores sur les différents dataset. Dans cette partie, on verra que la matrice de confusion nous permet d'obtenir diverses mesures de performance pour la classification binaire.

## La matrice et ses éléments

Dans cette partie, on traite un problème de **classification binaire** (prédiction de 0 ou 1). La matrice de confusion va présenter les résultats en confrontant la dimension **Vérité (Actual)** et **Prédiction (Predicted)**.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/machine-learning/confusion-matrix.png){: .align-center}

Prenons l'exemple de la reconnaissance de chat sur une image : 0 ce n'est pas un chat, 1 c'est un chat.

La diagonale des réussites en vert :
- Les **Vrai positifs (VP)** : L'algorithme a reconnu un chat sur l'image, et c'était réellement un chat.
- Les **Vrai négatifs (VN)** : L'algorithme n'a pas trouvé de chat sur l'image, et il n'y en avait pas.

La diagonale des erreurs en rouge :
- Les **Faux positifs (FP)** : L'algorithme a reconnu un chat, alors que c'était un chien.
- Les **Faux négatifs (FN)** : L'algorithme n'a pas trouvé de chat dans l'image, alors qu'il y en avait un.

Selon les cas d'usages, on va chercher à minimiser une erreur ou l'autre :
- Si notre algorithme classifie des mails comme spam ou non, on peut souhaiter minimiser les **faux positifs**, c'est à dire ne pas envoyer un mail important dans les spams.
- Si notre algorithme analyse des patients pour détecter des cas de cancer avant étude par un médecin, on souhaite détecter tout les cas de cancer, on ne veut pas avoir de **faux négatifs**. En contre-partie on augmentera le taux de faux positifs, qui seront alors écartés lors d'étude par un médecin.

## Accuracy / Justesse

Une mesure très courante que l'on tire de la matrice de confusion est **la justesse / l'accuracy**. C'est la rapport entre les prédictions justes, sur le nombre total de prédictions.

Pour que cette mesure soit pertinente, il faut que le jeu de données soit globalement **équilibré**.

L'accuracy ne convient pas du tout pour un dataset deséquilibré, en effet, si 5% des valeurs sont de la classe 1 et qu'on prédit uniformément la classe 0 pour tout les exemples, on aura une accuracy de 95%, ce qui n'est pas représentatif.

> Justesse : Dans quelle proportion des cas l'algorithme fait une bonne prédiction.

$$Justesse =  \frac{Succès}{Total} = \frac{VP + VF}{VP + VF + FP + FN}$$

## Précision

La précision nous informe sur la performance pour une classe donnée : Sur toutes les images où l'algorithme a trouvé un chat, quelle proportion contenait réellement un chat.

> Précision : Pour les prédictions d'une classe donnée, quelle proportion est bien classifiée.

$$Justesse =  \frac{Succès(Classe1)}{Total(Classe1)} = \frac{VP}{VP + FP}$$

# Sources

- [TowardsDataScience : Evaluation de modèles](https://towardsdatascience.com/metrics-to-evaluate-your-machine-learning-algorithm-f10ba6e38234)
- [Dezyre : Performance Metrics for ML](https://www.dezyre.com/data-science-in-python-tutorial/performance-metrics-for-machine-learning-algorithm)
- [Machine Learning Mastery : Cross validation](https://machinelearningmastery.com/k-fold-cross-validation/)
- [Confusion Matrix explained](https://medium.com/thalus-ai/performance-metrics-for-classification-problems-in-machine-learning-part-i-b085d432082b)
