---
title: Distinctions Entrée / Entrée & Sortie / Sortie en C
---

# Distinctions Entrée / Entrée & Sortie / Sortie en C

Soient p un paramètre et v une valeur quelconques.
"Type" est un type quelconque. Les paramètres et les types de sortie marqués "Type" ne coïncident pas forcément.

## Entrée

### Fonction
```c
Type fonction(Type p, ...) { // p est en entrée
  ...
  return ...;
}
```

### Procédure
```c
void procedure(Type p, ...) { // p est en entrée
  ...
}
```

## Entrée & Sortie

### Fonction
```c
Type fonction(Type *p, ...) { // p est en entrée & sortie grâce à son adresse mémoire
  ...
  return ...;
}
```

### Procédure
```c
void procedure(Type *p, ...) { // p est en entrée & sortie grâce à son adresse mémoire
  ...
}
```

## Sortie

### EXCLUSIF AUX FONCTIONS
```c
Type fonction(...) {
  return v; // v est en sortie uniquement
}
```

Il n'existe pas d'équivalent avec les procédures car, par définition, ils ne peuvent pas avoir d'éléments en sortie exclusive (ne retourne rien).