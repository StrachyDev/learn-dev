---
title: Git
---

# Git

## Sommaire

- [Utilité](#utilité)
- [Fonctionnement](#fonctionnement)
- [Jargon](#jargon)
- [Branches](#branches)
- [Commandes](#commandes)
    - [Exemple](#exemple)

## Utilité

Git permet de **versionner** un projet de code, et de faciliter son développement lorsqu'on est plusieurs à travailler dessus.

## Fonctionnement

Il existe **deux endroits** où sont stockés les versions :
- La version **mutualisée** et généralisée, sur un serveur distant,
- Une version **locale**, sur une station de travail.

Principe : on développe toujours la version **locale**, et lorsqu'on a terminé d'apporter nos modifications, on met à jour la version **mutualisée**. <abbr title="Cela permet notamment à plusieurs personnes de travailler sur des fonctionnalités différentes sans courir le risque de casser la base de code, et si jamais c'est le cas, pouvoir restaurer une version précédante stable">ⓘ</abbr>

## Jargon

- Un **fetch**<abbr title="En français : une extraction">ⓘ</abbr> récupère la version mutualisée,
- Un **pull**<abbr title="En français : un tirage, on &quot;tire&quot; la nouvelle version mutualisée vers la machine locale">ⓘ</abbr> met à jour la version locale à partir de la version mutualisée récupérée au préalable avec **fetch**,
- Un **add**<abbr title="En français : un ajout">ⓘ</abbr> ajoute un ou plusieurs fichier(s) au futur commit,
- Un **commit**<abbr title="En français : un engagement">ⓘ</abbr> constitue une liste de modifications apportée depuis la dernière mise à jour,
- Un **push**<abbr title="En français : une poussée, on &quot;pousse&quot; la nouvelle version locale vers le serveur distant">ⓘ</abbr> met à jour la version mutualisée à partir de la version locale à partir des changements déclarés au préalable avec **commit**.

## Branches

Si un projet devient conséquent, il devient nécessaire de le diviser en plusieurs parties distinctes mais complémentaires pour en **faciliter la gestion**. Les branches sont la réponse à ce problème.

La branche principale par défaut est nommée **master**<abbr title="En français : maître">ⓘ</abbr>.

- Un **branch**<abbr title="En français : une branche">ⓘ</abbr> crée une nouvelle branche à partir de la version locale,
- Un **checkout**<abbr title="En français : une vérification">ⓘ</abbr> sélectionne une autre branche et met à jour notre version locale avec le contenu de cette même branche,
- Un **merge**<abbr title="En français : une fusion">ⓘ</abbr> fusionne deux branches. <abbr title="De potentiels conflits qu'il faudra gérer peuvent survenir">ⓘ</abbr>

Imaginons notre projet comme un **arbre**.  
Chaque **point** est une **version du projet**.  
Chaque **branche** est une **liste de version**<abbr title="Elles peuvent cependant rentrer en collision les unes avec les autres">ⓘ</abbr>.

On nomme **head**<abbr title="En français : la tête">ⓘ</abbr> le point sur lequel se trouve la version locale.

## Commandes

Une commande git est systématiquement préfixée par **git**, suivi de l'action désirée, et éventuellement d'options et de paramètres.

Les options sont des **indications**<abbr title="le &quot;comment&quot;">ⓘ</abbr> sur **comment** exécuter la commande.  
Les paramètres sont les **composants**<abbr title="le &quot;quoi&quot;">ⓘ</abbr> nécessaires au **fonctionnement** de la commande.

### Exemple :

``git commit -m "Petit commit"``

- **git commit** est la **commande** à exécuter,
- **-m** est une **option**<abbr title="Ici, inclut un message dans le commit">ⓘ</abbr>,
- **"Petit commit"** est un **paramètre**<abbr title="Ici, le message à inclure dans le commit">ⓘ</abbr>.