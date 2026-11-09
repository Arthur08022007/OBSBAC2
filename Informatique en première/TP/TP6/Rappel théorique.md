# Les fonctions en C

Rappel théorique — TP 6
Syllabus, chapitre 4 : *Les fonctions et les procédures*

---

## Pourquoi utiliser une fonction ?

Une fonction regroupe un fragment de programme qui réalise une opération précise. Elle peut être appelée depuis plusieurs endroits du programme.

Cette organisation évite le copier-coller, réduit la redondance et facilite la correction ou l’amélioration du code. Elle permet aussi de décomposer un problème complexe en sous-problèmes plus simples.

Dans l’exercice, `multiplicite_facteur` réalise une seule opération : compter le nombre de divisions exactes de `n` par `f`.

---

## Fonction et procédure

Une **fonction** reçoit éventuellement des données, exécute des instructions et renvoie une valeur.

Une **procédure** est une fonction dont le type de retour est `void` : elle réalise une action, mais ne renvoie pas de valeur.

```c
type_retour nom(type1 parametre1, type2 parametre2)
{
    instructions;
    return valeur;
}
```

Exemple :

```c
unsigned multiplicite_facteur(unsigned n, unsigned f)
{
    unsigned m = 0;

    while (!(n % f)) {
        n /= f;
        m++;
    }

    return m;
}
```

- `unsigned` est le type de la valeur retournée ;
- `multiplicite_facteur` est le nom de la fonction ;
- `n` et `f` sont ses paramètres ;
- `m` est une variable locale ;
- `return m;` termine la fonction et renvoie la valeur calculée.

---

## Paramètres et arguments

Les **paramètres** sont les variables indiquées dans la définition de la fonction. Les **arguments** sont les valeurs fournies lors de l’appel.

```c
unsigned resultat;

resultat = multiplicite_facteur(324, 9);
```

Ici, `n` reçoit `324` et `f` reçoit `9`. En C, les arguments sont transmis **par valeur** : les paramètres sont des variables locales à l’appel de la fonction. Modifier `n` dans la fonction ne modifie donc pas directement une variable `n` située dans le code appelant.

---

## Appel et valeur de retour

Un appel de fonction s’écrit sous la forme :

```c
nom(argument1, argument2, ...);
```

Lors de l’évaluation de l’appel :

1. les arguments sont évalués ;
2. la fonction est exécutée avec ces valeurs ;
3. l’exécution reprend à l’endroit de l’appel ;
4. l’expression d’appel prend la valeur fournie par `return`.

Une fonction dont le type de retour n’est pas `void` doit retourner une valeur compatible avec ce type dans toutes les situations prévues.

---

## Déclaration, définition et prototype

La **définition** contient le corps de la fonction, c’est-à-dire les instructions exécutées :

```c
unsigned multiplicite_facteur(unsigned n, unsigned f)
{
    /* corps de la fonction */
}
```

La **déclaration**, ou **prototype**, indique seulement l’interface nécessaire pour appeler la fonction :

```c
unsigned multiplicite_facteur(unsigned, unsigned);
```

Un prototype est utile lorsque la fonction est définie dans un autre fichier ou plus bas dans le fichier courant. Les déclarations sont généralement regroupées dans un fichier d’en-tête `.h`, inclus avec `#include`.

---

## Interface et implémentation

L’**interface** décrit ce qu’il faut savoir pour utiliser une fonction :

- son nom ;
- le nombre et le type de ses paramètres ;
- la signification de ses paramètres ;
- le type et la signification de sa valeur de retour ;
- ses préconditions éventuelles.

L’**implémentation** décrit comment le résultat est calculé.

Pour `multiplicite_facteur` :

| Élément | Description |
|---|---|
| Nom | `multiplicite_facteur` |
| Paramètres | `n` et `f`, entiers strictement positifs |
| Retour | la multiplicité de `f` dans `n` |
| Précondition | `n > 0` et `f > 0` |
| Principe | diviser `n` par `f` tant que la division est exacte |

L’utilisateur de la fonction n’a pas besoin de connaître la boucle pour l’appeler correctement ; il doit seulement respecter son interface.

---

## Récursivité

Une fonction est **récursive** lorsqu’elle s’appelle elle-même, directement ou indirectement.

Une fonction récursive doit comporter :

1. un **cas de base**, qui ne provoque pas de nouvel appel ;
2. un ou plusieurs appels récursifs sur un problème plus petit ;
3. un mécanisme garantissant que l’on atteint le cas de base.

Exemple de factorielle :

```c
unsigned factorielle(unsigned n)
{
    if (n <= 1)
        return 1;

    return n * factorielle(n - 1);
}
```

Dans cet exemple, `n <= 1` est le cas de base et `n` diminue à chaque appel. La version itérative de l’exercice 1 utilise une boucle plutôt que la récursivité, mais les deux approches reposent sur la même idée : répéter une opération jusqu’à atteindre une condition d’arrêt.

---

## Lien avec l’invariant de l’exercice

Dans la fonction de l’exercice, l’invariant

```text
n₀ = n × f^m
```

décrit précisément le rôle des variables pendant l’exécution :

- `m` est le nombre de facteurs `f` déjà retirés ;
- `n` est la partie restante de la valeur initiale `n₀` ;
- le produit `n × f^m` conserve toujours la valeur initiale.

La condition `n % f == 0` autorise une nouvelle division. Lorsque cette condition devient fausse, `f` ne divise plus la partie restante : `m` est alors exactement la multiplicité recherchée.

---

## À retenir

- Une fonction encapsule une opération réutilisable.
- Les paramètres appartiennent à la fonction et reçoivent les valeurs des arguments.
- `return` termine une fonction et fournit sa valeur de retour.
- Un prototype décrit l’interface sans donner l’implémentation.
- Une bonne interface permet d’utiliser une fonction sans connaître ses détails internes.
- Une fonction récursive doit avoir un cas de base et progresser vers celui-ci.
