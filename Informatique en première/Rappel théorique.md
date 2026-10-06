# Rappel théorique

À présenter avant [[TP2]]. Quatre points du cours (slides `info-slides-2026`, chapitre 2, et `scanf` au chapitre 6).

## Types de variables

Une variable a un nom et un type. Le type fixe la place en mémoire, la façon d'encoder la valeur, et les opérations permises. On la déclare avant de l'utiliser : `type nom;` ou `type nom = valeur;`.

| Type | Contenu |
| --- | --- |
| `char` | caractère, ou entier sur 8 bits |
| `int` | entier. Taille selon la machine ; souvent 32 bits sur un PC actuel, de −2³¹ à 2³¹ − 1 |
| `float` | réel, simple précision (IEEE 754) |
| `double` | réel, double précision (IEEE 754) |

`signed` et `unsigned` rendent le type signé ou non signé (`int` est signé par défaut). `short`, `long` et `long long` changent la taille d'un `int` ; on peut omettre le mot `int`. Dans le TP, `long long` sert pour un entier trop grand pour un `int`.

Dans les programmes du TP : l'exercice 1 utilise des `double`, l'exercice 2 des `int`, l'exercice 4 un `long long`, l'exercice 5 lit un `double` puis le recopie dans un `int`. Cette copie abandonne la partie fractionnaire : `3.1416` devient `3`.

Le sens de `/` dépend du type. `2 / 3` vaut `0` ; `2.0 / 3.0` vaut `0.6666...`.

## `++` et `--`, avant ou après

`++` ajoute 1, `--` retire 1. L'opérande est une variable. La variable est modifiée dans les deux cas. Ce qui change, c'est la **valeur de l'expression** :

- **après** la variable (`y++`, `y--`) : l'expression vaut la variable **avant** la modification ;
- **avant** la variable (`++y`, `--y`) : l'expression vaut la variable **après** la modification.

Au départ, `x = y = 0` :

| Instruction | `x` | `y` |
| --- | --- | --- |
| `x = y++` | 0 | 1 |
| `x = ++y` | 1 | 1 |
| `x = y--` | 0 | −1 |
| `x = --y` | −1 | −1 |

Écrit seul, `i++` et `++i` font la même chose : on n'utilise pas la valeur de l'expression. C'est le cas de `i++` dans l'exercice 5. La différence n'apparaît que si cette valeur est lue, par exemple dans une affectation ou un `printf`.

On n'écrit pas `x = --x + x++` : la syntaxe est correcte, le résultat n'est pas défini.

## Les boucles

Les trois boucles répètent une instruction, ou un bloc `{ ... }`.

`while` teste **avant** chaque tour. Si le test est faux dès le début, le corps ne s'exécute pas.

```c
while (n >= 2) {
    i++;
    n = n / 2;
}
```

`do ... while` teste **après** le tour. Le corps s'exécute au moins une fois.

```c
do
    instr;
while (expr);
```

`for` place à trois endroits : l'initialisation, le test, et ce qui se fait entre deux tours.

```c
for (expr1; expr2; expr3)
    instr;
```

équivaut à

```c
{
    expr1;
    while (expr2) {
        instr;
        expr3;
    }
}
```

`expr1`, `expr3` et le corps peuvent être absents. Sans `expr2`, le test est toujours vrai. `expr1` peut être une déclaration : `for (long long i = 3; i * i <= n; i += 2)`.

L'exercice 2 n'initialise rien dans le `for`, parce que `n` et `k` sont déjà lus. On teste, on multiplie, **puis** on retire `k` :

```c
for (; n - k > 0; n -= k)
    result *= n;
```

## `printf` et `scanf`

Les deux sont des fonctions de `stdio.h`, pas des mots du langage. Tout programme du TP qui affiche ou lit commence par `#include <stdio.h>`.

`printf` affiche. `scanf` lit au clavier et écrit les valeurs **à l'adresse** des variables : on passe `&n`, pas `n`.

```c
printf("Entrez deux entiers : ");
scanf("%d %d", &n, &k);
printf("Le résultat est %d\n", result);
```

| Spécificateur | Type |
| --- | --- |
| `%d` | `int` |
| `%u` | entier non signé |
| `%lf` | `double` |
| `%lld` | `long long` |
| `%.2lf` | `double` affiché avec deux décimales |

`\n` passe à la ligne. Le spécificateur doit être celui du type : `%lf` pour un `double` (exercices 1 et 5), `%d` pour un `int` (exercice 2), `%lld` pour un `long long` (exercice 4).
