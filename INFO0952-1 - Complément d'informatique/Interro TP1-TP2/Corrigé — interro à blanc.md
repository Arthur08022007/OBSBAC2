# Corrigé — interro à blanc

[[interro_a_blanc_tp1_tp2.pdf]], 6 octobre 2026. Chaque réponse renvoie à la note qui traite la famille de questions.

## Connaissance générale du C

**1. Tableau de 10 chaînes : `malloc(10 * sizeof(char *))`.**

Un tableau de chaînes est un tableau de `char *`. Les trois autres expressions réservent 10 caractères, ne compilent pas, ou réservent 10 octets. [[Allocation et pointeurs]]

**2. `myf2(myf1)` renvoie 4.**

`v` vaut `{3}`. Le tableau passé à `myf1` est l'adresse de `v[0]`. L'incrément écrit 4 dans cette case, et `myf2` la relit. [[Allocation et pointeurs]]

**3. Type opaque `Point`.**

```c
Point *p = malloc(sizeof(Point));
p->x = 4;
```

Permis dans `bidule.c`. Le client qui n'a que le `.h` a un type incomplet : `sizeof(Point)` et le champ `x` lui sont inaccessibles.

```c
Point p;
p.x = 4;
```

Permis dans `bidule.c`. Déclarer un `Point` automatique demande sa taille.

```c
Point *p1 = malloc(sizeof(Point));
Point p2;
p2.x += p1.x;
```

Aucun des deux. `p1` est un `Point *` : le champ se lit avec `p1->x`. [[Types opaques]]

## TP 1

**1. `malloc` dans ta solution : non.**

`kendallTauSlow` n'alloue rien. `kendallTauFast` réserve son tampon de fusion par un tableau de taille variable (`double tmpx[n]`), pas par `malloc`. [[Tau de Kendall]]

**2. Paire discordante : il existe `i` et `j` tels que `x[i] < x[j]` et `y[i] > y[j]`.**

C'est l'ordre dans `x` contredit par l'ordre dans `y`. L'autre sens de la contradiction est la même paire, indices échangés.

**3. `x = [0, 1, 4]`, `y = [0, 2, 1]` : tau = 1/3.**

Une paire discordante sur les trois, `(1, 2)`. `1 - 4*1/(3*2) = 1/3`.

**4. `kendallTauSlow` avec des doublons : oui.**

La double boucle utilise des inégalités strictes. Une égalité n'est pas une discordance, et la formule reste calculable. Le résultat suit la définition par paires.

**5. `kendallTauFast` avec des doublons : seulement s'il n'y a pas de doublons dans `x`.**

Après le tri sur `x`, les inversions de `y` sont les paires discordantes tant que cet ordre est total. Deux `x` égaux peuvent être départagés par la fusion, et une inversion de `y` entre eux est alors comptée. Un doublon seulement dans `y` n'est pas une inversion, ni pour la version lente ni pour la version rapide.

**6. `kendallTauFast(x, y)` et `kendallTauFast(y, x)` : oui, toujours.**

Avec des valeurs uniques, échanger les deux tableaux ne change pas l'ensemble des paires discordantes. Le tri a le droit de les réordonner : les paires restent les mêmes.

**7. Espace de `kendallTauSlow` : O(1).**

Un compteur, deux indices, l'entrée.

**8. Espace de `kendallTauFast` : O(N).**

Le tampon de fusion. La profondeur d'appels O(log N) est dominée par ce tampon. O(N log N) est le temps, pas l'espace. [[Complexité]]

## TP 2

**9. `tab` est un `void *` pour accepter n'importe quel type de tableau.**

[[void et fonctions]]

**10. `param` transmet des données de contexte à `f`.**

La longueur est déjà le paramètre `length`.

**11. Le callback sur des `float` : non.**

`tab` est un `void *`. On le convertit, puis on indexe :

```c
bool f(void *tab, int i, void *param)
{
    return ((float *)tab)[i] > 0.0f;
}
```

**12. L'appel sur `"cccooooo"` : le code ne compile pas.**

`fo` indexe `tab`, qui est un `void *`. Le `char *tabp` est calculé et n'est pas utilisé. Avec `tabp[length - 1 - i]`, le prédicat est faux pour `i` de 0 à 4 et vrai ensuite, et `findFirstTrue` renvoie 5. [[findFirstTrue]]

**13. Version naïve en O(N).**

```c
int findFirstTrue(bool (*f)(void *, int, void *),
                   void *tab, int length, void *param)
{
    for (int i = 0; i < length; i++) {
        if (f(tab, i, param))
            return i;
    }
    return length;
}
```
