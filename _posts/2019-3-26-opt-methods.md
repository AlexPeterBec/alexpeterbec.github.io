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

![image-center]({{ site.url }}{https://cdn-images-1.medium.com/max/1600/1*5mHkZw3FpuR2hBNFlRxZ-A.png){: .align-center}

Comme souvent avec les réseaux de neurones, on cherche le compromis entre les deux cas extrêmes :

- La **descente de gradient stochastique**, quand on fixe m=1, le gradient est calculé pour chaque donnée d'entrainement.
- La **descente de gradient batch**, quand m=max, on effectue des passages avec l'ensemble des données d'entrainement.

![image-center]({{ site.url }}{https://cdn-images-1.medium.com/max/1600/1*PV-fcUsNlD9EgTIc61h-Ig.png){: .align-center}


# Optimisation de la direction du gradient
(EWMA, RMSprop, Adam)

# Variation du pas d'apprentissage


# Sources

- [Coursera - Deep Learning](www.coursera.org/learn/neural-networks-deep-learning)
