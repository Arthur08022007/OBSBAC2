# Exercice 6

Cours d’introduction à l’informatique  
Énoncés et solutions

Source : [[supports/info-jan2023.pdf]]

---

## Énoncé

L’indicatrice d’Euler est une fonction `φ` telle que pour tout nombre entier strictement positif `n`, `φ(n)` a pour valeur le nombre d’entiers `m` contenus dans l’intervalle `[1, n]` tels que `pgcd(m, n) = 1`, où `pgcd(m, n)` est le plus grand commun diviseur de `m` et de `n`.

### a)

Donner une implémentation de cette fonction, en supposant que l’on dispose d’une bibliothèque qui implémente déjà la fonction `pgcd`.

### b)

Calculer la complexité en temps de la fonction obtenue au point (a), en sachant que la complexité en temps de `pgcd(m, n)`, avec `m ≤ n`, est `O(log m)`.

---

## Solution

### a) Implémentation

On sait que `pgcd(1, n) = 1` pour tout `n`, donc on peut commencer l’énumération des valeurs `m` à partir de `2`.

```c
unsigned pgcd(unsigned, unsigned);

unsigned euler(unsigned n)
{
    unsigned e, m;

    for (e = 1, m = 2; m <= n; m++)
        if (pgcd(m, n) == 1)
            e++;

    return e;
}
```

### b) Complexité en temps

Le nombre total d’opérations effectuées est borné par :

```text
O(log 2 + log 3 + ··· + log n)
≤ O(log n + log n + ··· + log n)
= O((n − 1) log n)
= O(n log n)
```
