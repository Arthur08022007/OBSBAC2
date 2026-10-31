# Tau de Kendall

TP 1, exercice 7. Le code est dans `CompInfo/fichiers-tp1-2026-2027/ex7/kendalltau.c`. L'énoncé autorise à réordonner `x` et `y` tant que chaque `x[i]` reste associé au même `y[i]`, et il suppose des valeurs uniques. Les questions de l'interro à blanc testent ce qui, dans cet algorithme, utilise vraiment cette hypothèse.

Le tri fusion utilisé par la version rapide est au transparent 145. Son espace est rappelé dans [[Complexité]].

## Paires

On regarde les paires d'indices. La paire `(i, j)` est discordante lorsque l'ordre dans `x` et l'ordre dans `y` se contredisent :

```c
(x[i] < x[j] && y[i] > y[j]) || (x[i] > x[j] && y[i] < y[j])
```

S'il existe une telle paire, il existe aussi des indices qui la présentent dans un seul sens : `x[i] < x[j]` et `y[i] > y[j]`. C'est la formulation de l'interro. Une comparaison entre `x[i]` et `y[i]` mesure autre chose : elle mélange les deux tableaux case par case.

Une égalité dans `x` ou dans `y` ne rend pas la paire discordante. Les deux inégalités sont strictes.

## La formule

Soit `nd` le nombre de paires discordantes, et `nc` le nombre de paires concordantes. Sans égalité, toute paire est l'un ou l'autre, et le nombre de paires est `N(N-1)/2`.

```text
tau = (nc - nd) / (nc + nd)
    = (nc - nd) / (N(N-1)/2)
```

Comme `nc = N(N-1)/2 - nd` :

```text
tau = 1 - 4 * nd / (N * (N - 1))
```

C'est la formule des deux fonctions du TP. Le coefficient vaut 1 quand les deux classements coïncident, et −1 quand l'un est l'inverse de l'autre.

Exemple de l'interro : `x = [0, 1, 4]`, `y = [0, 2, 1]`.

| Paire | Ordre de x | Ordre de y | |
| --- | --- | --- | --- |
| (0, 1) | 0 < 1 | 0 < 2 | concordante |
| (0, 2) | 0 < 4 | 0 < 1 | concordante |
| (1, 2) | 1 < 4 | 2 > 1 | discordante |

`nd = 1`, `N = 3`, `tau = 1 - 4/(3*2) = 1/3`.

## Version lente

Double boucle sur les paires, un compteur, la formule. Temps O(N²), espace O(1) : aucun tableau auxiliaire.

Cette boucle reste fidèle à la définition lorsqu'il y a des doublons. Une paire avec une égalité n'incrémente pas `nd`. La formule reste définie : elle compte cette paire comme concordante. Le résultat est celui de la définition par inégalités strictes.

## Version rapide

On trie les paires `(x[i], y[i])` par `x` croissant, en emmenant `y` avec son `x`. Une fois `x` trié, chaque paire d'indices `i < j` a `x[i] < x[j]`. Elle est discordante exactement quand `y[i] > y[j]`. `nd` est le nombre d'inversions de `y`.

Ce compte se fait dans la fusion du tri, sans deuxième double boucle. Quand la fusion prend un élément dans la moitié droite, cet élément forme une inversion avec chacun des éléments encore présents dans la moitié gauche. Le tri et le compte sont alors tous les deux O(N log N). Une double boucle sur `y` après le tri ramène le temps à O(N²).

L'espace est celui du tampon de fusion : O(N). Voir [[Complexité]].

Dans ta soumission, ce tampon est un tableau de taille variable (`double tmpx[n]`), pas un `malloc`.

## Doublons et symétrie

La version rapide égale la version lente tant que les valeurs de `x` sont uniques. L'ordre après le tri est alors un ordre total, et chaque inversion de `y` est une vraie discordance.

Un doublon dans `x` laisse la fusion départager deux paires de même `x`. Si elle place le plus grand `y` devant l'autre, elle compte une inversion que la définition refuse, puisque les `x` sont égaux.

```text
x = [1, 1]    y = [0, 2]
```

La version lente voit une égalité dans `x` : `nd = 0`, `tau = 1`. Une fusion qui, à `x` égal, prend d'abord la moitié droite, produit `y = [2, 0]`, compte une inversion, et renvoie `1 - 4*1/(2*1) = -1`.

Un doublon seulement dans `y` ne crée pas cette divergence. `y[i] == y[j]` n'est pas une inversion, et la version lente ne compte pas non plus cette paire. Les deux fonctions renvoient la même valeur.

La symétrie `kendallTau(x, y) = kendallTau(y, x)` vient de la définition : échanger les noms des deux tableaux ne change pas l'ensemble des paires discordantes. Avec des valeurs uniques, la version rapide la respecte. Réordonner les deux tableaux en gardant les paires ne change pas non plus le coefficient : un deuxième appel sur les mêmes tableaux, après que le premier les a triés, revoit les mêmes paires.
