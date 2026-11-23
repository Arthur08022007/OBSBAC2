# Septembre 2019 — Exercice 1 — Plus grand préfixe commun de deux tableaux

## Énoncé

### a) Écriture de la fonction

Écrire une fonction C prenant en arguments deux tableaux d’entiers `t1` et `t2` ainsi que leur taille (supposée commune), et retournant la longueur de leur plus grand préfixe commun, c’est-à-dire le plus grand entier `n` tel que `t1[i] = t2[i]` pour tout `i` tel que `0 ≤ i < n`.

### b) Preuve par la méthode des invariants

Par la méthode des invariants, démontrer que la valeur retournée par cette fonction est correcte. Démontrer également que cette fonction se termine.

---

## Résolution

### a) Fonction C

Ce problème peut être résolu en comparant un à un les éléments situés à la même position dans les deux tableaux, tant que ces éléments sont égaux, et en comptant le nombre de positions pour lesquelles cette égalité est constatée. On obtient le code suivant :

```c
unsigned prefixe_commun(int t1[], int t2[], unsigned taille)
{
    unsigned i;

    for (i = 0; i < taille && t1[i] == t2[i]; i++);

    return i;
}
```

> Dans le corrigé officiel, le type du paramètre `taille` a été oublié ; il faut écrire `unsigned taille`.

### b) Preuve par invariant

#### Triplet à démontrer

Montrons d’abord que lorsque la fonction termine son exécution, la valeur qu’elle retourne est correcte. Cela revient à prouver le triplet :

```text
{ taille ≥ 0 }

for (i = 0; i < taille && t1[i] == t2[i]; i++);

{ i = longueur du plus grand préfixe commun de t1[] et t2[] }
```

En développant la boucle `for`, cela équivaut à démontrer :

```text
{ taille ≥ 0, i = 0 }

while (i < taille && t1[i] == t2[i])
    i++;

{ i = longueur du plus grand préfixe commun de t1[] et t2[] }
```

Cherchons un invariant de boucle `I`. Celui-ci doit satisfaire les trois propriétés suivantes :

- `I` doit être impliqué par la précondition (`taille ≥ 0` et `i = 0`) ;
- si `I` est vrai avant une itération de la boucle `while`, alors `I` doit également être vrai à la fin de cette itération ;
- après la dernière itération de la boucle, `I` doit impliquer la postcondition (`i` = longueur du plus grand préfixe commun de `t1[]` et `t2[]`).

#### Invariant

Ces trois propriétés sont vraies pour l’invariant :

```text
I : taille ≥ 0 et i ≤ taille et t1[0 : i − 1] = t2[0 : i − 1]
```

où `t[a : b]` dénote un tableau contenant les éléments de `t` compris entre les indices `a` et `b` (inclus).

#### Initialisation

Initialement, on a :

```text
(taille ≥ 0 et i = 0) ⇒ I
```

car deux tableaux de longueur nulle sont forcément égaux.

#### Conservation

D’une itération à l’autre de la boucle, on a le triplet :

```text
{ I, i < taille, t1[i] = t2[i] }

i++;

{ I }
```

qui est bien valide. En effet, si `i′` dénote la valeur de `i` après l’exécution du fragment de code, on a `i′ = i + 1`, donc :

```text
(I et i < taille et t1[i] = t2[i])
⇒ (i′ ≤ taille et t1[0 : i′ − 1] = t2[0 : i′ − 1])
```

#### Sortie de boucle

En sortie de boucle, on a :

```text
I et (i ≥ taille ou t1[i] ≠ t2[i])
```

qui implique bien `i` = longueur du plus grand préfixe commun de `t1[]` et `t2[]`. Pour le prouver, il y a deux cas à considérer :

- si `(I et i ≥ taille)` est vrai, alors on a `i = taille` et `t1[0 : taille − 1] = t2[0 : taille − 1]`, et le plus grand préfixe commun de `t1[]` et `t2[]` est bien de longueur `i = taille` ;
- si `(I et t1[i] ≠ t2[i])` est vrai, alors le plus grand préfixe commun de `t1[]` et `t2[]` est bien de longueur `i`, car on a alors `t1[0 : i − 1] = t2[0 : i − 1]` et `t1[i] ≠ t2[i]`.

#### Terminaison

Il reste à démontrer que l’exécution de la fonction se termine toujours. Cela peut se faire en considérant le variant de boucle :

```text
v = taille − i
```

qui est clairement un entier non négatif (car l’invariant de boucle `I` implique `i ≤ taille`), dont la valeur décroît strictement à chaque itération de la boucle.
