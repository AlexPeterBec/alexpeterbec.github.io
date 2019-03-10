---
published: true
title: "La descente de gradient et les graphes de calcul"
excerpt: "NN Basics"
toc: true
toc_sticky: true
toc_label: "NN Basics"
toc_icon: "microchip"
comments: true
header:
  overlay_image: "assets/images/nn1/cover.jpg"
  teaser: "assets/images/nn1/cover.jpg"
categories: [ml, graph, algebre]
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

# Principes

Nous verrons ici comment utiliser la descente de gradient pour apprendre les paramètres w et b sur l'ensemble de données d'apprentissage.

Fonction de coût :
$$J(w, b)=\frac{1}{m}\sum_{1}^{m}\mathfrak{L}(\hat y^{(i)},y^{(i)})$$

On veut trouver les paramètres w et b qui **minimisent** la fonction J(w, b). Si il était possible de représenter pour toutes les valeurs de l'espace des couples (w, b), on verrait facilement pour quelles valeurs la fonction de perte est minimale. Or, trouver un seul point de la valeur de la fonction de perte necessite du **temps de calcul** (et augmente avec la complexité de notre algorithme).

L'algorithme de **descente de gradient** est largement utilisé dans le machine learning pour éviter d'évaluer les performances pour un grand nombre de paramètres. Cet algorithme permet de faire évoluer nos paramètres (w, b) dans le bon sens (le sens qui induit une perte plus petite). On voit sur l'image ci-dessous le type d'évolution que l'on souhaite faire suivre à nos paramètres, on veut arriver sur les points les plus bas du paysage, qui correspondent aux valeurs basses de la fonction de coût.


<img src="https://cdn-images-1.medium.com/max/1600/1*f9a162GhpMbiTVTAua_lLQ.png" alt="" class="center">

Pour la descente de gradient, on a vu que l'on a besoin de calculer les dérivées selon chacune des variables d'entrée. Dans un réseau de neurone, on peut voir le problème comme un graphe de calcul et calculer les dérivées en chaine.

# La descente de gradient

Les étapes de l'algorithme :
- On initialise nos paramètres (w, b) à des valeurs aléatoires.
- A chaque étape, les paramètres sont mis à jour dans la direction qui "descend" le plus fort.
- Au bout d'un nombre fini d'itérations, le minimum global est atteint si la fonction est convexe. Les performances de notre algorithme sont optimales.

On écrit ainsi la mise à jour des paramètres :

$$w = w = \alpha . \frac{\partial J(w, b)}{\partial w}$$

$$w = w = \alpha . \frac{\partial J(w, b)}{\partial b}$$

Le paramètre **alpha** est le **pas d'apprentissage** ou **learning rate**, permet d'ajuster la taille des changements que l'on effectue. Nous verrons que sa valeur est importante selon les cas, on souhaite aller plus vite, ou bien affiner nos paramètres par de toutes petites variations.

# Le graphe de calcul

Les étapes de calcul dans un réseau de neurones sont organisés en deux étapes :
- La **propagation vers l'avant** ou **forward propagation** : On calcule la sortie du réseau.
- La **back-propagation** où l'on se sert des résultats de la première étape pour calculer les gradients et dérivées, pour mettre à jour les paramètres.

## Principe (forward/backward)

Le graphe de calcul ou **computation graph** est une manière de représenter des opérations successives utilisant plusieurs variables. Ces graphes sont particulièrement utiles quand on souhaite optimiser la valeur finale.

En effet, puisqu'on va s'intéresser aux dérivées par rapport à nos différents paramètres, on va suivre les deux mêmes étapes évoquées plus haut.
- On effectue d'abord les opérations sur les variables pour arriver à la valeur de sortie du graphe (forward).
- On calcule ensuite les dérivées partielles pour mettre à jour nos variables dans le sens souhaité (backward).

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/nn1/computation-graph.png" alt="" class="center">

## Le calcul de dérivées dans le graphe

Une fois que l'on a atteint la valeur finale de notre graphe de calcul, on souhaite connaitre l'importance de chacune des variables. On peut alos utiliser les valeurs du graphe pour estimer les dérivées.

Ici on connait déjà les valeurs des coefficient, donc la dérivée semble évidente. Mais il est important de remarquer que cette valeur se retrouve en prenant le ratio de la variation de J et la variation du paramètre.

On peut ensuite remonter la **chaine des dérivées** pour trouver l'impact des variables de départ sur les variables intermédiaires puis sur la valeur de sortie.

Habituellement il y a une variable finale à la sortie de notre algorithme, et on va essayer de trouver l'impact individuel de chacune des variables. $$\frac{dVariableFinale}{dVar}$$

## Dérivées en chaine

Pour remonter à l'influence d'une variable sur la sortie, on va utiliser les dérivées successives. Dans le graphe en exemple nous avons les variables a, b, c, u, v et J la variable finale.

- Pour calculer l'influence de la variable v, on augmente la valeur de v et on regarde l'impact sur la variable J. Si on augmente v de 0.001, J augmente de 0.003. Par le ratio des variations on a :

$$\frac{dJ}{dv} = \frac{0.003}{0.001} = 3$$

- On remonte ensuite vers les variables d'entrée, pour **a** qui est plus simple :

$$\frac{dJ}{da} = \frac{dJ}{dv} x \frac{dv}{da} = \frac{0.003}{0.001} . \frac{0.003}{0.001} = 3 x 1 = 3$$

- Ainsi de suite, on peut décomposer chaune des étapes pour remonter à l'influence des variables d'entrée.

# Sources

On a vu dans cet article le principe de la descente de gradient, et de dérivées en chaine. Ce sont des éléments très important pour les réseaux de neurones. On trouve quantité d'articles sur le sujet auprès des sources spécialisées, et cela constitue les bases pour l'enseignement du deep learning.

- <a href="https://docs.aws.amazon.com/cli/latest/index.html" target="_blank">[TowardsDataScience] Nombreux articles sur la descente de gradient</a>
- Coursera Deep Learning (Andrew Ng)
