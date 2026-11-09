# Exercice 1 — Multiplicité d’un facteur

## Énoncé

On considère deux entiers strictement positifs `n` et `f`.

### a) Écriture de la fonction

Écrire une fonction C qui calcule la **multiplicité du facteur `f` dans `n`**, c’est-à-dire le plus grand entier `m` tel que `f^m` divise `n`.

Par exemple, pour `n = 324` et `f = 9` :

```text
324 = 9² × 4
```

La multiplicité de `9` dans `324` vaut donc `2`.

### b) Preuve par la méthode des invariants

Démontrer que la valeur retournée par la fonction est correcte.

> On ne demande pas de démontrer que la fonction termine toujours son exécution. Il faut montrer que, **si elle se termine**, la valeur retournée est correcte.

---

## Résolution

### a) Fonction C

```c
unsigned multiplicite_facteur(unsigned n, unsigned f)
{
    unsigned m;

    for (m = 0; !(n % f); m++)
        n /= f;

    return m;
}
```

La boucle divise `n` par `f` tant que la division est exacte. La variable `m` compte le nombre de divisions effectuées.

### b) Preuve par invariant

#### Précondition et postcondition

On note `n₀` la valeur initiale de `n`.

- **Précondition :** `n = n₀ > 0`, `f > 0` et `m = 0` ;
- **Postcondition :** `m` est la multiplicité de `f` dans `n₀`.

En développant la boucle `for`, on obtient :

```c
m = 0;
while (!(n % f)) {
    n /= f;
    m++;
}
```

#### Invariant

On choisit l’invariant suivant :

```text
I : n > 0 et f > 0 et n₀ = n × f^m
```

Il exprime qu’après `m` divisions exactes, la valeur restante `n`, multipliée par `f^m`, est toujours égale à la valeur initiale `n₀`.

#### Initialisation

Avant le premier tour de boucle, `n = n₀` et `m = 0`. Ainsi :

```text
n₀ = n × f^0 = n
```

Comme `n₀ > 0` et `f > 0`, l’invariant est vrai avant la première itération.

#### Conservation

Supposons l’invariant vrai au début d’une itération et supposons que `n % f == 0`.

Après l’exécution du corps :

```text
n' = n / f
m' = m + 1
```

La division est exacte, donc `n' > 0`. De plus :

```text
n' × f^m'
= (n / f) × f^(m + 1)
= n × f^m
= n₀
```

L’invariant est donc encore vrai après l’itération.

#### Sortie de boucle

À la sortie, l’invariant est vrai et la condition de boucle est fausse :

```text
n % f != 0
```

On a donc :

```text
n₀ = n × f^m
```

et le facteur `f` ne divise plus `n`. Toutes les divisions exactes possibles par `f` ont donc été effectuées. Par définition, `m` est bien la multiplicité de `f` dans `n₀`.

La fonction retourne donc une valeur correcte lorsqu’elle termine.
