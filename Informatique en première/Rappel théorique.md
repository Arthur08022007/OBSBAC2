# Rappel théorique

Rappel à faire aux élèves **avant** qu'ils n'écrivent les programmes de [[TP2]]. Il reprend uniquement les notions des slides `info-slides-2026` (Bernard Boigelot) dont ces programmes ont besoin :

- chapitre 1 — algorithme, programme, premier exemple en C, compilation ;
- chapitre 2 — variables, expressions, `if`, `while`, `for` ;
- chapitre 3 — énumérer les diviseurs d'un entier, s'arrêter dès que la réponse est connue, ne tester que jusqu'à la racine ;
- chapitre 4 — fonction, `return`, `main`, `#include` ;
- chapitre 6 — le seul point utile ici : `&variable` pour que `scanf` sache où écrire.

Les quatre programmes du TP ne font qu'assembler ces briques. Un programme C exécute ses instructions **l'une après l'autre**, sauf lorsqu'un `if` choisit une branche ou qu'une boucle répète un bloc.

## 1. D'un problème à un programme

Un **algorithme** est une procédure qui résout un problème en décrivant précisément les opérations à effectuer. Il transforme des données d'entrée en données de sortie. Ces données peuvent être connues dès le départ, ou lues et affichées en cours d'exécution.

Ce même algorithme s'écrit ensuite sous la forme d'un **programme**. En C, on distingue :

- la **syntaxe** : ce qu'il est permis d'écrire ;
- la **sémantique** : ce que le programme fait quand on l'exécute.

La plupart des instructions se terminent par un point-virgule. Plusieurs instructions à la suite forment une **séquence** : elles s'exécutent dans l'ordre où elles sont écrites. Une séquence entourée d'accolades est un **bloc**. Un bloc joue le même rôle qu'une instruction seule.

Les espaces, tabulations et sauts de ligne ne changent pas le sens du programme. On les utilise pour l'indenter, donc pour le rendre lisible.

Le processeur n'exécute pas le fichier `.c`. Un **compilateur** le traduit en code machine :

```bash
gcc -o programme programme.c
./programme
```

Si le programme appelle une fonction de la bibliothèque mathématique (`sqrt`, et plus tard `sin`, `cos`), il faut lier cette bibliothèque :

```bash
gcc -o programme programme.c -lm
```

## 2. Le squelette d'un programme

La forme la plus simple est une fonction `main`. C'est le point d'entrée : elle est appelée dès le lancement du programme. Elle retourne un entier, le code de diagnostic. Par convention, `0` signifie « exécution sans erreur ».

```c
#include <stdio.h>

int main()
{
    /* instructions */
    return 0;
}
```

- `#include <stdio.h>` n'est pas une instruction. C'est une directive qui donne au compilateur les prototypes de `printf` et de `scanf`. Tout programme du TP qui affiche ou lit au clavier doit l'avoir. Le code de l'exercice 5, dans [[TP2]], ne la montre pas : il faut l'ajouter pour compiler.
- `#include <math.h>` joue le même rôle pour `sqrt`.
- `return 0;` termine `main` et renvoie le code 0.
- Un `return` placé plus haut termine la fonction **immédiatement**. Les instructions qui suivent ne s'exécutent pas. C'est ainsi que les exercices 1 et 4 s'arrêtent dès que la réponse est connue.

Le cours écrit `int main()`. L'exercice 4 est rédigé `void main()`. `void` est le type d'une procédure, une fonction qui ne renvoie pas de valeur : le `return` n'est alors pas suivi d'une expression. La forme du cours reste `int main()` avec `return 0;`.

## 3. Variables et types

Une variable est une zone mémoire qui retient une valeur. Elle a :

- un **identificateur** (son nom) : lettres, chiffres et `_`, en commençant par une lettre. Les majuscules et les minuscules sont distinctes ;
- un **type**, qui fixe la taille mémoire, l'encodage de la valeur, et les opérations permises.

Types utilisés dans le TP :

| Type | Rôle dans le TP | Exemple |
| --- | --- | --- |
| `int` | entier | compteur, produit, exposant |
| `double` | réel en double précision (IEEE 754) | coefficients, discriminant, logarithme |
| `long long` | entier de plus grande taille. Sur un PC actuel, souvent 64 bits | le nombre dont on teste la primalité |

Une variable se **déclare avant d'être utilisée** :

```c
double a, b, c, delta;
int result = 1;
long long n;
```

Le `= valeur` est facultatif : il donne la valeur initiale. Sans lui, la variable existe mais son contenu n'est pas défini tant qu'on ne lui a rien affecté.

La déclaration est valable dès qu'elle apparaît, et jusqu'à la fin du plus petit bloc qui la contient. On déclare les variables en début de bloc : ce n'est pas imposé par le langage, c'est ce qui rend le programme lisible. Les versions récentes du C permettent aussi de déclarer la variable de boucle directement dans le `for`, comme `for (long long i = 3; ...)`.

