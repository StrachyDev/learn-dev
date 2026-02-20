---
title: Glossaire: notions et jargon en programmation
---

# Glossaire: notions et jargon en programmation

## Sommaire



## Notions

### Contexte (scope)

Le contexte est (grossièrement) défini par ce dont vous disposez comme variables, types et méthodes dans certaines parties de votre programme, ou dans son intégralité.

Par exemple :

```c
int add(int a, int b) {
    int sum = a + b;
    return sum;
}

void main() {
    int n1 = 3;
    int n2 = 5;
    int n3 = sum(n1, n2);
    
    printf("La somme de %d et %d est %d.\n", n1, n2, n3);

    return 0;
}
```

Dans votre méthode principale main, vous disposez de différentes variables, mais elles ne sont disponibles qu'après les avoir déclaré. À peine rentré dans la fonction, vous n'avez rien. Après les 3 premières lignes, vous avez n1, n2 et n3.

Dans votre méthode add, vous disposez de sum après l'avoir déclaré, mais vous ne disposez pas de n1, n2 et n3 de la méthode main. Elle est **hors du contexte** de votre fonction.

"Out of scope" est un type d'erreur pouvant survenir lors de la compilation ou de l'exécution de votre programme si vous essayez d'accéder à une variable ou un type qui n'existe pas dans le contexte dans lequel vous essayez de l'utiliser.

C'est de loin (à mon avis) la notion la plus simple mais la plus difficile à comprendre lorsqu'on commence à programmer.

Si vous avez compris ça, vous avez compris 90% de la programmation.

## Jargon

### Déclaration

La déclaration d'une variable, d'un type ou d'une méthode est l'endroit auquel vous avez **déclaré** son existence.

Par exemple :

```c
int compteur; // On dit que compteur existe et peut être utilisé.
```

### Définition

La définition d'une variable, d'un type ou d'une méthode est l'endroit où on alloue la mémoire nécessaire pour stocker son contenu.

Par exemple :

```c
int compteur; // En C, les variables sont souvent à la fois déclarées et définies.
```

### Initialisation

L'initialisation d'une variable est le fait d'attribuer pour la première fois une valeur à cette variable.

Par exemple :

```c
compteur = 0;
```

### Incrémentation

L'incrémentation d'une variable est le fait d'ajouter 1 à la variable.

Par exemple :

```c
compteur += 1;
```

### Affectation

L'affectation à une variable est le fait de modifier son contenu.

En continuant l'exemple précédant :

```c
compteur = 73; // On dit que compteur est égal à 0. 
```

### Références

Les références d'une variable, d'un type ou d'une méthode sont les endroits dans lesquels vous lui avez fait **référence** (où vous l'avez utilisé).

En continuant l'exemple précédant :

```c
if (compteur < 5) { // On a référencé (utilisé) compteur
    // ...
}
```

### Assertion

Une assertion est un test réalisé lors de l'exécution de votre programme pour vous **assurer** que plusieurs conditions soient remplies. Son but est de prévenir les erreurs d'état de programme (State error) en arrêtant le programme, permettant ainsi d'éviter de débugger à l'avenir et de perdre du temps pour quelque chose qui n'aurait simplement jamais dû se passer.

Par exemple :

```c
double division(double a, double b) {
    assert(b != 0); // On s'assure que b ne soit pas égal à 0, sinon on stoppe l'exécution du programme avec une erreur.
    return a / b;
}
```

Ne voyez pas les assertions comme des ennemis qui mettent un frein à votre programme, mais plutôt comme des bons potes qui vous disent ce qui ne va pas

### 