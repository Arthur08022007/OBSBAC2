# Exercice 6

Cours d’introduction à l’informatique  
Énoncés et solutions

Source : [[supports/info-jan2023.pdf]]

---

## Énoncé

### a)

Écrire une fonction acceptant en arguments deux tableaux de nombres entiers `t1` et `t2` ainsi que le nombre (identique) `n` d’éléments de ces tableaux, et retournant le plus grand indice `i` pour lequel `t1[i] = t2[i]`.

Par exemple, pour les tableaux `[0, −1, 0, 10, 10]` et `[10, −1, −10, 10, 0]`, cette fonction doit retourner `3`.

Si la condition `t1[i] = t2[i]` n’est vraie pour aucun indice `i`, alors la fonction doit retourner `−1`.

### b)

Par la méthode des invariants, démontrer que la valeur retournée par cette fonction est correcte.

---

## Solution

### a) Écriture de la fonction

Il suffit de parcourir les tableaux depuis leur dernier élément vers le premier, en s’arrêtant dès que l’on trouve un indice pour lequel les deux tableaux possèdent la même valeur.

```c
int plus_grand_indice(int t1[], int t2[], unsigned n)
{
    int i;

    for (i = n - 1; i >= 0; i--)
        if (t1[i] == t2[i])
            break;

    return i;
}
```

### b) Preuve par invariant

On souhaite établir la validité du triplet suivant :

```text
{n ≥ 0}
for (i = n - 1; i >= 0; i--)
    if (t1[i] == t2[i])
        break;
{i = plus grand indice tel que t1[i] = t2[i],
 ou −1 s’il n’en existe pas}
```

Après avoir transformé la boucle `for`, ce triplet devient :

```text
{n ≥ 0, i = n − 1}
while (i >= 0)
{
    if (t1[i] == t2[i])
        break;
    i--;
}
{i = plus grand indice tel que t1[i] = t2[i],
 ou −1 s’il n’en existe pas}
```

La condition `t1[i] = t2[i]` provoque la sortie de la boucle, ce qui revient à dire que `t1[i] ≠ t2[i]` doit être satisfait pour rester dans cette boucle.

Cette condition peut être incorporée au gardien de la boucle, ce qui mène au triplet équivalent suivant :

```text
{n ≥ 0, i = n − 1}
while (i >= 0 && t1[i] != t2[i])
    i--;
{i = plus grand indice tel que t1[i] = t2[i],
 ou −1 s’il n’en existe pas}
```

Montrons par la méthode des invariants que ce triplet est valide. On trouve un invariant de boucle `I` en caractérisant les opérations effectuées jusqu’à une itération donnée.

Un invariant possible est :

```text
I : n > 0 et i ≥ −1 et ∀j : i < j < n ⇒ t1[j] ≠ t2[j]
```

Cet invariant exprime qu’avant et après chaque itération de la boucle, les tableaux `t1` et `t2` diffèrent pour tous les indices plus grands que la valeur courante de `i`.

Démontrons à présent que cet invariant est correct.

#### Initialisation

Initialement, on a `n ≥ 0` et `i = n − 1`, ce qui satisfait l’invariant. En effet, il n’existe dans ce cas aucun indice `j` satisfaisant `i < j < n`.

#### Conservation

Pour chaque itération de la boucle, on a le triplet :

```text
{I, i ≥ 0, t1[i] ≠ t2[i]}
i--;
{I}
```

Montrons que ce triplet est valide, en notant respectivement `x` et `x'` la valeur d’une variable `x` avant et après l’itération concernée.

On a `n' = n` et `i' = i − 1`. On a donc bien `n' ≥ 0`, et la condition `i ≥ 0` implique `i' ≥ −1`.

De plus, étant donné que l’on a initialement `t1[j] ≠ t2[j]` pour tout `j` tel que `i < j < n`, et que l’on présuppose `t1[i] ≠ t2[i]`, cette condition est également vraie pour tout `j` tel que `i' < j < n'`.

#### Sortie de boucle

En fin de boucle, on a :

```text
{I, i < 0 ou (i ≥ 0 et t1[i] = t2[i])}
```

Cela implique que `i` est bien le plus grand indice tel que `t1[i] = t2[i]` si cet indice existe, ou est égal à `−1` sinon.
