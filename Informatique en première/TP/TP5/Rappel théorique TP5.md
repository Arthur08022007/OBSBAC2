# Invariants de boucle en C

Rappel théorique — TP 5

---

# Pourquoi utiliser un invariant

Un invariant de boucle est une propriété qui reste vraie avant et après chaque tour de boucle.

Il sert à expliquer rigoureusement ce que le programme a déjà établi pendant son exécution. En particulier, il permet de vérifier que le résultat construit progressivement par la boucle est correct, sans avoir à suivre toutes les valeurs possibles une par une.

Pour trouver un invariant, on décrit l'état du programme **au début de chaque tour**, juste avant l'exécution du corps de la boucle.

---

# Les triplets de Hoare

Un triplet de Hoare s'écrit :

**{P} programme {Q}**

- **P** est la précondition : ce qui est vrai avant le programme ;
- **programme** est l'instruction ou la boucle étudiée ;
- **Q** est la postcondition : ce qui est vrai après le programme.

Pour une boucle, l'invariant est noté **I**. On cherche à montrer que :

**{P} initialisation ; boucle {Q}**

en utilisant les trois propriétés de l'invariant :

1. l'invariant est vrai au départ ;
2. chaque tour le conserve ;
3. lorsqu'on sort, l'invariant et la condition de sortie donnent le résultat attendu.

---

# Les trois propriétés à vérifier

## Initialisation

Avant le premier tour de boucle, l'invariant doit être vrai.

On vérifie cette propriété avec les valeurs données aux variables par l'initialisation. Pour une boucle `for`, il s'agit des valeurs juste après la première expression d'initialisation.

## Conservation

On suppose que l'invariant est vrai au début d'un tour et on montre qu'il reste vrai après l'exécution du corps.

Cette étape est une implication :

**invariant avant le tour** et **condition de boucle**

entraînent

**invariant après le tour**.

## Sortie

Quand la boucle se termine, la condition de boucle est fausse. On dispose donc à la fois de l'invariant et de la négation de la condition.

Il faut montrer que ces deux informations impliquent la postcondition voulue. C'est cette étape qui relie le calcul réalisé par la boucle au résultat annoncé par le programme.

---

# Exemple : somme des éléments d'un tableau

On veut calculer la somme des `n` premiers éléments de `tab` :

```c
int somme = 0;
for (int i = 0; i < n; i++)
    somme += tab[i];
```

Invariant au début d'un tour :

**`somme` est la somme des éléments `tab[0]` à `tab[i - 1]`.**

- **Initialisation :** avant le premier tour, `i == 0` et `somme == 0`. La somme des éléments déjà parcourus est donc bien nulle.
- **Conservation :** si `somme` contient la somme de `tab[0]` à `tab[i - 1]`, alors `somme += tab[i]` ajoute exactement le prochain élément. Après l'instruction, la somme correspond à `tab[0]` jusqu'à `tab[i]`, puis `i++` prépare le tour suivant.
- **Sortie :** la boucle s'arrête avec `i == n`. L'invariant affirme alors que `somme` est la somme de `tab[0]` à `tab[n - 1]`.

La postcondition est donc :

**`somme == tab[0] + tab[1] + ... + tab[n - 1]`.**

---

# Exemple : maximum dans un tableau

On suppose que `n > 0` et on cherche le maximum de `tab` :

```c
int maximum = tab[0];
for (int i = 1; i < n; i++) {
    if (tab[i] > maximum)
        maximum = tab[i];
}
```

Invariant au début d'un tour :

**`maximum` est le maximum des éléments `tab[0]` à `tab[i - 1]`.**

- **Initialisation :** avant le premier tour, `i == 1` et `maximum == tab[0]`. Le maximum du premier élément est bien `tab[0]`.
- **Conservation :** si `maximum` est le maximum des éléments déjà parcourus, on compare `tab[i]` à ce maximum. On garde le plus grand des deux ; la variable contient donc le maximum jusqu'à `tab[i]`. L'incrément de `i` prépare le tour suivant.
- **Sortie :** la boucle s'arrête avec `i == n`. `maximum` est alors le maximum de `tab[0]` à `tab[n - 1]`.

La postcondition est donc :

**`maximum` est le maximum de tout le tableau.**

---

# Correspondance entre `for` et `while`

Une boucle `for` :

```c
for (initialisation; condition; mise_a_jour) {
    corps;
}
```

correspond à :

```c
{
    initialisation;
    while (condition) {
        corps;
        mise_a_jour;
    }
}
```

L'invariant se place au même endroit dans les deux écritures : au début du corps, après l'initialisation et avant chaque nouveau tour.

Avec un `for`, il faut donc vérifier :

1. l'invariant après `initialisation` ;
2. sa conservation par `corps`, puis par `mise_a_jour` ;
3. la postcondition avec la condition de boucle devenue fausse.

---

# Invariant et terminaison : le variant

L'invariant prouve la **correction** : si le programme termine, le résultat obtenu est correct.

Il ne prouve pas que la boucle termine. Pour cela, on utilise un **variant de boucle** : une quantité entière ou naturelle qui :

- est bornée inférieurement ;
- diminue strictement à chaque tour ;
- permet donc de ne pas faire une infinité de tours.

Dans :

```c
for (int i = 0; i < n; i++)
```

on peut choisir `n - i` comme variant. Tant que la boucle continue, `n - i` est positif et il diminue de 1 à chaque tour.

À retenir :

- invariant : ce qui reste vrai pendant la boucle ;
- variant : ce qui garantit que la boucle finit.

---

Pour la méthode pratique appliquée au TP5, voir [[Méthode pratique TP5]].

---

# À retenir

Un invariant est une propriété vraie au début de chaque tour de boucle.

Pour prouver un invariant, on vérifie :

1. **initialisation** : il est vrai avant le premier tour ;
2. **conservation** : un tour le rend encore vrai ;
3. **sortie** : avec la condition de fin, il donne la postcondition.

L'invariant prouve la correction du résultat. Le variant prouve la terminaison.

Pour une boucle qui parcourt un tableau, l'invariant décrit généralement les éléments déjà traités et la valeur calculée à partir d'eux.
