---
published: true
title: "Application de la descente de gradient"
excerpt: "Regression Logistique et m exemples"
toc: true
toc_sticky: true
toc_label: "Descente de gradient"
toc_icon: "infinity"
comments: true
header:
overlay_image: "assets/images/nn1/cover.jpg"
teaser: "assets/images/nn1/cover.jpg"
categories: [ml]
---
<script type="text/javascript" async
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
# Descente de gradient pour la regression logistique

## Hypothèses de départ

On reprend le cadre simple de la regression logistique avec les éléments suivants :
- $$z = w^\intercal \mathbf{x} + b$$ : L'équation de regression.
- $$ \hat y = a = \sigma(z)$$ : La prédiction par la fonction d'activation.
- $$\mathfrak{L}(a, y) = -(y\log a+(1-y)\log(1-a))$$ : La fonction de perte pour une prédiction a.

Ainsi, pour deux variables d'entrée $$x_{1}$$ et $$x_{2}$$, avec leurs poids associés $$w_{1}$$ et $$w_{2}$$ et le terme de biais b on a :
- $$z(x_{1}, x_{2}) = w_{1}x_{1}+w_{2}x_{2}+b$$ : L'équation de classification
- $$\hat y = a = \sigma (z)$$ : La prédiction a.
- $$\mathfrak{L}(a, y)$$ : La fonction de perte se calcule finalement sur la prédiction a, et la vraie valeur y.

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/nn1/applied-schema1.png" alt="" class="center" width="700">

Le but de la descente de gradient est d'évaluer la fonction de perte L afin de mettre à jour les paramètres (dans la direction opposée au gradient) afin de minimiser L.

## Les dérivées successives

Comme vu dans le premier article sur la descente de gradient, on cherche à remonter successivement dans les dérivées. 

### Influence de a
La première dérivée qui nous interesse est celle de a : $$\frac{d\mathfrak{L}(a, y)}{da}$$. C'est **l'influence de a** sur l'évolution de la fonction de perte. Si on reprend l'expression de L(a, y), par la dérivation des fonctions Log on trouve : 

$$\frac{d\mathfrak{L}(a, y)}{da} = -\frac{y}{a} + \frac{1-y}{1-a}$$

### Influence de z
On remonte d'une étape dans le diagramme et on s'interesse à **l'influence de la variable Z** : 

$$\frac{d\mathfrak{L}(a, y)}{dz} = \frac{d\mathfrak{L}(a, y)}{da} . \frac{da}{dz}$$

Il s'agit d'un produit utilisant le terme trouvé à la première étape, il suffit de s'interesser à la fonction qui transforme Z pour arriver à A, c'est la fonction sigmoïde. Sa dérivée est égale à $$\frac{da}{dz} = a.(1-a)$$. Par produit on obtient : 

$$dz = \frac{d\mathfrak{L}(a, y)}{dz} = a - y$$

### Influence des variables d'entrée
L'étape finale du calcul est d'arrivée à **l'influence de chaque variable d'entrée** sur la fonction de perte grâce à l'expression précédente. Pour le paramètre $$x_{1}$$ on va modifier le poids $$w_{1}$$, on calcule donc : 

$$\frac{\partial L}{\partial w_{1}} = x_{1} . dz$$

L'expression est similaire pour le poids $$w_{2}$$. Pour le biais on a $$db = dz$$. Ce sont les quantités que l'on utilisera pour notre mise à jour des poids dans la descente de gradient :

$$w_{1} := w_{1} - \alpha dw_{1}$$

On a vu dans ce paragraphe comment effectuer la mise à jour des poids pour un seul exemple d'entrainement de notre algorithme. 

Dans la suite nous verrons comment appliquer le même raisonnement à **plusieurs données d'entrainement** : quand on dispose de nombreux couples $$(x_{1}, x_{2})$$.

# Descente de gradient sur m données d'entrainement



## Internet
<img src="https://cdn-images-1.medium.com/max/1600/1*f9a162GhpMbiTVTAua_lLQ.png" alt="" class="center">

## Hebergé Git
<img src="{{ site.url }}{{ site.baseurl }}/assets/images/docker/VM-containers.png" alt="" class="center" width="500">


# Sources
- <a href="https://towardsdatascience.com/its-only-natural-an-excessively-deep-dive-into-natural-gradient-optimization-75d464b89dbb" target="_blank">Nombreux articles sur la descente de gradient</a> (TowardsDataScience) 
- <a href="https://www.coursera.org/learn/neural-networks-deep-learning/home/welcome" target="_blank">Deep Learning course</a> (Coursera - Andrew Ng)
