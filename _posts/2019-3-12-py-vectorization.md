---
published: true
title: "Python : La vectorisation"
excerpt: "Fini les boucles for"
toc: true
toc_sticky: true
toc_label: "Vectorization"
toc_icon: "infinity"
comments: true
header:
    overlay_image: "assets/images/nn1/cover.jpg"
    teaser: "assets/images/nn1/cover.jpg"
categories: [ml, python]
---
<script type="text/javascript" async
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

# Vectorisation

La **vectorisation**, c'est la technique de base pour se débarasser des boucles *for* dans le code.

On a vu dans les premiers exemples de la regression logistique que la première opération consiste à multiplier deux vecteurs $$w$$ et $$x$$ dans la formule suivante :

$$z = w^\intercal \mathbf{x} + b$$

L'approche **classique**, non-vectorisée serait d'itérer sur chacun des indices de ces vecteurs avec une boucle for sur l'intervalle des indices.

Avec python, pour effectuer cette même opération de manière vectorisée, on utilise la fonction `np.dot(w, x) + b` , de la librairie numpy. 

Il se trouve que ce type d'opération est extrêmement **rapide** : Pour multiplier deux vecteurs de taille 1 million, la boucle for prend **500 fois plus de temps** que l'opération avec np.dot. 

En effet, les opérations de la librairie numpy sont capables de **paralleliser** les opérations sur le CPU/GPU au lieu de les effectuer séquentiellement (comme c'est le cas avec une boucle for).

# Quelques exemples

Multiplication de matrices :

`u = np.dot(A, v)`

On dispose d'un vecteur v de dimension n, et on souhaite **appliquer une fonction à chacun des éléments** du vecteur :

```python
u = np.exp(v)
u = np.log(v)
u = np.abs(v)
u = np.maximum(v, 0)
```

Utilisation d'un vecteur de poids en entrée du réseau de neurones, plutôt qu'une variable pour chacun :

```python
dw = np.zeros((nx, 1))  # Initialisation
dw += xi * dzi          # Mise à jour
dw /= m                 # Moyenne train-set
```

# Retour sur : Regression logistique

# Broadcasting

# Vecteurs numpy

# Sources
- <a href="https://www.coursera.org/learn/neural-networks-deep-learning/home/welcome" target="_blank">Deep Learning course</a> (Coursera - Andrew Ng)
