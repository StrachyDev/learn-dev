---
title: Gestion de la mémoire
---

# Gestion de la mémoire : comment ne pas faire exploser son pc

## Sommaire

- [Explication du concept de mémoire](#explication-du-concept-de-mémoire)
    - [La pile (stack)](#la-pile-stack)
    - [Le tas (heap)](#le-tas-heap)
    - [Différences entre stack et heap](#différences-entre-stack-et-heap)
- [Syntaxe](#syntaxe)
    - [Types](#types)
    - [Opérateurs](#opérateurs)
    - [Note](#note)
    

## Explication du concept de mémoire

Pour faire simple, un PC a ce qu'on a de la mémoire et doit la gérer à travers ses processus. La mémoire est un espace de stockage pour l'ordinateur. Il y stocke ce dont il a besoin pour exécuter des tâches ou des programmes. Toute variable déclarée dans un programme y est stockée.

Dans cette mémoire, on y retrouve deux parties :

### La pile (stack)

C'est la plus couramment utilisée.
Celle qui est utilisée lorsque vous déclarez une variable toute simple, par exemple :

```c
int compteur = 0;
```

Sa gestion par le développeur et la machine sont simplissimes.
Lorsque vous sortez du contexte où la variable est déclarée/utilisée, la mémoire est libérée automatiquement, sans action nécessaire du programmeur.

### Le tas (heap)

Là ça devient rigolo

La heap est une mémoire à la fois très flexible et permissive mais aussi très difficile à contrôler.

Grossièrement, l'ordinateur vous y donne le contrôle total, sans qu'il n'y fasse quoi que ce soit.
Vous devez :
- déclarer la variable
- y allouer la mémoire
- l'utiliser pour vos besoins
- libérer la mémoire

Même des développeurs seniors galèrent parfois, donc faut être vigilant.

Par exemple, en C :
```c
int* compteur = malloc(1 * sizeof(int));
compteur[0] = 0;

// utilisation...

// on libère la mémoire et on NE TOUCHE PLUS A COMPTEUR APRES
free(compteur);

// on marque compteur à NULL pour éviter d'accéder à nouveau à l'espace mémoire préalablement libéré, car si cet espace est à nouveau réservé, compteur peut y accéder, et on ne veut pas ça car ça peut entraîner des erreurs furtives et insupportables à corriger/débugger.
*(&compteur) = NULL;
```

Ce code revient strictement à la même chose que celui au-dessus, mais on préfèrera utiliser la stack si possible (vous comprenez pourquoi).

### Différences entre stack et heap

C'est grâce à la heap qu'on peut faire des tableaux dynamiques, car si par exemple j'aurai voulu avoir un tableau de 5 entiers, j'aurais pu faire la manière traditionnelle

```c
int compteurs[5];
compteur[0] = 0;
compteur[1] = 0;
// ...
```
ou bien avec la heap :

```c
int* compteur = calloc(5, sizeof(int));
```

La différence entre malloc et calloc est que calloc fait pareil que malloc mais en plus met toute la mémoire réservée à 0.

La heap est très utile pour avoir une mémoire persistante, c'est-à-dire qui survit à son contexte.
Par exemples :

```c
// ...
{
    int compteur = 0;
    // on utilise compteur

    // à la fin du contexte (défini par les accolades), compteur est libéré et on ne peut plus y accéder
}
// ...
```

en revanche

```c
// ...
{
    int* compteur = calloc(1, sizeof(int));
    // on utilise compteur

    // à la fin du contexte, compteur n'est PAS libéré. on ne peut plus y accéder car compteur (le pointeur vers la mémoire) est détruit, mais les données contenues à cette adresse mémoire sont toujours présentes et allouées.
    // si la mémoire n'est pas libérée, on appelle ça une fuite de mémoire, car on y perd à la fois l'accès et la place qui est réservée.
}
// ...
```

Il en va de soi d'utiliser la heap avec parcimonie.

## Syntaxe

### Types

Le symbole * (asterique), à la déclaration d'une variable, permet de déclarer une adresse pointant vers un \[type\].

Par exemple :

```c
float* adresseDeFlottant; // on a une adresse de flottant, un pointeur vers un flottant.
```

ou bien

```c
void* adresse; // on a une adresse de... on ne sait pas. ça peut être un entier, un flottant, ou juste rien.
```

### Opérateurs

Le symbole & (esperluette), précédant une variable, permet de récupérer l'adresse mémoire à laquelle sont stockées ses données.

Par exemple :

```c
int compteur = 0;
int* adresse = &compteur; // adresse détient l'adresse de la mémoire où se trouve notre compteur = 0
```

Le symbole * (asterisque), précédant une variable, permet à l'inverse de récupérer les données stockées à l'adresse mémoire.

Par exemple :

```c
// avec le contexte de l'exemple précédant
int valeur = *adresse; // on récupère la valeur d'adresse, qui est celle de compteur, donc valeur = compteur = 0
```

### Note

Attention à ne pas confondre * à la déclaration et * en tant qu'opérateur, qui sont littéralement à l'opposé en terme de comportement.
