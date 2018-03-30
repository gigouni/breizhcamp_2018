# 1. From a french monolith to a worldwide platform : a human story

Speaker: Stan Chollet

Dailymotion - Formateur Kubernetes et GraphQL

<!-- TOC -->

- [1. From a french monolith to a worldwide platform : a human story](#1-from-a-french-monolith-to-a-worldwide-platform -a-human-story)
    - [1.1. Transformation de la plateforme après un rachat de Dailymotion](#11-transformation-de-la-plateforme-après-un-rachat-de-dailymotion)
    - [1.2. Changement d'organisation de travail](#12-changement-dorganisation-de-travail)
    - [1.3. Timeline](#13-timeline)
    - [1.4. Conclusion](#14-conclusion)

<!-- /TOC -->

## 1.1. Transformation de la plateforme après un rachat de Dailymotion

Passage de

- Stack LAMP monolithique
- Hébergé en "bare-metal" (directement sur un serveur sans virtualisation)
- Un seul datacenter
- Une API REST

Vers une architecture

- micro-services
- géo-distribuée
- orchestrée au dessus de Kubernetes
- en plusieurs langages (Python, Go, ...)
- Une API GraphQL
- API-centrique

## 1.2. Changement d'organisation de travail

Passage en tribes et squads #spotify. Plus d'informations sur ce mode de fonctionnement sur le site [full-stackagile.com](http://www.full-stackagile.com/2016/02/14/team-organisation-squads-chapters-tribes-and-guilds/)

## 1.3. Timeline

- Le GraphQL tape sur les services pour les entités et nourrit le website
- Kubernetes on AWS (2016)
- Dès Janvier 2017, augmentation du nombre de personnes sur le projet (de 2 à 50) suite à un projet à une livraison inattendue en juin 2017 (6 mois plus tard)
- Abstraction des différents langages utilisés via des commandes make communs sur tous les projets pour gérer les différences de langages
- Les tâches make sont open source sur gazr.io (gather.io)
- Passage de AWS vers Google Cloud pour une meilleure gestion des réseaux, intégration native de Kubernetes
- Au final, ~ 150 noeuds à peu près à gérer sur cette plateforme mais toujours avec des noeuds AWS
- Contradiction: Google est le concurrent de Dailymotion mais la situation est temporaire. Le Google Cloud ne sert que de CDN
- Utilisation de Jenkins pour les pipelines d'intégration, par projet
- Utilisation de Google Cloud Federation pour gérer les clouds Kubernetes
- Problèmes détectés d'inconsistance entre les intégrations pour finalement revenir à la façon d'intégration précédente (scripts bash)
- **Morale** : ne pas forcément choisir les outils des GAFAM quand notre solution fonctionne déjà
- Utilisation de Helm (surcouche Kubernetes pour simplifier les configurations)
- Utilisation d'un cache sous le GraphQL (on peut en avoir un mais c'est nouveau avec Apollo Cache Control)

Après cela, passage de 

- Le build fait par les ingénieurs logiciels
    - Écrit le code
    - Développe les applications complexes
- Livraison par les ingénieurs d'intégration
    - Packager et déployer les applications
- Mise en route par les ingénieurs systèmes
    - Mise en place de l'infrastructure et de l'application
    - Incapables de corriger les applications par eux-mêmes

vers 

- Le build, la livraison et la mise en route par les ingénieurs de production

## 1.4. Conclusion

- Suite à un problème en production, ils ont utilisé un script de rollback de Helm pour corriger le problème
- En cas de crash en production, ne pas essayer de comprendre le problème dans l'immédiat mais relancer le produit puis APRÈS chercher la source du problème