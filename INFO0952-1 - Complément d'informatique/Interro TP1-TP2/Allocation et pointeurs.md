# Allocation et pointeurs

Slides : partie 1, transparents 44 à 47. L'allocation d'un tableau de chaînes est le même schéma que le tableau d'adresses du transparent 264 (`char **array = malloc(sizeQ * sizeof(char *))`).

## Ce qu'on alloue

`malloc(n)` réserve `n` octets et renvoie un `void *`, ou `NULL` si l'allocation échoue. La taille se calcule avec `sizeof` sur le type d'un élément, multiplié par le nombre d'éléments.

```c
int *q = malloc(10 * sizeof(int)); /* 10 int */
```

Un tableau et un pointeur vers son premier élément se manipulent de la même façon. `a[i]` et `*(a + i)` désignent le même objet. `p + 1` avance d'un élément du type pointé, pas d'un octet (transparent 44).

Une chaîne est un `char *` vers une suite de `char` terminée par `'\0'`. Un tableau de chaînes est donc un tableau de pointeurs : `char **`.

Allouer le tableau de 10 chaînes, c'est allouer 10 pointeurs :

```c
char **t = malloc(10 * sizeof(char *));
```

Cette allocation réserve les pointeurs. Chaque chaîne, si elle doit avoir ses propres caractères, s'alloue à part :

```c
t[i] = malloc(longueur * sizeof(char));
```

Les autres écritures de l'interro décrivent autre chose :

- `malloc(10 * sizeof(char))` réserve 10 caractères, donc une seule chaîne ;
- `malloc(sizeof(10 * char))` n'est pas une expression C valide ;
- `malloc(10)` réserve 10 octets, sans lien avec le type `char *`.

## Le passage d'un tableau

Dans l'appel `f(v)` où `v` est un `int v[1]`, l'argument reçu est l'adresse de `v[0]`. La fonction qui écrit à cette adresse modifie `v`.

```c
void myf1(void *data) {
    (((int *)data)[0])++;
}

int myf2(void (*f)(void *)) {
    int v[1] = {3};
    f(v);
    return v[0];
}
```

`myf2(myf1)` convertit `v` en `int *`, incrémente la case 0, et renvoie 4. L'objet modifié est celui de `myf2`.

La déclaration `void (*f)(void *)` est un pointeur vers une fonction qui reçoit un `void *` et ne renvoie rien. Les parenthèses autour de `*f` font partie du type. `void *f(void *)` serait une fonction qui renvoie un `void *`. Le détail est dans [[void et fonctions]].
