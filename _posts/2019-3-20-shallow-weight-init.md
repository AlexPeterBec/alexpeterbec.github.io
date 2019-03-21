---
published: true
title: "Initialisation des poids"
excerpt: ""
toc: true
toc_sticky: true
toc_label: "Descente de gradient"
toc_icon: "microchip"
comments: true
author_profile: false
header:
  overlay_image: "assets/images/covers/cover2.jpg"
  teaser: "assets/images/covers/cover2.jpg"
categories: [deep, learning, weights]
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

Quand on entraine un réseau de neurones, il est important d'initialiser les poids aléatoirement. Pour le cas basique de la régression logistique, initialiser à zéro ne posait pas problème, mais pour un réseau de neurones ça ne fonctionne pas.

# Initialisation à zéro

Prenons l'exemple d'un réseau avec :
- Deux variables d'entrée
- Deux neurones sur la couche cachée
- Un neurone d'activation

Avec une initialisation à zéro, la matrice des poids pour la couche cachée, ne contiendra que des zéros. Les poids étant identiques pour les deux neurones, ils vont donner la même valeur en sortie.

Il se trouve qu'au bout de quelques itérations, les neurones de la couche cachée calculent **exactement la même fonction**, car la mise à jour de leur poids est aussi identique. Ainsi de suite, les deux neurones donnent la même valeur à chaque itération. 

Il n'y a donc aucun intérêt à avoir plus d'un neurone dans la couche cachée, puisque chacun aura exactement la même influence sur la couche de sortie. 

> Il est donc important que les poids soit différents pour chacun des neurones, afin qu'ils "apprennent" de manière différente.

# Initialisation aléatoire

Création d'un vecteur de poids aléatoires, suivant une loi gaussienne aléatoire :

```python
w1 = np.random.randint((2, 2)) * 0.01
```

On multiplie par une très petite valeur pour s'assurer que les valeurs sont faibles, et être proche de zéro. Ainsi, on se situe dans la zone d'activation de la fonction non linéaire d'activation (sigmoid, tanh, relu). 

Si les valeurs d'initialisation des poids sont trop grands, on se situe dans la zone plate de la fonction d'activation, ce qui ralentirait fortement la vitesse de convergence de la descente de gradient.

Pour le **biais**, le problème de symétrie n'apparait pas et ça ne pose pas de problème de tout initialiser à zéro.

```python
b = np.zero((2, 1))
```

L'initialisation par des valeurs aléatoires de l'ordre de 0.01, peut bien fonctionner pour un réseau de faible profondeur. Pour les réseaux plus grands, il y a des techniques pour avoir une meilleure convergence de la descente de gradient. 

# Sources

- [Coursera - Deep Learning](www.coursera.org/learn/neural-networks-deep-learning)
