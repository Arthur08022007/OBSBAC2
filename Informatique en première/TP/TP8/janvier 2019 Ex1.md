# Janvier 2019 — Exercice 1 — Égalité de deux tableaux

## Énoncé

### a) Écriture de la fonction

Écrire une fonction C prenant en arguments deux tableaux d’entiers ainsi que la longueur (supposée commune) de ces tableaux, retournant `1` si ces tableaux possèdent le même contenu, et `0` sinon.

### b) Preuve par la méthode des invariants

Par la méthode des invariants, démontrer que la valeur retournée par cette fonction est correcte.

---

## Résolution

### a) Fonction C

Il suffit de parcourir les deux tableaux élément par élément, et de retourner `0` dès que l’on constate la première différence. Si le parcours se termine sans avoir détecté de différence, alors les tableaux sont égaux et la fonction doit retourner `1`. On obtient le code suivant :

```c
int compare(int t1[], int t2[], unsigned longueur)
{
    unsigned i;

    for (i = 0; i < longueur; i++)
        if (t1[i] != t2[i])
            return 0;

    return 1;
}
```

### b) Preuve par invariant

On demande uniquement de démontrer que la valeur retournée par la fonction `compare` est correcte, et non de prouver que cette fonction se termine.

#### Triplet à démontrer

Si `t1[]` et `t2[]` sont deux tableaux de taille `longueur`, cela revient à démontrer le triplet :

```text
{ longueur ≥ 0 }

for (i = 0; i < longueur; i++)
    if (t1[i] != t2[i])
        return 0;
return 1;

{ La valeur retournée est 0 ⇒ les tableaux t1[] et t2[] sont différents.
  La valeur retournée est 1 ⇒ les tableaux t1[] et t2[] sont égaux. }
```

Le plus simple consiste à déterminer un invariant de boucle `I` qui vérifie les trois propriétés suivantes :

- `I` est vrai avant la première itération de la boucle `for` ;
- si `I` est vrai avant une itération de cette boucle, alors `I` est également vrai après celle-ci ;
- après la dernière itération de la boucle, `I` implique la propriété souhaitée.

#### Invariant

Un invariant possible est le suivant :

```text
I : 0 ≤ i ≤ longueur et ∀k ∈ [0, i − 1] : t1[k] = t2[k]
```

#### Initialisation

Avant la première itération de la boucle, on a bien :

```text
{ longueur ≥ 0, i = 0 } ⇒ I
```

#### Conservation

D’une itération à l’autre de la boucle, on a le triplet :

```text
{ I, i < longueur }

if (t1[i] != t2[i])
    return 0;
i++;

{ I }
```

qui est bien valide. En effet :

- si `t1[i] = t2[i]`, alors `i` est incrémenté et la condition `∀k ∈ [0, i − 1] : t1[k] = t2[k]` reste vraie ;
- si `t1[i] ≠ t2[i]`, alors ce code retourne `0` sans avoir modifié `i`.

#### Sortie de boucle

Lorsqu’on sort de la boucle :

- soit la condition `t1[i] != t2[i]` est vraie, auquel cas les tableaux `t1[]` et `t2[]` sont différents et la fonction retourne `0` ;
- soit le gardien de boucle `i < longueur` est faux ; la fonction retourne alors `1`. Dans ce cas, on a :

```text
{ I, i ≥ longueur }
⇒ { I, i = longueur }
⇒ ∀k ∈ [0, longueur − 1] : t1[k] = t2[k]
```

ce qui montre que les tableaux `t1[]` et `t2[]` sont égaux.
