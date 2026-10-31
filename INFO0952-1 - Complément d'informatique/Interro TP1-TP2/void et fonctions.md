# void et fonctions

Slides : partie 4, transparents 191 à 196 (pointeurs de fonctions, puis `void *`, puis le tri générique qui combine les deux). C'est le mécanisme de `findFirstTrue`. Le mode d'emploi de cette fonction est dans [[findFirstTrue]].

## Pointeur de fonction

Une fonction a une adresse. Son nom désigne cette adresse. On stocke l'adresse dans un paramètre dont le type répète le prototype, avec `*` devant le nom et des parenthèses autour :

```c
bool (*f)(void *, int, void *)
```

L'appel s'écrit `f(tab, i, param)` ou `(*f)(tab, i, param)`. Les deux appellent la fonction pointée.

À l'appel, on passe le nom de la fonction, sans le rappeler :

```c
findFirstTrue(isPointOutOfBall, tab, length, param);
```

## void *

`void *` est un pointeur vers un objet dont le type n'est pas fixé par la fonction qui le reçoit. Il sert à accepter un tableau de n'importe quel type d'élément. Il sert aussi à passer un bloc de contexte dont seule la fonction callback connaît la disposition.

On ne déréférence pas un `void *`, et on ne l'indexe pas : le compilateur ne connaît pas la taille d'un élément. On convertit d'abord vers le type réel, puis on indexe.

```c
float *valeurs = (float *)tab;
return valeurs[i] > 0.0f;
```

L'écriture `((float *)tab)[i]` est la même chose. L'écriture `(float)tab[i]` demande d'indexer d'abord le `void *`, puis de convertir la valeur : elle ne compile pas.

`void *` laisse modifier les éléments après la conversion. Le type opaque, qui empêche le client de voir les champs, est un autre mécanisme : [[Types opaques]].

## Le paramètre de contexte

Dans

```c
int findFirstTrue(bool (*f)(void *, int, void *),
                   void *tab, int length, void *param);
```

`length` est le nombre d'éléments. `param` est transmis tel quel à `f`. Il porte ce que le prédicat a besoin de savoir en plus du tableau et de l'indice : un rayon, un percentile, une longueur, un seuil. La fonction générique n'interprète pas ce bloc.

Le callback relit le bloc avec le type qu'il a choisi au moment de l'appel :

```c
int length = *(int *)param;
float radius = *(float *)param;
```

Si plusieurs valeurs voyagent ensemble, `param` pointe vers un tableau ou une structure, et le callback et l'appelant se mettent d'accord sur l'ordre des champs.
