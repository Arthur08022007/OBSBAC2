# Juin 2021 — Exercice 1 — Histogramme des octets d’un tableau

## Énoncé

### a) Écriture de la procédure

Écrire en langage C une procédure prenant en arguments :

- un tableau `t` d’octets non signés,
- le nombre `n ≥ 0` d’octets contenus dans `t`,
- un tableau `h` de 256 entiers de type `int`.

L’opération effectuée par cette procédure consiste à modifier le contenu du tableau `h` de la façon suivante : après l’exécution de la procédure, pour tout `i ∈ [0, 255]`, `h[i]` doit contenir le nombre d’octets de `t` égaux à `i`.

Par exemple, si le tableau `t` contient `[7, 0, 42, 7, 0, 7]`, alors on doit avoir `h[0] = 2`, `h[7] = 3`, `h[42] = 1`, et `h[i] = 0` pour les autres valeurs de `i`.

### b) Complexité

Déterminer la complexité en temps de la procédure obtenue au point (a).

### c) Preuve par la méthode des invariants

Par la méthode des invariants, démontrer que l’opération effectuée par la procédure obtenue au point (a) est correcte.

---

## Résolution

### a) Procédure C

On peut commencer par initialiser tous les éléments du tableau `h` à `0`. Ensuite, on énumère tous les éléments du tableau `t` et on incrémente pour chacun d’entre eux la case correspondante de `h`. (En d’autres termes, si la valeur de l’élément considéré est `α`, alors on incrémente la case de `h` possédant l’indice `α`.) On obtient le code suivant :

```c
void compter(unsigned char t[], unsigned n, int h[])
{
    unsigned i;

    for (i = 0; i < 256; i++)
        h[i] = 0;

    for (i = 0; i < n; i++)
        h[t[i]]++;
}
```

### b) Complexité en temps

On détermine l’évolution du temps de calcul de la procédure en fonction de la taille `n` du tableau d’entrée `t`.

- La première boucle effectue 256 itérations quelle que soit la valeur de `n`.
- La seconde boucle exécute quant à elle `n` itérations.

La complexité en temps de la procédure vaut donc :

```text
O(256 + n) = O(n)
```

### c) Preuve par invariants

#### Triplet à démontrer

On souhaite établir la validité du triplet suivant :

```text
{ n ≥ 0 }

for (i = 0; i < 256; i++)
    h[i] = 0;
for (i = 0; i < n; i++)
    h[t[i]]++;

{ ∀k ∈ [0, 255] : h[k] = nombre de valeurs de t[0 : n − 1] égales à k }
```

où la notation `t[a : b]` dénote le sous-tableau de `t` commençant à l’indice `a` et se terminant à l’indice `b`.

#### Première boucle

La première boucle est chargée d’initialiser les éléments de `h`. Pour montrer que cette opération est réalisée correctement, on peut démontrer le triplet :

```text
{ n ≥ 0 }

for (i = 0; i < 256; i++)
    h[i] = 0;

{ ∀k ∈ [0, 255] : h[k] = 0 }
```

Ce triplet est équivalent à :

```text
{ n ≥ 0, i = 0 }

while (i < 256)
{
    h[i] = 0;
    i++;
}

{ ∀k ∈ [0, 255] : h[k] = 0 }
```

Pour trouver un invariant de boucle `I1`, on exprime le traitement effectué par la boucle jusqu’à une itération donnée, ce qui donne :

```text
I1 : 0 ≤ i ≤ 256 et ∀k ∈ [0, i − 1] : h[k] = 0
```

Montrons que cet invariant est valide.

- **Initialisation :** initialement, on a `{ n ≥ 0, i = 0 } ⇒ I1`.
- **Conservation :** pour chaque itération de la boucle, on a le triplet

  ```text
  { I1, i < 256 }
  h[i] = 0;
  i++;
  { I1 }
  ```

  qui est clairement valide.
- **Sortie de boucle :** en fin de boucle, on a `{ I1, i ≥ 256 } ⇒ { ∀k ∈ [0, 255] : h[k] = 0 }`. En effet, `i ≥ 256` et `i ≤ 256` impliquent `i = 256`.

#### Deuxième boucle

En utilisant le triplet que nous venons de démontrer pour la première boucle, il reste à établir le triplet suivant :

```text
{ n ≥ 0 et ∀k ∈ [0, 255] : h[k] = 0 }

for (i = 0; i < n; i++)
    h[t[i]]++;

{ ∀k ∈ [0, 255] : h[k] = nombre de valeurs de t[0 : n − 1] égales à k }
```

Ce triplet est équivalent à :

```text
{ n ≥ 0, i = 0 et ∀k ∈ [0, 255] : h[k] = 0 }

while (i < n)
{
    h[t[i]]++;
    i++;
}

{ ∀k ∈ [0, 255] : h[k] = nombre de valeurs de t[0 : n − 1] égales à k }
```

On trouve un candidat invariant de boucle `I2` en caractérisant le travail réalisé par la boucle jusqu’à une itération donnée :

```text
I2 : n ≥ 0 et 0 ≤ i ≤ n et
     ∀k ∈ [0, 255] : h[k] = nombre de valeurs de t[0 : i − 1] égales à k
```

Montrons que cet invariant est valide.

- **Initialisation :** initialement, on a bien

  ```text
  { n ≥ 0, i = 0 et ∀k ∈ [0, 255] : h[k] = 0 } ⇒ I2
  ```

  car `i = 0` implique que le nombre d’éléments à considérer dans le tableau `t` est nul.
- **Conservation :** pour chaque itération de la boucle, on a le triplet

  ```text
  { I2, i < n }
  h[t[i]]++;
  i++;
  { I2 }
  ```

  qui est valide : le seul élément du tableau `h` qui change de valeur est celui d’indice `t[i]`.
- **Sortie de boucle :** en fin de boucle, on a bien

  ```text
  { I2, i ≥ n } ⇒ ∀k ∈ [0, 255] : h[k] = nombre de valeurs de t[0 : n − 1] égales à k
  ```
