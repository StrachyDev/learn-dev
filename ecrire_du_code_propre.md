---
title: Coder proprement et efficacement
---

# Coder proprement ; intelligemment et pertinemment pour économiser du temps et des maux de crâne (en toute modestie)

## Sommaire

- [Organiser son code intelligemment](#i-organiser-son-code-intelligemment)
    - [Dé-indentation](#1-dé-indentation)
    - [Espacer son code](#2-espacer-son-code)
- [Nommer pertinemment](#ii-nommer-pertinemment)
    - [Les fonctions et procédures](#1-les-fonctions-et-procédures)
    - [Les variables](#2-les-variables)
    - [Les structures](#3-les-structures)
- [Relecture et refactorisation du code](#iii-relecture-et-refactorisation-du-code)
    - [Problèmes de logique](#1-problèmes-de-logique)
    - [Répétitions](#2-répétitions)
    - [Touches personnelles](#3-touches-personnelles)
- [Avertissement concernant les commentaires (j'ai un problème perso avec eux)](#avertissement)
- [Note](#v-note)
- [Fin](#vi-fin)

## I. Organiser son code intelligemment

### 1. Dé-indentation

Regardez le code suivant.

```c
matrix_t* mMat(matrix_t *A, matrix_t *B) {
    if (A->nc == B->nl) {
        matrix_t *C = cMat(A->nl, B->nc);
        int ne = C->nl * C->nc;
        for (int i = 0; i < ne; i++)
        {
            int x = i % C->nc;
            int y = i / C->nl;
            double v = 0;
            for (int ax = 0, ay = y, bx = x, by = 0; ax < C->nc; ax++, by++) {
                v += A->v[xytoi(C, ax, ay)] * B->v[xytoi(C, bx, by)];
            }
            C->v[i] = v;
        }
        return C;
    }
    return NULL;
}
```

Pour comprendre finement la logique derrière, on doit toujours avoir en mémoire la condition de départ, ce qui est lourd et inutile.

On peut faciliter sa compréhension en inversant la première condition et en sortant de la fonction :

```c
matrix_t* mMat(matrix_t *A, matrix_t *B) {
    if (A->nc != B->nl) return NULL; // "A->nc == B->nl" devient "A->nc != B->nl"
    matrix_t *C = cMat(A->nl, B->nc);
    int ne = C->nl * C->nc;
    for (int i = 0; i < ne; i++)
    {
        int x = i % C->nc;
        int y = i / C->nl;
        double v = 0;
        for (int ax = 0, ay = y, bx = x, by = 0; ax < C->nc; ax++, by++) {
            v += A->v[xytoi(C, ax, ay)] * B->v[xytoi(C, bx, by)];
        }
        C->v[i] = v;
    }
    return C;
}
```

Cela permet d'économiser des indentations et de la mémoire cérébrale : vous pouvez vous concentrer sur l'essentiel et mettre de côté les cas particuliers ou les éventuelles erreurs à prendre en compte.

### 2. Espacer son code

Reprenons notre code.

```c
matrix_t* mMat(matrix_t *A, matrix_t *B) {
    if (A->nc != B->nl) return NULL;
    matrix_t *C = cMat(A->nl, B->nc);
    int ne = C->nl * C->nc;
    for (int i = 0; i < ne; i++)
    {
        int x = i % C->nc;
        int y = i / C->nl;
        double v = 0;
        for (int ax = 0, ay = y, bx = x, by = 0; ax < C->nc; ax++, by++) {
            v += A->v[xytoi(C, ax, ay)] * B->v[xytoi(C, bx, by)];
        }
        C->v[i] = v;
    }
    return C;
}
```

Plutôt difficile de repérer les différentes parties du code, n'est-ce pas ?

- Où est-ce que j'initialise ?
- Où sont mes vérifications ?
- Où est-ce que j'ajoute le produit à la matrice ?
- Et puis à quoi correspond l'ajout à v dans la double boucle ?

Des questions que vous vous poserez en lisant ce code après une longue période et en l'ayant oublié.\\
Des questions qui vous feront perdre un temps précieux et qui aurait pu servir à bien d'autres utilités.

Pour cela,  e  s  p  a  c  e  z  votre code.\\
Ce sera déjà un peu mieux par la suite, vous verrez.\\
Regardez :

```c
matrix_t* mMat(matrix_t *A, matrix_t *B) {
    if (A->nc != B->nl) return NULL;

    matrix_t *C = cMat(A->nl, B->nc);
    int ne = C->nl * C->nc;

    for (int i = 0; i < ne; i++)
    {
        int x = i % C->nc;
        int y = i / C->nl;
        double v = 0;

        for (int ax = 0, ay = y, bx = x, by = 0; ax < C->nc; ax++, by++) {
            v += A->v[xytoi(C, ax, ay)] * B->v[xytoi(C, bx, by)];
        }

        C->v[i] = v;
    }

    return C;
}
```

Ahh ! On respire.\\
On arrive déjà mieux à discerner distinctement chaque partie : en premier les tests, ensuite les déclarations et initialisations, puis la boucle principale, dans laquelle on déclare et initialise, puis la seconde boucle, etc..

Mais on peut faire mieux.

## II. Nommer pertinemment

Le code que l'on écrit est subjectif et est sujet à changer tout comme le développeur tout au long de sa vie.\\
Le problème est lorsqu'on a commencé à travailler en groupe et que les programmeurs ont dû lire le code des autres et se familiariser avec.\\
C'est vite devenu un cauchemar car ils ont dû comprendre réellement le code au lieu que cela soit instinctif et au lieu de travailler dessus : c'est une perte de temps phénoménale.

Pour résoudre ce problème, on a créé des conventions de nommage.

Il en existe des tas, mais parmi les plus connues :

- le snake_case (chaque mot espacé d'un underscore "_")
- le PascalCase (chaque mot commence par une majuscule)
- le camelCase (chaque mot commence par une majuscule, excepté le premier)

Elles sont propres à certaines entreprises, mais aussi à certains langages de programmations.

Nous utiliserons la convention de nommage camelCase et les noms seront en français (il est important de le définir dès le début pour éviter le franglish ou des mixes de convention).

Reprenons notre code à nouveau :

```c
matrix_t* mMat(matrix_t *A, matrix_t *B) {
    if (A->nc != B->nl) return NULL;

    matrix_t *C = cMat(A->nl, B->nc);
    int ne = C->nl * C->nc;

    for (int i = 0; i < ne; i++)
    {
        int x = i % C->nc;
        int y = i / C->nl;
        double v = 0;

        for (int ax = 0, ay = y, bx = x, by = 0; ax < C->nc; ax++, by++) {
            v += A->v[xytoi(C, ax, ay)] * B->v[xytoi(C, bx, by)];
        }

        C->v[i] = v;
    }
    
    return C;
}
```

- Que sont "ne", "nc", "nl", "xytoi", "cMat", "A->v" et le reste... ?

Hormi le développeur ayant créé ce code (et encore, il doit s'en souvenir), personne n'arriverait à déchiffrer chaque instruction clairement et lisiblement.

### 1. Les fonctions et procédures

On va donc reformuler tout ça, et ce en commançant par le nom de la fonction :

```c
matrix_t* produitMatriciel(matrix_t *A, matrix_t *B) { // <--
    if (A->nc != B->nl) return NULL;

    matrix_t *C = cMat(A->nl, B->nc);
    int ne = C->nl * C->nc;

    for (int i = 0; i < ne; i++)
    {
        int x = i % C->nc;
        int y = i / C->nl;
        double v = 0;

        for (int ax = 0, ay = y, bx = x, by = 0; ax < C->nc; ax++, by++) {
            v += A->v[xytoi(C, ax, ay)] * B->v[xytoi(C, bx, by)];
        }

        C->v[i] = v;
    }
    
    return C;
}
```

C'est mieux, non ?\\
Poursuivons avec les fonctions et procédures utilisées :

```c
matrix_t* produitMatriciel(matrix_t *A, matrix_t *B) {
    if (A->nc != B->nl) return NULL;

    matrix_t *C = MatriceVide(A->nl, B->nc); // <--
    int ne = C->nl * C->nc;

    for (int i = 0; i < ne; i++)
    {
        int x = i % C->nc;
        int y = i / C->nl;
        double v = 0;

        for (int ax = 0, ay = y, bx = x, by = 0; ax < C->nc; ax++, by++) {
            v += A->v[ConvCoordsAIndice(C, ax, ay)] * B->v[ConvCoordsAIndice(C, bx, by)]; // <-- *
        }

        C->v[i] = v;
    }
    
    return C;
}
```
**où "Conv" et "Coords" veulent respectivement dire "Conversion" et "Coordonnées"*

Déjà plus clair, mais on peut continuer.

### 2. Les variables

Désormais, les variables :

```c
matrix_t* produitMatriciel(matrix_t *A, matrix_t *B) {
    if (A->nc != B->nl) return NULL;

    matrix_t *C = MatriceVide(A->nl, B->nc);
    int nombreElements = C->nl * C->nc; // <--

    for (int i = 0; i < nombreElements; i++) // <--
    {
        int x = i % C->nc;
        int y = i / C->nl;
        double produit = 0; // <--

        for (int xA = 0, yA = y, xB = x, yB = 0; xA < C->nc; xA++, yB++) {
            produit += A->v[ConvCoordsAIndice(C, xA, yA)] * B->v[ConvCoordsAIndice(C, xB, yB)]; // <--
        }

        C->v[i] = produit; // <--
    }
    
    return C;
}
```

On y est presque !

### 3. Les structures

En modifiant le type matrix_t :

```c
typedef struct matrix {
    int nl;
    int ncbCol;
    double *v;
} matrix_t;
```

qui devient :

```c
typedef struct matrix {
    int nombreLignes;   // ou nbLig
    int nombreColonnes; // ou nbCol
    double *elements;   // ou elts
} matrix_t;
```

Notre code devient :

```c
matrix_t* produitMatriciel(matrix_t *A, matrix_t *B) {
    if (A->nombreColonnes != B->nombreLignes) return NULL; // <--

    matrix_t *C = MatriceVide(A->nombreLignes, B->nombreColonnes); // <--
    int nombreElements = C->nombreLignes * C->nombreColonnes; // <--

    for (int i = 0; i < nombreElements; i++)
    {
        int x = i % C->nombreColonnes; // <--
        int y = i / C->nombreLignes; // <--
        double produit = 0;

        for (int xA = 0, yA = y, xB = x, yB = 0; xA < C->nombreColonnes; xA++, yB++) { // <--
            produit += A->elements[ConvCoordsAIndice(C, xA, yA)] * B->elements[ConvCoordsAIndice(C, xB, yB)]; // <--
        }

        C->elements[i] = produit; // <--
    }
    
    return C;
}
```

Pas mal,\\
et c'est pas terminé.

PS¹: Vous pouvez faire des sacrifices de lisibilité pour gagner en place, mais uniquement si vous comprenez toujours le code de manière simple et rapide.\\
Par exemple, en écrivant "nbLig" dans matrix_t au lieu de "nombreLignes", on peut toujours comprendre que ça désigne le nombre de lignes de la matrice. Le choix de nommage reste votre décision, et seul vous peut déterminer si tel ou tel nom est approprié, trop peu ou excessivement informatif. Les goûts et les couleurs.

PS²: N'ayez pas peur d'avoir des noms de variables plus lisibles au prix de la longueur. Les éditeurs de code modernes proposent des complétions de noms, lorsque vous commencez à taper par exemple "nomV" pour "nomVariable", il vous proposera certainement "nomVariable", que vous pourrez valider communément avec la touche "Tab".\\
Vous perdez très peu de temps à écrire votre code en comparaison avec essayer de le re-comprendre des semaines voire des mois après.\\
Vous êtes gagnant au long terme.

## III. Relecture et refactorisation du code

On dit "refactor" lorsqu'on retravaille un bout de code pour par exemples en simplifier son usage, l'optimiser, le restructurer, ...

### 1. Problèmes de logique

Dans notre code, on se rend compte qu'utiliser la fonction ConvCoordsAIndice est inutile car cela revient à retrouver i depuis les coordonnées x et y. Or, on connait i, donc les deux calculs sont inutiles.

On peut donc simplifier comme suit :

```c
matrix_t* produitMatriciel(matrix_t *A, matrix_t *B) {
    if (A->nombreColonnes != B->nombreLignes) return NULL;

    matrix_t *C = MatriceVide(A->nombreLignes, B->nombreColonnes);
    int nombreElements = C->nombreLignes * C->nombreColonnes;

    for (int i = 0; i < nombreElements; i++)
    {
        int x = i % C->nombreColonnes;
        int y = i / C->nombreLignes;
        double produit = 0;

        for (int xA = 0, yA = y, xB = x, yB = 0; xA < C->nombreColonnes; xA++, yB++) {
            produit += A->elements[i] * B->elements[i]; // i à la place de ConvCoordsAIndice(C, x_, y_)
        }

        C->elements[i] = produit;
    }
    
    return C;
}
```

### 2. Répétitions

Dans notre dernier exemple, nous n'avons pas vraiment de problèmes de répétitions.\\
Mais si on devait garder ConvCoordsAIndice, on aurait pu cacher (= mettre en cache, stocker sous forme de variable) son résultat, étant donné qu'on l'utilise deux fois. Cela permet d'économiser un calcul et de gagner en efficacité !

Si on devait le faire pour x ou y raisons, le code serait devenu :

```c
matrix_t* produitMatriciel(matrix_t *A, matrix_t *B) {
    if (A->nombreColonnes != B->nombreLignes) return NULL;

    matrix_t *C = MatriceVide(A->nombreLignes, B->nombreColonnes);
    int nombreElements = C->nombreLignes * C->nombreColonnes;

    for (int i = 0; i < nombreElements; i++)
    {
        int x = i % C->nombreColonnes;
        int y = i / C->nombreLignes;
        double produit = 0;

        for (int xA = 0, yA = y, xB = x, yB = 0; xA < C->nombreColonnes; xA++, yB++) {
            int indice = ConvCoordsAIndice(C, xA, yA);
            produit += A->elements[indice] * B->elements[indice]; // Notez également que cette ligne devient plus lisible en déplaçant une partie de son contenu à la ligne supérieure. 
        }

        C->elements[i] = produit;
    }
    
    return C;
}
```

Attention : il ne faut pas pas exagérer le fait de ne rien répéter, sinon vous transformerez votre code en code spaghetti (code qui est entremêlé, par exemple : A dépend de B mais B dépend de A, avec C dépendant des deux, etc.), ce qui est insupportable à maintenir dans le futur. Utilisé localement comme ici et à courte échelle fait économiser du temps à la fois d'écriture, d'exécution, et de lecture, mais globalement et à grande échelle provoque exactement l'inverse.

### 3. Touches personnelles

À titre exclusivement personnel, mon code final ressemble à ça :

```c
matrix_t* produitMatriciel(matrix_t *A, matrix_t *B) {
    if (A->nombreColonnes != B->nombreLignes) return NULL;

    matrix_t *C = MatriceVide(A->nombreLignes, B->nombreColonnes);
    int nombreElements = C->nombreLignes * C->nombreColonnes;

    for (int i = 0; i < nombreElements; i++)
    {
        int x = i % C->nombreColonnes;
        int y = i / C->nombreLignes;
        double produit = 0;

        for (int xA = 0, yA = y, xB = x, yB = 0; // <--
            xA < C->nombreColonnes;              // <--
            xA++, yB++) {                        // <--
                                                 // <-- J'ai rajouté un espace après la déclaration de la boucle pour la séparer du contenu de la boucle
            int indice = ConvCoordsAIndice(C, xA, yA);
            produit += A->elements[indice] * B->elements[indice];
        }

        C->elements[i] = produit;
    }
    
    return C;
}
```

La seule chose que j'ai subjectivement modifié est d'avoir sauté des lignes pour chaque partie de la boucle for, car je trouve que lorsque la boucle devient longue, avec plusieurs variables et/ou conditions et/ou incrémentations, il devient compliqué de déterminer ce que la boucle fait. En sautant des lignes à chaque partie, la lecture se simplifie, en tout cas à mon goût.

Tout ça pour vous dire que votre code est avant tout une matière de goûts personnels et que vous avez librement le droit de l'organiser et le structurer comme bon vous semble, ne restez pas figés sur les manières dont les professeurs écrivent ou les gens sur internet, trouvez le style qui vous plaît et vous aide à le lire plus aisément.

## Avertissement

Je vous invite **très fortement** à lire [Avertissement sur les commentaires](avertissement_commentaires.md).

C'est un complément de ce cours, couplé à une petite analyse personnelle.\\
Je débunk une vérité prétendue universelle et indispensable concernant les commentaires.

## V. Note

Bien sûr, ce ne sont pas les seules manières d'améliorer son code ; ce ne sont que des exemples de ce qu'il est possible de faire. Libre à vous de trouver d'autres façons d'améliorer votre code, et ce dans n'importe quel aspect quel qu'il soit !

## VI. Fin

Voici un petit avant/après du programme :

<table>
<tr>
<th>Avant</th>
<th>Après</th>
</tr>

<tr>
<td>

<pre><code class="language-c">matrix_t* mMat(matrix_t *A, matrix_t *B) {
    if (A->nc == B->nl) {
        matrix_t *C = cMat(A->nl, B->nc);
        int ne = C->nl * C->nc;
        for (int i = 0; i < ne; i++)
        {
            int x = i % C->nc;
            int y = i / C->nl;
            double v = 0;
            for (int ax = 0, ay = y, bx = x, by = 0; ax < C->nc; ax++, by++) {
                v += A->v[xytoi(C, ax, ay)] * B->v[xytoi(C, bx, by)];
            }
            C->v[i] = v;
        }
        return C;
    }
    return NULL;
}</code></pre>

</td>

<td>

<pre><code class="language-c">matrix_t* produitMatriciel(matrix_t *A, matrix_t *B) {
    if (A->nombreColonnes != B->nombreLignes) return NULL;

    matrix_t *C = MatriceVide(A->nombreLignes, B->nombreColonnes);
    int nombreElements = C->nombreLignes * C->nombreColonnes;

    for (int i = 0; i < nombreElements; i++)
    {
        int x = i % C->nombreColonnes;
        int y = i / C->nombreLignes;
        double produit = 0;

        for (int xA = 0, yA = y, xB = x, yB = 0;
            xA < C->nombreColonnes;
            xA++, yB++) {

            int indice = ConvCoordsAIndice(C, xA, yA);
            produit += A->elements[indice] * B->elements[indice];
        }

        C->elements[i] = produit;
    }
    
    return C;
}</code></pre>

</td>
</tr>
</table>

Merci d'avoir suivi ce petit cours, si vous avez des suggestions n'hésitez pas.\\
N'hésitez pas également à le relire, autant de fois que nécessaires, afin d'intégrer au mieux les notions abordées.

Programmez bien les loulous