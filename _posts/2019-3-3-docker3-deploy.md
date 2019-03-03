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

Passons à l'écriture de la recette pour construire l'image Docker. Pour rappel : l'image Docker est une sorte d'emporte-pièce, qui permet de créer de nouveaux containers avec une configuration précise. Notre application s'executera alors dans chacun des containers.

Pour créer notre image docker, on se sert du **Dockerfile** : c'est un enchainement de commandes permettant d'automatiser des opérations lors de la création de l'image.

Voici les différentes étapes :

```bash
# Spécification de l'image de base utilisée pour notre nouvelle image
FROM ubuntu:latest

# Optionnel : Information dur l'auteur
MAINTAINER Alexandre

# Mises à jour de l'image et installation des packages spécifiques
RUN apt-get update -y
RUN apt-get install -y python3-pip python3-dev build-essential

# Copie de tout les fichiers dans un nouveau sous-dossier
COPY . /app
# Définir app comme le dossier de travail
WORKDIR /app

# Installer toutes les dépendances avec pip3
RUN pip3 install -r requirements.txt

# Lancement de l'appli
ENTRYPOINT ["python3"]
CMD ["main.py"]
```


## Sources

- [Documentation Docker](https://docs.docker.com)
