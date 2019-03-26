---
published: true
title: "Optimisation de l'apprentissage"
excerpt: "Solutions pour mieux apprendre"
toc: true
toc_sticky: true
toc_label: "Optimization methods"
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

Dans les contenus précedents, on a vu uniquement des exemples où l'on calculait en bloc les sorties prédites par le réseau, pour l'ensemble des données d'entrainement. Mais à l'heure du big data, on utilise la technique du mini-batch, afin de traiter l'ensemble des données en **m** blocs.

- Mode **batch**, on fait passer d'un seul coup, toutes les données dans notre réseau.
- Mode **mini-batch**, on sépare les données en **m** sous-ensembles. C'est à ce mode que l'on va désormais s'intéresser le plus.

# Mode mini-batch

## Séparation des données

Supposons que l'on dispose de 5,000,000 données d'entrainement, et que l'on souhaite utiliser des mini-batch contenant 1000 exemples. On va donc créer 5,000 sous-ensembles et utiliser la notation suivante :

$$X = [X^{{1}}, X^{{2}}, ... , X^{{5000}}]$$

$$Y =[Y^{{1}}, Y^{{2}}, ... , Y^{{5000}}]$$

$$X^{{1}}$$ a pour dimension $$(n_X, 1000)$$ et $$Y^{{1}}$$ a pour dimension $$(1, 1000)$$.

## Algorithme de descente

Une fois que l'on dispose de nos 5,000 blocs de données, on applique la même logique que pour le jeu de données complet. La boucle suivante représente **1 epoch**, c'est à dire un passage sur le jeu complet d'entrainement, composé de 5000 étapes :

```
for t=1 to 5000:
    Forward propagation sur X{t}
    Calcul de la fonction de cout (moyenne sur 1000 éléments)
    Backpropagation, calcul du gradient J{t}
    Mise à jour poids, biais
```

Rien de nouveau donc pour cet algorithme, qui reprend les principe de forward, backward. 

## Choix du batch-size

Le choix du nombre de données dans chaque batch va avoir un impact sur l'allure de la progression dans la descente de gradient.

La différence est que le réseau commence rapidement à apprendre, il utilise moins de données pour faire plusieurs petit pas de la descente de gradient. Comme illustré sur le graphique ci-dessous, la descente mini-batch est plus volatile :

<img src="https://cdn-images-1.medium.com/max/1600/1*5mHkZw3FpuR2hBNFlRxZ-A.png" alt="" class="center">

Comme souvent avec les réseaux de neurones, on cherche le compromis entre les deux cas extrêmes :

- La **descente de gradient stochastique**, quand on fixe m=1, le gradient est calculé pour chaque donnée d'entrainement.
- La **descente de gradient batch**, quand m=max, on effectue des passages avec l'ensemble des données d'entrainement.

<img src="https://cdn-images-1.medium.com/max/1600/1*PV-fcUsNlD9EgTIc61h-Ig.png" alt="" class="center">

On utilisera des valeurs typiques : 64, 128, 256, 512. Puissances de 2, qui permettent d'optimiser la mémoire utilisée. Attention aussi à ne pas inclure dans le batch plus de données que la mémoire RAM ne peut supporter.

# Optimisation de la direction du gradient

Dans cette partie, on verra quelques outils pour faire en sorte que le gradient aille dans une direction optimisée. 

## Moyenne mobile, poids exponentiels

On trouve aussi l'appelation EWMA pour *exponential weight moving average*. 

> Il s'agit de conserver en mémoire les valeurs précédentes lors du calcul d'une nouvelle valeur. Ainsi, on lisse les nouvelles valeurs et on résiste aux valeurs anormales. On contrôle l'historique mémorisé avec le paramètre $$\beta$$.

$$V_t = \beta V_{t-1} + (1 - \beta) \theta_t$$

Les valeurs calculées précédemment sont comprises $$V_{t-1}$$, si on détaille la valeur $$V_100$$ :

$$V_100 = 0,1\cdot\theta_100 + 0.1\cdot0.9\cdot\theta_99 + 0.1\cdot(0.9)^2\cdot\theta_98 + 0.1\cdot(0.9)^3\cdot\theta_97 ... $$

Avec $$\beta$$ on contrôle l'historique conservé :

- Pour 0.9, on conserve l'information sur 10 valeurs.
- Pour 0.98, on conserve l'information sur 50 valeurs

Pour connaitre cette information, on considère qu'une valeur dont le coefficient est inférieur à **1/e** n'est plus conservée, ainsi $$0.9^10 = \frac{1}{e}$$.

## Correction du biais initial

Gardons à l'esprit qu'on cherche à **optimiser la direction du gradient**. Pour utiliser la méthode EWMA ci-dessus, il faut bien initialiser les valeurs, et si on initialise à zéro, on démarre l'algorithme avec un biais important.

Pour corriger ce biais initial, on utilise alors un facteur dépendant du temps : On va calculer $$\frac{V_t}{1-\beta^t}$$. Ainsi, pour les premières valeurs, la valeur sera augmentée, pour les valeurs suivantes, cette correction aura de moins en moins d'effet.

## Momentum

La **méthode du moment** est l'application directe de la pondération exponentielle vue plus haut. Cette méthode va directement s'implémenter lors de la mise à jour des poids pour l'apprentissage :

Calcul de dw et db

$$V_dw = \beta_1 V_dw + (1- \beta_1)dw

V_db = \beta_1 V_db + (1- \beta_1)db

w = w - \alpha V_dw

b = b - \alpha V_db$$

Le paramètre $$\beta$$ est le même que dans la partie EWMA, c'est lui qui influe sur la "mémoire".

## RMSprop

Le **Root Mean Square propagation** permet également à la descente de gradient d'aller plus rapidement dans la meilleure direction. Ici aussi, on applique un coefficient dynamique pour s'assurer que le gradient n'oscille pas trop.

- Calcul de dw et db
- $$S_dw = \beta_2 S_dw + (1- \beta_2)dw^2$$
- $$S_db = \beta_2 S_db + (1- \beta_2)db^2$$
- $$w = w - \alpha \frac{dw}{\sqrt{S_dw + \epsilon}}$$
- $$b = b - \alpha \frac{db}{\sqrt{S_db + \epsilon}}$$

En divisant par le terme $$S_db$$, on corrige les valeurs trop extrêmes et on adoucit la trajectoire du gradient.

## Adam Optimisation

Adam signifie en réalité **Adaptative Moment Estimation**, il s'agit d'un assemblage des deux méthodes précédentes : RMSprop et EWMA.

- Calcul de dw et db sur le mini-batch courant

# Variation du pas d'apprentissage


# Sources

- [Coursera - Deep Learning](www.coursera.org/learn/neural-networks-deep-learning)
