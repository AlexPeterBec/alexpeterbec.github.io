---
published: true
title: "Qu'est-ce qu'un réseau de neurones ?"
excerpt: ""
classes: wide
comments: true
author_profile: false
header:
  overlay_image: "assets/images/covers/cover1.jpg"
  teaser: "assets/images/covers/cover1.jpg"
categories: [nn]
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

Parmi les exemples d'usages classiques des algorithmes de machine learning on peut citer : la prédiction du prix d'une maison avec sa surface habitable, la detection de chats sur une image... Nous verrons que pour chaque problème, on trouve des algorithmes particuliers dans la famille des réseaux de neurones.

Pour introduire la notion de réseau de neurones, commençons par prendre l'exemple d'un neurone seul : C'est le Perceptron, inventé en 1957 par Frank Rosenblatt. Le Perceptron est une seule cellule, un seul neurone, qui permet de résoudre les problèmes de classification binaire : prédire 0 ou 1. Le neurone va trouver la frontière séparant les données 0 et 1.

Le Perceptron est à la base de l'analogie avec les neurones:
- Il s'agit d'une cellule qui reçoit des informations en entrée, tout comme un neurone humain capte des signaux par les *Dendrites*.
- Les variables en entrée sont passées dans une fonction d'activation (de décision), comme les signaux captés sont rassemblés dans le corps cellulaire, ou *Soma*, décide de transmettre l'information à d'autres neurones du cerveau.

Le Perceptron est une fonction mathématique, prenant des variables d'entrée pondérées par des poids, et un terme de biais. Dans un espace à deux dimensions, ceux-ci sont comparables au coefficient directeur, et à l'ordonnée à l'origine.

**Dans un espace à deux dimensions, le Perceptron est capable de tracer une droite pour séparer des points entre deux classes.**

![image](/assets/images/nn1/perceptron.png){: .align-center }


# Apprentissage supervisé avec les Neural Nets

### Exemples d'applications

- Caractéristiques d'une maison, prediction de son prix. (NN)
- Publicités et données utilisateur, prédire le clic. (NN)
- Images avec labels, trouver les objets sur l'image. (CNN)
- Audio, transcription de texte. (RNN)
- Image et radar, navigation véhicules. (Custom, Hybride)

### L'apprentissage supervisé

En entrée des réseaux, on trouve des données **structurées** comme des tables de prix, des tables de données utilisateur : Des occurrences de données avec plusieurs champs renseignés.

On trouve également des données **non structurées** : les données audio, les images, les textes. C'est une tâche qui a été plus complexe à maitriser pour les algorithmes et qui connait un succès récent.

# Comment expliquer le succès du Deep Learning ?

Historiquement, les **algorithmes classiques** ne donnaient pas de meilleures performances lorsqu'ils disposent de plus de données. On a désormais accès à de plus en plus de données avec la digitalisation.

Les **réseaux de neurones** ont permis de tirer avantage de ces plus grandes quantités de données et d'augmenter les performances.

C'est donc un **effet d'échelle** qui a permis le progrès des réseaux de neurones, l'échelle des données, mais aussi l'échelle du réseau de neurones : la profondeur du réseau a augmenté au cours du temps.