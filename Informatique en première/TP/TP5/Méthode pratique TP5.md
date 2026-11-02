# Méthode pratique pour les exercices d'invariants

Les exercices d'examen demandent généralement deux choses :

- écrire une fonction ou une procédure ;
- démontrer par la méthode des invariants que le résultat est correct, et parfois que le programme se termine.

La preuve doit décrire le travail déjà effectué par la boucle, pas seulement affirmer que le résultat semble correct.

---

# 1. Caractériser le programme

Avant de chercher l'invariant, écrire le triplet de Hoare :

**{précondition} programme {postcondition}**

Préciser notamment :

- les contraintes sur les tailles (`n >= 0`, `n > 0`, `m <= n`, etc.) ;
- ce que contient le tableau ou la chaîne en entrée ;
- la signification exacte de la valeur retournée ;
- les éléments qui doivent rester inchangés ;
- le comportement demandé dans les cas particuliers, par exemple un tableau vide.

Une postcondition doit être formulée avec des mots précis. Par exemple :

**`t2[0 : j - 1]` contient, dans le même ordre, les éléments strictement positifs de `t1[0 : n - 1]`.**

---

# 2. Décomposer la boucle

Les corrigés réécrivent souvent un `for` sous la forme d'un `while`. Cela rend explicite l'endroit où l'invariant doit être vrai :

```c
for (initialisation; condition; mise_a_jour) {
    corps;
}
```

devient :

```c
{
    initialisation;
    while (condition) {
        corps;
        mise_a_jour;
    }
}
```

L'invariant est alors affirmé **avant le test du `while` et au début du corps**. Dans la preuve, il doit être vrai après la mise à jour, juste avant le tour suivant.

## Gérer un `return` ou un `break`

Une sortie anticipée rend la postcondition plus difficile à rattacher à la boucle. On peut introduire une variable fictive `r` qui représente la valeur retournée :

```c
int r = 1;
int i = 0;
while (i < n && r == 1) {
    if (condition_echec)
        r = 0;
    i++;
}
return r;
```

L'invariant précise alors ce que signifie `r` pour le préfixe déjà inspecté. À la sortie, on distingue les cas `r == 0` et `r != 0`, ainsi que la sortie due à la fin du tableau.

Cette transformation ne change pas le résultat si la sortie anticipée ne modifie pas une variable utilisée dans la postcondition. Il faut toutefois le signaler si l'indice ou une autre variable est modifié différemment.

---

# 3. Trouver un bon invariant

Partir des mots **déjà parcourus**, **déjà copiés**, **déjà comptés**, **déjà vérifiés** ou **déjà triés**.

Pour une boucle dont l'indice est `i`, le préfixe déjà traité est souvent :

**`t[0 : i - 1]`**

On décrit ensuite exactement les variables qui résument ce préfixe :

- un compteur contient le nombre d'éléments possédant une propriété ;
- un accumulateur contient leur somme ;
- une variable contient le maximum ou le minimum du préfixe ;
- un tableau auxiliaire contient les éléments sélectionnés, dans l'ordre ;
- un booléen indique si la propriété est encore vraie pour tout le préfixe ;
- une variable d'ordre décrit si le préfixe est croissant, décroissant ou constant.

Un invariant utile contient aussi les bornes des indices, par exemple `0 <= i <= n`, et les relations nécessaires entre les variables.

## Exemples de formulations

Pour recopier les éléments positifs :

**`0 <= i <= n` et `t2[0 : j - 1]` contient les éléments strictement positifs de `t1[0 : i - 1]`, dans le même ordre.**

Pour compter les signes :

**`nb_positifs` et `nb_negatifs` sont les nombres d'éléments positifs et négatifs de `t[0 : i - 1]`.**

Pour vérifier une propriété de tous les préfixes :

**`r == 1` si la propriété est vraie pour les préfixes déjà examinés, et `r == 0` dès qu'un contre-exemple a été trouvé.**

Pour un maximum :

**`maximum` est le maximum de `t[0 : i - 1]`.**

Une propriété de tableau peut nécessiter un invariant par cas. Par exemple, pour un tableau monotone, on peut avoir :

- `ordre == 1` et le préfixe est croissant ;
- `ordre == -1` et le préfixe est décroissant ;
- `ordre == 0` et le préfixe est constant ;
- `r == 0` et le tableau n'est déjà plus monotone.

---

> "Montrons que cet invariant est valide."


# 4. Prouver l'initialisation

Écrire les valeurs des variables juste avant le premier tour, puis vérifier l'invariant.

Exemple :

```c
i = 0;
j = 0;
```