On choisit des noms qui disent à quoi sert la variable (`delta`, `partieReelle`, `n_copy`).

## 4. Expressions, calculs, affectations

Une expression calcule une valeur. Ce peut être une variable, une constante (`1`, `2.0`, `3`), ou des opérateurs appliqués à d'autres expressions.

Opérateurs arithmétiques : `+`, `-`, `*`, `/`, et `%` (reste de la division, réservé aux entiers). `+` et `-` existent aussi en unaire : `-b`, `-delta`.

La priorité est celle de l'algèbre. `b * b - 4 * a * c` se lit `(b * b) - ((4 * a) * c)`. On met des parenthèses dès que l'ordre doit être évident, comme dans `(-b - sqrt(delta)) / (2 * a)`.

Le sens de `/` dépend du type des opérandes :

```c
2 / 3        /* entier : 0 */
2.0 / 3.0    /* réel   : 0.6666... */
```

`%` ne correspond au modulo mathématique que pour des opérandes positifs. `n % i == 0` signifie « `i` divise `n` ». Le cours écrit souvent la même condition sous la forme `!(n % i)` : le reste vaut 0, donc la négation est vraie.

Affecter, c'est évaluer le membre droit et l'écrire dans la variable de gauche :

```c
delta = b * b - 4 * a * c;
x1 = -b / (2 * a);
```

Les opérateurs `+=`, `-=`, `*=`, `/=`, `%=` abrègent une mise à jour. `result *= n` est exactement `result = result * n`. De même, `n -= k` est `n = n - k`, et `i += 2` est `i = i + 2`.

Les comparaisons `<`, `>`, `<=`, `>=`, `==`, `!=` produisent une valeur vraie ou fausse. En C, **faux** vaut `0`, et **vrai** vaut n'importe quel entier non nul. C'est pour cela qu'un `if (a)` et un `while (a)` testent « `a` est non nul ».

`==` teste l'égalité. `=` affecte. Les deux s'écrivent dans le TP : `a == 0` est un test, `delta = b * b - 4 * a * c` est un calcul.

## 5. Choisir : `if`, `else`

```c
if (expr)
    instr1;
else
    instr2;
```

On évalue `expr`. Si elle est vraie (non nulle), on exécute `instr1`. Sinon, et seulement si le `else` est présent, on exécute `instr2`. Chaque branche peut être un bloc, ou une autre instruction de contrôle.

Un `else` se rattache au `if` le plus proche du même bloc. Pour enchaîner trois cas, on écrit un `else` dont l'instruction est un nouveau `if`. C'est le schéma de l'exercice 1, le même que celui du test d'année bissextile dans les slides :

```c
if (delta > 0) {
    /* deux racines réelles */
}
else if (delta == 0) {
    /* une racine double */
}
else {
    /* delta < 0 : deux racines complexes */
}
```

Le dernier `else` n'a pas de condition : on y arrive précisément quand les deux tests précédents sont faux.

## 6. Répéter : `while` et `for`

`while` répète une instruction **tant que** la condition est vraie. La condition est testée **avant** chaque tour. Si elle est fausse dès le début, le corps ne s'exécute jamais.

```c
while (n >= 2) {
    i++;
    n = n / 2;
}
```

`for` est le même mécanisme, avec trois emplacements explicites : ce qu'on fait avant d'entrer, le test de continuation, et ce qu'on fait entre deux tours.

```c
for (expr1; expr2; expr3)
    instr;
```

est équivalent à

```c
{
    expr1;
    while (expr2) {
        instr;
        expr3;
    }
}
```

`expr1`, `expr3` et le corps sont facultatifs. Si `expr2` est absente, elle est considérée comme toujours vraie. La boucle de l'exercice 2 n'a pas d'initialisation : `n` et `k` ont déjà leur valeur, lue au clavier.

```c
for (; n - k > 0; n -= k) {
    result *= n;
}
```

se lit donc

```c
while (n - k > 0) {
    result *= n;
    n -= k;
}
```

L'ordre compte : on teste, on multiplie par la valeur **actuelle** de `n`, et seulement ensuite on retire `k`.

`i++` ajoute 1. Dans l'exercice 4, `i += 2` avance de 2, donc ne visite que les impairs si l'on part de 3.

## 7. Afficher, lire, convertir

`printf` affiche sur la console. `scanf` lit ce qui est tapé au clavier. Ce ne sont pas des mots-clés : ce sont des fonctions de la bibliothèque standard, déclarées dans `stdio.h`.

`scanf` ne reçoit pas la variable, mais **l'endroit où elle se trouve**. Si `v` est une variable, `&v` est l'adresse de `v`. La fonction écrit la valeur lue à cette adresse.

