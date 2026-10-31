# Types opaques

Slides : partie 4, transparents 183 à 186. Le transparent 185 résume la restriction utile en interro : le client manipule le type par pointeur.

## Le partage entre .h et .c

Le `.h` annonce le nom du type et cache sa disposition :

```c
typedef struct Point_t Point;
```

`Point` est alors un type incomplet. Le compilateur connaît le nom, pas la taille, pas les champs.

Le `.c` du module donne la disposition, après avoir inclus le `.h` :

```c
struct Point_t {
    int x;
    int y;
};
```

À partir de cette définition, et seulement dans ce fichier, `Point` est un type complet.

## Ce qui compile

| Extrait | Dans le `.c` qui définit `struct Point_t` | Dans un fichier qui n'inclut que le `.h` |
| --- | --- | --- |
| `Point *p;` | oui | oui |
| `Point *p = malloc(sizeof(Point));` | oui | non : `sizeof` d'un type incomplet |
| `p->x = 4;` | oui | non : les champs sont inconnus |
| `Point p;` | oui | non : la taille est inconnue |
| `p.x = 4;` | oui | non |

`malloc` a besoin de `stdlib.h` dans les deux fichiers. Cet include ne change pas la colonne du tableau : l'erreur qui sépare les deux fichiers est le type incomplet.

Un pointeur vers un type incomplet est un pointeur ordinaire : sa taille est connue, on peut le déclarer, le passer, le renvoyer. On ne peut pas réserver un `Point` automatique, ni calculer `sizeof(Point)`, ni lire un champ.

## Le point et la flèche

`p.x` exige que `p` soit une structure. `p->x` exige que `p` soit un pointeur vers une structure. Les deux exigent que le type soit complet.

```c
Point *p1 = malloc(sizeof(Point));
Point p2;
p2.x += p1.x;
```

`p1` a le type `Point *`. L'accès au champ s'écrit `p1->x`. L'expression `p1.x` est rejetée dans le `.c` du module comme dans le client.

Le transparent 48 rappelle que `p->c` est une abréviation de `(*p).c`.
