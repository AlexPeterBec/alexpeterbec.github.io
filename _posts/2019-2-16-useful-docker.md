---
published: true
title: "Docker : Les bonnes bases 1"
excerpt: "Container, Image, Dockerfile"
classes: wide
comments: true
header:
  overlay_image: "assets/images/docker/cover.jpg"
categories: [docker, containers]
---

# Le concept

Les containers sont énormément utilisés pour améliorer la sécurité, la reproductibilité et la scalablité des développements en data science. Docker est une plateforme qui permet de déployer des applications dans des containers.

## Concepts importants de Docker

Qu'attend-t-on d'un container ?
- **Contenir des choses** : On veut pouvoir y mettre notre application.
- **Être portable** : Il peut être utilisé en local, reproduit sur la machine du collègue, ou même sur un service cloud.
- **Avoir des interfaces d'accès précises** : Un container Docker dispose de mécanismes pour interagir avec l'exterieur (ports, command line..)
- **Pouvoir l'obtenir à distance** : Docker permet d'enregistrer une image dans un registre global et permet de re-télécharger l'image du container autant de fois que nécessaire.

On peut comparer un container Docker comme **une chose vivante**, qui existe sous une forme unique, qui a une durée de vie. Un container Docker est une image Docker à qui on a donné vie.

Un container Docker est finalement un logiciel, dans lequel des programmes s'executent. Il peut y en avoir plusieurs en parallèle sur une unique machine, qui peuvent individuellement être executés, inspectés, stoppés, supprimés.

### Machine virtuelle
Les machines virtuelles sont les ancètres des containers Docker. Les machines virtuelles, elles aussi, isolent une application et ses dépendances (ce dont elle a besoin pour s'executer).

Les containers sont supérieurs car ils utilisent beaucoup moins de ressources, sont portables, et sont rapidement deployables.

<img src=https://scr.sad.supinfo.com/articles/resources/219471/6673/0.png alt=\"Docker Header\" style=\"height: 200px;\"/>

### Docker image
On peut comparer les images Docker à des emporte pièces, ou des moules en patisserie. Une image est le modèle sur lequel on construit un nouveau container identique.

**L'image Docker contient dans un package : le Dockerfile, les librairies, et le code de l'application.**

### Dockerfile
C'est le fichier qui indique à Docker comment construire notre image :
- Elle fait référence à une image de base, les plus populaires étant python, ubuntu, alpine.
- Une image intermédiaire par dessus l'image de base. Pour une application machine learning, typiquement charger Numpy, Pandas, et SciKit learn.

### Lancement et enregistrement
Une image docker, associée à la commande ```docker run image_name``` démarre un container avec l'image demandée.

Pour distribuer cette image, il existe le [Docker Hub](https://hub.docker.com/) qui recense toutes les images que l'on peut obtenir avec ```docker run *```


## Exemple


## Sources

[Containers & Virtualization](https://www.smartfile.com/blog/what-is-containerization-and-has-it-killed-virtualization/)
[Enough Docker to be useful](https://towardsdatascience.com/learn-enough-docker-to-be-useful-b7ba70caeb4b)