| Spécificateur vu dans le cours ou dans le TP | Type lu ou affiché |
| --- | --- |
| `%d` | `int` |
| `%u` | entier non signé |
| `%lf` | `double` |
| `%lld` | `long long` (c'est celui qu'utilise l'exercice 4) |

`%.2lf` est un `%lf` dont on n'affiche que deux chiffres après la virgule. `\n` passe à la ligne. Un appel peut lire plusieurs valeurs : `scanf("%d %d", &n, &k)` attend deux entiers.

On peut ranger une valeur numérique dans une variable d'un autre type numérique. La conversion est alors faite automatiquement. Le cours donne l'exemple d'un `double` recopié dans un `int` : la partie fractionnaire est abandonnée (`3.1416` devient `3`). C'est exactement `int n_copy = n;` quand `n` est un `double`. L'opérateur `(type) expr` force la même conversion explicitement : `(int) a / (int) b` divise des entiers, donc `2.0 / 3.0` tronqués donnent `0`, alors que `2.0 / 3.0` vaut `0.6666...`.

Appeler une fonction, c'est évaluer `f(expr1, expr2, ...)`. Si elle retourne une valeur, l'appel vaut cette valeur. `sqrt(delta)` retourne la racine carrée de `delta`. Son prototype est dans `math.h`, et l'édition de liens demande `-lm`.

## 8. Exercice 1 — équation du second degré

Énoncé résolu par le programme : étant donnés trois réels `a`, `b`, `c`, résoudre `a x^2 + b x + c = 0`.

Algorithme, dans l'ordre où le programme le déroule :

1. Lire `a`, `b` et `c` dans des `double` (`%lf`, et l'adresse de chaque variable).
2. Si `a == 0`, ce n'est pas une équation du second degré. On l'affiche et on s'arrête (`return`).
3. Calculer le discriminant `delta = b * b - 4 * a * c`.
4. Choisir selon le signe de `delta`.
   - `delta > 0` : deux racines réelles distinctes, `(-b - sqrt(delta)) / (2 * a)` et `(-b + sqrt(delta)) / (2 * a)`.
   - `delta == 0` : une racine réelle double, `-b / (2 * a)`.
   - sinon (`delta < 0`) : deux racines complexes conjuguées. La partie réelle est `-b / (2 * a)`. La partie imaginaire est `sqrt(-delta) / (2 * a)`. On affiche `partie réelle - partie imaginaire i` et `partie réelle + partie imaginaire i`.

Ce qu'il faut avoir en main pour l'écrire : `double`, un enchaînement `if` / `else if` / `else`, `sqrt` (donc `math.h` et `-lm`), et `%.2lf` pour afficher les résultats avec deux décimales.

`==` sur un `double` teste l'égalité exacte des valeurs stockées. C'est bien ce que le programme fait pour `a` et pour `delta`.

## 9. Exercice 2 — produit le long d'une suite

Le programme lit deux entiers `n` et `k`, part de `result = 1`, et répète : tant que `n - k > 0`, multiplier `result` par `n`, puis remplacer `n` par `n - k`.

Les termes pris dans le produit sont donc ceux de la suite `n`, `n - k`, `n - 2k`, … qui sont strictement supérieurs à `k`. Le terme suivant, qui ne satisfait plus `n > k`, n'est pas multiplié.

Trace pour `n = 10` et `k = 3` :

| Avant le tour | Test `n - k > 0` | `result` après `result *= n` | `n` après `n -= k` |
| --- | --- | --- | --- |
| `n = 10` | `7 > 0`, on entre | `1 * 10 = 10` | `7` |
| `n = 7` | `4 > 0`, on entre | `10 * 7 = 70` | `4` |
| `n = 4` | `1 > 0`, on entre | `70 * 4 = 280` | `1` |
| `n = 1` | `-2 > 0` est faux | on s'arrête | |

Le programme affiche `280`.

Ce qu'il faut avoir en main : `scanf("%d %d", &n, &k)`, un `for` sans initialisation, et les abréviations `*=` et `-=`. Réécrire la boucle en `while` (section 6) est le bon contrôle avant de la coder.

## 10. Exercice 4 — un entier est-il premier ?

Le cours pose « déterminer si un nombre naturel est premier » comme problème algorithmique type. Le chapitre sur les nombres parfaits donne la méthode qui sert ici : un entier positif `n` est premier lorsqu'il est supérieur ou égal à 2 et qu'aucun entier `d` avec `2 ≤ d ≤ n - 1` ne le divise.

On n'a pas besoin de tester tous ces candidats.

- 1 divise tout le monde : on ne le teste pas, et tout `n < 2` est déclaré non premier tout de suite.
- Si `d` divise `n` et `d ≤ n / d`, alors `d ≤ √n`. Il suffit donc de tester les candidats tant que `d * d <= n`. C'est l'amélioration du cours : on écrit `d * d <= n` plutôt que de calculer une racine. Le produit reste entier, ce qui évite de passer par un `double`.
- Dès qu'un diviseur est trouvé, la réponse est connue. On l'affiche et on quitte la fonction (`return`), comme le cours arrête l'énumération dès que continuer ne peut plus changer le résultat.
- Après avoir traité 2 à part, les candidats pairs sont inutiles. On part de `i = 3` et on avance avec `i += 2`.

Le programme du TP suit ce schéma avec un `long long`, lu par `%lld` :

1. si `n < 2`, afficher que `n` n'est pas premier et s'arrêter ;
2. si `n == 2`, afficher que `n` est premier et s'arrêter ;
3. pour `i = 3`, `5`, `7`, … tant que `i * i <= n`, si `n % i == 0`, afficher que `n` n'est pas premier, afficher le diviseur `i`, et s'arrêter ;
4. si la boucle se termine sans avoir trouvé de diviseur, afficher que `n` est premier.

Point à dire explicitement : la boucle ne teste que des diviseurs impairs. Pour que l'algorithme soit correct, un entier **pair et supérieur à 2** doit être écarté avant elle (`n % 2 == 0`), sinon 2 n'est jamais essayé. Le code recopié dans [[TP2]] ne fait pas ce test : 4, 6, 8… y sont déclarés premiers. La version à faire écrire aux élèves est celle qui rejette ces pairs.

## 11. Exercice 5 — partie entière du logarithme en base 2

Pour un réel `n ≥ 1`, la partie entière de `log2(n)` est le nombre de fois que l'on peut diviser `n` par 2 avant d'obtenir une valeur strictement inférieure à 2. Chaque division fait descendre l'exposant de 1 : `8 → 4 → 2 → 1` compte 3, et `log2(8) = 3`.

Le programme :

1. lit un `double` avec `%lf` (le message demande un entier, mais la variable est un réel) ;
2. en garde une copie entière, `int n_copy = n`, **avant** de modifier `n`. La conversion `double` vers `int` supprime la partie fractionnaire. Cette copie sert seulement à l'affichage final : la boucle, elle, détruit `n` ;
3. part de `i = 0` et, tant que `n >= 2`, incrémente `i` et remplace `n` par `n / 2` ;
4. affiche `i`.

Comme `n` est un `double`, `n / 2` est une division réelle, pas une division entière. Le compteur augmente d'une unité à chaque division, donc la valeur affichée est la même que si l'on avait divisé un entier par 2 en division entière.

Trace pour l'entrée `13` :

| Tour | `n` avant | `n >= 2` | `i` après | `n` après `n / 2` |
| --- | --- | --- | --- | --- |
| 1 | 13 | oui | 1 | 6,5 |
| 2 | 6,5 | oui | 2 | 3,25 |
| 3 | 3,25 | oui | 3 | 1,625 |
|  | 1,625 | non, on sort |  |  |

`n_copy` vaut 13, et le programme affiche que la partie entière du logarithme en base 2 de 13 est 3. On a bien `2^3 = 8 ≤ 13 < 16`.

Ce qu'il faut avoir en main : le `while` testé avant le corps, la différence entre division entière et division réelle, et la troncature lors du passage `double` → `int`. Ne pas oublier `#include <stdio.h>`, absent du fragment dans [[TP2]].

## À vérifier avant de les laisser coder

- Tout programme qui utilise `printf` ou `scanf` commence par `#include <stdio.h>`, et `sqrt` demande `#include <math.h>` puis `gcc ... -lm`.
- `main` retourne `0` quand tout s'est bien passé. Un `return` au milieu abandonne le reste de la fonction.
- Chaque `scanf` reçoit l'adresse de la variable (`&a`) et un spécificateur du bon type (`%d`, `%lf`, `%lld`).
- `/` entre entiers tronque ; `/` entre `double` ne tronque pas. `%` sert à tester un diviseur.
- `result *= n` et `n -= k` sont des affectations, pas des tests. `==` est le test d'égalité.
- Un `else` se rattache au `if` le plus proche. Trois cas s'écrivent `if` / `else if` / `else`.
- `for (expr1; expr2; expr3)` est un `while`. Si `expr1` est vide, rien ne s'exécute avant le premier test, et `expr3` s'exécute après le corps.
- Pour un nombre premier, on s'arrête au premier diviseur, on ne dépasse pas `i * i <= n`, et on écarte les pairs après avoir traité 2.
- Pour la partie entière de `log2(n)` avec `n ≥ 1`, on compte les divisions par 2 tant que la valeur reste supérieure ou égale à 2, et on conserve une copie de l'entrée avant de la modifier.
