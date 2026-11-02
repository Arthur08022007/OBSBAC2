# Résolution de l'exercice 3 du chapitre 3

## Énoncé

Le fragment de code suivant calcule la somme des chiffres de `n` :

```c
unsigned m, s;
for (m = n, s = 0; m; m /= 10)
    s += m % 10;
```

Il faut :

1. démontrer à l'aide d'un invariant que le résultat calculé est correct ;
2. prouver la terminaison à l'aide d'un variant.

On note **`S(x)`** la somme des chiffres de l'entier non signé `x`, en base 10. En particulier, `S(0) = 0`.

---

## Triplet de Hoare à vérifier

Avant de décomposer le `for`, on écrit le triplet complet :

**`{n est un entier non signé} for (m = n, s = 0; m; m /= 10) s += m % 10; {s = S(n) et m = 0}`**

La réécriture en `while` permet ensuite de vérifier ce triplet à l'aide
de l'invariant.

---

## Réécriture avec `while`

Pour rendre l'invariant explicite :

```c
unsigned m, s;
m = n;
s = 0;
while (m != 0) {
    s += m % 10;
    m /= 10;
}
```

À chaque tour, `m % 10` est le dernier chiffre de `m` et `m / 10` supprime ce dernier chiffre.

---

## Invariant

L'invariant est :

**I : `S(n) = s + S(m)`.**

En d'autres termes, `s` contient la somme des chiffres déjà retirés de `m`, tandis que `S(m)` contient la somme des chiffres qui restent à traiter.

On peut aussi ajouter la propriété évidente :

**`m >= 0` et `s >= 0`.**

Cette formulation fonctionne également lorsque `n = 0`.

---

## Initialisation

Avant le premier test :

- `m = n` ;
- `s = 0`.

On a donc :

**`s + S(m) = 0 + S(n) = S(n)`.**

L'invariant est vrai avant le premier tour. Si `n = 0`, la boucle ne s'exécute pas et le résultat `s = 0` est déjà correct.

---

## Conservation

Supposons l'invariant vrai au début d'un tour et la condition `m != 0` vraie.

Effectuons la division euclidienne de `m` par 10 :

**`m = 10q + r`**, avec

- **`q = m / 10`** ;
- **`r = m % 10`**, le dernier chiffre de `m`.

La somme des chiffres vérifie :

**`S(m) = S(q) + r`.**

Le corps du programme exécute :

```c
s += m % 10;
m /= 10;
```

Après le corps :

- `s' = s + r` ;
- `m' = q`.

En utilisant l'invariant avant le tour :

**`s' + S(m') = (s + r) + S(q) = s + S(m) = S(n)`.**

L'invariant est donc conservé.

---

## Sortie et correction

La boucle se termine lorsque `m == 0`.

L'invariant devient :

**`S(n) = s + S(0) = s + 0`.**

Donc :

**`s = S(n)`.**

La variable `s` contient bien la somme des chiffres de `n`.

---

## Terminaison

On choisit comme variant :

**`v = m`.**

Avant chaque tour, `m` est un entier non signé et la condition impose `m > 0`, donc `v > 0`.

Après la mise à jour :

**`m' = m / 10`.**

Pour tout entier `m > 0`, la division entière par 10 donne `m / 10 < m`. Le variant reste dans les entiers naturels et diminue strictement à chaque tour.

La boucle termine donc toujours.

---

## Exemple

Pour `n = 5072` :

| Début du tour | `m` | `m % 10` | `s` après ajout |
| --- | ---: | ---: | ---: |
| 1 | 5072 | 2 | 2 |
| 2 | 507 | 7 | 9 |
| 3 | 50 | 0 | 9 |
| 4 | 5 | 5 | 14 |

Après le dernier tour, `m = 0` et `s = 14`, qui est bien `5 + 0 + 7 + 2`.

---

## Résumé de la preuve

- **Invariant :** `S(n) = s + S(m)`.
- **Initialisation :** `m = n` et `s = 0`.
- **Conservation :** on retire le dernier chiffre `m % 10` et on remplace `m` par `m / 10`.
- **Sortie :** `m = 0`, donc `s = S(n)`.
- **Variant :** `m`, qui diminue strictement par division entière par 10.
