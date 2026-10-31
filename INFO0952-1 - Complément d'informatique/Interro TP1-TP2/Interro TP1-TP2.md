# Interro TP1-TP2

Synthèse pour les interros du type de l'[[interro_a_blanc_tp1_tp2.pdf|interro à blanc du 6 octobre 2026]] (connaissance générale du C, TP 1, TP 2).

Le corrigé de cette interro est dans [[Corrigé — interro à blanc]]. Les notes ci-dessous sont faites pour la question suivante, du même genre : un extrait à faire compiler dans la tête, un rappel de ce que calcule ton code de TP, une complexité, une trace, une fonction courte à écrire.

Les slides sont [[slides-info0952-2026-2027.pdf]]. Les numéros cités sont ceux imprimés en bas des transparents.

Le code des TP est dans `~/Documents/Unif/BAC2/CompInfo/` :

- TP 1, exercice 7 : `fichiers-tp1-2026-2027/ex7/` (`kendalltau.c`)
- TP 2, exercice 2 : `fichiers-tp2-2026-2027/ex2/` (`findfirsttrue.c`), énoncé `60511458.pdf`

## Où relire

| La question demande… | Note | Slides |
| --- | --- | --- |
| `malloc`, `sizeof`, un tableau de pointeurs, un prototype | [[Allocation et pointeurs]] | Partie 1, slides 44-47 ; exemple `char **` slide 264 |
| un `void *`, un pointeur de fonction, un `param` | [[void et fonctions]] | Partie 4, slides 191-196 |
| un `typedef struct` dans un `.h`, et ce qui compile dans le `.c` ou dans un client | [[Types opaques]] | Partie 4, slides 183-186 |
| une paire discordante, une valeur de tau, les doublons, la symétrie | [[Tau de Kendall]] | la formule vient du TP ; le tri fusion est aux slides 144-146 |
| `findFirstTrue`, un callback, une trace, la version en O(N) | [[findFirstTrue]] | recherche dichotomique, slides 135-138 |
| un O(…) en temps ou en espace | [[Complexité]] | slides 107-119, et l'espace de la recherche aux slides 137-138 |

## Comment lire une question

Trois familles reviennent. Chacune se traite dans un ordre fixe.

**Un extrait de C, cases « ça compile / ça renvoie ».** On relève le type de chaque nom, puis on se demande si ce type est complet dans le fichier où l'extrait est collé. Ensuite seulement on exécute. Un `void *` ne s'indexe pas : on le convertit, puis on indexe le pointeur converti. Un pointeur de fonction s'appelle comme la fonction. Le tableau passé en argument est l'adresse de son premier élément : une écriture à travers ce pointeur modifie l'objet de l'appelant.

**Une question sur ton TP.** On réécrit d'abord l'invariant de la fonction, en une phrase, avant de regarder les cases. Pour Kendall : une paire discordante, la formule, ce que le tri a le droit de réordonner. Pour `findFirstTrue` : le prédicat est faux sur un préfixe et vrai sur le suffixe, et la valeur renvoyée est l'indice de la frontière. La case correcte est une conséquence de cette phrase. Les options qui comparent `x[i]` à `y[i]`, ou qui prennent `param` pour la longueur, décrivent une autre fonction.

**Une complexité.** Le mot « temps » ou « espace » change la réponse. On compte les opérations pour le temps, les tableaux auxiliaires et la pile d'appels pour l'espace. L'entrée ne compte pas dans l'espace auxiliaire. Les quatre cases habituelles sont O(1), O(N), O(N log N), O(N²) : ce sont exactement le temps et l'espace des deux versions, et les confondre est la question.

**Une fonction à écrire.** On écrit la version demandée, pas la version efficace du TP. L'interro à blanc demande la version naïve en O(N) de `findFirstTrue`, alors que le TP demandait O(log N). On respecte la signature imposée, y compris le cas où aucun élément ne convient (`return length`).
