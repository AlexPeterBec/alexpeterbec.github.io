---
published: true
title: "Kaggle : Challenge Avazu"
excerpt: "Prédiction des clics sur les publicités"
toc: true
toc_sticky: true
toc_label: "Challenge Avazu"
toc_icon: "mouse-pointer"
comments: true
author_profile: false
header:
  overlay_image: "assets/images/covers/cover5.png"
  teaser: "assets/images/covers/cover5.png"
categories: [kaggle]
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

# Le challenge

Dans le monde de la publicité en ligne, le taux de conversion des clics (Click Through Rate - CTR), est un indicateur très répandu pour mesurer la performance d'une publicité. Les systèmes de **prédiction** des clics sont largement utilisés dans le secteur des enchères de publicité, et pour la publicité sponsorisée.

Pour cette compétition, Kaggle a mis à disposition 11 jours de données provenant de la plateforme Avazu, afin d'entrainer et tester des modèles.

> Le but de ce challenge est donc de **prédire si l'utilisateur a cliqué** ou non sur la publicité affichée : Prédiction de 0 ou 1.

# Exploration des données

Dans un premier temps, on affiche les données disponibles et on effectue quelques observations.

## Equilibre des données

On constate que le dataset est fortement déséquilibré. La variable "click", qui est la variable de sortie 0/1, comporte seulement 17% de 1. C'est à dire que sur les données disponibles, **l'utilisateur a cliqué sur la publicité dans 17% des cas**.

## Les variables catégorielles

Les variables catégorielles disponibles devront être traitées avant d'être utilisées. On obtient les variables non numériques (discrètes), avec la commande suivante :

```python
df_train.select_dtypes(exclude='int64').columns
```

On a donc les variables suivantes qui sont de type categorielle :

```
['id', 'site_id', 'site_domain', 'site_category', 'app_id', 'app_domain', 'app_category', 'device_id', 'device_ip', 'device_model']
```



# Sources

- [Kaggle Challenge - Avazu CTR](https://www.kaggle.com/c/avazu-ctr-prediction)