# OpenFaas, un framework serverless au dessus de Docker et Kubernetes

Laurent Grangeau (@laurentgrangeau), Cloud solution architect, SOGETI

## Définitions

"Serverless computing is a cloud computing execution model in which the cloud provider dynamically maanges the allocation of machine resources"

## Why?

- Reduce Time-to-Market
- Easier deployment
- Scale automatically
- Developers focus on business logic
- Ops don't have to worry about patch management or system upgrades
- Leads to cost reduction

## Problematic

On alloue des serveurs pour gérer les flux entrants mais lors de grandes montées de charge, les serveurs peuvent ne pas être prêts à gérer les flux entrants et les utilisateurs ne pourront plus utiliser le service --> perte d'utilisateurs et d'argent

## How

On développe une application différente de ce qui existe habituellemment
- Quand on cherche à accéder à un site/service, on arrive sur une API Gateway
- Cette gateway va chercher la fonction qui est en rapport avec cette URL
- La fonction retourne des données
- L'API renvoit les réponses

OpenFaas est une solution open source pour travailler sur du serverless avec DOcker et Kybernetes

Deux manières de déployer avec OpenFaas : le portail avec le dépoloiement de fonctions (un peu ce qu'ils veulent, soit via la CLI ( en trois étapes avec un build, un push sur le Docker hub ou sur un registry interne puis après un déploiemnt sur OpenFaas))

## What's next

- Add an API manager (like Kong)
- Add a static storage (like Minio)
- Add some js framework (likre VueJS)