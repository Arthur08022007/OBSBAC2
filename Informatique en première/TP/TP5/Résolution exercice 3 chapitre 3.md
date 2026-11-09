# Résolution de l'exercice 3 du chapitre 3

## Énoncé

L'exercice 3 demande de démontrer la correction et de déterminer la complexité
des programmes obtenus pour les exercices **2, 3, 5 et 6 de la section 1.5**,
ainsi que **5 et 7 de la section 2.6** du syllabus.

Les preuves ci-dessous supposent qu'aucun dépassement arithmétique ne se produit.
Les produits vides valent `1`.

---

## 1.5, exercice 2 — Multifactorielle

Pour `n > 0` et `k > 0`, la multifactorielle est

`M(n, k) = n(n-k)(n-2k)...`

en ne conservant que les termes strictement positifs.

```c
int i = n;
int resultat = 1;

while (i > 0) {
    resultat *= i;
    i -= k;
}
```

### Invariant

Au début de chaque tour, `i = n - qk` pour un entier `q >= 0`, et
`resultat` est le produit des termes déjà retirés :

`resultat = n(n-k)...(i+k)`.

Autrement dit, `resultat` contient le produit des termes de la multifactorielle
strictement supérieurs à `i`.

### Initialisation

Avant le premier tour, `i = n` et `resultat = 1`. Aucun terme n'a encore été
retiré ; le produit vide vaut donc `1`. L'invariant est vrai.

### Conservation

Supposons l'invariant vrai et `i > 0`. Le corps multiplie `resultat` par le
terme courant `i`, puis remplace `i` par `i-k`. Le nouveau produit est donc

`n(n-k)...(i+k) * i`,

qui correspond exactement aux termes strictement supérieurs à la nouvelle
valeur `i-k`. L'invariant est conservé.

### Sortie et correction

À la sortie, `i <= 0`. Tous les termes strictement positifs de la suite
`n, n-k, n-2k, ...` ont été multipliés. Ainsi `resultat = M(n,k)`.

### Terminaison et complexité

Le variant est `i` tant que `i > 0`. Après chaque tour, il diminue de `k > 0`.
La boucle termine après `floor((n-1)/k)+1` tours.

La complexité en temps est **`Theta(n/k)`**, et la complexité en espace est
**`Theta(1)`**.

---

## 1.5, exercice 3 — Statistiques d'une séquence

On reçoit `n > 0` nombres réels `x[1]`, ..., `x[n]` séquentiellement.

```c
double somme, produit, moyenne, minimum, maximum, x;
int i;

scanf("%lf", &x);
somme = produit = x;
minimum = maximum = x;

for (i = 2; i <= n; i++) {
    scanf("%lf", &x);
    somme += x;
    produit *= x;
    if (x < minimum)
        minimum = x;
    if (x > maximum)
        maximum = x;
}

moyenne = somme / n;
```

### Invariant

Au début de l'itération d'indice `i`, après lecture des `i-1` premiers
éléments :

- `somme = x[1] + ... + x[i-1]` ;
- `produit = x[1] * ... * x[i-1]` ;
- `minimum` est le minimum de `x[1], ..., x[i-1]` ;
- `maximum` est le maximum de `x[1], ..., x[i-1]` ;
- `2 <= i <= n+1`.

### Initialisation

Après la lecture de `x[1]`, on a `somme = produit = minimum = maximum = x[1]`
et `i = 2`. L'invariant est donc vrai.

### Conservation

À une itération, `x[i]` est lu. L'ajout et la multiplication donnent
respectivement la somme et le produit des `i` premiers éléments. Les deux
comparaisons conservent le plus petit et le plus grand de ces éléments.
Enfin, `i++` prépare l'itération suivante. L'invariant est conservé.

### Sortie et correction

À la sortie, `i = n+1`. Les variables contiennent donc les statistiques des
`n` éléments :

- `somme` est leur somme ;
- `produit` est leur produit ;
- `moyenne = somme/n` est leur moyenne ;
- `minimum` et `maximum` sont leurs minimum et maximum.

### Terminaison et complexité

Le variant est `n+1-i`. Il est strictement positif au début d'une itération et
diminue de `1`. La boucle termine après `n-1` itérations.

La complexité en temps est **`Theta(n)`**, et la complexité en espace
supplémentaire est **`Theta(1)`**.

---

## 1.5, exercice 5 — Calcul de `floor(log2(n))`

Pour `n > 0`, on peut calculer le résultat sans appeler de fonction
logarithmique :

```c
int puissance = 1;
int resultat = 0;

while (2 * puissance <= n) {
    puissance *= 2;
    resultat++;
}
```

### Invariant

Au début de chaque tour :

`puissance = 2^resultat` et `puissance <= n`.

### Initialisation

`puissance = 1 = 2^0`, `resultat = 0`, et `1 <= n` puisque `n > 0`.
L'invariant est vrai.

### Conservation

La condition donne `2 * puissance <= n`. Après le corps,

`puissance' = 2 * puissance = 2^(resultat+1)`

et `resultat' = resultat+1`. De plus, `puissance' <= n`. L'invariant est
conservé.

### Sortie et correction

À la sortie, `2 * puissance > n`. Avec l'invariant :

`puissance <= n < 2 * puissance`.

Comme `puissance = 2^resultat`, on obtient
`2^resultat <= n < 2^(resultat+1)`. Par définition,
`resultat = floor(log2(n))`.

### Terminaison et complexité

Le variant `n - puissance` est un entier naturel. À chaque tour,
`puissance` est remplacée par `2*puissance`, donc le variant diminue
strictement. Il y a `floor(log2(n))` tours.

