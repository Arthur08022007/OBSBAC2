# Exercice 5

Cours d’introduction à l’informatique  
Énoncés et solutions

Source : [[supports/info-sep2022.pdf]]

---

## Énoncé

### a)

Écrire une fonction prenant en argument un nombre entier non signé et non nul, et retournant le nombre de zéros situés à la fin de son écriture décimale.

Par exemple :

- pour le nombre `42000`, la fonction doit retourner `3` ;
- pour le nombre `2022`, elle doit retourner `0`.

### b)

Par la méthode des invariants, démontrer que la valeur retournée par cette fonction est correcte.

---

## Solution

### a) Écriture de la fonction

Il suffit d’écrire une boucle dans laquelle on divise le nombre par `10` tant que cela est possible, en incrémentant un compteur à chaque itération.

On obtient le code suivant :

```c
unsigned nombre_zeros(unsigned n)
{
    unsigned nb = 0;

    while (!(n % 10))
    {
        n /= 10;
        nb++;
    }

    return nb;
}
```

### b) Preuve par invariant

On souhaite établir la validité du triplet suivant :

```text
{n = n₀ > 0, nb = 0}
while (!(n % 10))
{
    n /= 10;
    nb++;
}
{nb = nombre de zéros à la fin de l’écriture de n₀}
```

Pour trouver un invariant de boucle `I`, on caractérise les opérations effectuées par la boucle jusqu’à une itération donnée. Un invariant possible est :

```text
I : n₀ > 0 et nb > 0 et n₀ = n × 10^nb
```

Cet invariant exprime qu’avant et après chaque itération de la boucle, la valeur de `nb` correspond au nombre de facteurs `10` qui ont été extraits de la valeur initiale de `n`.

Montrons maintenant que cet invariant est valide.

#### Initialisation

Initialement, on a `n = n₀ > 0` et `nb = 0`, ce qui satisfait l’invariant.

#### Conservation

Pour chaque itération de la boucle, on a le triplet :

```text
{I, n est divisible par 10}
n /= 10;
nb++;
{I}
```

Montrons que ce triplet est valide, en notant respectivement `x` et `x'` la valeur d’une variable `x` avant et après l’itération concernée.

On a :

```text
n₀' = n₀
n' = n / 10
nb' = nb + 1
```

L’égalité `n₀ = n × 10^nb` se réécrit alors :

```text
n₀' = 10 × n' × 10^(nb' - 1)
     = n' × 10^nb'
```

ce qui prouve la validité du triplet.

#### Sortie de boucle

En fin de boucle, on a :

```text
{I, n n’est pas divisible par 10}
```

On a donc `n₀ = n × 10^nb`, avec `n` non divisible par `10`. Cela signifie que `nb` est la plus grande puissance de `10` qui divise `n₀`, en d’autres termes que `nb` est égal au nombre de zéros situés à la fin de l’écriture de `n₀`.
