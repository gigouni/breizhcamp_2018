# 1. Machine learning for dummies

"Tout ce que vous avez toujours voulu savoir sur le machine learning"

Conférence par Cérès Carton, data scienttist chez Energiency

<!-- TOC -->

- [1. Machine learning for dummies](#1-machine-learning-for-dummies)
    - [1.1. Principe](#11-principe)
    - [1.2. Mesurer les performances](#12-mesurer-les-performances)
    - [1.3. Types de résultats](#13-types-de-résultats)
    - [1.4. Corrélation VS causalité](#14-corrélation-vs-causalité)
    - [1.5. Familles d'algorithmes](#15-familles-dalgorithmes)
        - [1.5.1. Exemple de méthodes à base d'arbre](#151-exemple-de-méthodes-à-base-darbre)
        - [1.5.2. Avantages des arbres de décision](#152-avantages-des-arbres-de-décision)
        - [1.5.3. Inconvénients des arbres de décision](#153-inconvénients-des-arbres-de-décision)
        - [1.5.4. Autres méthodes](#154-autres-méthodes)
    - [1.6. Réseaux de neurones (RN)](#16-réseaux-de-neurones-rn)
    - [1.7. Deep learning](#17-deep-learning)
    - [1.8. Résultats mauvais, que faire](#18-résultats-mauvais-que-faire)
    - [1.9. Conclusion](#19-conclusion)

<!-- /TOC -->

## 1.1. Principe

- On a des données, un algorithme et on en tire des informations
- Plusieurs types de ML : le non supervisé (on ne sait pas ce que l'on cherche) et supervisé (on sait ce que l'on cherche)
- Apprentissage supervisé (classification) : prédire une variable catégorielle
- Apprentissage supervisé (régression) : prédire une variable quantitative
- Pour l'algorithme, on travaille sur un modèle afin de trouver une formule qui permette de s'approcher au mieux de la réalité
- Aucun modèle n'est parfait
 - Typiquement, on ne devrait pas donner un pourcentage de votes pour les candidats d'élection mais plutôt un intervalle de valeurs de pourcentage de votes

## 1.2. Mesurer les performances

- Régression
  - Mesure de l'écart entre prédiction et réalité
- Classification
  - Est-ce que la prédiction est correcte ?

## 1.3. Types de résultats

- *Underfitting* : les résultats sont majoritairement faux
- *Overfitting* : le bon élève, celui qui a bien appris son cours mais par coeur. Donc quand on lui présente quelque chose qu'il ne connaît pas, il rate
- *Juste ce qu'il faut* : un élève qui réussit globalement autant ce qu'il connaît que ce qu'il ne connaît pas encore

## 1.4. Corrélation VS causalité

- Corrélation : faire le lien entre des résultats proches (attaques de requins et achat de glaces en été par exemple)
- Causalité : en été, il y a plus de monde donc plus d'achat de glaces et potentiellement plus de gens sur les plages donc plus d'attaques

La corrélation mène souvent à de mauvaises interprétations

## 1.5. Familles d'algorithmes

- Modèles linéaires
- Méthodes à base d'arbres (couteau suisse, applicable à beaucoup de cas)
- Réseaux de neurones

### 1.5.1. Exemple de méthodes à base d'arbre

Prédiction des chances de survie des passagers du Titanic

- Récupération de plusieurs informations sur les passagers (âge, famille présente sur le bateau, etc ...)
- Partir de base sur un seul noeud. Cela donne 40% d'erreur possible mais avec plusieurs classes représentées
- On divise en deux sur le genre de la personne
  - On voit que le fait d'être une femme permettait d'avoir près de 75% de chances de survivre contre seulement 40% pour un homme
- On redécoupe en deux pour purifier encore un peu plus les résultats
  - On découpe sur l'âge. On voit que les personnes de moins de 13 ans avaient plus de chances de survivre ("les femmes et les enfants d'abord")
  - On remarque qu'en fonction de la classe 1, 2 ou 3 de la personne, on remarque qu'une femme en troisième classe avait plus de chance de mourir qu'une femme de première classe
- On continue de diviser jusq'à arriver dans un cas d'overfitting
- On a trop divisé sur trop de critères et la règle n'est plus applicable à d'autres éléments
- Il faut savoir ne pas trop diviser pour garder un résultat utilisable
- On ne continue pas si on a moins de 5 personnes dans chaque noeud pour éviter de ne cibler qu'une ou deux personnes

### 1.5.2. Avantages des arbres de décision

- Faciles à comprendre et à visualiser
- Peu de préparation des données
- Interprétation rapide et claire des résultats
- Besoin de "peu" de points de données (entre 300 et 400 points de données minimum)

### 1.5.3. Inconvénients des arbres de décision

- Pas très performant
- Pas très robuste (faire des coupures étranges quand on a des variables complexes)

### 1.5.4. Autres méthodes

- Méthode de bagging ("plusieurs avis valent mieux qu'un")
- Random forest
- Méthode boosting ("on apprend plus que de nos erreurs que de nos succès")
  - on fait une première séparation d'élements dans un ensemble triés et pour les éléments mal triés, on augmente leur importance dans l'algorithme de tri, de manière récursive jusqu'à que l'on trouve tous les éléments recherchés

## 1.6. Réseaux de neurones (RN)

On essaye de reproduire le comportement du cerveau avec des neurones artificiels

- un neurone = un peitt modèle : on prend des données que l'on vient faire une somme pondérée, on passe cela dans une fonction d'activation pour obtenir un résultat
- un RN commence par une couche d'entrées, puis des couches cachées puis une couche de sortie
- Pour chaque neoud d'entrée, on le fait passer par chaque noyau des couches cachées
- Des opérations peuvent revenir en arrière pour modifier des calculs, d'où la lenteur extrême des réseaux de neurones
- Il y a plusieurs d'architectures de RN, en fonction des données à traiter et des résultats recherchés (régression, classification binaire, classification multinomiale)
- on rend plus robuste l'algorithme en lui demandant de synthétiser en permanence, ainsi il ne peut pas apprendre par coeur

## 1.7. Deep learning

- Concrètement ? Réseau de neurones avec beaucoup de couches cachées
- Pourquoi ? Apprendre automatiquement les features
- Utilisation ? Traitement d'iamges, Google Translate, ...
- Peut plus ou moins trouver lui-même les variables, contrairement aux autres outils de machine learning
- Besoin de plusieurs milliers de points de données pour être utile/efficace

## 1.8. Résultats mauvais, que faire

- Pas assez de données ?
- Données non représentatives ?
- Mauvais choix de modèle ?
- Features manquantes ?
- Overfitting ?
- Les résidus ont-ils une forme trop décalés de la ligne de recherche ? Si oui, il manque peut-être une donnée d'étude. Si non, on se retrouve avec un modèle disparate représentative des résultats

## 1.9. Conclusion

- Un algorithme est quelque chose de très "bête", il n'a pas l'intelligence de ne pas répondre quand il n'a pas la réponse, il cherchera toujours à donner une réponse, quitte à ce qu'elle soit erronée