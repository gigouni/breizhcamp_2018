# 1. Applications temps réel avec GraphQL

Benjamin Plouzennec et Mahdi Aici, Zenika

<!-- TOC -->

- [1. Applications temps réel avec GraphQL](#1-applications-temps-réel-avec-graphql)
    - [1.1. Problème soulevé](#11-problème-soulevé)
    - [1.2. Comment faire alors](#12-comment-faire-alors)
    - [1.3. Le temps réel et les Subscriptions](#13-le-temps-réel-et-les-subscriptions)
    - [1.4. Architecture](#14-architecture)
    - [1.5. Démos](#15-démos)
    - [1.6. Autres nouveautés](#16-autres-nouveautés)
    - [1.7. Avantages de GraphQL](#17-avantages-de-graphql)

<!-- /TOC -->

## 1.1. Problème soulevé

Les API REST telles qu'elles sont actuellement renvoit trop de données (overdata) et demande de faire des jointures gourmandes (overfetching).

_Solutions possibles_

1. Utiliser un paramètre `fields` dans la requête avec l'ensemble des champs demandés
1. Utiliser un custom endpoint pour que la requête ne renvoit que ce qui est réellement désiré

La première solution amène une complexité, tant côté frontend que backend. Si l'on veut pleins de champs sans pour autant tout prendre, on peut vite s'y perdre.

La deuxième solution est sale. Pas vraiment sûr d'avoir besoin de détailler plus que ça ...

## 1.2. Comment faire alors

**GraphQL !**

- Le backend n'a qu'un seul endpoint (plus besoin de se demander sur quelle route il faut taper)
- Passage en payload d'un Objet Query { ... }
- C'est une spécification
- Utilisation possible de ̀ Mutations` pour utiliser des fonctions
- Plusieurs langages utilisables (Javascript, Go, Scala, ...)
- Pluggable sur plusieurs types de backend
  - PostgreSQL
  - Elastic
  - REST
  - etc...

## 1.3. Le temps réel et les Subscriptions

On fait de moins en moins de F5, on s'attend de plus en plus à avoir des données "fraîches" via des systèmes de notifications par exemple

Pour répondre à ça, deux solutions avec GraphQL

- le **pooling**: demande régulière au serveur pour savoir si les données ont changé
    - -> Coûteux car on interroge régulièrement le serveur pour des données qui ne changent pas forcément = plus de traffic inutile
- le **push**: le serveur prévient le client de modifications (via des Web Sockets par exemple)

## 1.4. Architecture

- GraphQl vient avec des briques, des modules pré-fait afin de facilité le branchement de GraphQL avec différents backend
- Dans la démo, ils utilisent `gql-subscriptions-back` et `gql-subscriptions-front`
- Ajout d'une brique `notify` pour prévenir le front via des Web Sockets
- Dans le schéma, ajout d'un type Root Subscription

## 1.5. Démos

- Première préparation du démo sur une application collaborative de dessin avec des formes géométriques et des drag&drop
  - Les événements soulevés par le drag&drop sont gourmands et passent par de l'HTTP et non pas les Web Sockets ouvertes pour GraphQL
  - Nécessité de changer d'application car GraphQL n'était pas une choix optimale de technos dans ce cas
- Deuxième tentative d'application : un tchat
  - Scaling des serveurs GraphQL avec plusieurs clients
  - Il est marqué dans la documentation d'Apollo qu'il ne faut pas le faire car il n'y a pas de moyen autre que F5 pour notifier les autres clients lors du push de la mutation
  - solution trouvée pour régler le problème : un système de pub/sub

## 1.6. Autres nouveautés

- Live Query (expérimental mais peut-être utilisable dici quelques mois)

```javascript
Query @live {
    orgas {
        name
    }
}
```

## 1.7. Avantages de GraphQL

- Centralisation des données (un seul endpoint)
- Optimsation
- Subscription