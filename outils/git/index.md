# Git

## Utilité

Git permet de **versionner** un projet de code, et de faciliter son développement lorsqu'on est plusieurs à travailler dessus.

## Fonctionnement

Il existe **deux endroits** où sont stockés les versions :
- La version **mutualisée** et généralisée, sur un serveur distant,
- Une version **locale**, sur une station de travail.

Le principe est le suivant : lorsqu'on développe notre projet, on développe toujours la version **locale**, et lorsqu'on a terminé d'apporter nos modifications, on met à jour la version **mutualisée**. Cela permet notamment à plusieurs personnes de travailler sur des fonctionnalités différentes sans courir le risque de casser la base de code, et si jamais c'est le cas, pouvoir restaurer une version précédante stable.

## Jargon

- Un **fetch** récupère la version mutualisée,
- Un **pull** met à jour la version locale à partir de la version mutualisée récupérée au préalable avec **fetch**,
- Un **add** ajoute un ou plusieurs fichier(s) au futur commit,
- Un **commit** constitue une liste de modifications apportée depuis la dernière mise à jour,
- Un **push** met à jour la version mutualisée à partir de la version locale à partir des changements déclarés au préalable avec **commit**.

## Branches

Si une grosse équipe sur un projet, il devient nécessaire de le diviser en plusieurs parties distinctes mais complémentaires pour en **faciliter la gestion**. Les branches sont la réponse à ce problème.

La branche principale par défaut est nommée **master** *(maître)*.

- Un **branch** crée une nouvelle branche à partir de la version locale,
- Un **checkout** sélectionne une autre branche et met à jour notre version locale avec le contenu de cette même branche,
- Un **merge** fusionne deux branches *(de potentiels conflits qu'il faudra gérer peuvent survenir)*.

Imaginons notre projet comme un **arbre**.
Chaque **point** est une **version du projet**,
Chaque **branche** est une **liste de version** qui peuvent rentrer en collision mais permettent de **séparer le travail** en plusieurs équipes pour ensuite les fusionner.

On nomme **head** *(tête)* le point sur lequel se trouve la version locale.

## Commandes

Une commande git est systématiquement préfixée par **git**, suivi de la commande désirée, et éventuellement d'options et de paramètres.

Les options sont des **indications** sur **comment exécuter la commande** (le *comment*).
Les paramètres sont les **éléments** nécessaires au **fonctionnement de la commande** (le *quoi*).

### Exemple :

git commit -m "Petit commit"

- **git commit** est la **commande à exécuter**,
- **-m** est une **option de la commande** permettant d'inclure un message dans le commit,
- **"Petit commit"** est un **paramètre de la commande**, le message à inclure dans le commit.