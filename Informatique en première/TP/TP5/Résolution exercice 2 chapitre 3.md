# Résolution de l'exercice 2 du chapitre 3

## Énoncé

Le fragment de code suivant calcule la factorielle de `n` :

```c
int i, fact;
for (i = 2, fact = 1; i <= n; i++)
    fact *= i;
```

On suppose que `n` est strictement positif et qu'aucun dépassement arithmétique ne se produit pendant l'exécution.

Il faut :

1. démontrer que

   **`2 <= i <= n + 1` et `fact = produit des j pour 2 <= j < i`**

   est un invariant de la boucle ;
2. prouver la terminaison à l'aide d'un variant.

---

## Réécriture avec `while`

Pour rendre l'emplacement de l'invariant explicite :

```c
int i, fact;
i = 2;
fact = 1;
while (i <= n) {
    fact *= i;
    i++;
}
```

L'invariant est vrai avant le test de la condition et au début de chaque tour.

On note :

**`P(i) = produit des j pour 2 <= j < i`.**

Ainsi, `P(2)` est un produit vide, égal à `1`.

---

## Invariant

L'invariant est :

**I : `2 <= i <= n + 1` et `fact = P(i)`.**

En toutes lettres, `fact` contient le produit des entiers de `2` à `i - 1`, et `i` est compris entre `2` et `n + 1`.

Cet invariant décrit exactement le travail déjà effectué : les facteurs strictement inférieurs à `i` ont déjà été multipliés dans `fact`.

---

## Initialisation

Avant le premier tour :

- `i = 2` ;
- `fact = 1`.

Comme `n > 0`, on a `2 <= n + 1`. De plus, `P(2)` est le produit vide, donc vaut `1`.

On obtient :

**`2 <= i <= n + 1` et `fact = 1 = P(2)`.**

L'invariant est donc vrai avant le premier test de boucle.

---

## Conservation

Supposons l'invariant vrai au début d'un tour et supposons que la condition de boucle `i <= n` soit vraie.

On a alors :

**`fact = P(i)`.**

Le corps exécute :

```c
fact *= i;
i++;
```

Après `fact *= i`, on a :

**`fact = P(i) * i = P(i + 1)`.**

Après `i++`, la nouvelle valeur de `i` est `i' = i + 1`, donc :

**`fact = P(i')`.**

Pour les bornes :

- avant le tour, `i >= 2`, donc `i' >= 3`, et en particulier `i' >= 2` ;
- la condition `i <= n` donne `i' = i + 1 <= n + 1`.

Ainsi, après le corps et la mise à jour :

**`2 <= i' <= n + 1` et `fact = P(i')`.**

L'invariant est conservé.

---

## Sortie et correction

À la sortie de la boucle, la condition `i <= n` est fausse. On a donc `i > n`.

L'invariant donne aussi `i <= n + 1`. Comme `i` est entier :

**`i = n + 1`.**

En remplaçant `i` par `n + 1` dans l'invariant :

**`fact = produit des j pour 2 <= j < n + 1`.**

Les facteurs concernés sont `2, 3, ..., n`. Donc :

**`fact = 2 * 3 * ... * n = n!`.**

Le programme calcule bien la factorielle de `n`.

---

## Terminaison

On choisit comme variant :

**`v = n + 1 - i`.**

Pendant un tour :

- l'invariant donne `i <= n + 1`, donc `v >= 0` ;
- la condition de boucle donne `i <= n`, donc avant le tour `v >= 1` ;
- après `i++`, le variant devient `v' = n + 1 - (i + 1) = v - 1`.

Le variant est donc un entier naturel qui diminue strictement à chaque tour. Il ne peut pas diminuer indéfiniment : la boucle termine toujours.

---

## Résumé de la preuve

- **Invariant :** `2 <= i <= n + 1` et `fact` contient le produit des entiers de `2` à `i - 1`.
- **Initialisation :** `i = 2` et `fact = 1`, qui est le produit vide.
- **Conservation :** le corps multiplie par le facteur courant `i`, puis avance `i`.
- **Sortie :** `i = n + 1`, donc `fact = n!`.
- **Variant :** `n + 1 - i`, qui diminue de 1 à chaque tour.