La complexité en temps est **`Theta(log n)`**, et la complexité en espace est
**`Theta(1)`**.

---

## 1.5, exercice 6 — Exponentiation modulaire

On veut calculer `a^b mod m`, avec `b >= 0` et `m > 0`, par exponentiation
rapide.

```c
int resultat = 1 % m;
int base = a % m;
int exposant = b;

while (exposant > 0) {
    if (exposant % 2 == 1)
        resultat = (resultat * base) % m;
    base = (base * base) % m;
    exposant /= 2;
}
```

### Invariant

Au début de chaque tour :

`resultat * base^exposant ≡ a^b (mod m)`.

Initialement, `resultat = 1` et `base ≡ a (mod m)`, donc l'invariant est
vrai.

### Conservation

Si `exposant` est impair, on remplace d'abord `resultat` par
`resultat * base`. Le produit restant à traiter devient alors
`base^(exposant-1)`. Si `exposant` est pair, `resultat` ne change pas.

Dans les deux cas, on remplace ensuite `base` par `base^2 mod m` et
`exposant` par `floor(exposant/2)`. Les puissances vérifient donc

- si `exposant = 2q` : `base^(2q) = (base^2)^q` ;
- si `exposant = 2q+1` : `base^(2q+1) = base * (base^2)^q`.

L'invariant est conservé modulo `m`.

### Sortie et correction

À la sortie, `exposant = 0`. L'invariant devient

`resultat ≡ a^b (mod m)`.

Le programme retourne donc bien `a^b mod m`.

### Terminaison et complexité

Le variant est `exposant`. La division entière par `2` le diminue
strictement lorsqu'il est positif. Il y a `Theta(log b)` tours pour `b > 0`
et un seul cas traité pour `b = 0`.

La complexité en temps est **`Theta(log b)`**, et la complexité en espace est
**`Theta(1)`**.

---

## 2.6, exercice 5 — Nombres de Fibonacci

On rappelle `F1 = 1`, `F2 = 1` et `Fn = Fn-1 + Fn-2`.

```c
int fibonacci(int n) {
    int precedent, courant, suivant, i;

    if (n <= 2)
        return 1;

    precedent = 1;  /* F1 */
    courant = 1;    /* F2 */
    i = 2;

    while (i < n) {
        suivant = precedent + courant;
        precedent = courant;
        courant = suivant;
        i++;
    }

    return courant;
}
```

### Invariant

Au début de chaque tour, `2 <= i <= n` et

`précédenat = F(i-1)` et `courant = F(i)`.

### Initialisation

Après l'initialisation, `i = 2`, `precedent = F1 = 1` et
`courant = F2 = 1`. L'invariant est vrai.

### Conservation

Le corps calcule

`suivant = precedent + courant = F(i-1) + F(i) = F(i+1)`.

Après les affectations, `precedent = F(i)` et `courant = F(i+1)`, puis
`i` devient `i+1`. L'invariant est conservé.

### Sortie et correction

La boucle s'arrête avec `i = n`. L'invariant donne `courant = F(n)`, qui est
la valeur retournée. Les cas `n = 1` et `n = 2` sont traités directement.

### Terminaison et complexité

Le variant est `n-i`, qui diminue de `1` à chaque tour. La boucle effectue
`n-2` tours.

La complexité en temps est **`Theta(n)`**, contre `Theta(2^n)` pour une
version récursive naïve. La complexité en espace supplémentaire est
**`Theta(1)`**.

---

## 2.6, exercice 7 — Coefficient binomial

Pour `0 <= m <= n`, on utilise la relation

`C(n,i) = C(n,i-1) * (n-i+1) / i`.

```c
int coefficient_binomial(int n, int m) {
    int coefficient = 1;
    int i = 0;

    while (i < m) {
        i++;
        coefficient =
            coefficient * (n - i + 1) / i;
    }

    return coefficient;
}
```

La division est exacte à chaque itération, puisque les coefficients
binomiaux sont entiers. On suppose également que les calculs intermédiaires
ne provoquent pas de dépassement.

### Invariant

Au début de chaque tour :

`0 <= i <= m` et `coefficient = C(n,i)`.

### Initialisation

`i = 0` et `coefficient = 1 = C(n,0)`. L'invariant est vrai.

### Conservation

La mise à jour donne, par la relation entre coefficients binomiaux :

`coefficient' = C(n,i) * (n-i) / (i+1) = C(n,i+1)`.

Puisque `i` devient `i+1`, l'invariant est conservé.

### Sortie et correction

À la sortie, `i = m`. L'invariant donne
`coefficient = C(n,m)`, qui est le résultat demandé.

### Terminaison et complexité

Le variant est `m-i`. Il diminue de `1` à chaque tour. La boucle effectue
exactement `m` tours.

La complexité en temps est **`Theta(m)`**, donc **`O(n)`**, et la complexité
en espace supplémentaire est **`Theta(1)`**.

---

## Synthèse

| Programme | Invariant central | Complexité en temps |
| --- | --- | --- |
| Multifactorielle | produit des termes déjà traités | `Theta(n/k)` |
| Statistiques | statistiques du préfixe déjà lu | `Theta(n)` |
| `floor(log2(n))` | `puissance = 2^resultat` | `Theta(log n)` |
| Exponentiation modulaire | `resultat * base^exposant ≡ a^b (mod m)` | `Theta(log b)` |
| Fibonacci | `precedent = F(i-1)`, `courant = F(i)` | `Theta(n)` |
| Coefficient binomial | `coefficient = C(n,i)` | `Theta(m)` |
