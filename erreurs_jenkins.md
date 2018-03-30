# Les erreurs à ne pas faire avec Jenkins

Adrien et Damien, CloudBees

## Historique et informations de fonctionnement

- Initialement, on parlait d'Hudson mais ça a été racheté
- Les agents sont des machines utilisées par Jenkins pour déléguer le travail. Utile si le build corrompt la machine
- Nombre d'exécuteurs (workers) == nombre de coeurs CPU
- Nouvelles façons de consommer Jenkins
    - [Jenkins X (tout public)](https://goog.gl/rbZBNd) --> Kubernetes
    - [Jenkins Essentials](https://goog.gl/o6A7mr) --> Version minimale de Jenkins, avec une configuration minimale et une gestion primitive
    - [Configuration-as-code](https://goog.gl/5Bz29F)
- Jenkins est un produit open source
    - La communauté est importante, il faut l'entretenir en l'aidant
    - Voter pour la LTS
    - Participer à la doc sur [jenkins.io](http://jenkins.io)
    - Participer aux conférences Jenkins

## Installation

- Utilisation d'une image Docker Jenkins
- Faire attention à la version de Jenkins (version de l'image)
- Prendre des versions LTS pour la production

## Configuration

- Dépend de l'agent
- On peut créer des agents à la volée
    - EC2
    - Kubernetes
    - Docker Swarm
- Penser au Jenkinsfile
- Faire des pipelines, du multibranch pipeline ou de l'organisation par dossier ou passer par le couplage avec GitHub/BitBucket pour faire en sorte que Jenkins fasse lui-même des recherches sur tous les projets ayant des Jenkinsfile
- Partager les librairies/binaires au lieu de les copier
- Configurer des builds à chaque push/merge requests mais ne garder que les vingt derniers builds pour ne pas surcharger le disque dur
- Utiliser archiveArtifact pour gérer la notion d'historique et pour aider aux debugs ou comprendre les erreurs lors des tests
- Partage sur le réseau
    - Snapshots
    - Disaster recovery
- Stockage local pour war et plugins
- Ne pas oublier de faire de back-ups sur une autre machine
- Ajouter le plugin **Blue Ocean** (plugin React) pour surcharger l'interface existante et ajouter des fonctionnalités d'un côté utilisateur
- Faire attention aux configurations dans le cadre de JVM
- Être sûir que la machine hôte est accessible en SSH ou bureau à distance pour que les utilisateurs puissent s'en servir

## A ne pas faire

- Changer de dossier en dehors du workspace, la struture peut changer et le job peut être renommé
- Builder sur master, on build plutôt sur l'agent car sur master, on a accès à tout (les credentials, ...)
- Se servir de Jenkins comme un serveur web, on ne tape pas dessus pour récupérer/gérer des fichiers de build
- Copier les jobs pour plusieurs projets est bien mais attention
    - il faudra répliquer toutes modifications ultérieures
    - faire attention aux noms des binaires, plugins dans les configurations
    - faire attention aux bugs, si on copie tout
- Toutes les équipes ne doivent pas voir ce qui se passe sur les projets des autres
- Avoir plus de 500 jobs qui tournent sur le même Jenkins
- Avoir plus de 4-5 équipes sur le même Jenkins
- Rester sur la même version en permanence, même si c'est stable ne serait-ce que pour faire des mises à jour de sécurité
- Downgrade après un fail sur un upgrade
- Ne pas faire de back-ups avant de faire de mises à jour