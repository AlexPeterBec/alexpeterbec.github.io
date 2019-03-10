---
published: true
title: "La descente de gradient"
excerpt: ""
toc: true
toc_sticky: true
toc_label: "Descente de gradient"
toc_icon: "terminal"
comments: true
header:
  overlay_image: "assets/images/nn1/cover.jpg"
  teaser: "assets/images/nn1/cover.jpg"
categories: [ml, algebre]
---

# Principe

Nous verrons ici comment utiliser la descente de gradient pour apprendre les paramètres w et b sur l'ensemble de données d'apprentissage.

Fonction de coût : $$J(w, b)=\frac{1}{m}\sum_{1}^{m}\mathfrak{L}(\hat y^{(i)},y^{(i)})$$

On veut donc trouver les paramètres w et b qui minimisent la fonction J(w, b). Si il nous était possible de représenter pour toutes les valeurs de l'espace des couples (w, b), on verrait facilement pour quelles valeurs la fonction de perte est minimale. Or, trouver un seul point de la valeur de la fonction de perte necessite du temps de calcul (et augmente avec la complexité de notre algorithme). 

L'algorithme de descente de gradient est donc largement utilisé dans le machine learning pour éviter d'évaluer les performances pour un grand nombre de paramètres. Cet algorithme permet de faire évoluer nos paramètres (w, b) dans le bon sens (le sens qui induit une perte plus petite). 

# Algorithme

Les étapes de l'algorithme :
- On initialise nos paramètres (w, b) à des valeurs aléatoires.
- A chaque étape, les paramètres sont mis à jour dans la direction qui "descend" le plus fort. 
- Au bout d'un nombre fini d'itérations, le minimum global est atteint si la fonction est convexe. Les performances de notre algorithme sont optimales.

On écrit ainsi la mise à jour des paramètres :

$$w = w = \alpha . \frac{\partial J(w, b)}{\partial w}$$

$$w = w = \alpha . \frac{\partial J(w, b)}{\partial b}$$

Le paramètre **alpha** est le **pas d'apprentissage** ou **learning rate**, permet d'ajuster la taille des changements que l'on effectue. Nous verrons que sa valeur est importante selon les cas, on souhaite aller plus vite, ou bien affiner nos paramètres par de toutes petites variations.

# Sources

- <a href="https://docs.aws.amazon.com/cli/latest/index.html" target="_blank">[TowardsDataScience] Nombreux articles sur la descente de gradient</a>
- Coursera Deep Learning
