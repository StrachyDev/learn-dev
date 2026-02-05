---
title: Avertissement concernant les commentaires
---

# Avertissement concernant les commentaires

## Sommaire

- [La thèse en question](#i-la-thèse-en-question)
- [N'Écrivez. PAS. De. Commentaires. (conseil)](#ii-nécrivez-pas-de-commentaires-conseil)
    - [C'est une perte de temps titanesque](#1-cest-une-perte-de-temps-titanesque)
    - [C'est instable et dur à maintenir dans le temps](#2-cest-instable-et-dur-à-maintenir-dans-le-temps)
    - [C'est fondamentalement inutile](#3-cest-fondamentalement-inutile)
- [Réponse aux contre-arguments](#iii-réponse-aux-contre-arguments)
    - ["Tu oublieras le fonctionnement du code"](#1-tu-oublieras-le-fonctionnement-du-code)
    - ["En équipe"](#2-en-équipe)
- [Solution (#ad)](#iv-solution-ad)
    - [En complément](#en-complément)
- [Conclusion](#v-conclusion)

## I. La thèse en question

Je voulais vous avertir concernant quelque chose de répandu, non-remis en question, et adopté par beaucoup de programmeurs, y compris les professeurs.

**"Commentez le plus possible votre code"**

Ce qui veut dire l'annoter/le documenter en mettant des commentaires.\\
Par exemples :

1.
```c
    …
    int n = 0; // Le nombre d'éléments comptés, on démarre à 0
    …
```

ou bien :

2.
```c
    …
    int s = 0; // La somme totale des nombres du tableau, on démarre à 0
    …
```

Je suis d'accord dans l'idée car cela permet de faciliter grandement la compréhension du code, peu importe à quel moment on le relit.

Pour autant, je vais vous dire quelque chose qui paraît absolument incohérent :

## II. N'Écrivez. PAS. De. Commentaires. (conseil)

Et je suis clair dessus.\\
Les commentaires ne sont pas aussi utiles que ce qu'on vous vend, et ce pour plusieurs raisons :

### 1. C'est une perte de temps titanesque

Et c'est sûrement la raison la plus importante à retenir.

On disait dans [Coder proprement et efficacement](ecrire_du_code_propre.md) que sacrifier un peu de temps ou de place pour un peu plus de lisibilité est clairement acceptable, mais là, imaginez-vous deux secondes.

Pour CHAQUE ligne (ou du moins chaque action que vous documenterez)\\
**vous aurez le double du travail à faire**.

Non seulement vous devez écrire le code, mais **AUSSI** l'annoter.

La charge de travail est littéralement doublée.

Alors non, ce n'est pas acceptable de sacrifier AUTANT de temps pour gagner en compréhension, et je dis bien compréhension, car commenter son texte n'améliore pas sa lisibilité.\\
Autrement dit, si votre code est compact au possible, vous pouvez rajouter autant de commentaires que vous voulez, vous continuerez à perdre autant de temps qu'avant à essayer de le lire.

### 2. C'est instable et dur à maintenir dans le temps

Que faire si vous avez modifié le code après ?\\
Vous allez devoir réexpliquer dans les commentaires son fonctionnement, modifier les noms des variables utilisés, etc..

Les commentaires ne sont pas définitifs, au contraire, ils sont très volatiles.

On rejoint l'argument précédant ; vous doublez le travail à faire.

De même, si vous oubliez par malheur de mettre à jour vos commentaires et que vous revenez sur votre code quelque temps plus tard, en lisant vos commentaires, vous aurez une vision complètement erronée de votre code.\\
C'est tout sauf productif.

### 3. C'est fondamentalement inutile

Un programmeur (sauf dans des cas précis où le programme nécessite de mobiliser pas mal de neurones pour le comprendre) **n'a pas besoin** de commentaires pour comprendre un programme.

Un algorithme devrait être compris aussi vite qu'il est lu, c'est-à-dire d'une traite, du premier coup.

## III. Réponse aux contre-arguments

### 1. "Tu oublieras le fonctionnement du code"

**"Oui mais si tu le lis dans quelques temps sans t'en souvenir tu ne sauras plus ce que cela fait"**

C'est faux, et à minima pour une raison.

Dans [Coder proprement et efficacement](ecrire_du_code_propre.md), j'ai expressément écris de **nommer correctement ses fonctions, procédures, variables, structures, etc.**.

Si vous nommez correctement (et j'insiste sur le **correctement**) ces choses-ci, alors vous n'aurez AUCUN problème à comprendre votre code.

Que ce soit demain, la semaine prochaine, ou dans 10 ans, et ce car vous l'aurez tellement bien annoté (de par les noms utilisés, la structure, et tout ce qu'on a vu dans ce cours) que vous n'aurez juste jamais besoin de commentaires pour compléter votre compréhension.

### 2. "En équipe"

**"Oui mais si vous êtes plusieurs à travailler sur le même code"**

Dans ce cas, on sépare les tâches pour éviter ce problème et chacun applique les méthodes que j'ai donnée dans ce document.

Comme ça, même si un programmeur devait quitter l'équipe, ou si un nouveau arrive, tant qu'il sait programmer, il comprendra.

## IV. Solution (#ad)

Reprenons les exemples précédents.

1.
```c
    …
    int n = 0; // Le nombre d'éléments comptés, on démarre à 0
    …
```

2.
```c
    …
    int s = 0; // La somme totale des nombres du tableau, on démarre à 0
    …
```

Les commentaires sont tous deux inutiles.\\
Si on les retire et renomme les variables à la place :

1.
```c
    …
    int compteur = 0;
    …
```
**on peut aussi écrire "count" de l'anglais*

2.
```c
    …
    int somme = 0;
    …
```
**on peut aussi écrire "sum" de l'anglais*

… tout devient plus clair.

On a pas besoin de savoir **explicitement** par un commentaire que compteur représente le nombre d'éléments comptés ET EN PLUS qu'on démarre à 0.

On a juste à le **constater**.

compteur est initialisé à 0 et, un peu plus tard dans le code, on aura sûrement un truc du style :

```c
    …
    for (…) {
        compteur++;
    }
    …
```

On sait, et ça se voit.

Tout comme l'exemple 2., où on aura quelque chose comme :

```c
    …
    for (…) {
        somme += tableau[i];
    }
    …
```

… et même si on venait à modifier légèrement quelque chose, on comprendrait toujours.

Retenez simplement ceci :

Un **bon code compréhensible** n'est **pas** un code **rempli d'annotations et/ou entièrement documenté**,\\
c'est un code qui **se documente lui-même**.

### En complément

Je vous invite **très fortement** à lire [Coder proprement et efficacement](ecrire_du_code_propre.md), qui est une grosse extension de cette partie.

## V. Conclusion

Bref, faites ce que vous voulez.\\
Je n'essaie ni de convaincre, ni de persuader ici.\\Je tente simplement de vous apporter ma réflexion à ce sujet, et surtout en espérant vous faire gagner du temps.