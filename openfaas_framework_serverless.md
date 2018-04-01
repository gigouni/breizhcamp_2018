# 1. OpenFaas, un framework serverless au dessus de Docker et Kubernetes

Laurent Grangeau (@laurentgrangeau), Cloud solution architect, SOGETI

<!-- TOC -->

- [1. OpenFaas, un framework serverless au dessus de Docker et Kubernetes](#1-openfaas-un-framework-serverless-au-dessus-de-docker-et-kubernetes)
    - [1.1. Définitions](#11-définitions)
    - [1.2. Pourquoi utiliser OpenFaas](#12-pourquoi-utiliser-openfaas)
    - [1.3. Problématique répondue par ce framework](#13-problématique-répondue-par-ce-framework)
    - [1.4. Comment fonctionne OpenFaas dans le contexte serverless](#14-comment-fonctionne-openfaas-dans-le-contexte-serverless)
    - [1.5. Que rajouter ou faire ensuite](#15-que-rajouter-ou-faire-ensuite)

<!-- /TOC -->

## 1.1. Définitions

> "Serverless computing is a cloud computing execution model in which the cloud provider dynamically manages the allocation of machine resources"

## 1.2. Pourquoi utiliser OpenFaas

- Réduction du Time-To-Market (temps nécessaire avant une commercialisation d'un produit)
- Déploiement plus facile
- Mise à l'échelle plus facile
- Les développeurs peuvent rester concentrer sur le code métier
- Les ops n'ont pas à se soucier des problèmes de patch ou de mises à jour systèmes
- Mène à des réductions de coût

## 1.3. Problématique répondue par ce framework

On alloue des serveurs pour gérer les flux entrants mais lors de grandes montées de charge, les serveurs peuvent ne pas être prêts à gérer les flux entrants et les utilisateurs ne pourront plus utiliser le service --> perte d'utilisateurs et d'argent

## 1.4. Comment fonctionne OpenFaas dans le contexte serverless

On développe une application différente de ce qui existe habituellemment
- Quand on cherche à accéder à un site/service, on arrive sur une API Gateway
- Cette gateway va chercher la fonction qui est en rapport avec cette URL
- La fonction retourne des données
- L'API renvoit les réponses

OpenFaas est une solution open source pour travailler sur du serverless avec Docker et Kubernetes

Deux manières de déployer avec OpenFaas : le portail avec le dépoloiement de fonctions (un peu ce qu'ils veulent), soit via la CLI ( en trois étapes avec un build, un push sur le Docker hub ou sur un registry interne puis après un déploiemnt sur OpenFaas)

## 1.5. Que rajouter ou faire ensuite

- Ajouter un gestionnaire d'API (comme Kong)
- Ajouter un stockage statique (comme Minio)
- Ajouter un framework JS (comme VueJS)