---
published: true
title: "Architectures scalables avec les solutions Apache"
excerpt: "Cassandra, Kafka, Spark, Elastic"
toc: true
toc_sticky: true
toc_label: "Apache Scalable"
toc_icon: "align-center"
comments: true
header:
overlay_image: "assets/images/nn1/cover.jpg"
teaser: "assets/images/nn1/cover.jpg"
categories: []
---

Les technologies open-source Apache sont présentes dans la quasi-totalité des architectures distribuées. Avec plus de <a href="https://streamdata.io/blog/open-source-apache-big-data-projects/" target="_blank">30 projets</a> actifs rien que pour les problématiques data, Apache est un incontournable pour construire un architecture. Dans cet article je détaille quatre solutions open-source très répandues, rapides, et scalables.

# Apache Cassandra

Cassandra a été développé par Facebook et rendu open-source en 2008. C'est un SGBD de type NoSQL qui répond aux contraintes suivantes :
- Stocker un volume massif de données
- Assurer la haute disponibilité des données
- Répartir les données sur plusieurs noeuds
- Éviter les 'single point of failure'

Cassandra peut être vu comme une table de hashage grand volumes. Chaque donnée stockée dans le système possède un identifiant unique. C'est grâce à une table de correspondance de chacun de ces identifiants que les données sont réparties à travers les différents serveurs : il existe plusieurs mécanismes de répartition, et de réplication.

## Quand l'utiliser

- Transactionnel
- Stockage Cross-DC
- Forte contraintes de disponibilité, SLA 99.999%

## Quand ne pas l'utiliser

- Analytics & Data warehouse
- Applications temps réel et visualisation AdHoc
- Ne respecte pas ACID (?) notamment l'isolation
- Utiliser Cassandra comme une file d'attente

# Apache Kafka

Kafka est une solution très populaire pour la gestion de files de messages. C'est un système qui centralise les flux, un Hub. Comme pour les aéroports, le traffic est centralisé et géré efficacement. Le fonctionnement de Kafka est articulé autour de plusieurs éléments : 
- Les **topics**, qui sont des files de messages, où les messages s'accumulent.
- Les **producers** qui produisent des messages et les stockent dans un ou plusieurs topics.
- Les **consumers** qui consomment les messages d'un ou plusieurs topics.

## Quand l'utiliser

- Micro-services
- Message bus, metrics
- Data masking, filtering avec Kafka streams (tâches de transformation)

## Quand ne pas l'utiliser

- Ne pas utiliser Kafka comme une source de données
- Traiter toutes les données séquentiellement depuis un topic.
- Les cas de contraintes temps réel ne sont pas adaptés.

# Apache Spark

Apache Spark propose une alternative plus performante au paradigme MapReduce. Spark est capable de s'executer selon différents schemas :
- En mode **stand-alone**, en local sur un laptop par exemple.
- **YARN**, le négociateur de ressources du framework Hadoop.
- **Mesos**, le scheduler pour gérer les ressources d'un datacenter (similaire à YARN mais cadre plus large).
- **Kubernetes**, déploiement automatisé d'application en containers.

## Quand l'utiliser

- Quand on souhaite travailler sur de **gros volumes de données**. Spark n'est pas adapté aux traitements de faible volumes, en effet, les jobs ont besoin de temps pour être déployés et pour se lancer. Une fois passé ce temps de lancement, la valeur ajoutée de Spark augmente avec le volume de données traitées.
- Pour les tâches dites d'**ETL (Extract, Transform, Load)** : Spark est idéal pour créer des pipelines des données, dans lesquels on peut intégrer des opérations de transformations complexes sur le schema de données, des jointures.
- Faire des opérations AdHoc et des requêtes exploratoires complexes.

## Quand ne pas l'utiliser

Spark ne convient pas pour des opérations en temps réel, en raison du temps de mise en route élevé.

# Elasticsearch (Apache Lucene)

ElasticSearch est open source, et il est basé sur la solution Apache Lucene. Elasticsearch est aujourd'hui très répandu dans les contextes big data car il propose des temps de réponse très faibles pour explorer les données en mode 'moteur de recherche'. Il est basé sur les éléments suivants :

A l'intérieur d'Elasticsearch les données sont réparties sous forme de **documents** dans des **index**. A l'intérieur d'un index, chacun des documents possèdent les mêmes champs.

## Quand l'utiliser

- Applications de recherche dans des données full-text
- Très pratique pour les GeoData
- Agréger et croiser différentes sources de données.

## Quand ne pas l'utiliser

- On n'utilise pas Elasticsearch comme une base de données. On lui adresse des **recherches**, qui sont différentes des requêtes en bases de données. Une recherche ne renvoie pas un résultat exacte, mais s'effectue beaucoup plus rapidement qu'une requête structurée dans une base de données.
- Comme source de données, Elasticsearch ne convient pas. Comme vu au premier point, on ne peut pas lui adresser de requêtes, ainsi les données obtenues ne respectent pas les contraintes que l'on peut attendre d'une BDD classique.

# Exemples d'architecture

## Microservices

Pour les micro services, Kafka est l'outil de prédilection, il centralise les flux grâce à ses nombreux connecteurs. Les demandes utilisateur peuvent être regroupées en topics afin de consommer les tâches au rythme le plus adapté et de répartir la charge.

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/architectures/kafka-microservices.png" alt="" class="center">

## ETL

Les données sont réparties dans divers systèmes de stockage selon les besoins et les usages qui en sont fait. Ici on se sert essentiellement de Spark pour des opérations ETL de migration ou d'enrichissement entre ces espaces de stockage.

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/architectures/spark-etl.png" alt="" class="center">

## Objets connectés

Les données collectées sont rassemblées dans Kafka, qui répartit les flux vers chaque système approprié pour le traitement.

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/architectures/kafka-iot.png" alt="" class="center">

# Images
<img src="https://cdn-images-1.medium.com/max/1600/1*f9a162GhpMbiTVTAua_lLQ.png" alt="" class="center">

# Sources
- <a href="https://towardsdatascience.com/its-only-natural-an-excessively-deep-dive-into-natural-gradient-optimization-75d464b89dbb" target="_blank">Nombreux articles sur la descente de gradient</a> (TowardsDataScience) 
- <a href="https://www.coursera.org/learn/neural-networks-deep-learning/home/welcome" target="_blank">Deep Learning course</a> (Coursera - Andrew Ng)
