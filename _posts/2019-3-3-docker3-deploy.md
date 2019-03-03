---
published: true
title: "Docker 3 : Déployer une application Python"
excerpt: "Création d'un container custom"
classes: wide
comments: true
header:
  overlay_image: "assets/images/docker/cover.jpg"
categories: [docker, python]
---

## Pré-requis
- Connaitre les concepts de base de Docker.
- Disposer d'une appli python prête à déployer avec ```python3 main.py```
- Avoir installé Docker sur son environnement de travail

## Dossier de travail

Nous allons créer un dossier de travail contenant tout les fichiers de notre application, ils seront ensuite intégrés à notre container. Appellons ce dossier **docker-app**, ce sera notre point de départ.

Ce dossier **docker-app** contient à présent uniquement les fichiers de notre application.

## Dépendances

Dans notre dossier **docker-app** nous allons créer le fichier **requirements.txt**. C'est ici que nous allons définir les librairies nécessaires à notre application, car notre container sera créé à partir d'une image Ubuntu nue.

On liste donc dans **requirements.txt** chacune des librairies nécessaires : numpy, pandas... une par ligne.

```bash
numpy
pandas
Flask
...
```

## Construction de l'image






## Sources

- [Documentation Docker](https://docs.docker.com)
