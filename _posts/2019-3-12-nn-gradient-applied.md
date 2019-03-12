---
published: true
title: "Application de la descente de gradient"
excerpt: "Regression Logistique et m exemples"
toc: true
toc_sticky: true
toc_label: "Descente de gradient"
toc_icon: "microchip"
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

Ainsi, pour deux variables d'entrée $$X_{1}$$ et $$X_{2}$$, avec leurs poids associés $$w_{1}$$ et $$w_{2}$$ et le terme de biais b on a :
- $$z = w_{1}x_{1}+w_{2}x_{2}+b$$ : L'équation de classification
- $$\hat y = a = \sigma (z)$$ : La prédiction a.

# Activer les extraits Latex


$$J(w, b)=\frac{1}{m}\sum_{1}^{m}\mathfrak{L}(\hat y^{(i)},y^{(i)})$$

# Images
## Internet
<img src="https://cdn-images-1.medium.com/max/1600/1*f9a162GhpMbiTVTAua_lLQ.png" alt="" class="center">

## Hebergé Git
<img src="{{ site.url }}{{ site.baseurl }}/assets/images/docker/VM-containers.png" alt="" class="center" width="500">


# Sources
- <a href="https://towardsdatascience.com/its-only-natural-an-excessively-deep-dive-into-natural-gradient-optimization-75d464b89dbb" target="_blank">Nombreux articles sur la descente de gradient</a> (TowardsDataScience) 
- <a href="https://www.coursera.org/learn/neural-networks-deep-learning/home/welcome" target="_blank">Deep Learning course</a> (Coursera - Andrew Ng)
