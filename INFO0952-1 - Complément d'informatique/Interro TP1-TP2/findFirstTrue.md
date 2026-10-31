# findFirstTrue

TP 2, exercice 2. Énoncé : `CompInfo/fichiers-tp2-2026-2027/ex2/60511458.pdf`. Le mécanisme `void *` et pointeur de fonction est dans [[void et fonctions]]. La recherche dichotomique du cours est aux transparents 135 à 138.

## Le contrat

```c
int findFirstTrue(bool (*f)(void *, int, void *),
                   void *tab, int length, void *param);
```

`f(tab, i, param)` est vrai lorsque l'élément d'indice `i` a la propriété cherchée. Le tableau est disposé en un préfixe où `f` est faux, suivi d'un suffixe où `f` est vrai. La fonction renvoie le premier indice du suffixe. Si `f` est faux partout, elle renvoie `length`.

`tab` est un `void *` pour que le même algorithme serve à des `float`, des `Point`, des `int`, des `char`. `param` est le contexte passé tel quel à `f` : un rayon, un percentile, une longueur. `length` suffit pour le nombre d'éléments ; `param` ne le remplace pas.

## Version naïve, O(N)

C'est celle demandée à la fin de l'interro à blanc. Elle parcourt depuis la gauche et s'arrête au premier vrai.

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

Elle fait au plus N appels à `f`. Elle n'alloue rien. Elle reste correcte même si le tableau n'a pas la forme préfixe faux puis suffixe vrai, parce qu'elle regarde les indices dans l'ordre.

## Version dichotomique, O(log N)

La recherche du transparent 138 cherche une clé et renvoie −1 si elle est absente. Ici on cherche une frontière. L'intervalle `[left, right[` contient cette frontière : tout indice avant `left` est faux, tout indice à partir de `right` est vrai.

```c
int findFirstTrue(bool (*f)(void *, int, void *),
                   void *tab, int length, void *param)
{
    int left = 0;
    int right = length;

    while (left < right) {
        int middle = left + (right - left) / 2;
        if (f(tab, middle, param))
            right = middle;
        else
            left = middle + 1;
    }
    return left;
}
```

`left + (right - left) / 2` est le milieu du transparent 136, écrit ainsi pour éviter le dépassement de `left + right`. Chaque tour appelle `f` une fois et coupe l'intervalle en deux : O(log N) appels, O(1) en espace. La forme préfixe puis suffixe est indispensable. Sans elle, le test sur `middle` ne dit rien des autres indices.

## Tracer un appel

On écrit la valeur de `f` à chaque indice, on vérifie qu'elle passe une seule fois de faux à vrai, puis on applique la boucle.

Pour `tab = "cccooooo"`, `length = 8`, et le prédicat « le caractère d'indice `length - 1 - i` vaut `'c'` » :

| i | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| caractère en `7 - i` | o | o | o | o | o | c | c | c |
| f | faux | faux | faux | faux | faux | vrai | vrai | vrai |

| left | right | middle | f(middle) | mise à jour |
| --- | --- | --- | --- | --- |
| 0 | 8 | 4 | faux | left = 5 |
| 5 | 8 | 6 | vrai | right = 6 |
| 5 | 6 | 5 | vrai | right = 5 |

`left == right == 5`. La frontière est à l'indice 5.

Le prédicat de l'interro est écrit `tab[length - 1 - i]` alors que `tab` est un `void *`, avec un `char *tabp` calculé et non utilisé. Indexer un `void *` ne compile pas. La version qui compile utilise `tabp` :

```c
bool fo(void *tab, int i, void *param)
{
    int length = *(int *)param;
    char *tabp = (char *)tab;
    return tabp[length - 1 - i] == 'c';
}
```

## Les deux applications du TP

`findLastPointinBall` reçoit des points triés par distance croissante au premier. Le prédicat est vrai quand la distance au premier dépasse le rayon. `param` porte ce rayon. L'indice renvoyé par `findFirstTrue` est le premier point dehors ; le dernier point dedans est cet indice moins un. Si tous sont dedans, `findFirstTrue` renvoie `length` et le dernier indice est `length - 1`.

`getPercentile` reçoit un tableau d'entiers trié croissant. Le prédicat est vrai quand `tab[i] > p * tab[length - 1]`. `param` porte `p` et la longueur, puisque le callback ne reçoit pas `length` à part. La fonction renvoie directement la frontière.
