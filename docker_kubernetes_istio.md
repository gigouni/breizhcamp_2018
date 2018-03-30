# 1. Transformer une application legacy avec Kubernetes et Istio

Speaker: David Gageot, developer advocate Google

[Lien vers un comic fait sur le sujet](https://cloud.google.com/kubernetes-engine/kubernetes-comic/)

<!-- TOC -->

- [1. Transformer une application legacy avec Kubernetes et Istio](#1-transformer-une-application-legacy-avec-kubernetes-et-istio)
    - [1.1. Kubernetes](#11-kubernetes)
    - [1.2. Istio](#12-istio)
    - [Attention](#attention)

<!-- /TOC -->

## 1.1. Kubernetes

- On part d'une application monolithique (Java PetStore EE7) pour construire cette application avec Kubernetes et Istio
- On construit l'application avec un Docker en multi-stage (un pour le build, un autre pour le déploiement)
- Kubernetes es un logiciel que l'on installe sur un cluster de machines pour gérer des conteneurs
- Kubernetes a une configuration en YAML (typo proche de Docker Compose)
- On veut envoyer les deux fichiers (Dockerfile + configuration YAML) via un cycle
- La gestion de Kubernetes se fait en oigne de commande avec `kubectl`
- Un pod est un container qui tourne sur un noeud
- On va ajouter un système de proxy pour pouvoir accéder au PetStore (Nginx)
  - Ajout de gestion des gzip, ajout d'une 404 et URL rewriting
- Ajout d'un conteneur pour le front via le fichiers de configuraiton de Kubernetes
- On change les configurations de Kubernetes via le pattern Façade pour changer des notions comme l'URL d'accès au site
- Ingress est une autre fonctionnalité de Kubernetes qui permet notamment de changer les URL
- Sur Mac, on peut activer Kubernetes via Docker dans les configurations en cochant "Activer Kubernetes"
- Google propose Google Kubernetes Engine pour, en une ligne de commande, lancer un Kubernetes avec une résilience des données
- Pour en savoir plus, aller sur [Google Cloud](https://cloud.google.com/kubernetes-engine/kubernetes-comic/)

## 1.2. Istio

- Istio est un ensemble de containers qui viennent se mettre par dessus les conteneurs de Kubernetes pour ajouter des fonctionnalités
- On  crée deux copies des deux fichiers pour gérer une version en staging pour faire les tests de validation
- On veut faire du load balancing sur les deux versions pour faire de l'A/B Testing mais Kubernetes ne permet pas de le faire (très complexe)
- RouteRule un gestionnaire intelligent de routes très utile
- On modifie un fichier de configuration de Kubernetes avec `kubectl edit -f filename`. Ça ouvre un éditeur et à la sauvegarde de ce dernier, Kubernetes se recharge et permet de prendre en compte automatiquement les différences
- On ajoute un service Graphana sur le cluster pour faire du monitoring en temps réel grâce à Promoetheus qui renvoit les métriques
- On éclate la monolith pour avoir un micro service pour le front
- La compréhension de ce qui se passe peut vite être compliqué si on a plusieurs versions différentes à gérer avec plusieurs micro-services qui tournent en même temps
- Istio propose un service de graphes `kubectl -n istio-system plugin forward servicegraph`
- On peut ajouter des policies entre les services
- On peut injecter des timeouts, des erreurs entre tels services pour vérifier les réactions du système
- On peut limiter le nombre de requêtes qui arrivent sur les services pour éviter que l'application ne casse

## Attention

- Istio n'est pas considéré comme production ready car il y a des breaking changes
- La démo a lieu sur le 0.4 même si la 0.7 sort bientôt
- La v1 sera production ready
- Depuis Istio 0.5, il faut utiliser Kubernetes 1.9