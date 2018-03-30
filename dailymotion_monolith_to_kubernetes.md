# 1. From a french monolith to a worldwide platform : a human story

Speaker: Stan Chollet

Dailymotion - Formateur Kubernetes et GraphQL

<!-- TOC -->

- [1. From a french monolith to a worldwide platform : a human story](#1-from-a-french-monolith-to-a-worldwide-platform -a-human-story)
    - [1.1. Transformation de la plateforme après un rachat de Dailymotion](#11-transformation-de-la-plateforme-après-un-rachat-de-dailymotion)
    - [1.2. Changement d'organisation de travail](#12-changement-dorganisation-de-travail)
    - [1.3. Technique](#13-technique)

<!-- /TOC -->

## 1.1. Transformation de la plateforme après un rachat de Dailymotion

From

- monolith LAMP stack
- hosted on bare-metal
- mono-datacenter
- REST API
- fullstack website

To (SOA architecture)

- geo-distributed
- apps runs in container (docker)
- orchestrated on top of Kubernetes
- multiple languages (python, golang, ...)
- GraphQL API
- fully API Centric

## 1.2. Changement d'organisation de travail

Passage en tribes et squads #spotify

## 1.3. Technique

- Le GraphQL tape sur les services pour les entités et nourrit le website
- Kubernetes on AWS (2016
- Dès Janvier 2017, augmentation du nombre de personnessur le projet (2 to 50) suite à un projet à livrer en juin 2017
- Abstraction des différents langages utilisés via des commandes make communs à tous les langages
- Les tâches sont open source sur gazr.io (gather.io)
- PAssage de AWS vers Google Cloud pour une meilleure gestion des réseaux, intégration native de Kubernetes
- Au final, ~ 150 noeuds à peu près à gérer sur cette plateforme mais toujours avec des noeuds AWS
- Contradiction: Google est le concurrent de Dailymotion mais la situation est temporaire. Le Google Cloud ne sert que de CDN
- Utilisation de JEnkins pour les pieplines d'intégration, par projet
- Utilisation de Google Cloud Federation pour gérer les clouds Kubernetes
- Problèmes détectés d'inconsistance entre les intégrations pour finalement revenir à la façon d'intégration précédente (scripts bash)
- Morale : ne pas forcément choisir les outils des GAFAM quand notre solution fonctionne déjà
- Utilisation de Helm (surcouche Kubernetes pour simplifier les configurations)
- Utilisation d'un cache sous le GraphQL (on peut en avoir un mais c'est nouveau avec Apollo Cache Control)

From

- Build by software engineer
    - Write code
    - Build applications which aren't easy to operate
- Ship by release engineer
    - Package and deploy applications
- Run by system engineer
    - Operate infrastrucutre & app
    - Unable to fix applications by themselves

To

- Build / Ship / Run by production engineer

- Suite à un problème en production, ils ont utilisé un script de rollback de Helm pour corriger le problème
- En cas de crash en production, ne pas essayer de comprendre le problème dans l'immédiat mais relancer le produit puis APRÈS chercher la source du problème