Le préfixe `t1[0 : -1]` est vide. Il contient donc exactement les mêmes éléments positifs que `t2[0 : j - 1]`, qui est lui aussi vide. L'invariant est vrai.

Ne pas oublier les cas limites :

- un tableau vide correspond souvent à un préfixe vide ;
- un tableau à un élément est déjà monotone ;
- un maximum initialisé avec `t[0]` exige `n > 0`.

---

# 5. Prouver la conservation

Supposer l'invariant vrai au début d'un tour et ajouter la condition de boucle :

**{I, condition de boucle} corps ; mise à jour {I}**

Suivre les nouvelles valeurs avec des apostrophes si nécessaire : `i'`, `j'`, `r'`.

>**"Montrons que ce triplet est valide, en notant respectivement x et x′**
>**la valeur d’une variable x avant et après l’itération concernée."**

Traiter chaque branche du corps séparément. Pour une copie conditionnelle :

- si la condition est vraie, l'élément courant est ajouté et `j` augmente ;
- sinon, `j` reste inchangé ;
- dans les deux cas, `i` augmente et le préfixe traité s'étend d'un élément.

Pour une vérification avec sortie anticipée :

- si un contre-exemple est trouvé, montrer que `r == 0` signifie bien que la postcondition négative est vraie ;
- sinon, montrer que la propriété reste vraie sur le préfixe agrandi.

Ne pas oublier la mise à jour de l'indice. L'invariant doit être vrai après le corps **et** après cette mise à jour.

---

# 6. Fin de boucle

À la fin, on dispose de l'invariant et de la négation du gardien de boucle.

Si le gardien était `i < n`, la sortie donne `i >= n`. Avec `0 <= i <= n`, on obtient généralement `i == n`.

Si le gardien était `i < n && r == 1`, la sortie donne :

- soit `r == 0` : un contre-exemple a été trouvé ;
- soit `i >= n` : tout le tableau a été parcouru sans contre-exemple.

Il faut écrire explicitement ces cas et montrer, dans chacun, la postcondition. C'est souvent la partie la plus importante de la preuve.

---

# 7. Prouver la terminaison avec un variant

L'invariant prouve la correction, pas la terminaison. Pour la terminaison, choisir un variant entier qui :

1. est positif ou nul avant chaque tour ;
2. diminue strictement à chaque tour ;
3. ne peut pas diminuer indéfiniment.

Pour un parcours croissant jusqu'à `n`, le choix standard est :

**`v = n - i`**

L'invariant donne `0 <= i <= n`, donc `v >= 0`, et la mise à jour `i++` diminue `v` de 1.

Pour une boucle qui décrémente `i` jusqu'à 0, choisir `v = i`. Pour une boucle qui réduit progressivement une taille, choisir cette taille comme variant.

---

# 8. Modèle de rédaction

Pour un exercice, on peut suivre ce plan :

1. **Spécification :** donner la précondition et la postcondition.
2. **Réécriture :** décomposer le `for` en `initialisation`, `while`, corps et mise à jour.
3. **Invariant :** donner une formule précise, avec les bornes des indices.
4. **Interprétation :** expliquer en français ce que l'invariant signifie.
5. **Initialisation :** vérifier les valeurs avant le premier tour.
6. **Conservation :** traiter les branches du corps et montrer que l'invariant revient vrai.
7. **Sortie :** combiner l'invariant et la négation du gardien, en distinguant les cas.
8. **Terminaison :** proposer un variant si elle est demandée.

Une preuve courte mais complète vaut mieux qu'une simulation de quelques valeurs.

---

# Erreurs fréquentes

- décrire seulement la valeur finale, sans dire ce qui est vrai pour un indice quelconque ;
- écrire « les éléments précédents » sans préciser les bornes `0` et `i - 1` ;
- oublier les bornes de `i`, `j` ou d'un autre indice ;
- vérifier l'initialisation mais pas la mise à jour ;
- traiter seulement la branche principale et oublier la branche `else` ;
- utiliser l'invariant seul à la sortie, sans la négation de la condition ;
- confondre « la boucle est correcte si elle termine » avec une preuve de terminaison ;
- oublier les tableaux vides ou les préconditions nécessaires à `t[0]` ;
- proposer un invariant trop faible, qui ne permet pas de déduire la postcondition.

---

# Résumé à retenir

Décrire le travail fait sur le préfixe déjà parcouru.

Puis vérifier, dans cet ordre :

1. **initialisation** ;
2. **conservation** pour chaque branche ;
3. **sortie** avec la négation du gardien ;
4. **variant** pour la terminaison.

La formule utile est :

**invariant + sortie de boucle = postcondition**

et la méthode de rédaction est :

**spécifier, normaliser, formuler, initialiser, conserver, sortir, terminer.**
