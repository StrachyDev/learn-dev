---
title: Git
---

# Git

## Utilité

Git permet de **versionner** un projet de code, et de faciliter son développement lorsqu'on est plusieurs à travailler dessus.

## Fonctionnement

Il existe **deux endroits** où sont stockés les versions :
- La version **mutualisée** et généralisée, sur un serveur distant,
- Une version **locale**, sur une station de travail.

Principe : on développe toujours la version **locale**, et lorsqu'on a terminé d'apporter nos modifications, on met à jour la version **mutualisée**. <span title="Cela permet notamment à plusieurs personnes de travailler sur des fonctionnalités différentes sans courir le risque de casser la base de code, et si jamais c'est le cas, pouvoir restaurer une version précédante stable">ⓘ</span>

## Jargon

- Un **fetch**<span title="En français : une extraction">ⓘ<span> récupère la version mutualisée,
- Un **pull**<span title="En français : un tirage, on &quot;tire&quot; la nouvelle version mutualisée vers la machine locale">ⓘ<span> met à jour la version locale à partir de la version mutualisée récupérée au préalable avec **fetch**,
- Un **add**<span title="En français : un ajout">ⓘ<span> ajoute un ou plusieurs fichier(s) au futur commit,
- Un **commit**<span title="En français : un engagement">ⓘ<span> constitue une liste de modifications apportée depuis la dernière mise à jour,
- Un **push**<span title="En français : une poussée, on &quot;pousse&quot; la nouvelle version locale vers le serveur distant">ⓘ<span> met à jour la version mutualisée à partir de la version locale à partir des changements déclarés au préalable avec **commit**.

## Branches

Si un projet devient conséquent, il devient nécessaire de le diviser en plusieurs parties distinctes mais complémentaires pour en **faciliter la gestion**. Les branches sont la réponse à ce problème.

La branche principale par défaut est nommée **master**<span title="En français : maître">ⓘ<span>.

- Un **branch**<span title="En français : une branche">ⓘ<span> crée une nouvelle branche à partir de la version locale,
- Un **checkout**<span title="En français : une vérification">ⓘ<span> sélectionne une autre branche et met à jour notre version locale avec le contenu de cette même branche,
- Un **merge**<span title="En français : une fusion">ⓘ<span> fusionne deux branches. <span title="De potentiels conflits qu'il faudra gérer peuvent survenir">ⓘ<span>

Imaginons notre projet comme un **arbre**.  
Chaque **point** est une **version du projet**.  
Chaque **branche** est une **liste de version**<span title="Elles peuvent cependant rentrer en collision les unes avec les autres">ⓘ<span>.

On nomme **head** *(tête)* le point sur lequel se trouve la version locale.

## Commandes

Une commande git est systématiquement préfixée par **git**, suivi de la commande désirée, et éventuellement d'options et de paramètres.

Les options sont des **indications**<span title="le &quot;comment&quot;">ⓘ<span> sur **comment** exécuter la commande.  
Les paramètres sont les **composants**<span title="le &quot;quoi&quot;">ⓘ<span> nécessaires au **fonctionnement** de la commande.

### Exemple :

``git commit -m "Petit commit"``

- **git commit** est la **commande** à exécuter,
- **-m** est une **option**<span title="Ici, inclut un message dans le commit">ⓘ<span>,
- **"Petit commit"** est un **paramètre**<span title="Ici, le message à inclure dans le commit">ⓘ<span>.