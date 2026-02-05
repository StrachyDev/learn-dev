---
title: Entrée / Entrée & Sortie / Sortie en C
---

# Distinctions Entrée / Entrée & Sortie / Sortie en C

## Sommaire

- [Entrée](#i-entrée)
  - [Fonction](#1-fonction)
  - [Procédure](#2-procédure)
- [Entrée & Sortie](#ii-entrée--sortie)
  - [Fonction](#1-fonction-1)
  - [Procédure](#2-procédure-1)
- [Sortie](#iii-sortie)
  - [EXCLUSIF AUX FONCTIONS](#1-exclusif-aux-fonctions)

Soient p un paramètre et v une valeur quelconques.\\
"Type" est un type quelconque. Les paramètres et les types de sortie marqués "Type" ne coïncident pas forcément.

## I. Entrée

### 1. Fonction
```c
Type fonction(Type p, ...) { // p est en entrée
  ...
  return ...;
}
```

### 2. Procédure
```c
void procedure(Type p, ...) { // p est en entrée
  ...
}
```

## II. Entrée & Sortie

### 1. Fonction
```c
Type fonction(Type *p, ...) { // p est en entrée & sortie grâce à son adresse mémoire
  ...
  return ...;
}
```

### 2. Procédure
```c
void procedure(Type *p, ...) { // p est en entrée & sortie grâce à son adresse mémoire
  ...
}
```

## III. Sortie

### 1. EXCLUSIF AUX FONCTIONS
```c
Type fonction(...) {
  return v; // v est en sortie uniquement
}
```

Il n'existe pas d'équivalent avec les procédures car, par définition, elles ne peuvent pas avoir d'éléments en sortie exclusive (les procédures ne retournent rien).