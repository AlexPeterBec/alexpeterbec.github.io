---
published: true
title: "Descente de gradient"
excerpt: "Avec une couche cachée"
toc: true
toc_sticky: true
toc_label: "Descente de gradient"
toc_icon: "microchip"
comments: true
author_profile: false
header:
  overlay_image: "assets/images/covers/cover2.jpg"
  teaser: "assets/images/covers/cover2.jpg"
categories: [deep, learning, gradient]
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

# Hypothèses

On considère un réseau avec une couche cachée :
- $n_{x} = n^{[0]}$ le nombre d'entrées.
- $n^{[1]}$ le nombre de neurones de la couche cachée.
- $n^{[2]} = 1$ le neurone constituant la couche de sortie.

Paramètres :
- $w^{[1]}$ les poids de la couche cachée, de dimensions $(n^{[1]}, n^{[0]})$ 
- $b^{[1]}$ les biais de la couche cachée, de dimensions $(n^{[1]}, 1)$
- $w^{[2]}$ les poids de la couche de sortie, de dimension $(n^{[2]}, n^{[1]})$ 
- $b^{[2]}$ les biais de la couche de sortie, de dimension $(n^{[2]}, 1)$ 

La fonction de cout : $J(w^{[1]}, b^{[1]}, w^{[2]}, b^{[2]})=\frac{1}{m}\sum_{1}^{m}\mathfrak{L}(a^{[2]},y)$

$a^{[2]}$ étant le résultat du neurone de la couche de sortie.

# Descente de gradient

Après avoir initialisé l'ensemble des paramètres de notre réseau, on effectue les prédictions pour notre ensemble de données d'entrainement. On va également calculer les dérivées partielles de la fonction de coût, par rapport à chacun des paramètres.

Ensuite, chacun des paramètres est mis à jour en fonction de la dérivée de la fonction de coût, avec un facteur correspondant au pas d'apprentissage :

$$w^{[1]} = w^{[1]} - \alpha dw^{[1]}$$

Ce qui va nous interesser maintenant est le calcul de la dérivée $$dw^{[1]}$$.

## Forward propagation

$$Z^{[1]}=W^{[1]}X+b^{[1]}$$

$$A^{[1]}=g^{[1]}(Z^{[1]})$$

$$Z^{[2]}=W^{[2]}A^{[1]}+b^{[2]}$$

$$A^{[2]} = g^{[2]}(Z^{[2]}) = \sigma (Z^{[2]})$$

## Backward propagation

$$dZ^{[2]} = A^{[2]} - Y$$

$$dw^{[2]} = \frac{1}{m}dZ^{[2]}A^{[1]T}$$

$$db^{[2]} = \frac{1}{m}np.sum(dZ^{[2]}, axis=1, keepdims=True)$$

$$d2^{[1]} = W^{[2]T}dZ^{[2]} * g^{[1]'}(Z^{[1]})$$

$$dw^{[1]}=\frac{1}{m}dZ^{[1]}X^T$$

$$db^{[1]} = \frac{1}{m}np.sum(dZ^{[1]}, axis=1, keepdims=True)$$

## Explications

Dans un article précédent j'ai détaillé le calcul des dérivées successives, dans le cas de la regression logistique. Ici le raisonnement est le même, on l'applique deux fois, puisque l'on a une couche cachée.

# Sources
- [Coursera - Deep Learning](www.coursera.org/learn/neural-networks-deep-learning)
